# AI Prompt

**Since Camel 4.24**

**Only consumer is supported**

The AI Prompt component exposes Camel routes as reusable prompt templates through an MCP server. Each prompt has a name, description, optional title and a set of string arguments. MCP clients discover the prompt with `prompts/list` and request the rendered messages with `prompts/get`.

Maven users will need the following dependency:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ai-prompt</artifactId>
    <version>x.x.x</version>
</dependency>
```

## URI format

ai-prompt:promptName\[?options\]

The **promptName** is the stable identifier shown to MCP clients.

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

The AI Prompt component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **arguments** (consumer) | Prompt arguments. Configure each argument with argument.NAME.description=TEXT and/or argument.NAME.required=true or false. An argument is declared by either option. This is a multi-value option with prefix: argument. |  | Map |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **configuration** (consumer) | The component configuration. |  | AiPromptConfiguration |
| **description** (consumer) | Human-readable description of what this prompt provides. When omitted, defaults to the prompt name. |  | String |
| **tags** (consumer) | Comma-separated list of tags used to group prompts. MCP servers select which prompts to expose using these tags. When omitted, the prompt goes into a default pool that is not exposed to remote clients. |  | String |
| **title** (consumer) | Optional display title for MCP prompt listings. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The AI Prompt endpoint is configured using URI syntax:

ai-prompt:promptName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **promptName** (consumer) | **Required** The prompt name advertised to MCP clients. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **arguments** (consumer) | Prompt arguments. Configure each argument with argument.NAME.description=TEXT and/or argument.NAME.required=true or false. An argument is declared by either option. This is a multi-value option with prefix: argument. |  | Map |
| **description** (consumer) | Human-readable description of what this prompt provides. When omitted, defaults to the prompt name. |  | String |
| **tags** (consumer) | Comma-separated list of tags used to group prompts. MCP servers select which prompts to expose using these tags. When omitted, the prompt goes into a default pool that is not exposed to remote clients. |  | String |
| **title** (consumer) | Optional display title for MCP prompt listings. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

## Message Body

The message body at each side of the AI Prompt component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `null` | No body is sent to the route. Each prompt argument is available as a message header with its configured argument name; values are strings. |
| **Consumer reply** | `text`, `list`, `bytes`, `stream` or `file` | A String, byte array, stream or file is converted to one user message. A List may contain Strings or Maps with role (user or assistant) and content. Content may be a String or an MCP content block. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

Each configured prompt argument is received by the route as a message header whose name is the argument name. MCP prompt arguments are strings. Configure an argument with `argument.NAME.description` and/or `argument.NAME.required`:

```java
from("ai-prompt:summarize_account"
    + "?tags=crm"
    + "&description=Summarize an account"
    + "&title=Account summary"
    + "&argument.accountId.description=The account identifier"
    + "&argument.accountId.required=true")
    .setBody(simple("Summarize account ${header.accountId}, including its status and recent activity."));
```

A String route body becomes one MCP `user` message. A List route body becomes several messages, allowing a multi-turn prompt. List elements may be Strings (converted to `user` messages) or Maps containing `role` (`user` or `assistant`) and `content`. Content may be a String or an MCP content block, such as an image or embedded resource content object.

```java
from("ai-prompt:review_code?tags=developer&argument.language.required=true")
    .process(exchange -> {
        String language = exchange.getMessage().getHeader("language", String.class);
        exchange.getMessage().setBody(List.of(
            "Review this " + language + " code for correctness and security.",
            Map.of("role", "assistant", "content", "I will focus on correctness, security and maintainability."),
            Map.of("role", "user", "content", "Return findings ordered by severity.")
        ));
    });
```

## Tags and exposure

Tags group prompts so an MCP server can select which prompts to expose. A prompt without tags is placed in a default pool and is not exposed to remote clients. Configure `camel.server.mcp-tags` to select prompt routes alongside `ai-tool` and `ai-resource` routes.

## Lifecycle and errors

A prompt is registered when its route starts or resumes and removed when it stops or suspends. Supporting MCP engines notify clients with `notifications/prompts/list_changed` when the prompt list changes.

Missing required arguments are rejected before the route executes. Route exceptions are logged server-side and returned to remote MCP clients as a generic prompt execution error. The MCP server applies a per-prompt execution timeout; a timed-out route may continue running on its worker thread until it completes.

## Security

The messages returned by a prompt route are sent to the MCP client and placed in the model’s context as they are. When a route builds a prompt from data that outsiders can write, such as ticket comments, emails or documents, that data can contain instructions aimed at the model (prompt injection). Camel does not filter or mark such content. Include only data from sources you trust, or clearly mark untrusted content in the prompt, for example by placing it in its own delimited block and telling the model to treat it as data.