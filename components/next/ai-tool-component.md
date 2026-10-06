# AI Tool

**Since Camel 4.22**

**Only consumer is supported**

The AI Tool component exposes Camel routes as tools that AI models can call. Any AI producer component (such as [LangChain4j Agent](langchain4j-agent-component.md) or [Spring AI Chat](spring-ai-chat-component.md)) discovers registered tools using tag-based filtering.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ai-tool</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

ai-tool:toolName\[?options\]

Where **toolName** is the name the LLM sees and uses to invoke the tool.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The AI Tool component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **argSchema** (consumer) | Raw JSON Schema for tool input parameters. Supports inline JSON and resource references (classpath:, file:, resource:). Mutually exclusive with the parameter multi-value options. Use for nested objects, arrays, oneOf, and other complex schemas. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **configuration** (consumer) | The component configuration. |  | AiToolConfiguration |
| **description** (consumer) | Human-readable description of what this tool does. Passed verbatim to the LLM; be precise and action-oriented. When omitted, defaults to the tool name. |  | String |
| **destructiveHint** (consumer) | MCP hint that the tool may perform destructive or irreversible updates. Advisory for MCP clients; not enforced by Camel. | false | Boolean |
| **idempotentHint** (consumer) | MCP hint that repeating the tool call with the same arguments has no additional effect. Advisory for MCP clients; not enforced by Camel. | false | Boolean |
| **openWorldHint** (consumer) | MCP hint that the tool interacts with external systems outside the application’s control. Advisory for MCP clients; not enforced by Camel. | false | Boolean |
| **outputParameters** (consumer) | Tool output schema fields. Format: outputParameter.NAME=TYPE, outputParameter.NAME.description=TEXT. Supported types: string, integer, number, boolean. Mutually exclusive with outputSchema. This is a multi-value option with prefix: outputParameter. |  | Map |
| **outputSchema** (consumer) | Raw JSON Schema describing the tool’s structured output. Supports inline JSON and resource references (classpath:, file:, resource:). Mutually exclusive with the outputParameter multi-value options. When declared, the route body is parsed as JSON and exposed as structured content to MCP clients. |  | String |
| **parameters** (consumer) | Tool input parameters. Format: parameter.NAME=TYPE, parameter.NAME.description=TEXT, parameter.NAME.required=true or false, parameter.NAME.enum=val1,val2. Supported types: string, integer, number, boolean. Mutually exclusive with argSchema. This is a multi-value option with prefix: parameter. |  | Map |
| **readOnlyHint** (consumer) | MCP hint that the tool only reads data and does not modify state. Advisory for MCP clients; not enforced by Camel. | false | Boolean |
| **returnDirect** (consumer) | When true, AI producers that support agentic tool loops (such as camel-openai) return this tool’s result directly to the caller without sending it back to the model. Also published as an MCP tool annotation when the tool is exposed via camel-mcp-server. | false | Boolean |
| **tags** (consumer) | Comma-separated list of tags used to group tools. Producers filter the registry by these tags to select which tools to expose to the LLM. When omitted, the tool goes into a default pool available to all producers. |  | String |
| **title** (consumer) | Optional display title for MCP tool listings. Advisory hint for MCP clients only. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **authorizationPolicy** (security) | Reference to an org.apache.camel.spi.AuthorizationPolicy used to authorize tool calls before the route runs. Set it on the component to guard every tool route by construction, or per endpoint to override. The policy authorizes on trustworthy input only: the tool name comes from the route (never from model output), and the caller identity is carried as an exchange property set before the agent ran (for example by camel-spiffe or camel-keycloak), which the model cannot set. Authorize on exchange properties or validated tokens only, never on message headers (on a tool route the headers carry the model-controlled tool arguments). A denied call surfaces to the model as a short refusal rather than a stack trace. |  | AuthorizationPolicy |

## Endpoint Options

The AI Tool endpoint is configured using URI syntax:

