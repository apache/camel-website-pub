# ![ai tool source](_images/kamelets/ai-tool-source.svg) AI Tool Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Offers the steps that follow it as a tool that an AI agent can call, such as an MCP client like Claude Desktop or Cursor, with the arguments of each call as JSON.

Use it to let an AI assistant look up or change data through a flow you control, such as returning the status of an order. In a route (YAML), the steps after `from: kamelet:ai-tool-source` run for each call; they can also hand the call on with `to: kamelet:<name>`. To offer the tool over MCP, set `camel.server.mcp-enabled=true` and `camel.server.mcp-tags` to its tag, in `application.properties` or with `--prop` or `-D`: Camel JBang then adds `camel-mcp-server` by itself, other applications need it and `camel-platform-http-main` as dependencies. MCP clients connect with streamable HTTP to `[http://<host>:<port>/mcp](http://\<host\>:\<port\>/mcp)`, on the HTTP port of the application (`camel.server.port`, 8080 by default with Camel JBang). The `openai` component can call the tools of a tag as well, with its `tags` option.

Output: the body is the arguments of the call, as JSON text, such as `{"orderId":"42"}`, with only the arguments that `argSchema` declares (`{}` for a tool without arguments). Each of them is also a header of its own name, such as `orderId`. The body at the end of the flow, as text, is the result the caller gets back; the headers are not sent back. A flow that does not change the body gives the caller its own arguments back.

Good to know: an MCP client is an untrusted sender. Anyone who can reach the MCP endpoint can call every tool it offers, with any arguments, so check them before you use them. The MCP server offers only the tools whose tag is in `camel.server.mcp-tags`, never one with another tag. It listens on all network interfaces by default (`camel.server.host`) and has no login: protect it with OAuth (`camel.server.mcp-oauth-profile`) or network rules. A call from a web page of another host is refused, unless `camel.server.mcp-allowed-origins` allows it. A call that misses a required argument, has one of the wrong type, or has one that `argSchema` does not declare, is refused before the flow runs. An error in the flow reaches the caller only as `Tool execution failed`, and a call that takes longer than `camel.server.mcp-tool-timeout` (20 seconds by default) as `Tool execution timed out`, while the flow goes on. The hints are advice for the client, which Camel does not enforce. `allowedRoles` checks the roles of a caller logged in with OAuth, so without OAuth a tool with `allowedRoles` refuses every call.

## Configuration Options

The following table summarizes the configuration options available for the `ai-tool-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **description** | Description | **Required** What the tool does and when to use it, written for the AI model, which reads it to decide whether to call the tool, such as `Returns the status of an order by its id`. | string |  | Returns the status of an order by its id |
| **tags** | Tags | **Required** One or more tags, separated by commas, that put the tool in groups, such as `orders`. An MCP server offers only the tools whose tag is in its `camel.server.mcp-tags` setting. | string |  | orders |
| **toolName** | Tool Name | **Required** The name of the tool, which the AI model sees and calls it by. Letters, digits, `_` and `-` only, at most 64 characters, such as `get_order_status`. It must be unique among the tools the application offers. | string |  | get\_order\_status |
| **allRolesRequired** | All Roles Required | Whether the caller needs all the roles of `allowedRoles` instead of one of them. | boolean | false |  |
| **allowedRoles** | Allowed Roles | The roles, separated by commas, of which the caller needs one to call the tool, such as `finance`. The roles come from the login of the caller (MCP over HTTP with OAuth); a caller without a login is refused. | string |  | finance |
| **argSchema** | Arguments Schema | The JSON Schema of the arguments of the tool, an `object` with its `properties` and the `required` ones, such as `\{"type":"object","properties":\{"orderId":\{"type":"string","description":"The order id"}},"required":["orderId"]}`. It can also be read from a file, with `file:` or `classpath:` in front of its location. When it does not set `additionalProperties`, Camel adds `additionalProperties: false`, so a call with an argument it does not declare is refused; with any schema, only the declared arguments reach the flow. Without it, the tool takes no arguments. | string |  | {"type":"object","properties":{"orderId":{"type":"string","description":"The order id"}},"required":\["orderId"\]} |
| **destructiveHint** | Destructive Hint | Tells an MCP client that the tool may delete or overwrite data. A hint only, which Camel does not check. | boolean |  |  |
| **idempotentHint** | Idempotent Hint | Tells an MCP client that calling the tool again with the same arguments changes nothing more. A hint only, which Camel does not check. | boolean |  |  |
| **openWorldHint** | Open World Hint | Tells an MCP client that the tool works with systems outside the application, such as the internet. A hint only, which Camel does not check. | boolean |  |  |
| **readOnlyHint** | Read Only Hint | Tells an MCP client that the tool only reads data and changes nothing. A hint only, which Camel does not check. | boolean |  |  |
| **title** | Title | A name of the tool for people, which an MCP client may show instead of the tool name, such as `Order status`. | string |  | Order status |

## Dependencies

At runtime, the `ai-tool-source` Kamelet relies upon the presence of the following dependencies:

-   camel:ai-tool
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:ai-tool-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ai-tool-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ai-tool-source.kamelet.yaml)