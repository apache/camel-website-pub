# LangChain4j Chat

**Since Camel 4.5**

**Both producer and consumer are supported**

The LangChain4j Chat Component allows you to integrate with any Large Language Model (LLM) supported by [LangChain4j](https://github.com/langchain4j/langchain4j).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-langchain4j-chat</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

langchain4j-chat:chatId\[?options\]

Where **chatId** can be any string to uniquely identify the endpoint

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

The LangChain4j Chat component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **chatOperation** (common) | 
**Required** Operation in case of Endpoint of type CHAT. The value is one of the values of org.apache.camel.component.langchain4j.chat.LangChain4jChatOperations.

Enum values:

-   CHAT\_SINGLE\_MESSAGE
    
-   CHAT\_SINGLE\_MESSAGE\_WITH\_PROMPT
    
-   CHAT\_MULTIPLE\_MESSAGES
    





 | CHAT\_SINGLE\_MESSAGE | LangChain4jChatOperations |
| **configuration** (common) | The configuration. |  | LangChain4jChatConfiguration |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **chatModel** (advanced) | **Autowired** Chat Model of type dev.langchain4j.model.chat.ChatModel. |  | ChatModel |

## Endpoint Options

The LangChain4j Chat endpoint is configured using URI syntax:

langchain4j-chat:chatId

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **chatId** (common) | **Required** The id. |  | String |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **chatOperation** (common) | 
**Required** Operation in case of Endpoint of type CHAT. The value is one of the values of org.apache.camel.component.langchain4j.chat.LangChain4jChatOperations.

Enum values:

-   CHAT\_SINGLE\_MESSAGE
    
-   CHAT\_SINGLE\_MESSAGE\_WITH\_PROMPT
    
-   CHAT\_MULTIPLE\_MESSAGES
    





 | CHAT\_SINGLE\_MESSAGE | LangChain4jChatOperations |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **chatModel** (advanced) | **Autowired** Chat Model of type dev.langchain4j.model.chat.ChatModel. |  | ChatModel |

## Message Headers

The LangChain4j Chat component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelLangChain4jChatPromptTemplate** (common) Constant: [`PROMPT_TEMPLATE`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-chat/latest/org/apache/camel/component/langchain4j/chat/LangChain4jChat$Headers.html#PROMPT_TEMPLATE) | The prompt Template. |  | String |
| **CamelLangChain4jChatAugmentedData** (common) Constant: [`AUGMENTED_DATA`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-chat/latest/org/apache/camel/component/langchain4j/chat/LangChain4jChat$Headers.html#AUGMENTED_DATA) | Augmented Data for RAG. |  | String |

## Spring Boot Auto-Configuration

When using langchain4j-chat with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-langchain4j-chat-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.langchain4j-chat.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.langchain4j-chat.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.langchain4j-chat.chat-model** | Chat Model of type dev.langchain4j.model.chat.ChatModel. The option is a dev.langchain4j.model.chat.ChatModel type. |  | ChatModel |
| **camel.component.langchain4j-chat.chat-operation** | Operation in case of Endpoint of type CHAT. The value is one of the values of org.apache.camel.component.langchain4j.chat.LangChain4jChatOperations. | chat-single-message | LangChain4jChatOperations |
| **camel.component.langchain4j-chat.configuration** | The configuration. The option is a org.apache.camel.component.langchain4j.chat.LangChain4jChatConfiguration type. |  | LangChain4jChatConfiguration |
| **camel.component.langchain4j-chat.enabled** | Whether to enable auto configuration of the langchain4j-chat component. This is enabled by default. |  | Boolean |
| **camel.component.langchain4j-chat.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |

## Usage

### Using a specific Chat Model

The Camel LangChain4j chat component provides an abstraction for interacting with various types of Large Language Models (LLMs) supported by [LangChain4j](https://github.com/langchain4j/langchain4j).

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

Initialize the OpenAI Chat Model, and add it to the Camel Registry:

```java
ChatModel model = OpenAiChatModel.builder()
                .apiKey(openApiKey)
                .modelName(GPT_3_5_TURBO)
                .temperature(0.3)
                .timeout(ofSeconds(3000))
                .build();
context.getRegistry().bind("chatModel", model);
```

Use the model in the Camel LangChain4j Chat Producer

```java
 from("direct:chat")
      .to("langchain4j-chat:test?chatModel=#chatModel")
```

> **Note**
> To switch to another Large Language Model and its corresponding dependency, replace the `langchain4j-open-ai` dependency with the appropriate dependency for the desired model. Update the initialization parameters accordingly in the code snippet provided above.

### Send a prompt with variables

To send a prompt with variables, use the Operation type `LangChain4jChatOperations.CHAT_SINGLE_MESSAGE_WITH_PROMPT`. This operation allows you to send a single prompt message with dynamic variables, which will be replaced with values provided in the request.

Route example:

```java
 from("direct:chat")
      .to("langchain4j-chat:test?chatModel=#chatModel&chatOperation=CHAT_SINGLE_MESSAGE_WITH_PROMPT")
```

Usage example:

```java
var promptTemplate = "Create a recipe for a {{dishType}} with the following ingredients: {{ingredients}}";

Map<String, Object> variables = new HashMap<>();
variables.put("dishType", "oven dish");
variables.put("ingredients", "potato, tomato, feta, olive oil");

String response = template.requestBodyAndHeader("direct:chat", variables,
                LangChain4jChat.Headers.PROMPT_TEMPLATE, promptTemplate, String.class);
```

### Chat with history

You can send a new prompt along with the chat message history by passing all messages in a list of type `dev.langchain4j.data.message.ChatMessage`. Use the Operation type `LangChain4jChatOperations.CHAT_MULTIPLE_MESSAGES`. This operation allows you to continue the conversation with the context of previous messages.

Route example:

```java
 from("direct:chat")
      .to("langchain4j-chat:test?chatModel=#chatModel&chatOperation=CHAT_MULTIPLE_MESSAGES")
```

Usage example:

```java
List<ChatMessage> messages = new ArrayList<>();
messages.add(new SystemMessage("You are asked to provide recommendations for a restaurant based on user reviews."));
// Add more chat messages as needed

String response = template.requestBody("direct:send-multiple", messages, String.class);
```

### Retrieval Augmented Generation (RAG)

Use the RAG feature to enrich exchanges with data retrieved from any type of Camel endpoint. The feature is compatible with all LangChain4 Chat operations and is ideal for orchestrating the RAG workflow, utilizing the extensive library of components and Enterprise Integration Patterns (EIPs) available in Apache Camel.

There are two ways for utilizing the RAG feature:

#### Using RAG with Content Enricher and LangChain4jRagAggregatorStrategy

Enrich the exchange by retrieving a list of strings using any Camel producer. The `LangChain4jRagAggregatorStrategy` is specifically designed to augment data within LangChain4j chat producers.

Usage example:

```java
// Create an instance of the RAG aggregator strategy
LangChain4jRagAggregatorStrategy aggregatorStrategy = new LangChain4jRagAggregatorStrategy();

from("direct:test")
     .enrich("direct:rag", aggregatorStrategy)
     .to("langchain4j-chat:test1?chatOperation=CHAT_SIMPLE_MESSAGE");

  from("direct:rag")
          .process(exchange -> {
                List<String> augmentedData = List.of("data 1", "data 2" );
                exchange.getIn().setBody(augmentedData);
              });
```

> **Note**
> This method leverages a separate Camel route to fetch and process the augmented data.

It is possible to enrich the message from multiple sources within the same exchange.

Usage example:

```java
// Create an instance of the RAG aggregator strategy
LangChain4jRagAggregatorStrategy aggregatorStrategy = new LangChain4jRagAggregatorStrategy();

from("direct:test")
     .enrich("direct:rag-from-source-1", aggregatorStrategy)
     .enrich("direct:rag-from-source-2", aggregatorStrategy)
     .to("langchain4j-chat:test1?chatOperation=CHAT_SIMPLE_MESSAGE");
```

#### Using RAG with headers

Directly add augmented data into the header. This method is particularly efficient for straightforward use cases where the augmented data is predefined or static. You must add augmented data as a List of `dev.langchain4j.rag.content.Content` directly inside the header `CamelLangChain4jChatAugmentedData`.

Usage example:

```java
import dev.langchain4j.rag.content.Content;

...

Content augmentedContent = new Content("data test");
List<Content> contents = List.of(augmentedContent);

String response = template.requestBodyAndHeader("direct:send-multiple", messages, LangChain4jChat.Headers.AUGMENTED_DATA , contents, String.class);
```