ai-tool:toolName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **toolName** (consumer) | **Required** The tool name. This is the name the LLM sees and uses to invoke the tool. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **argSchema** (consumer) | Raw JSON Schema for tool input parameters. Supports inline JSON and resource references (classpath:, file:, resource:). Mutually exclusive with the parameter multi-value options. Use for nested objects, arrays, oneOf, and other complex schemas. |  | String |
| **description** (consumer) | Human-readable description of what this tool does. Passed verbatim to the LLM; be precise and action-oriented. When omitted, defaults to the tool name. |  | String |
| **destructiveHint** (consumer) | MCP hint that the tool may perform destructive or irreversible updates. Advisory for MCP clients; not enforced by Camel. | false | Boolean |
| **idempotentHint** (consumer) | MCP hint that repeating the tool call with the same arguments has no additional effect. Advisory for MCP clients; not enforced by Camel. | false | Boolean |
| **openWorldHint** (consumer) | MCP hint that the tool interacts with external systems outside the application’s control. Advisory for MCP clients; not enforced by Camel. | false | Boolean |
| **outputParameters** (consumer) | Tool output schema fields. Format: outputParameter.NAME=TYPE, outputParameter.NAME.description=TEXT. Supported types: string, integer, number, boolean. Mutually exclusive with outputSchema. This is a multi-value option with prefix: outputParameter. |  | Map |
| **outputSchema** (consumer) | Raw JSON Schema describing the tool’s structured output. Supports inline JSON and resource references (classpath:, file:, resource:). Mutually exclusive with the outputParameter multi-value options. When declared, the route body is parsed as JSON and exposed as structured content to MCP clients. |  | String |
| **parameters** (consumer) | Tool input parameters. Format: parameter.NAME=TYPE, parameter.NAME.description=TEXT, parameter.NAME.required=true or false, parameter.NAME.enum=val1,val2. Supported types: string, integer, number, boolean. Mutually exclusive with argSchema. This is a multi-value option with prefix: parameter. |  | Map |
| **readOnlyHint** (consumer) | MCP hint that the tool only reads data and does not modify state. Advisory for MCP clients; not enforced by Camel. | false | Boolean |
| **returnDirect** (consumer) | When true, AI producers that support agentic tool loops (such as camel-openai) return this tool’s result directly to the caller without sending it back to the model. Also published as an MCP tool annotation when the tool is exposed via camel-mcp-server. | false | Boolean |
| **tags** (consumer) | Comma-separated list of tags used to group tools. Producers filter the registry by these tags to select which tools to expose to the LLM. When omitted, the tool goes into a default pool available to all producers. |  | String |
| **title** (consumer) | Optional display title for MCP tool listings. Advisory hint for MCP clients only. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **authorizationPolicy** (security) | Reference to an org.apache.camel.spi.AuthorizationPolicy used to authorize tool calls before the route runs. Set it on the component to guard every tool route by construction, or per endpoint to override. The policy authorizes on trustworthy input only: the tool name comes from the route (never from model output), and the caller identity is carried as an exchange property set before the agent ran (for example by camel-spiffe or camel-keycloak), which the model cannot set. Authorize on exchange properties or validated tokens only, never on message headers (on a tool route the headers carry the model-controlled tool arguments). A denied call surfaces to the model as a short refusal rather than a stack trace. |  | AuthorizationPolicy |

## Usage

### Basic Tool Definition

-   Java
    
-   XML
    
-   YAML
    

```java
from("ai-tool:weather?tags=weather&description=Get current weather for a city" +
    "&parameter.city=string&parameter.city.description=The city name")
    .to("bean:weatherService");
```

```xml
<route>
  <from uri="ai-tool:weather?tags=weather&amp;description=Get current weather for a city&amp;parameter.city=string&amp;parameter.city.description=The city name"/>
  <to uri="bean:weatherService"/>
</route>
```

```yaml
- route:
    from:
      uri: ai-tool:weather
      parameters:
        tags: weather
        description: "Get current weather for a city"
        parameter.city: string
        parameter.city.description: "The city name"
      steps:
        - to:
            uri: bean:weatherService
```

### Tool with Multiple Parameters

-   Java
    
-   XML
    
-   YAML
    

```java
from("ai-tool:calculator?tags=math" +
    "&description=Calculate a math expression" +
    "&parameter.a=number" +
    "&parameter.a.description=First operand" +
    "&parameter.a.required=true" +
    "&parameter.b=number" +
    "&parameter.b.description=Second operand" +
    "&parameter.b.required=true" +
    "&parameter.operation=string" +
    "&parameter.operation.description=The operation to perform" +
    "&parameter.operation.enum=add,subtract,multiply,divide")
    .to("direct:calculator");
```

