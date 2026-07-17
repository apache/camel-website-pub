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

The AI Tool component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **configuration** (consumer) | The component configuration. |  | AiToolConfiguration |
| **description** (consumer) | Human-readable description of what this tool does. Passed verbatim to the LLM; be precise and action-oriented. When omitted, defaults to the tool name. |  | String |
| **parameters** (consumer) | Tool input parameters. Format: parameter.NAME=TYPE, parameter.NAME.description=TEXT, parameter.NAME.required=true or false, parameter.NAME.enum=val1,val2. Supported types: string, integer, number, boolean. This is a multi-value option with prefix: parameter. |  | Map |
| **tags** (consumer) | Comma-separated list of tags used to group tools. Producers filter the registry by these tags to select which tools to expose to the LLM. When omitted, the tool goes into a default pool available to all producers. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The AI Tool endpoint is configured using URI syntax:

ai-tool:toolName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **toolName** (consumer) | **Required** The tool name. This is the name the LLM sees and uses to invoke the tool. |  | String |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **description** (consumer) | Human-readable description of what this tool does. Passed verbatim to the LLM; be precise and action-oriented. When omitted, defaults to the tool name. |  | String |
| **parameters** (consumer) | Tool input parameters. Format: parameter.NAME=TYPE, parameter.NAME.description=TEXT, parameter.NAME.required=true or false, parameter.NAME.enum=val1,val2. Supported types: string, integer, number, boolean. This is a multi-value option with prefix: parameter. |  | Map |
| **tags** (consumer) | Comma-separated list of tags used to group tools. Producers filter the registry by these tags to select which tools to expose to the LLM. When omitted, the tool goes into a default pool available to all producers. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

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

## See Also

-   [LangChain4j Agent Component](langchain4j-agent-component.md) — will discover ai-tool tools in a future release
    
-   [Spring AI Chat Component](spring-ai-chat-component.md) — will discover ai-tool tools in a future release