# LangChain4j Tools

> **Warning**
> **Deprecated:** This langchain4j-tools is deprecated and may be removed in a future release.

**Since Camel 4.8**

**Both producer and consumer are supported**

> **Warning**
> This component is deprecated since Camel 4.22. Use [camel-ai-tool](ai-tool-component.md) to define tools and [camel-langchain4j-agent](langchain4j-agent-component.md) to invoke them.

The LangChain4j Tools Component allows you to use function calling features from Large Language Models (LLMs) supported by [LangChain4j](https://github.com/langchain4j/langchain4j).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-langchain4j-tools</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

Producer

langchain4j-tools:toolSet\[?options\]

Consumer

langchain4j-tools:toolSet\[?options\]

Where **toolSet** can be any string to uniquely identify the endpoint

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

The LangChain4j Tools component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | The configuration. |  | LangChain4jToolsConfiguration |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **chatModel** (advanced) | **Autowired** Chat Model of type dev.langchain4j.model.chat.ChatModel. |  | ChatModel |

## Endpoint Options

The LangChain4j Tools endpoint is configured using URI syntax:

langchain4j-tools:toolId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **toolId** (common) | **Required** The tool id. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **tags** (common) | **Required** The tags for the tools. |  | String |
| **description** (consumer) | Tool description. |  | String |
| **exposed** (consumer) | Whether the tool is automatically exposed to the LLM. When false, the tool is added to a searchable list and can be discovered via the tool-search-tool. | true | boolean |
| **name** (consumer) | Tool name. |  | String |
| **parameters** (consumer) | List of Tool parameters with optional metadata. Format: parameter.=, parameter..description=, parameter..required=, parameter..enum=. Example: parameter.location=string, parameter.location.description=The city and state, parameter.location.required=true, parameter.unit.enum=celsius,fahrenheit. This is a multi-value option with prefix: parameter. |  | Map |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **camelToolParameter** (consumer (advanced)) | Tool’s Camel Parameters, programmatically define Tool description and parameters. |  | CamelSimpleToolParameter |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **maxToolCallingRoundTrips** (producer) | Maximum number of tool-calling round trips (iterations) allowed before stopping. This prevents infinite loops when the LLM keeps requesting tool calls indefinitely. Each round trip consists of one LLM call and the execution of all tools requested in that call. Set to 0 for unlimited (not recommended). | 10 | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **chatModel** (advanced) | **Autowired** Chat Model of type dev.langchain4j.model.chat.ChatModel. |  | ChatModel |

## Message Headers

The LangChain4j Tools component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelLangChain4jToolsFinishReason** (common) Constant: [`FINISH_REASON`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-tools/latest/org/apache/camel/component/langchain4j/tools/LangChain4jToolsHeaders.html#FINISH_REASON) | 
The Finish Reason.

Enum values:

-   STOP
    
-   LENGTH
    
-   TOOL\_EXECUTION
    
-   CONTENT\_FILTER
    
-   OTHER
    





 |  | FinishReason |
| **CamelLangChain4jToolsInputTokenCount** (common) Constant: [`INPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-tools/latest/org/apache/camel/component/langchain4j/tools/LangChain4jToolsHeaders.html#INPUT_TOKEN_COUNT) | The Input Token Count. |  | int |
| **CamelLangChain4jToolsOutputTokenCount** (common) Constant: [`OUTPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-tools/latest/org/apache/camel/component/langchain4j/tools/LangChain4jToolsHeaders.html#OUTPUT_TOKEN_COUNT) | The Output Token Count. |  | int |
| **CamelLangChain4jToolsTotalTokenCount** (common) Constant: [`TOTAL_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-tools/latest/org/apache/camel/component/langchain4j/tools/LangChain4jToolsHeaders.html#TOTAL_TOKEN_COUNT) | The Total Token Count. |  | int |

## Usage

This component helps to use function-calling features from LLMs so that models can decide what functions (routes, in case of Camel) can be called (i.e.; routed).

Consider, for instance, two consumer routes capable of query an user database by user ID or by social security number (SSN).

Queries user by ID

-   Java
    
-   XML
    
-   YAML
    

```java
from("langchain4j-tools:userInfo?tags=users&description=Query database by user ID")
    .to("sql:SELECT name FROM users WHERE id = :#number");
```

```xml
<route>
  <from uri="langchain4j-tools:userInfo?tags=users&amp;description=Query database by user ID"/>
  <to uri="sql:SELECT name FROM users WHERE id = :#number"/>
</route>
```

```yaml
- route:
    from:
      uri: langchain4j-tools:userInfo
      parameters:
        tags: users
        description: Query database by user ID
      steps:
        - to:
            uri: "sql:SELECT name FROM users WHERE id = :#number"
```

Queries user by SSN

-   Java
    
-   XML
    
-   YAML
    

```java
from("langchain4j-tools:userInfo?tags=users&description=Query database by user social security ID")
    .to("sql:SELECT name FROM users WHERE ssn = :#ssn");
```

```xml
<route>
  <from uri="langchain4j-tools:userInfo?tags=users&amp;description=Query database by user social security ID"/>
  <to uri="sql:SELECT name FROM users WHERE ssn = :#ssn"/>
</route>
```

```yaml
- route:
    from:
      uri: langchain4j-tools:userInfo
      parameters:
        tags: users
        description: Query database by user social security ID
      steps:
        - to:
            uri: "sql:SELECT name FROM users WHERE ssn = :#ssn"
```

Now, consider a producer route that receives unstructured data as input. Such a route could consume this data, pass it to a LLM with function-calling capabilities (such as [llama3.1](https://huggingface.co/meta-llama/Meta-Llama-3.1-8B), [Granite Code 20b function calling, etc](https://huggingface.co/ibm-granite/granite-20b-functioncalling)) and have the model decide which route to call.

Such a route could receive questions in english such as:

-   _"What is the name of the user with user ID 1?"_
    
-   _"What is the name of the user with SSN 34.400.96?"_
    

_Java-only: uses a Java variable for the source endpoint_

```java
from(source)
    .to("langchain4j-tools:userInfo?tags=users");
```

### Tool Tags

Consumer routes must define tags that groups [together](https://en.wikipedia.org/wiki/Set_theory). The aforementioned routes would be part have the `users` tag. The `users` tag has two routes: `queryById` and `queryBySSN`

### Parameters

The Tool Input parameter can be defined as an Endpoint multiValue option in the form of `parameter.<name>=<type>`, or via the endpoint option `camelToolParameter` for a programmatic approach. The parameters can be found as headers in the consumer route, in particular, if you define `parameter.userId=5`, in the consumer route `${header.userId}` can be used.

Parameters support optional metadata:

-   `parameter.<name>=<type>` — defines the parameter type (`string`, `integer`, `number`, `boolean`)
    
-   `parameter.<name>.description=<text>` — defines a description passed to the LLM
    
-   `parameter.<name>.required=<true|false>` — marks the parameter as required (default: `false`)
    
-   `parameter.<name>.enum=<value1,value2>` — restricts the parameter to a set of allowed values (comma-separated)
    

Producer and consumer example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:test")
    .to("langchain4j-tools:test1?tags=users");

from("langchain4j-tools:test1?tags=users&description=Query user database by user ID&parameter.userId=integer")
    .to("sql:SELECT name FROM users WHERE id = :#userId");
```

```xml
<route>
  <from uri="direct:test"/>
  <to uri="langchain4j-tools:test1?tags=users"/>
</route>

<route>
  <from uri="langchain4j-tools:test1?tags=users&amp;description=Query user database by user ID&amp;parameter.userId=integer"/>
  <to uri="sql:SELECT name FROM users WHERE id = :#userId"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:test
      steps:
        - to:
            uri: langchain4j-tools:test1
            parameters:
              tags: users

- route:
    from:
      uri: langchain4j-tools:test1
      parameters:
        tags: users
        description: Query user database by user ID
        parameter.userId: integer
      steps:
        - to:
            uri: "sql:SELECT name FROM users WHERE id = :#userId"
```

_Java-only: uses string concatenation for URI and process callback_

```java
from("langchain4j-tools:weather?tags=weather&description=Get weather forecast"
    + "&parameter.location=string"
    + "&parameter.location.description=The city and state"
    + "&parameter.location.required=true"
    + "&parameter.unit=string"
    + "&parameter.unit.description=Temperature unit"
    + "&parameter.unit.enum=celsius,fahrenheit")
    .process(exchange -> {
        String location = exchange.getIn().getHeader("location", String.class);
        // ...
    });
```

When using the programmatic `CamelSimpleToolParameter` approach, required parameters can be specified as a list of parameter names. The full constructor also accepts `additionalProperties` (to restrict extra fields) and `definitions` (for recursive schemas using `JsonReferenceSchema`):

```java
CamelSimpleToolParameter toolParameter = new CamelSimpleToolParameter(
    "Get weather forecast",
    List.of(
        new NamedJsonSchemaProperty("location",
            JsonStringSchema.builder().description("The city and state").build()),
        new NamedJsonSchemaProperty("unit",
            JsonEnumSchema.builder().enumValues("celsius", "fahrenheit")
                .description("Temperature unit").build())),
    List.of("location"),  // required parameter names
    false,                // additionalProperties
    null);                // definitions (for recursive schemas)
```

Usage example:

```java
List<ChatMessage> messages = new ArrayList<>();
        messages.add(new SystemMessage("""
                You provide information about specific user name querying the database given a number.
                """));
        messages.add(new UserMessage("""
                What is the name of the user 1?
                """));

        Exchange message = fluentTemplate.to("direct:test").withBody(messages).request(Exchange.class);
```

### Tool Names

Each tool route is registered with a name that the LLM uses to invoke it. By default, the name is derived automatically from the `description` option by converting it to CamelCase. For example:

 
| Description | Generated Tool Name |
| --- | --- |
| `Query user database by user ID` | `QueryUserDatabaseByUserId` |
| `Get current promotions` | `GetCurrentPromotions` |
| `Amend an order by its ID` | `AmendAnOrderByItsID` |

You can override the generated name by setting the `name` option explicitly on the consumer endpoint:

-   Java
    
-   XML
    
-   YAML
    

```java
from("langchain4j-tools:test1?tags=orders&name=amendOrder&description=Amend an order by its ID&parameter.orderId=string")
    .setBody(constant("order amended"));
```

```xml
<route>
  <from uri="langchain4j-tools:test1?tags=orders&amp;name=amendOrder&amp;description=Amend an order by its ID&amp;parameter.orderId=string"/>
  <setBody>
    <constant>order amended</constant>
  </setBody>
</route>
```

```yaml
- route:
    from:
      uri: langchain4j-tools:test1
      parameters:
        tags: orders
        name: amendOrder
        description: Amend an order by its ID
        parameter.orderId: string
      steps:
        - setBody:
            constant: order amended
```

### Using stop() in Tool Routes

Tool routes can use the `stop()` EIP to discontinue route processing early. When the LLM invokes multiple tools in parallel, each tool route executes independently — `stop()` in one tool does not affect the others.

Example with two tools where one uses stop():

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-tools:test1?tags=orders")
    .log("response is: ${body}");

from("langchain4j-tools:test1?tags=orders&description=Amend an order by its ID&parameter.orderId=string")
    .setBody(constant("order amended"))
    .stop();

from("langchain4j-tools:test1?tags=orders&description=Get current promotions")
    .setBody(constant("{\"status\":\"ok\",\"promotions\":[\"10% off\"]}"));
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-tools:test1?tags=orders"/>
  <log message="response is: ${body}"/>
</route>

<route>
  <from uri="langchain4j-tools:test1?tags=orders&amp;description=Amend an order by its ID&amp;parameter.orderId=string"/>
  <setBody>
    <constant>order amended</constant>
  </setBody>
  <stop/>
</route>

<route>
  <from uri="langchain4j-tools:test1?tags=orders&amp;description=Get current promotions"/>
  <setBody>
    <constant>{"status":"ok","promotions":["10% off"]}</constant>
  </setBody>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-tools:test1
            parameters:
              tags: orders
        - log:
            message: "response is: ${body}"

- route:
    from:
      uri: langchain4j-tools:test1
      parameters:
        tags: orders
        description: Amend an order by its ID
        parameter.orderId: string
      steps:
        - setBody:
            constant: order amended
        - stop: {}

- route:
    from:
      uri: langchain4j-tools:test1
      parameters:
        tags: orders
        description: Get current promotions
      steps:
        - setBody:
            constant: '{"status":"ok","promotions":["10% off"]}'
```

When the LLM invokes both tools, each produces its own result. The `stop()` in the first tool does not prevent the second tool from executing, nor does it stop the calling route from continuing after the tools producer completes.

### Using a specific Model

The Camel LangChain4j tools component provides an abstraction for interacting with various types of Large Language Models (LLMs) supported by [LangChain4j](https://github.com/langchain4j/langchain4j).

#### Integrating with specific LLM

To integrate with a specific LLM, users should follow the steps described below, which explain how to integrate with OpenAI.

Add the dependency for LangChain4j OpenAI support:

Example

```xml
<dependency>
      <groupId>dev.langchain4j</groupId>
      <artifactId>langchain4j-open-ai</artifactId>
    <version>x.x.x</version>
</dependency>
```

Initialize the OpenAI Chat Language Model, and add it to the Camel Registry:

```java
ChatLanguageModel model = OpenAiChatModel.builder()
                .apiKey("NO_API_KEY")
                .modelName("llama3.1:latest")
                .temperature(0.0)
                .timeout(ofSeconds(60000))
                .build();
context.getRegistry().bind("chatModel", model);
```

Use the model in the Camel LangChain4j Chat Producer

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-tools:test?tags=users&chatModel=#chatModel");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-tools:test?tags=users&amp;chatModel=#chatModel"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-tools:test
            parameters:
              tags: users
              chatModel: "#chatModel"
```

> **Note**
> To switch to another Large Language Model and its corresponding dependency, replace the `langchain4j-open-ai` dependency with the appropriate dependency for the desired model. Update the initialization parameters accordingly in the code snippet provided above.

#### Handling no Tools Called

In some circumstances, the LLM may decide not to call a tool. This is a valid scenario that needs to be handled by application developers. To do so, developers can get the `LangChain4jTools.NO_TOOLS_CALLED_HEADER` from the exchange.

### Tool Search Tool

The Tool Search Tool is a native feature that allows LLMs to discover and access tools dynamically without consuming the entire context window with tool definitions.

#### Overview

When you have many tools available, exposing all of them to the LLM in every request can:

-   Consume significant context window space
    
-   Reduce the space available for actual conversation
    
-   Potentially confuse the LLM with too many options
    

The Tool Search Tool solves this by allowing you to mark certain tools as "searchable" (non-exposed). These tools are not automatically sent to the LLM but can be discovered when needed.

#### Using the `exposed` Parameter

By default, all tools are exposed to the LLM (`exposed=true`). To make a tool searchable instead:

-   Java
    
-   XML
    
-   YAML
    

```java
from("langchain4j-tools:queryBySSN?tags=users&description=Query user database by social security number&parameter.ssn=string&exposed=false")
    .to("sql:SELECT name FROM users WHERE ssn = :#ssn");
```

```xml
<route>
  <from uri="langchain4j-tools:queryBySSN?tags=users&amp;description=Query user database by social security number&amp;parameter.ssn=string&amp;exposed=false"/>
  <to uri="sql:SELECT name FROM users WHERE ssn = :#ssn"/>
</route>
```

```yaml
- route:
    from:
      uri: langchain4j-tools:queryBySSN
      parameters:
        tags: users
        description: Query user database by social security number
        parameter.ssn: string
        exposed: false
      steps:
        - to:
            uri: "sql:SELECT name FROM users WHERE ssn = :#ssn"
```

#### How It Works

1.  When you define tools with `exposed=false`, they are added to a searchable tool registry
    
2.  A native `toolSearchTool` is automatically exposed to the LLM when searchable tools exist
    
3.  The LLM can invoke `toolSearchTool` with tags to discover available tools
    
4.  The search results are returned to the LLM, which can then decide which tools to use
    

#### Example: Mixed Exposed and Searchable Tools

-   Java
    
-   XML
    
-   YAML
    

```java
// This tool is immediately available to the LLM
from("langchain4j-tools:queryById?tags=users&description=Query user database by user ID&parameter.userId=integer")
    .to("sql:SELECT name FROM users WHERE id = :#userId");

// This tool is searchable but not immediately exposed
from("langchain4j-tools:queryBySSN?tags=users&description=Query user database by social security number&parameter.ssn=string&exposed=false")
    .to("sql:SELECT name FROM users WHERE ssn = :#ssn");

// Another searchable tool with different tags
from("langchain4j-tools:sendEmail?tags=users,email&description=Send email to a user&parameter.email=string&parameter.message=string&exposed=false")
    .to("smtp://mailserver");
```

```xml
<!-- This tool is immediately available to the LLM -->
<route>
  <from uri="langchain4j-tools:queryById?tags=users&amp;description=Query user database by user ID&amp;parameter.userId=integer"/>
  <to uri="sql:SELECT name FROM users WHERE id = :#userId"/>
</route>

<!-- This tool is searchable but not immediately exposed -->
<route>
  <from uri="langchain4j-tools:queryBySSN?tags=users&amp;description=Query user database by social security number&amp;parameter.ssn=string&amp;exposed=false"/>
  <to uri="sql:SELECT name FROM users WHERE ssn = :#ssn"/>
</route>

<!-- Another searchable tool with different tags -->
<route>
  <from uri="langchain4j-tools:sendEmail?tags=users,email&amp;description=Send email to a user&amp;parameter.email=string&amp;parameter.message=string&amp;exposed=false"/>
  <to uri="smtp://mailserver"/>
</route>
```

```yaml
# This tool is immediately available to the LLM
- route:
    from:
      uri: langchain4j-tools:queryById
      parameters:
        tags: users
        description: Query user database by user ID
        parameter.userId: integer
      steps:
        - to:
            uri: "sql:SELECT name FROM users WHERE id = :#userId"

# This tool is searchable but not immediately exposed
- route:
    from:
      uri: langchain4j-tools:queryBySSN
      parameters:
        tags: users
        description: Query user database by social security number
        parameter.ssn: string
        exposed: false
      steps:
        - to:
            uri: "sql:SELECT name FROM users WHERE ssn = :#ssn"

# Another searchable tool with different tags
- route:
    from:
      uri: langchain4j-tools:sendEmail
      parameters:
        tags: "users,email"
        description: Send email to a user
        parameter.email: string
        parameter.message: string
        exposed: false
      steps:
        - to:
            uri: smtp://mailserver
```

In this example:

-   The `queryById` tool is immediately available to the LLM
    
-   The `queryBySSN` and `sendEmail` tools can be discovered by searching for tags like "users" or "email"
    
-   The LLM can use the `toolSearchTool` to find these additional capabilities when needed
    

#### Benefits

-   **Reduced Context Usage**: Only expose the most commonly used tools initially
    
-   **Scalability**: Support hundreds or thousands of tools without overwhelming the LLM
    
-   **Dynamic Discovery**: Let the LLM discover tools as needed based on the conversation
    
-   **Better Organization**: Group related tools by tags for easier discovery
    

#### Best Practices

When using the Tool Search Tool feature, consider the following best practices:

-   **Tag Strategy**: Use meaningful, hierarchical tags (e.g., "users", "users.admin", "database.users") to organize tools logically
    
-   **Expose Common Tools**: Keep frequently used tools exposed (`exposed=true`) and make specialized tools searchable (`exposed=false`)
    
-   **Performance Considerations**: While the search is efficient, having thousands of searchable tools may impact search performance. Consider grouping tools by functional area
    
-   **LLM Guidance**: In your system message, inform the LLM about the availability of the `toolSearchTool` and when to use it
    
-   **Tag Naming**: Use consistent, lowercase tag names without special characters for best compatibility
    
-   **Tool Descriptions**: Write clear, descriptive tool descriptions as they are returned in search results to help the LLM choose the right tool
    
-   **Testing**: Test your tool organization with real queries to ensure the LLM can discover and use tools effectively
    

#### Limitations

-   The LLM must be instructed to use the `toolSearchTool` - it won’t automatically know to search for tools
    
-   Search is based on exact tag matching - fuzzy matching or semantic search is not currently supported
    
-   The feature requires an LLM with good function-calling capabilities to work effectively