Camel Quarkus

# MCP Server

JVM since3.39.0 Native since3.39.0

The MCP Server extension exposes Camel routes registered via the `ai-tool` component as tools of a Model Context Protocol (MCP) server, served through the quarkiverse [quarkus-mcp-server](https://docs.quarkiverse.io/quarkus-mcp-server/dev/index.md) extension. No route is needed for the server itself: add the extension, tag the `ai-tool` routes to expose, and any MCP client (another Camel application, an IDE, a coding agent) can discover and call them.

Tool semantics — tag-based opt-in (the untagged default pool is never exposed), flat-namespace collision refusal, per-call timeout and error sanitization — are owned by the runtime-agnostic `camel-mcp-server-api` bridge and are identical on every Camel runtime. Serving concerns (endpoint path, transports, authentication) are owned by quarkus-mcp-server and configured via `quarkus.mcp.server.*`.

## What’s inside

-   [MCP Server](../../../../components/4.22.x/others/mcp-server.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-mcp-server)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-mcp-server</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

Define tools as regular `ai-tool` routes and give them tags:

```java
from("ai-tool:query_db?tags=crm&description=Query customer database"
     + "&parameter.customerId=string&parameter.customerId.required=true")
    .to("jdbc:dataSource");
```

or in YAML DSL:

```yaml
- route:
    from:
      uri: "ai-tool:send_email"
      parameters:
        description: "Send email notification"
        tags: "notify"
        parameter.to: string
        parameter.to.description: "Recipient address"
        parameter.to.required: "true"
        parameter.subject: string
        parameter.priority: string
        parameter.priority.enum: "low,normal,high"
      steps:
        - to: "smtp://mail.example.com"
```

Tool parameters are declared with the `parameter.NAME` options: the value is the JSON type (`string`, `integer`, `number`, `boolean`), and the `parameter.NAME.description`, `parameter.NAME.required` and `parameter.NAME.enum` options refine the generated input schema. Arguments arrive as message headers in the route (`${header.customerId}`).

### Combining the Camel and quarkus-mcp-server configuration

The configuration is split by ownership: `quarkus.camel.mcp-server.` **decides \*which tools exist and how they execute** (identical semantics on every Camel runtime), while `quarkus.mcp.server.` **decides \*how the server is exposed**. Both are set side by side in `application.properties`:

```properties
# Camel-owned: tool selection and execution
quarkus.camel.mcp-server.tags = crm,notify
quarkus.camel.mcp-server.tool-timeout = 10000

# quarkus-mcp-server-owned: serving and server identity
quarkus.mcp.server.server-info.name = my-integration-app
quarkus.mcp.server.server-info.version = 1.0.0
quarkus.mcp.server.http.root-path = /mcp

# quarkus-mcp-server-owned: diagnostics while developing
quarkus.mcp.server.traffic-logging.enabled = true
quarkus.mcp.server.traffic-logging.text-limit = 200
```

See the [quarkus-mcp-server configuration reference](https://docs.quarkiverse.io/quarkus-mcp-server/dev/index.html#configuration-reference) for the full list of `quarkus.mcp.server.*` properties (transports, dev UI, authentication, guardrails, pagination, timeouts).

### Connecting MCP clients

Any MCP client can connect over streamable HTTP. Another Camel integration can consume the tools with the camel-openai MCP client and automatic tool execution:

```java
from("direct:agent")
    .to("openai:chat-completion"
        + "?model={{llm.model}}"
        + "&autoToolExecution=true"
        + "&mcpServer.myCamelTools.transportType=streamableHttp"
        + "&mcpServer.myCamelTools.url=http://localhost:8080/mcp");
```

A coding agent or IDE is configured with the same URL, e.g. in an `mcp.json`\-style client configuration:

```json
{
  "mcpServers": {
    "my-integration-app": {
      "type": "http",
      "url": "http://localhost:8080/mcp"
    }
  }
}
```

### Serving over stdio

Out of the box the tools are served over streamable HTTP. MCP clients that launch the server as a subprocess speak over stdin/stdout instead — add the stdio transport alongside the extension:

```xml
<dependency>
    <groupId>io.quarkiverse.mcp</groupId>
    <artifactId>quarkus-mcp-server-stdio</artifactId>
    <!-- the same version as the quarkus-mcp-server-http extension pulled in
         by camel-quarkus-mcp-server; the transports share their core module -->
    <version>1.13.1</version>
</dependency>
```

The stdio transport is active as soon as it is on the classpath (`quarkus.mcp.server.stdio.enabled` defaults to `true`), and the same Camel tools are then served over both transports. To serve over stdio **only**, disable the HTTP transport of the default MCP server:

```properties
quarkus.mcp.server."<default>".http.enabled = false
```

The server name of the default MCP server is the literal string `<default>`, so it has to be quoted. Conversely, `quarkus.mcp.server.stdio.enabled = false` keeps the stdio extension on the classpath without activating it, which is useful when the same application is deployed both ways.

Because stdout carries the MCP protocol, nothing else may be written to it; `quarkus-mcp-server-stdio` takes care of this by routing console logging to stderr. A stdio server is typically built as a native executable and launched by the client:

```json
{
  "mcpServers": {
    "my-integration-app": {
      "command": "/path/to/target/my-integration-app-1.0.0-runner"
    }
  }
}
```

See the [quarkus-mcp-server stdio guide](https://docs.quarkiverse.io/quarkus-mcp-server/dev/getting-started-stdio.md) and the [configuration reference](https://docs.quarkiverse.io/quarkus-mcp-server/dev/reference-configuration.md) for the transport options. On Spring Boot the equivalent setup is described in the [Spring AI MCP Server Boot Starter documentation](https://docs.spring.io/spring-ai/reference/api/mcp/mcp-server-boot-starter-docs.md).

### Mixing with quarkus-mcp-server annotated tools

Camel tools coexist with tools defined natively with quarkus-mcp-server — both are served by the same MCP server and appear in the same `tools/list`. For example, a `@Tool`\-annotated business method:

```java
public class CalculatorTools {

    @Tool(name = "add_numbers", description = "Add two numbers")
    String add(
            @ToolArg(description = "First addend") long a,
            @ToolArg(description = "Second addend") long b) {
        return String.valueOf(a + b);
    }
}
```

is exposed alongside the `ai-tool` routes. Annotated tools are registered at build time; Camel tools are added and removed dynamically with the route lifecycle. Choose distinct tool names — MCP has a flat tool namespace.

### Dynamic tools

The exposed tool list follows the route lifecycle: stopping or suspending an `ai-tool` route removes its tool, starting or resuming it publishes the tool again, and connected clients are notified via `notifications/tools/list_changed`:

```java
camelContext.getRouteController().stopRoute("query-db-route");   // tool disappears
camelContext.getRouteController().startRoute("query-db-route");  // tool is back
```

### Error handling

Results returned to MCP clients are sanitized by the bridge: a route exception produces an error result with the generic message `Tool execution failed` (the cause is logged server-side and never sent to the client), a missing or invalid argument returns the validation message, and a call exceeding `quarkus.camel.mcp-server.tool-timeout` returns `Tool execution timed out` while the route keeps running until it completes on its own.

On Camel Main and Camel JBang the equivalent setup is the `camel-mcp-server` module with the `camel.server.mcp-*` options; on Spring Boot it is the `camel-mcp-server-starter`.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.mcp-server.enabled](#quarkus-camel-mcp-server-enabled)`
Whether to expose ai-tool routes as MCP tools through the quarkus-mcp-server extension.

 | `boolean` | `true` |
| `[quarkus.camel.mcp-server.tags](#quarkus-camel-mcp-server-tags)`

Comma-separated list of ai-tool tags to expose as MCP tools. Only tools registered under one of these tags are exposed; the untagged default pool is never exposed. When not set, no tools are exposed.

 | `string` |  |
| `[quarkus.camel.mcp-server.tool-timeout](#quarkus-camel-mcp-server-tool-timeout)`

Per-call tool execution timeout in milliseconds. A call exceeding the timeout returns an error result to the MCP client; the underlying route keeps running until it completes on its own.

 | `long` | `20000` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.