```xml
<route>
  <from uri="ai-tool:calculator?tags=math&amp;description=Calculate a math expression&amp;parameter.a=number&amp;parameter.a.description=First operand&amp;parameter.a.required=true&amp;parameter.b=number&amp;parameter.b.description=Second operand&amp;parameter.b.required=true&amp;parameter.operation=string&amp;parameter.operation.description=The operation to perform&amp;parameter.operation.enum=add,subtract,multiply,divide"/>
  <to uri="direct:calculator"/>
</route>
```

```yaml
- route:
    from:
      uri: ai-tool:calculator
      parameters:
        tags: math
        description: "Calculate a math expression"
        parameter.a: number
        parameter.a.description: "First operand"
        parameter.a.required: true
        parameter.b: number
        parameter.b.description: "Second operand"
        parameter.b.required: true
        parameter.operation: string
        parameter.operation.description: "The operation to perform"
        parameter.operation.enum: "add,subtract,multiply,divide"
      steps:
        - to:
            uri: direct:calculator
```

### Complex Parameters with argSchema

Use `argSchema` when the flat `parameter.*` syntax is not expressive enough for nested objects, arrays, or other advanced JSON Schema constructs. `argSchema` is mutually exclusive with `parameter.*`.

-   YAML
    

```yaml
- route:
    from:
      uri: ai-tool:createOrder
      parameters:
        tags: orders
        description: "Create an order"
        argSchema: |
          {
            "type": "object",
            "properties": {
              "customer": {
                "type": "object",
                "properties": {
                  "id": { "type": "string" }
                },
                "required": ["id"]
              },
              "items": {
                "type": "array",
                "items": {
                  "type": "object",
                  "properties": {
                    "sku": { "type": "string" },
                    "qty": { "type": "integer" }
                  }
                }
              }
            },
            "required": ["customer", "items"],
            "additionalProperties": false
          }
      steps:
        - to:
            uri: direct:createOrder
```

Top-level schema properties are exposed as exchange headers. Nested values are passed as Map or List objects.

`argSchema` also supports Camel resource references such as `classpath:schemas/create-order.json`.

The root schema must be a JSON Schema object with a top-level `properties` map. Camel always allowlists top-level property names when invoking the tool route, even if the schema sets `additionalProperties: true`. Nested fields are not flattened into headers; only top-level properties become exchange headers (Map/List/primitive values).

### Structured Tool Output (outputSchema)

MCP tools can declare an `outputSchema` and return `structuredContent` (typed JSON) so clients parse tool results reliably instead of re-interpreting free text. Use `outputParameter.*` for flat field definitions or `outputSchema` for raw JSON Schema (mirroring the input-side `parameter.*` / `argSchema` pattern). The two options are mutually exclusive.

When an output schema is declared, the route body must be JSON (a JSON string, `Map`, or `List`). Camel parses it into structured content and forwards it through the MCP bridge as `CallToolResult.structuredContent`. The text representation remains available for LLM adapters (LangChain4j, Spring AI) that consume string tool results.

-   Java
    
-   YAML
    

```java
from("ai-tool:getWeather?tags=weather&description=Get weather"
     + "&outputSchema=classpath:schemas/weather-result.json")
    .process(exchange -> exchange.getMessage().setBody(
        "{\"temperature\":21.5,\"unit\":\"celsius\"}"));
```

```yaml
- route:
    from:
      uri: ai-tool:getWeather
      parameters:
        tags: weather
        description: "Get weather"
        outputParameter.temperature: number
        outputParameter.unit: string
      steps:
        - setBody:
            expression:
              constant:
                expression: '{"temperature":21.5,"unit":"celsius"}'
```

Flat `outputParameter.*` options use the same sub-option syntax as input `parameter.*`:

-   `outputParameter.NAME=TYPE` — field type (`string`, `integer`, `number`, `boolean`)
    
-   `outputParameter.NAME.description=TEXT` — field description in the generated JSON Schema
    
