# Spring AI Tools

**Since Camel 4.17**

**Both producer and consumer are supported**

The Spring AI Tools component provides support for integrating function calling capabilities with [Spring AI](https://docs.spring.io/spring-ai/reference/api/tools.md) chat models. This component enables AI models to invoke Camel routes as tools/functions, allowing the model to perform actions, retrieve data, or interact with external systems during conversations.

Function calling (also known as tool use) allows AI models to:

-   Execute Camel routes as callable functions
    
-   Retrieve data from external systems during conversations
    
-   Perform actions based on conversation context
    
-   Extend AI capabilities with custom business logic
    
-   Build Agentic AI applications
    

## URI format

spring-ai-tools:toolId\[?options\]

Where **toolId** is a unique identifier for the tool or tool set

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

The Spring AI Tools component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | The configuration. |  | SpringAiToolsConfiguration |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Spring AI Tools endpoint is configured using URI syntax:

spring-ai-tools:toolId

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **toolId** (common) | **Required** The tool id. |  | String |

### Query Parameters (10 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **tags** (common) | **Required** The tags for the tools. |  | String |
| **description** (consumer) | Tool description. |  | String |
| **inputType** (consumer) | Input type class for the tool. |  | Class |
| **name** (consumer) | Tool name. |  | String |
| **parameters** (consumer) | List of Tool parameters with optional metadata. Format: parameter.=, parameter..description=, parameter..required=, parameter..enum=. Example: parameter.location=string, parameter.location.description=The city and state, parameter.location.required=true, parameter.unit.enum=C,F. This is a multi-value option with prefix: parameter. |  | Map |
| **returnDirect** (consumer) | Whether the tool result should be returned directly or passed back to the model. Default is false, meaning the result is passed back to the model for further processing. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Usage

The Camel Spring AI Tools component is used as a consumer to expose Camel routes as tools that AI models can call. The route processes tool invocations and returns results to the model.

> **Important**
> This component is designed to work with the [Spring AI Chat Component](spring-ai-chat-component.md). Define tools using `spring-ai-tools` consumer endpoints, then use them via `spring-ai-chat` with the `tags` parameter. See the [Integration with Spring AI Chat Component](#_integration_with_spring_ai_chat_component) section below for details.

### Basic Tool Definition

_Java-only: Java DSL with class literal parameter_

```java
from("spring-ai-tools:weatherTool?tags=weather&description=Get current weather for a location")
    .log("Getting weather for ${header.location}")
    .to("https://api.weather.example.com/current")
    .convertBodyTo(String.class);
```

The AI model can invoke this tool when it needs weather information, and the route will execute to retrieve the data.

### Tool with Parameters

Tools can define typed parameters using the `parameter.*` prefix:

_Java-only: Java lambda Processor with string concatenation_

```java
from("spring-ai-tools:weatherTool?tags=weather" +
    "&description=Get weather forecast" +
    "&name=getWeather" +
    "&parameter.location=string" +
    "&parameter.location.description=The city and state" +
    "&parameter.location.required=true" +
    "&parameter.unit=string" +
    "&parameter.unit.description=Temperature unit" +
    "&parameter.unit.enum=C,F" +
    "&parameter.unit.required=false")
    .log("Location: ${header.location}, Unit: ${header.unit}")
    .process(exchange -> {
        String location = exchange.getIn().getHeader("location", String.class);
        String unit = exchange.getIn().getHeader("unit", String.class);
        // Fetch and process weather data
        exchange.getIn().setBody("Weather data for " + location);
    });
```

Parameter metadata is passed to the AI model to help it understand how to call the tool.

### Using Java Classes for Input

Instead of parameter maps, you can use a Java class to define the tool’s input schema:

_Java-only: Java class definition with lambda Processor_

```java
public class WeatherRequest {
    private String location;
    private String unit;
    // getters and setters
}

from("spring-ai-tools:weatherTool?tags=weather" +
    "&description=Get weather forecast" +
    "&inputType=com.example.WeatherRequest")
    .log("Processing weather request")
    .process(exchange -> {
        // Headers are set from the input object fields
        String location = exchange.getIn().getHeader("location", String.class);
        exchange.getIn().setBody("Weather for " + location);
    });
```

### Return Direct Mode

By default, tool results are passed back to the AI model for further processing. Use `returnDirect=true` to return the tool’s result directly to the user:

_Java-only: Java lambda Processor_

```java
from("spring-ai-tools:calculator?tags=math" +
    "&description=Calculate mathematical expressions" +
    "&returnDirect=true")
    .process(exchange -> {
        // Calculate and return result immediately to user
        exchange.getIn().setBody("Result: 42");
    });
```

### Tool Organization with Tags

Tags are used to organize and group tools. The [Spring AI Chat Component](spring-ai-chat-component.md) uses tags to discover which tools should be available to the AI model:

_Java-only: Java lambda Processor with multiple routes_

```java
// Define tools with tags
from("spring-ai-tools:weatherTool?tags=weather,external-api" +
    "&description=Get current weather for a location")
    .to("https://weather-api.example.com");

from("spring-ai-tools:timeTool?tags=time,utility" +
    "&description=Get current time")
    .process(exchange -> exchange.getIn().setBody(LocalDateTime.now().toString()));

// Use tools via spring-ai-chat component with tags
from("direct:weatherChat")
    .to("spring-ai-chat:chat?tags=weather,time&chatClient=#chatClient"); // Both tools available

from("direct:utilityChat")
    .to("spring-ai-chat:chat?tags=utility&chatClient=#chatClient"); // Only time tool available
```

A single tool can have multiple tags, allowing flexible tool organization and reuse across different chat contexts.

### Error Handling

If a tool execution fails, the error is propagated back to the AI model, which can handle it or report it to the user:

_Java-only: Java onException handler_

```java
from("spring-ai-tools:riskyOperation?tags=ops&description=Perform risky operation")
    .onException(Exception.class)
        .handled(true)
        .setBody(simple("Error occurred: ${exception.message}"))
    .end()
    .to("direct:performOperation");
```

## Complete Example

Here’s a complete example showing tool registration and usage:

_Java-only: Java RouteBuilder class_

```java
// Register a database query tool
from("spring-ai-tools:queryDb?tags=database" +
    "&description=Query the customer database" +
    "&parameter.query=string" +
    "&parameter.query.description=SQL query to execute" +
    "&parameter.query.required=true")
    .to("jdbc:dataSource")
    .convertBodyTo(String.class);

// Register a notification tool
from("spring-ai-tools:sendNotification?tags=notifications" +
    "&description=Send notification to user" +
    "&parameter.message=string" +
    "&parameter.message.required=true" +
    "&returnDirect=true")
    .to("telegram:bots")
    .setBody(constant("Notification sent"));

// Chat endpoint with access to both tools
from("direct:assistantChat")
    .to("spring-ai-chat:assistant?tags=database,notifications&chatClient=#chatClient")
    .log("Response: ${body}");
```

When a user sends "Show me all customers and notify me when done" to the assistant endpoint: 1. The model may call the `queryDb` tool to fetch customers 2. The model may then call `sendNotification` to inform the user 3. The final response is returned

## Headers

When a tool is invoked, all tool parameters are set as message headers. The parameter names correspond to header names:

_Java-only: Java lambda Processor_

```java
// Tool definition with parameter.location=string
from("spring-ai-tools:myTool?tags=t&parameter.location=string")
    .process(exchange -> {
        String location = exchange.getIn().getHeader("location", String.class);
        // Process with location parameter
    });
```

## Integration with Spring AI Chat Component

The Spring AI Tools component is designed to work seamlessly with the [Spring AI Chat Component](spring-ai-chat-component.md). Define tools using `spring-ai-tools` consumer endpoints, then reference them in `spring-ai-chat` endpoints using the `tags` parameter to enable function calling capabilities.

### How the Integration Works

When you configure the `tags` parameter on a `spring-ai-chat` endpoint:

1.  The chat component discovers all `spring-ai-tools` consumer endpoints registered with matching tags
    
2.  These tools are automatically registered with Spring AI’s ChatClient as available functions
    
3.  When a user sends a message, the LLM can decide to call these tools based on the conversation context
    
4.  The chat component executes the corresponding Camel routes and sends results back to the LLM
    
5.  The LLM processes tool results and generates the final response
    
6.  Multiple tools can be called in sequence if needed
    

### Complete Integration Example

_Java-only: Java RouteBuilder class_

```java
public class ChatWithToolsConfig {

    public RouteBuilder chatWithToolsRoutes() {
        return new RouteBuilder() {
            @Override
            public void configure() throws Exception {
                // Define tools using spring-ai-tools consumer
                from("spring-ai-tools:queryCustomers?tags=database" +
                     "&description=Search the customer database" +
                     "&parameter.searchTerm=string" +
                     "&parameter.searchTerm.description=Name or company to search for" +
                     "&parameter.searchTerm.required=true")
                    .to("sql:SELECT * FROM customers WHERE name LIKE '%${header.searchTerm}%'?dataSource=#dataSource")
                    .marshal().json();

                from("spring-ai-tools:sendEmail?tags=email" +
                     "&description=Send an email to a customer" +
                     "&parameter.email=string" +
                     "&parameter.subject=string" +
                     "&parameter.body=string")
                    .to("smtp://mailserver");

                from("spring-ai-tools:createInvoice?tags=billing" +
                     "&description=Create an invoice for a customer" +
                     "&parameter.customerId=string" +
                     "&parameter.amount=number")
                    .to("bean:invoiceService?method=create");

                // Chat endpoint with access to all tools
                from("direct:assistantChat")
                    .to("spring-ai-chat:assistant?tags=database,email,billing&chatClient=#chatClient");

                // Chat with specific tool subsets
                from("direct:customerServiceChat")
                    .to("spring-ai-chat:support?tags=database,email&chatClient=#chatClient");

                from("direct:billingChat")
                    .to("spring-ai-chat:billing?tags=database,billing&chatClient=#chatClient");
            }
        };
    }
}

// Usage examples
String response1 = template.requestBody("direct:assistantChat",
    "Find customers with 'Smith' in their name and send them a promotional email", String.class);

String response2 = template.requestBody("direct:billingChat",
    "Create an invoice for customer ABC123 for $500", String.class);
```

## See Also

-   [Spring AI Chat Component](spring-ai-chat-component.md)
    
-   [Spring AI Documentation](https://docs.spring.io/spring-ai/reference/)
    
-   [Spring AI Function Calling](https://docs.spring.io/spring-ai/reference/api/tools.md)