-   `outputParameter.NAME.required=true` — marks the field as required in the output schema
    
-   `outputParameter.NAME.enum=val1,val2` — restricts allowed values
    

`outputSchema` supports Camel resource references such as `classpath:schemas/weather-result.json`.

### MCP Tool Annotation Hints

When exposing `ai-tool` routes through the MCP Server component, you can declare optional behavioral hints aligned with the MCP specification (`ToolAnnotations`). MCP clients may use these hints for per-tool policy (for example auto-approving read-only tools or requiring confirmation before destructive ones).

These hints are **advisory only** — Camel does not enforce them. MCP clients must treat them as untrusted UX metadata (per the MCP specification), not as authorization. Inaccurate hints can mislead client-side confirmation flows.

-   Java
    
-   YAML
    

```java
from("ai-tool:delete_order?tags=orders&description=Delete an order"
     + "&title=Delete order"
     + "&readOnlyHint=false"
     + "&destructiveHint=true"
     + "&idempotentHint=false"
     + "&openWorldHint=true")
    .to("direct:deleteOrder");
```

```yaml
- route:
    from:
      uri: ai-tool:delete_order
      parameters:
        tags: orders
        description: "Delete an order"
        title: "Delete order"
        readOnlyHint: false
        destructiveHint: true
        idempotentHint: false
        openWorldHint: true
      steps:
        - to:
            uri: direct:deleteOrder
```

Supported options: `title`, `readOnlyHint`, `destructiveHint`, `idempotentHint`, `openWorldHint`, and `returnDirect`. When a hint is omitted, it is not published; MCP clients then apply their own defaults (for example assuming destructive/open-world unless told otherwise). The `returnDirect` hint is also honoured by AI producers such as [OpenAI](../4.22.x/openai-component.md) when route tools are exposed via the `tags` option.

The `title` option maps to the MCP tool’s top-level `title` field (not `ToolAnnotations.title`). Boolean hint options use nullable configuration: when unset, Camel omits them from the published MCP tool even though the component catalog may list `defaultValue: false` for documentation tooling.

### Tag-Based Discovery

Tags group tools so that AI producers can select relevant subsets.

-   Java
    
-   XML
    
-   YAML
    

```java
// Define tools with tags
from("ai-tool:weather?tags=weather,external-api&description=Get weather for a city" +
    "&parameter.city=string&parameter.city.description=The city name")
    .to("bean:weatherService");

from("ai-tool:lookupUser?tags=users&description=Look up a user by ID" +
    "&parameter.id=integer&parameter.id.description=The user ID&parameter.id.required=true")
    .to("bean:userService?method=findById(${header.id})");
```

```xml
<!-- Define tools with tags -->
<route>
  <from uri="ai-tool:weather?tags=weather,external-api&amp;description=Get weather for a city&amp;parameter.city=string&amp;parameter.city.description=The city name"/>
  <to uri="bean:weatherService"/>
</route>

<route>
  <from uri="ai-tool:lookupUser?tags=users&amp;description=Look up a user by ID&amp;parameter.id=integer&amp;parameter.id.description=The user ID&amp;parameter.id.required=true"/>
  <to uri="bean:userService?method=findById(${header.id})"/>
</route>
```

```yaml
# Define tools with tags
- route:
    from:
      uri: ai-tool:weather
      parameters:
        tags: weather,external-api
        description: "Get weather for a city"
        parameter.city: string
        parameter.city.description: "The city name"
      steps:
        - to:
            uri: bean:weatherService

- route:
    from:
      uri: ai-tool:lookupUser
      parameters:
        tags: users
        description: "Look up a user by ID"
        parameter.id: integer
        parameter.id.description: "The user ID"
        parameter.id.required: true
      steps:
        - to:
            uri: "bean:userService?method=findById(${header.id})"
```

## The calling exchange

Each tool invocation runs on a copy of the **calling exchange** — the exchange that drives the agent (the `langchain4j-agent`, `openai` or `spring-ai-chat` producer). The context the caller set before the agent ran is carried onto the tool route:

-   exchange **properties** — most importantly an authenticated caller’s identity kept as a property, so a tool route can be guarded on it (for example `exchangeProperty.subject`) and the model cannot forge it;
    
-   exchange **variables**.
    

The message itself is **clean**: the tool route receives only its own arguments (supplied by the model and placed on the message as headers), not the caller’s body or inbound headers, and a tool that sets no body returns `No result` rather than echoing the caller’s body back to the model. Any change the tool makes — to its message, body or exception — is isolated to the copy and does not leak back into the calling exchange.

The tool exchange runs in its own **unit of work** and with its own exchange id; it does not share the caller’s. So each tool call is independent: the tool route’s own `onCompletion`, error handler and `useOriginalMessage()` apply to the tool call rather than to the caller, parallel tool calls in a batch get distinct exchange ids, and an error handler cannot restore the caller’s message into the result.

All route-tool runtimes build the tool exchange the same way, so an authorization check on an exchange property behaves identically whether the agent loop is driven by `camel-langchain4j-agent`, `camel-openai` or `camel-spring-ai-chat`.

## Authorizing tool calls

A tool call is a security boundary: an AI model decides, from its own output, which `ai-tool` route to invoke. Set an `authorizationPolicy` — a reference to an `org.apache.camel.spi.AuthorizationPolicy` bean — to authorize every call before the route runs. Set it on the **component** to guard every tool route by construction, or on a single endpoint to override.

-   Java
    
-   YAML
    

```java
// one policy guarding every ai-tool route
AiToolComponent ai = context.getComponent("ai-tool", AiToolComponent.class);
ai.getConfiguration().setAuthorizationPolicy(myAuthorizationPolicy);

from("ai-tool:transferFunds?tags=banking&description=Transfer funds")
    .to("bean:ledger");

// ...or override on a single endpoint
from("ai-tool:transferFunds?tags=banking&description=Transfer funds&authorizationPolicy=#myAuthorizationPolicy")
    .to("bean:ledger");
```

```yaml
- route:
    from:
      uri: ai-tool:transferFunds
      parameters:
        tags: banking
        description: "Transfer funds"
        authorizationPolicy: "#myAuthorizationPolicy"
      steps:
        - to:
            uri: bean:ledger
```

The guard runs in front of the route: it wraps the route’s outer processor, so it executes before the route’s unit of work, tracing and error handling. A denied call (`CamelAuthorizationException`) is returned to the model as a short refusal it can relay — not as a tool result and not as a stack trace — regardless of the tool-execution error strategy; the denial is logged at `WARN`, but it does not produce a route span or metric.

The policy authorizes on **trustworthy** input only:

-   the **tool name** comes from the route (the tool’s id), never from model output;
    
-   the **caller identity** comes from an exchange **property** (or a validated token) set before the agent ran — for example by `camel-spiffe` or `camel-keycloak`. Authorize on properties or validated tokens only, **never** on message headers: on a tool route the headers carry the model-controlled tool arguments (and, on the `langchain4j-agent` path, the caller’s inbound HTTP headers), so a policy such as OPA with the default `includeHeaders="*"` would otherwise read attacker-influenced values.
    

Which runtimes carry the caller identity:

-   `camel-langchain4j-agent`, `camel-openai` and `camel-spring-ai-chat` all copy the calling exchange (see [The calling exchange](#_the_calling_exchange) above), so the identity property reaches the tool route.
    
-   Over the [MCP server](others/mcp-server.md) the authenticated transport caller is carried onto the tool exchange as the `CamelMcpSecurityPrincipal` property (the raw transport principal — for the Vert.x streamable HTTP server, an `io.vertx.ext.auth.User`). A policy over MCP reads that property directly; Camel’s shipped identity/token policies (Keycloak, Spring Security, Shiro) do not read it yet, so MCP authorization needs a policy that inspects `CamelMcpSecurityPrincipal`. Exposing a runtime-neutral principal name and roles for the shipped policies is tracked as a follow-up.
    

## See Also

-   [LangChain4j Agent Component](langchain4j-agent-component.md) — discovers ai-tool tools via the `tags` option
    
-   [Spring AI Chat Component](spring-ai-chat-component.md) — discovers ai-tool tools via the `tags` option
    
-   [MCP Server](others/mcp-server.md) — exposes ai-tool routes as MCP tools over streamable HTTP