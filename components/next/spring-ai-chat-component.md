# Spring AI Chat

**Since Camel 4.17**

**Only producer is supported**

The Spring AI Chat component allows you to integrate with any Large Language Model (LLM) supported by [Spring AI](https://docs.spring.io/spring-ai/reference/).

Maven users will need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spring-ai-chat</artifactId>
    <version>x.x.x</version>
</dependency>
```

## URI format

spring-ai-chat:chatId\[?options\]

Where **chatId** can be any string to uniquely identify the endpoint.

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

The Spring AI Chat component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **chatModel** (advanced) | The ChatModel instance to use for chat operations. |  | ChatModel |

## Endpoint Options

The Spring AI Chat endpoint is configured using URI syntax:

spring-ai-chat:chatId

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **chatId** (producer) | The ID of the chat endpoint. |  | String |

### Query Parameters (35 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **chatClient** (producer) | **Autowired** The ChatClient instance to use for chat operations. ChatClient provides advanced features like memory management and advisors. If not provided, a ChatClient will be created from the ChatModel. |  | ChatClient |
| **chatModel** (producer) | **Autowired** The ChatModel instance to use for chat operations. This is used to create a ChatClient if one is not explicitly provided. |  | ChatModel |
| **chatOperation** (producer) | 
**Required** The chat operation to perform.

Enum values:

-   CHAT\_SINGLE\_MESSAGE
    
-   CHAT\_SINGLE\_MESSAGE\_WITH\_PROMPT
    
-   CHAT\_MULTIPLE\_MESSAGES
    





 | CHAT\_SINGLE\_MESSAGE | SpringAiChatOperations |
| **systemMessage** (producer) | Default system message to set context for the conversation. Can be overridden by the CamelSpringAiChatSystemMessage header. |  | String |
| **tags** (producer) | Tags for discovering and calling Camel route tools. |  | String |
| **toolNames** (producer) | Comma-separated tool names for selecting tools by name via Spring AI’s ToolCallbackResolver. This enables selecting Spring Tool annotated beans or any registered ToolCallback by name. |  | String |
| **userMessage** (producer) | Default user message text for multimodal requests. Can be combined with media data in the message body. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **advisors** (advanced) | List of custom advisors to add to the ChatClient. These advisors will be added after the built-in advisors (SimpleLogger, SafeGuard, ChatMemory, QuestionAnswer) in the order they are provided in the list. |  | List |
| **chatMemory** (advanced) | **Autowired** ChatMemory instance for maintaining conversation history across requests. When provided, conversation context will be automatically managed using MessageChatMemoryAdvisor. |  | ChatMemory |
| **chatMemoryVectorStore** (advanced) | VectorStore instance for maintaining conversation history using semantic search. When provided, conversation context will be automatically managed using VectorStoreChatMemoryAdvisor. This is an alternative to chatMemory that uses vector embeddings for long-term memory with semantic retrieval. |  | VectorStore |
| **entityClass** (advanced) | The Java class to use for entity response conversion using ChatClient.entity(Class). When specified, the response will be automatically converted to this type instead of returning a String. |  | Class |
| **maxFileSize** (advanced) | Maximum file size in bytes for multimodal content (images, audio, PDFs, etc.). Files exceeding this size will be rejected with an exception. Default is 1048576 bytes (1MB). Set to 0 to disable size checking (not recommended). | 1048576 | long |
| **maxTokens** (advanced) | Maximum tokens in the response. |  | Integer |
| **mcpServer** (advanced) | MCP server configurations. Define servers using prefix notation: mcpServer..transportType=stdiosse, mcpServer..command= (stdio), mcpServer..args= (stdio), mcpServer..url= (sse), mcpServer..oauthProfile= (OAuth profile for HTTP auth, requires camel-oauth). This is a multi-value option with prefix: mcpServer. |  | Map |
| **mcpTimeout** (advanced) | Timeout in seconds for MCP operations including tool execution and initialization. | 20 | int |
| **outputClass** (advanced) | The Java class to use for BEAN output format conversion. Required when outputFormat is BEAN. |  | Class |
| **outputFormat** (advanced) | The output format for structured output conversion (BEAN, MAP, LIST). Used in conjunction with outputClass for BEAN format. |  | String |
| **structuredOutputConverter** (advanced) | **Autowired** A StructuredOutputConverter for converting the chat response to structured output (e.g., BeanOutputConverter, MapOutputConverter, ListOutputConverter). When provided, the converter will be used to transform the response into the desired format. |  | StructuredOutputConverter |
| **structuredOutputValidation** (advanced) | Enable structured output validation with automatic retry on validation failure. When enabled, the StructuredOutputValidationAdvisor validates the response against a JSON Schema and re-prompts the LLM with validation errors if the output is invalid. | false | boolean |
| **structuredOutputValidationMaxAttempts** (advanced) | Maximum number of retry attempts for structured output validation. | 3 | int |
| **systemMetadata** (advanced) | Metadata to attach to system messages. This metadata can be used for tracking system prompt versions, model configurations, or other application-specific data. |  | Map |
| **temperature** (advanced) | Temperature parameter for response randomness (0.0-2.0). |  | Double |
| **toolCallbacks** (advanced) | **Autowired** List of ToolCallback instances to register alongside Camel route tools. Use MethodToolCallbackProvider.builder().toolObjects(bean).build().getToolCallbacks() to resolve callbacks from Tool-annotated beans. |  | List |
| **toolContext** (advanced) | Context map to pass to tools during execution. Tool methods accepting a ToolContext parameter will receive these values. |  | Map |
| **topKSampling** (advanced) | Top K parameter for sampling. |  | Integer |
| **topP** (advanced) | Top P parameter for nucleus sampling. |  | Double |
| **userMetadata** (advanced) | Metadata to attach to user messages. This metadata can be used for tracking conversation context, message identifiers, or other application-specific data. |  | Map |
| **ragTemplate** (rag) | Template for formatting RAG (Retrieval Augmented Generation) prompts when augmented data is provided. The template supports two placeholders: {context} for the retrieved documents and {question} for the user’s question. Default template is Context:\\n{context}\\n\\nQuestion: {question}. | Context:\\n{context}\\n\\nQuestion: {question} | String |
| **similarityThreshold** (rag) | Similarity threshold for RAG retrieval (default: 0.7). | 0.7 | double |
| **topK** (rag) | Number of top documents to retrieve for RAG (default: 5). | 5 | int |
| **vectorStore** (rag) | **Autowired** VectorStore for automatic RAG retrieval. |  | VectorStore |
| **safeguardFailureResponse** (security) | Failure response message for SafeGuard advisor when sensitive content is detected. If not specified, a default message will be used. |  | String |
| **safeguardSensitiveWords** (security) | Comma-separated list of sensitive words for SafeGuard advisor. When provided, the SafeGuard advisor will be enabled to prevent generation of content containing these words. |  | String |
| **safeguardOrder** (security (advanced)) | Order of execution for SafeGuard advisor. Lower numbers execute first. Default is 0. |  | Integer |

## Message Headers

The Spring AI Chat component supports 32 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSpringAiChatResponse** (producer) Constant: [`CHAT_RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#CHAT_RESPONSE) | The response from the chat model. |  | String |
| **CamelSpringAiInputTokenCount** (producer) Constant: [`INPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#INPUT_TOKEN_COUNT) | The number of input tokens used. |  | Integer |
| **CamelSpringAiOutputTokenCount** (producer) Constant: [`OUTPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#OUTPUT_TOKEN_COUNT) | The number of output tokens used. |  | Integer |
| **CamelSpringAiTotalTokenCount** (producer) Constant: [`TOTAL_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#TOTAL_TOKEN_COUNT) | The total number of tokens used. |  | Integer |
| **CamelSpringAiChatPromptTemplate** (producer) Constant: [`PROMPT_TEMPLATE`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#PROMPT_TEMPLATE) | The prompt template with placeholders for variable substitution. |  | String |
| **CamelSpringAiChatAugmentedData** (producer) Constant: [`AUGMENTED_DATA`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#AUGMENTED_DATA) | Augmented data for RAG as List. |  | List |
| **CamelSpringAiChatSystemMessage** (producer) Constant: [`SYSTEM_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#SYSTEM_MESSAGE) | System message for the conversation. |  | String |
| **CamelSpringAiChatTemperature** (producer) Constant: [`TEMPERATURE`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#TEMPERATURE) | Temperature parameter for response randomness (0.0-2.0). |  | Double |
| **CamelSpringAiChatMaxTokens** (producer) Constant: [`MAX_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#MAX_TOKENS) | Maximum tokens in the response. |  | Integer |
| **CamelSpringAiChatTopP** (producer) Constant: [`TOP_P`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#TOP_P) | Top P parameter for nucleus sampling. |  | Double |
| **CamelSpringAiChatTopK** (producer) Constant: [`TOP_K`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#TOP_K) | Top K parameter for sampling. |  | Integer |
| **CamelSpringAiChatUserMessage** (producer) Constant: [`USER_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#USER_MESSAGE) | User message text for multimodal requests. |  | String |
| **CamelSpringAiChatMediaData** (producer) Constant: [`MEDIA_DATA`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#MEDIA_DATA) | Media data for multimodal requests (image or audio). |  | byte\[\] |
| **CamelSpringAiChatMediaType** (producer) Constant: [`MEDIA_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#MEDIA_TYPE) | Media type (MIME type) for multimodal requests (e.g., image/png, audio/wav). |  | String |
| **CamelSpringAiChatOutputFormat** (producer) Constant: [`OUTPUT_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#OUTPUT_FORMAT) | The output format type for structured output conversion (BEAN, MAP, LIST). |  | String |
| **CamelSpringAiChatOutputClass** (producer) Constant: [`OUTPUT_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#OUTPUT_CLASS) | The Java class to use for structured output bean conversion. |  | Class |
| **CamelSpringAiChatStructuredOutput** (producer) Constant: [`STRUCTURED_OUTPUT`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#STRUCTURED_OUTPUT) | The structured output converted from the chat response. |  | Object |
| **CamelSpringAiChatSafeguardSensitiveWords** (producer) Constant: [`SAFEGUARD_SENSITIVE_WORDS`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#SAFEGUARD_SENSITIVE_WORDS) | Comma-separated list of sensitive words for SafeGuard advisor. |  | String |
| **CamelSpringAiChatSafeguardFailureResponse** (producer) Constant: [`SAFEGUARD_FAILURE_RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#SAFEGUARD_FAILURE_RESPONSE) | Failure response message for SafeGuard advisor when sensitive content is detected. |  | String |
| **CamelSpringAiChatSafeguardOrder** (producer) Constant: [`SAFEGUARD_ORDER`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#SAFEGUARD_ORDER) | Order of execution for SafeGuard advisor. |  | Integer |
| **CamelSpringAiChatAdvisors** (producer) Constant: [`ADVISORS`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#ADVISORS) | List of custom advisors to add to the request. |  | List |
| **CamelSpringAiChatEntityClass** (producer) Constant: [`ENTITY_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#ENTITY_CLASS) | The Java class to use for entity response conversion. |  | Class |
| **CamelSpringAiChatUserMetadata** (producer) Constant: [`USER_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#USER_METADATA) | Metadata to attach to user messages. |  | Map |
| **CamelSpringAiChatSystemMetadata** (producer) Constant: [`SYSTEM_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#SYSTEM_METADATA) | Metadata to attach to system messages. |  | Map |
| **CamelSpringAiChatConversationId** (producer) Constant: [`CONVERSATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#CONVERSATION_ID) | Conversation ID for managing separate conversation contexts in chat memory. |  | String |
| **CamelSpringAiChatMaxFileSize** (producer) Constant: [`MAX_FILE_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#MAX_FILE_SIZE) | Maximum file size in bytes for multimodal content. Overrides endpoint configuration. |  | Long |
| **CamelSpringAiChatFinishReason** (producer) Constant: [`FINISH_REASON`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#FINISH_REASON) | The reason why the chat response generation stopped (e.g., STOP, LENGTH, TOOL\_CALLS). |  | String |
| **CamelSpringAiChatModelName** (producer) Constant: [`MODEL_NAME`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#MODEL_NAME) | The name of the AI model used to generate the response. |  | String |
| **CamelSpringAiChatResponseId** (producer) Constant: [`RESPONSE_ID`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#RESPONSE_ID) | The unique ID of the chat response. |  | String |
| **CamelSpringAiChatResponseMetadata** (producer) Constant: [`RESPONSE_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#RESPONSE_METADATA) | Full response metadata as a Map containing all available metadata fields. |  | Map |
| **CamelSpringAiChatToolNames** (producer) Constant: [`TOOL_NAMES`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#TOOL_NAMES) | Comma-separated tool names for selecting tools by name via ToolCallbackResolver. |  | String |
| **CamelSpringAiChatToolContext** (producer) Constant: [`TOOL_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-chat/latest/org/apache/camel/component/springai/chat/SpringAiChatConstants.html#TOOL_CONTEXT) | Context map to pass to tools during execution. |  | Map |

## Usage

### Configuring the ChatModel

The component requires a Spring AI `ChatModel` to be configured. The component automatically creates a `ChatClient` internally and handles all the advanced features for you, including:

-   **ChatMemory**: Automatic conversation history management via MessageChatMemoryAdvisor or VectorStoreChatMemoryAdvisor
    
-   **VectorStore RAG**: Automatic context retrieval from vector databases via QuestionAnswerAdvisor
    
-   **SafeGuard**: Content filtering based on sensitive words
    
-   **Custom Advisors**: Any additional advisors you configure
    
-   **System Messages**: Default system prompts
    

Simply provide a `ChatModel` bean in your configuration, and the component will take care of the rest.

### Chat Operations

The component supports three types of chat operations:

1.  **CHAT\_SINGLE\_MESSAGE**: Send a simple text message to the LLM
    
2.  **CHAT\_SINGLE\_MESSAGE\_WITH\_PROMPT**: Use templates with variable substitution
    
3.  **CHAT\_MULTIPLE\_MESSAGES**: Support conversation history with multiple messages
    

#### Simple Chat (Single Message)

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("spring-ai-chat:test?chatModel=#chatModel");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="spring-ai-chat:test?chatModel=#chatModel"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: spring-ai-chat:test
            parameters:
              chatModel: "#chatModel"
```

_Java-only: ProducerTemplate test API_

```java
String response = template.requestBody("direct:chat", "What is the capital of Italy?", String.class);
```

#### Chat with Prompt Templates

Use the `CHAT_SINGLE_MESSAGE_WITH_PROMPT` operation to leverage Spring AI’s template engine:

_Java-only: ProducerTemplate test API with `Map.of()` and Spring AI constants_

```java
from("direct:chat")
    .to("spring-ai-chat:test?chatModel=#chatModel&chatOperation=CHAT_SINGLE_MESSAGE_WITH_PROMPT");

// Usage:
String promptTemplate = "Create a recipe for {{dish}} using {{ingredients}}";
Map<String, Object> variables = Map.of(
    "dish", "pasta carbonara",
    "ingredients", "eggs, cheek lard, parmesan, black pepper"
);

String response = template.requestBodyAndHeader(
    "direct:chat",
    variables,
    SpringAiChatConstants.PROMPT_TEMPLATE,
    promptTemplate,
    String.class
);
```

#### Conversation History (Multiple Messages)

Maintain conversation context by sending multiple messages:

_Java-only: uses Spring AI `Message` types and ProducerTemplate_

```java
import org.springframework.ai.chat.messages.*;

from("direct:chat")
    .to("spring-ai-chat:test?chatModel=#chatModel&chatOperation=CHAT_MULTIPLE_MESSAGES");

// Usage:
List<Message> conversation = new ArrayList<>();
conversation.add(new SystemMessage("You are a helpful cooking assistant."));
conversation.add(new UserMessage("What's a good pasta recipe?"));
conversation.add(new AssistantMessage("I recommend pasta carbonara..."));
conversation.add(new UserMessage("Can I make it vegetarian?"));

String response = template.requestBody("direct:chat", conversation, String.class);
```

### Retrieval Augmented Generation (RAG)

RAG allows you to augment prompts with relevant context from your data sources, enabling the LLM to answer questions based on your specific information.

#### Automatic RAG with VectorStore

Configure a VectorStore for automatic context retrieval:

_Java-only: programmatic VectorStore and registry configuration_

```java
import org.springframework.ai.vectorstore.VectorStore;
import org.springframework.ai.vectorstore.SimpleVectorStore;

// Create and populate vector store
VectorStore vectorStore = new SimpleVectorStore();
// ... add documents to vector store ...

context.getRegistry().bind("vectorStore", vectorStore);

from("direct:chat")
    .to("spring-ai-chat:test?chatModel=#chatModel&vectorStore=#vectorStore&topK=5");
```

The component will automatically:

1.  Take the user’s question
    
2.  Query the VectorStore for the most similar documents (top 5 by default)
    
3.  Augment the prompt with the retrieved context
    
4.  Send the enriched prompt to the LLM
    

#### RAG with Content Enricher Pattern

Use the `SpringAiRagAggregatorStrategy` with Camel’s Content Enricher EIP:

_Java-only: programmatic aggregation strategy configuration_

```java
import org.apache.camel.component.springai.chat.rag.SpringAiRagAggregatorStrategy;

SpringAiRagAggregatorStrategy aggregatorStrategy = new SpringAiRagAggregatorStrategy();

from("direct:chat")
    .enrich("direct:retrieve-context", aggregatorStrategy)
    .to("spring-ai-chat:test?chatModel=#chatModel");

from("direct:retrieve-context")
    .setBody(simple("Retrieved context based on question ${body}"));
```

#### RAG with Headers

Directly provide augmented data via the `AUGMENTED_DATA` header:

_Java-only: uses Spring AI `Document` type and ProducerTemplate_

```java
import org.springframework.ai.document.Document;
import static org.apache.camel.component.springai.chat.SpringAiChatConstants.AUGMENTED_DATA;

List<Document> context = List.of(
    new Document("The Eiffel Tower is located in Paris, France."),
    new Document("It was built in 1889 for the World's Fair.")
);

String response = template.requestBodyAndHeader(
    "direct:chat",
    "Where is the Eiffel Tower located?",
    AUGMENTED_DATA,
    context,
    String.class
);
```

### Controlling Response Parameters

#### Via Endpoint Configuration

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("spring-ai-chat:test?chatModel=#chatModel&temperature=0.8&maxTokens=500");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="spring-ai-chat:test?chatModel=#chatModel&amp;temperature=0.8&amp;maxTokens=500"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: spring-ai-chat:test
            parameters:
              chatModel: "#chatModel"
              temperature: 0.8
              maxTokens: 500
```

### Adding System Messages

System messages provide instructions or context to the LLM. You can configure them via endpoint parameters for default behavior:

_Java-only: route definition with ProducerTemplate usage_

```java
from("direct:chat")
    .to("spring-ai-chat:test?chatModel=#chatModel&systemMessage=You are a professional chef specializing in Italian cuisine.");

// Usage:
String response = template.requestBody("direct:chat",
    "What should I cook tonight?", String.class);
```

### Response Headers and Metadata

The component automatically tracks token usage and response metadata, providing them via headers. You can access these headers in your Camel routes:

_Java-only: route with `.log()` header interpolation and ProducerTemplate usage_

```java
from("direct:chat")
    .to("spring-ai-chat:test?chatModel=#chatModel")
    .log("Token usage - Input: ${header.CamelSpringAiInputTokenCount}")
    .log("Token usage - Output: ${header.CamelSpringAiOutputTokenCount}")
    .log("Token usage - Total: ${header.CamelSpringAiTotalTokenCount}")
    .log("Finish reason: ${header.CamelSpringAiChatFinishReason}")
    .log("Model used: ${header.CamelSpringAiChatModelName}");

// Usage:
template.requestBody("direct:chat", "Explain quantum computing", String.class);
```

The following headers are set after each chat operation:

**Token Usage Headers:**

-   `CamelSpringAiInputTokenCount` - Number of tokens in the prompt
    
-   `CamelSpringAiOutputTokenCount` - Number of tokens in the response
    
-   `CamelSpringAiTotalTokenCount` - Total tokens used (input + output)
    

**Response Metadata Headers:**

-   `CamelSpringAiChatFinishReason` - Why the generation stopped (e.g., "STOP", "LENGTH", "TOOL\_CALLS")
    
-   `CamelSpringAiChatModelName` - The name of the AI model used for the response
    
-   `CamelSpringAiChatResponseId` - Unique identifier for the response
    
-   `CamelSpringAiChatResponseMetadata` - Full metadata Map containing all available fields
    

> **Note**
> Not all AI models provide all metadata fields. The availability of specific metadata depends on the underlying model and provider. Most models provide at least finish reason and token counts.

### Message Metadata

The component supports attaching metadata to both user and system messages. This is useful for tracking message identifiers, conversation context, priority levels, or other application-specific data.

#### User Message Metadata

You can attach metadata to user messages via headers or endpoint configuration:

-   Java
    
-   XML
    
-   YAML
    

```java
// Using URL parameters - nested property syntax
from("direct:chat")
    .to("spring-ai-chat:test?chatModel=#chatModel"
        + "&userMetadata.messageId=msg-123"
        + "&userMetadata.userId=user-456"
        + "&userMetadata.priority=high");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="spring-ai-chat:test?chatModel=#chatModel&amp;userMetadata.messageId=msg-123&amp;userMetadata.userId=user-456&amp;userMetadata.priority=high"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: spring-ai-chat:test
            parameters:
              chatModel: "#chatModel"
              userMetadata.messageId: msg-123
              userMetadata.userId: user-456
              userMetadata.priority: high
```

#### System Message Metadata

Similarly, you can attach metadata to system messages:

-   Java
    
-   XML
    
-   YAML
    

```java
// Using URL parameters - nested property syntax
from("direct:chat")
    .to("spring-ai-chat:test?chatModel=#chatModel"
        + "&systemMetadata.version=1.0"
        + "&systemMetadata.model=gpt-4"
        + "&systemMetadata.promptVersion=2024-01");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="spring-ai-chat:test?chatModel=#chatModel&amp;systemMetadata.version=1.0&amp;systemMetadata.model=gpt-4&amp;systemMetadata.promptVersion=2024-01"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: spring-ai-chat:test
            parameters:
              chatModel: "#chatModel"
              systemMetadata.version: "1.0"
              systemMetadata.model: gpt-4
              systemMetadata.promptVersion: "2024-01"
```

### Conversation Memory

The component provides automatic conversation memory management via Spring AI’s ChatClient and ChatMemory. Two memory strategies are supported:

-   **MessageChatMemoryAdvisor** - Traditional message-based memory using ChatMemory implementations
    
-   **VectorStoreChatMemoryAdvisor** - Vector-based semantic memory using VectorStore for long-term retrieval
    

> **Important**
> Do not configure both `chatMemory` and `chatMemoryVectorStore` on the same endpoint. If both are provided, `chatMemory` (MessageChatMemoryAdvisor) will take precedence.

> **Note**
> Chat memory is only activated when the `CamelSpringAiChatConversationId` header is set on the exchange. Without this header, the memory advisor is not applied, even if `chatMemory` or `chatMemoryVectorStore` is configured. This allows you to selectively enable memory on a per-request basis.

#### Message-based Memory (ChatMemory)

Configure a `ChatMemory` on the endpoint for automatic conversation tracking using traditional message window approach. This strategy keeps a configurable number of recent messages in memory.

_Java-only: programmatic Spring AI `ChatMemory` setup and ProducerTemplate usage_

```java
// Create chat memory with message window
ChatMemory chatMemory = MessageWindowChatMemory.builder()
    .chatMemoryRepository(new InMemoryChatMemoryRepository())
    .maxMessages(10)  // Keep last 10 messages
    .build();

context.getRegistry().bind("chatMemory", chatMemory);

// Configure endpoint with memory
from("direct:chat")
    .to("spring-ai-chat:memory?chatModel=#chatModel&chatMemory=#chatMemory");

// Conversation ID for isolation
template.requestBodyAndHeader("direct:chat", "My name is Alice",
    SpringAiChatConstants.CONVERSATION_ID, "user-123", String.class);

template.requestBodyAndHeader("direct:chat", "What's my name?",
    SpringAiChatConstants.CONVERSATION_ID, "user-123", String.class); // Will remember: "Alice"
```

#### Vector-based Semantic Memory (ChatMemoryVectorStore)

For long-term memory with semantic retrieval capabilities, configure a `VectorStore` for chat memory. This strategy uses vector embeddings to enable semantic search over conversation history, making it ideal for retrieving contextually relevant information rather than just recent messages.

_Java-only: programmatic Ollama embedding model and VectorStore setup_

```java
OllamaApi ollamaApi = OllamaApi.builder()
                .baseUrl(OLLAMA.baseUrl())
                .build();

EmbeddingModel embeddingModel = OllamaEmbeddingModel.builder()
        .ollamaApi(ollamaApi)
        .defaultOptions(OllamaEmbeddingOptions.builder()
                .model("embeddinggemma:300m")
                .build())
        .build();

// Create vector store for chat memory
chatMemoryVectorStore = SimpleVectorStore.builder(embeddingModel)
        .build();

// Create vector store for chat memory
VectorStore chatMemoryVectorStore = SimpleVectorStore.builder(embeddingModel)
    .build();

context.getRegistry().bind("chatMemoryVectorStore", chatMemoryVectorStore);

// Configure endpoint with vector memory
from("direct:vector-memory")
    .to("spring-ai-chat:vmem?chatModel=#chatModel&chatMemoryVectorStore=#chatMemoryVectorStore");

// Memory is managed automatically with semantic search
template.requestBodyAndHeader("direct:vector-memory",
    "My favorite programming language is Java",
    SpringAiChatConstants.CONVERSATION_ID, "user-123", String.class);

template.requestBodyAndHeader("direct:vector-memory",
    "What programming language did I mention?",
    SpringAiChatConstants.CONVERSATION_ID, "user-123", String.class); // Will use semantic search to retrieve: "Java"
```

> **Note**
> The component automatically configures conversation isolation using metadata filters, ensuring each conversation ID maintains separate memory context. However, conversation isolation via metadata filtering requires a VectorStore implementation that supports filter expressions.

### Function Calling / Tool Integration

The component integrates with the [Spring AI Tools Component](spring-ai-tools-component.md) to enable LLMs to call Camel routes as functions/tools. This extends the LLM’s capabilities with custom logic, external APIs, database queries, and more.

When you configure the `tags` parameter, the chat component discovers all matching tools from `spring-ai-tools` routes, registers them with Spring AI’s ChatClient, and allows the LLM to call them during conversation.

-   Java
    
-   XML
    
-   YAML
    

```java
// Define tools
from("spring-ai-tools:weather?tags=weather&description=Get current weather for a location")
    .setBody(constant("Sunny"));

from("spring-ai-tools:calculator?tags=math&description=Evaluate mathematical expressions")
    .setBody(constant("42"));

from("spring-ai-tools:stock?tags=finance&description=Get current stock price")
    .setBody(constant("42"));

// Chat endpoints with different tool combinations
from("direct:weatherChat")
    .to("spring-ai-chat:chat?tags=weather&chatClient=#chatClient");

from("direct:mathChat")
    .to("spring-ai-chat:chat?tags=math&chatClient=#chatClient");

from("direct:multiToolChat")
    .to("spring-ai-chat:chat?tags=weather,math,finance&chatClient=#chatClient");
```

```xml
<!-- Define tools -->
<route>
  <from uri="spring-ai-tools:weather?tags=weather&amp;description=Get current weather for a location"/>
  <setBody><constant>Sunny</constant></setBody>
</route>

<route>
  <from uri="spring-ai-tools:calculator?tags=math&amp;description=Evaluate mathematical expressions"/>
  <setBody><constant>42</constant></setBody>
</route>

<route>
  <from uri="spring-ai-tools:stock?tags=finance&amp;description=Get current stock price"/>
  <setBody><constant>42</constant></setBody>
</route>

<!-- Chat endpoints with different tool combinations -->
<route>
  <from uri="direct:weatherChat"/>
  <to uri="spring-ai-chat:chat?tags=weather&amp;chatClient=#chatClient"/>
</route>

<route>
  <from uri="direct:mathChat"/>
  <to uri="spring-ai-chat:chat?tags=math&amp;chatClient=#chatClient"/>
</route>

<route>
  <from uri="direct:multiToolChat"/>
  <to uri="spring-ai-chat:chat?tags=weather,math,finance&amp;chatClient=#chatClient"/>
</route>
```

```yaml
# Define tools
- route:
    from:
      uri: spring-ai-tools:weather
      parameters:
        tags: weather
        description: Get current weather for a location
      steps:
        - setBody:
            constant: Sunny

- route:
    from:
      uri: spring-ai-tools:calculator
      parameters:
        tags: math
        description: Evaluate mathematical expressions
      steps:
        - setBody:
            constant: "42"

- route:
    from:
      uri: spring-ai-tools:stock
      parameters:
        tags: finance
        description: Get current stock price
      steps:
        - setBody:
            constant: "42"

# Chat endpoints with different tool combinations
- route:
    from:
      uri: direct:weatherChat
      steps:
        - to:
            uri: spring-ai-chat:chat
            parameters:
              tags: weather
              chatClient: "#chatClient"

- route:
    from:
      uri: direct:mathChat
      steps:
        - to:
            uri: spring-ai-chat:chat
            parameters:
              tags: math
              chatClient: "#chatClient"

- route:
    from:
      uri: direct:multiToolChat
      steps:
        - to:
            uri: spring-ai-chat:chat
            parameters:
              tags: weather,math,finance
              chatClient: "#chatClient"
```

**How it works:**

1.  LLM analyzes the question and decides which tools to call
    
2.  LLM generates function call requests with parameters
    
3.  Component executes Camel routes with parameters as headers
    
4.  Tool results are sent back to the LLM
    
5.  LLM processes results and generates final response
    
6.  Multiple tool calls can happen in sequence if needed
    

**Tool Definition Parameters:**

-   `tags`: Comma-separated tags for organizing tools (required)
    
-   `description`: What the tool does - shown to the LLM (required for consumer)
    
-   `name`: Tool name (auto-generated from description if not provided)
    
-   `inputType`: Java class for input validation (optional)
    

**Best Practices:**

1.  **Clear Descriptions**: Provide detailed tool descriptions so the LLM knows when to use them
    
2.  **Appropriate Tags**: Organize tools with meaningful tags
    
3.  **Error Handling**: Implement proper error handling in tool routes
    
4.  **Parameter Validation**: Validate input parameters in tool processors
    
5.  **Response Format**: Return clear, concise text responses from tools
    

### Multimodal Support (Images, Audio, and Documents)

The component supports multimodal input for models that support vision, audio, and document capabilities.

The component seamlessly integrates with Camel file components (file, ftp, sftp, smb) through `WrappedFile` support, enabling direct routing from file sources to AI chat. Media can also be sent as byte arrays or as lists of files with appropriate headers.

_Java-only: uses ProducerTemplate, `WrappedFile` aggregation, and Spring AI `UserMessage`/`Media` types_

```java
// Direct file-to-AI pipeline (MIME type auto-detected)
from("file:input-images?noop=true")
    .setHeader(SpringAiChatConstants.USER_MESSAGE, constant("What's in this image?"))
    .to("spring-ai-chat:vision?chatModel=#chatModel");

// With default user message configured
from("direct:vision")
    .to("spring-ai-chat:vision?chatModel=#chatModel&userMessage=Describe this image in detail");

// Byte array input with headers
byte[] imageData = Files.readAllBytes(Paths.get("photo.jpg"));
template.requestBodyAndHeaders("direct:vision", imageData,
    Map.of(USER_MESSAGE, "What objects do you see?", MEDIA_TYPE, "image/jpeg"),
    String.class);

// Multiple files via aggregation (as List<WrappedFile>)
from("file:comparison-images?noop=true")
    .aggregate(constant(true), new GroupedBodyAggregationStrategy())
    .completionSize(2)
    .setHeader(USER_MESSAGE, constant("Compare these images"))
    .to("spring-ai-chat:comparator?chatModel=#chatModel");

// UserMessage with Media for maximum control
Media media = new Media(MimeTypeUtils.IMAGE_PNG, imageData);
UserMessage message = new UserMessage("Analyze this scan", media);
template.requestBody("direct:scan-analyzer", message, String.class);
```

**Supported Input Types:**

-   `String` - Simple text message
    
-   `byte[]` - Single media file (image, audio, etc.)
    
-   `WrappedFile` - Single file from file components
    
-   `List<WrappedFile>` - Multiple files for comparison or analysis
    
-   `UserMessage` - Spring AI UserMessage with text and/or media
    
-   `Message` - Any Spring AI Message type
    
-   `List<Message>` - Full conversation history (CHAT\_MULTIPLE\_MESSAGES operation)
    

**MIME Type Detection Priority:**

1.  `CamelSpringAiChatMediaType` header (highest priority)
    
2.  `CamelFileContentType` header from file components
    
3.  Auto-detection from file extension
    
4.  Default to `image/png` if not recognized
    

**Supported File Formats (Auto-Detection):**

-   **Images**: PNG, JPEG, GIF, WebP, BMP, TIFF, SVG
    
-   **Videos**: MP4, WebM, MOV, MKV, FLV, MPEG, WMV, 3GP
    
-   **Audio**: WAV, MP3, OGG, M4A, FLAC
    
-   **Documents**: PDF, CSV, DOC, DOCX, XLS, XLSX, HTML, TXT, Markdown
    

**File Size Validation:**

To prevent out-of-memory errors with large media files, the component validates file sizes before loading them into memory. The default maximum file size is 1MB, configurable via:

-   Java
    
-   XML
    
-   YAML
    

```java
// Configure via endpoint parameter (in bytes)
from("file:uploads")
    .to("spring-ai-chat:vision?chatModel=#chatModel&maxFileSize=5242880"); // 5MB

// Override via header for dynamic control
from("direct:upload")
    .setHeader(SpringAiChatConstants.MAX_FILE_SIZE, constant(10485760L)) // 10MB
    .to("spring-ai-chat:vision?chatModel=#chatModel");

// Disable size checking (not recommended)
from("file:trusted")
    .to("spring-ai-chat:vision?chatModel=#chatModel&maxFileSize=0");
```

```xml
<!-- Configure via endpoint parameter (in bytes) - 5MB -->
<route>
  <from uri="file:uploads"/>
  <to uri="spring-ai-chat:vision?chatModel=#chatModel&amp;maxFileSize=5242880"/>
</route>

<!-- Override via header for dynamic control - 10MB -->
<route>
  <from uri="direct:upload"/>
  <setHeader name="CamelSpringAiChatMaxFileSize">
    <constant>10485760</constant>
  </setHeader>
  <to uri="spring-ai-chat:vision?chatModel=#chatModel"/>
</route>

<!-- Disable size checking (not recommended) -->
<route>
  <from uri="file:trusted"/>
  <to uri="spring-ai-chat:vision?chatModel=#chatModel&amp;maxFileSize=0"/>
</route>
```

```yaml
# Configure via endpoint parameter (in bytes) - 5MB
- route:
    from:
      uri: file:uploads
      steps:
        - to:
            uri: spring-ai-chat:vision
            parameters:
              chatModel: "#chatModel"
              maxFileSize: 5242880

# Override via header for dynamic control - 10MB
- route:
    from:
      uri: direct:upload
      steps:
        - setHeader:
            name: CamelSpringAiChatMaxFileSize
            constant: "10485760"
        - to:
            uri: spring-ai-chat:vision
            parameters:
              chatModel: "#chatModel"

# Disable size checking (not recommended)
- route:
    from:
      uri: file:trusted
      steps:
        - to:
            uri: spring-ai-chat:vision
            parameters:
              chatModel: "#chatModel"
              maxFileSize: 0
```

Files exceeding the configured limit will be rejected with an `IllegalArgumentException`.

### SafeGuard - Content Filtering

The component provides content filtering capabilities through Spring AI’s SafeGuard advisor. SafeGuard monitors LLM responses for sensitive words and blocks responses containing restricted content, returning a customizable failure message instead.

This feature is useful for: \* Preventing disclosure of sensitive information (passwords, secrets, API keys) \* Enforcing content policies in customer-facing applications \* Compliance with data protection requirements \* Filtering inappropriate or restricted topics

-   Java
    
-   XML
    
-   YAML
    

```java
// Configure safeguard with sensitive words
from("direct:safeguard")
    .to("spring-ai-chat:test?chatModel=#chatModel"
        + "&safeguardSensitiveWords=password,secret,confidential,api-key"
        + "&safeguardFailureResponse=I cannot provide information containing sensitive words");
```

```xml
<route>
  <from uri="direct:safeguard"/>
  <to uri="spring-ai-chat:test?chatModel=#chatModel&amp;safeguardSensitiveWords=password,secret,confidential,api-key&amp;safeguardFailureResponse=I cannot provide information containing sensitive words"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:safeguard
      steps:
        - to:
            uri: spring-ai-chat:test
            parameters:
              chatModel: "#chatModel"
              safeguardSensitiveWords: "password,secret,confidential,api-key"
              safeguardFailureResponse: "I cannot provide information containing sensitive words"
```

**Configuration Options:**

-   `safeguardSensitiveWords`: Comma-separated list of words to block in responses
    
-   `safeguardFailureResponse`: Message returned when sensitive content is detected
    
-   Headers: `CamelSpringAiChatSafeguardSensitiveWords`, `CamelSpringAiChatSafeguardFailureResponse`
    

> **Note**
> SafeGuard checks the LLM’s response content. If any configured sensitive word is found in the response, the entire response is replaced with the failure message. The check is case-insensitive.

### Structured Output Conversion

The component supports structured output conversion, allowing you to convert LLM responses into typed Java objects, Maps, or Lists. This feature is based on [Spring AI’s Structured Output Converter](https://docs.spring.io/spring-ai/reference/api/structured-output-converter.md).

Three output formats are supported: **BEAN** (Java records/POJOs), **MAP** (key-value structures), and **LIST** (arrays). Each can be configured via converter bean, endpoint parameters, or headers.

_Java-only: uses Java record definition and ProducerTemplate_

```java
// Bean output - convert to typed Java objects
@JsonPropertyOrder({ "actor", "movies" })
public record ActorFilms(String actor, List<String> movies) {}

from("direct:bean")
    .to("spring-ai-chat:test?chatModel=#chatModel&outputFormat=BEAN&outputClass="
        + ActorFilms.class.getName());

// Map output - convert to key-value structure
from("direct:map")
    .to("spring-ai-chat:test?chatModel=#chatModel&outputFormat=MAP");

// List output - convert to array
from("direct:list")
    .to("spring-ai-chat:test?chatModel=#chatModel&outputFormat=LIST");

// Dynamic conversion via headers
template.requestBodyAndHeader("direct:chat", "List programming languages",
    SpringAiChatConstants.OUTPUT_FORMAT, "LIST", List.class);
```

**Best Practices:**

1.  Use `@JsonPropertyOrder` for consistent property ordering
    
2.  Keep structures simple for better LLM accuracy
    
3.  Validate output (LLMs may occasionally produce unexpected formats)
    
4.  Use lower temperatures (0.1-0.3) for consistent structured output
    

#### Advanced: Using ChatClient Directly

For maximum control, you can provide a pre-configured `ChatClient` instead of a `ChatModel`:

_Java-only: programmatic `ChatClient` builder configuration_

```java
ChatClient chatClient = ChatClient.builder(chatModel)
    .defaultAdvisors(new MessageChatMemoryAdvisor(chatMemory))
    .defaultSystem("You are a helpful assistant")
    .build();

from("direct:chat")
    .to("spring-ai-chat:client?chatClient=#chatClient");
```

> **Note**
> Most users should use `ChatModel` and let the component handle `ChatClient` creation automatically. Only use this approach if you have specific requirements that cannot be met with standard configuration options.

### Spring @Tool Bean Discovery

In addition to Camel route tools (via `tags`), you can use Spring AI `@Tool`\-annotated beans directly.

#### Camel Spring Boot (Recommended)

When using Camel Spring Boot, Spring AI’s auto-configuration automatically discovers `@Tool`\-annotated methods from Spring beans via `ToolCallbackResolver`. Simply define your tool as a Spring bean and reference it by name using `toolNames`:

_Java-only: Spring `@Component` with `@Tool` annotation_

```java
@Component
public class MyTools {

    @Tool(description = "Get the capital city of a country", name = "getCapital")
    public String getCapital(String country) {
        return switch (country.toLowerCase()) {
            case "france" -> "Paris";
            case "germany" -> "Berlin";
            case "italy" -> "Rome";
            default -> "Unknown";
        };
    }
}

// In your route — no manual callback registration needed
from("direct:chat")
    .to("spring-ai-chat:chat?chatModel=#chatModel&toolNames=getCapital");
```

#### Without Spring Boot

Outside Spring Boot (e.g., in plain Camel or tests), there is no `ToolCallbackResolver`. You need to resolve the callbacks manually and bind them in the registry:

_Java-only: programmatic `ToolCallbackProvider` setup_

```java
ToolCallbackProvider provider = MethodToolCallbackProvider.builder()
    .toolObjects(new MyTools())
    .build();
context.getRegistry().bind("myTools", Arrays.asList(provider.getToolCallbacks()));

from("direct:chat")
    .to("spring-ai-chat:chat?chatModel=#chatModel&toolCallbacks=#myTools");
```

#### Tool Selection by Name

Select specific tools by name using the `toolNames` parameter, instead of (or in addition to) tag-based discovery. This is useful for selecting individual `@Tool` methods or controlling which tools are available per endpoint:

_Java-only: route definition with dynamic tool selection via ProducerTemplate header_

```java
// Select only the getCapital tool by name
from("direct:chat")
    .to("spring-ai-chat:chat?chatModel=#chatModel&toolNames=getCapital");

// Select tools dynamically at runtime via header
template.requestBodyAndHeader("direct:chat", "What is the capital of France?",
    SpringAiChatConstants.TOOL_NAMES, "getCapital", String.class);
```

Tool names are resolved via Spring AI’s `ToolCallbackResolver`. You can combine `toolNames` with `tags` — both tool sources are additive.

### Tool Context

Pass contextual data (user ID, session info, tenant ID, etc.) to tools during execution. Tools with a `ToolContext` parameter receive these values automatically:

_Java-only: `@Tool` with `ToolContext` and ProducerTemplate_

```java
// Tool that uses context
@Tool(description = "Get user profile")
public String getUserProfile(@ToolParam(description = "detail level") String detail,
                              ToolContext toolContext) {
    String userId = (String) toolContext.getContext().get("userId");
    return "Profile for user: " + userId;
}

// Via endpoint configuration
from("direct:chat")
    .to("spring-ai-chat:chat?chatModel=#chatModel&toolCallbacks=#myTools"
        + "&toolContext.userId=user-42"
        + "&toolContext.role=admin");

// Via header (overrides endpoint config)
template.request("direct:chat", e -> {
    e.getIn().setBody("Get my profile");
    e.getIn().setHeader(SpringAiChatConstants.TOOL_CONTEXT,
        Map.of("userId", "user-99", "role", "admin"));
});
```

> **Note**
> Tool context works with Spring AI `@Tool` methods and MCP tools. Camel route tools (defined via `spring-ai-tools` consumer) do not receive the `ToolContext`.

### Structured Output Validation

Enable automatic validation of structured output with retry on failure. When the LLM produces invalid output (doesn’t match the expected JSON Schema), the advisor re-prompts the LLM with validation errors:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("spring-ai-chat:chat?chatModel=#chatModel"
        + "&outputFormat=BEAN"
        + "&outputClass=com.example.ActorFilms"
        + "&structuredOutputValidation=true"
        + "&structuredOutputValidationMaxAttempts=3");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="spring-ai-chat:chat?chatModel=#chatModel&amp;outputFormat=BEAN&amp;outputClass=com.example.ActorFilms&amp;structuredOutputValidation=true&amp;structuredOutputValidationMaxAttempts=3"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: spring-ai-chat:chat
            parameters:
              chatModel: "#chatModel"
              outputFormat: BEAN
              outputClass: com.example.ActorFilms
              structuredOutputValidation: true
              structuredOutputValidationMaxAttempts: 3
```

If all retry attempts fail, the exception propagates to Camel’s error handler:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .doTry()
        .to("spring-ai-chat:chat?chatModel=#chatModel"
            + "&outputFormat=BEAN&outputClass=com.example.ActorFilms"
            + "&structuredOutputValidation=true&structuredOutputValidationMaxAttempts=2")
    .doCatch(Exception.class)
        .log("Structured output validation failed: ${exception.message}")
        .to("direct:fallback")
    .end();
```

```xml
<route>
  <from uri="direct:chat"/>
  <doTry>
    <to uri="spring-ai-chat:chat?chatModel=#chatModel&amp;outputFormat=BEAN&amp;outputClass=com.example.ActorFilms&amp;structuredOutputValidation=true&amp;structuredOutputValidationMaxAttempts=2"/>
    <doCatch>
      <exception>java.lang.Exception</exception>
      <log message="Structured output validation failed: ${exception.message}"/>
      <to uri="direct:fallback"/>
    </doCatch>
  </doTry>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - doTry:
            steps:
              - to:
                  uri: spring-ai-chat:chat
                  parameters:
                    chatModel: "#chatModel"
                    outputFormat: BEAN
                    outputClass: com.example.ActorFilms
                    structuredOutputValidation: true
                    structuredOutputValidationMaxAttempts: 2
            doCatch:
              - exception:
                  - java.lang.Exception
                steps:
                  - log:
                      message: "Structured output validation failed: ${exception.message}"
                  - to:
                      uri: direct:fallback
```

The advisor requires `outputClass` or `entityClass` to be set so it can generate a JSON Schema for validation. A warning is logged if neither is configured.

### MCP Client (Model Context Protocol)

The component supports connecting to MCP servers, enabling the LLM to use tools provided by external MCP-compatible services. This follows the same pattern as the [OpenAI component](openai-component.md)'s MCP support.

Configure MCP servers using the `mcpServer.<name>.<property>` prefix notation:

#### Stdio Transport

-   Java
    
-   XML
    
-   YAML
    

```java
// Connect to MCP filesystem server via stdio
from("direct:chat")
    .to("spring-ai-chat:chat?chatModel=#chatModel"
        + "&mcpServer.fs.transportType=stdio"
        + "&mcpServer.fs.command=npx"
        + "&mcpServer.fs.args=-y,@modelcontextprotocol/server-filesystem,/tmp");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="spring-ai-chat:chat?chatModel=#chatModel&amp;mcpServer.fs.transportType=stdio&amp;mcpServer.fs.command=npx&amp;mcpServer.fs.args=-y,@modelcontextprotocol/server-filesystem,/tmp"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: spring-ai-chat:chat
            parameters:
              chatModel: "#chatModel"
              mcpServer.fs.transportType: stdio
              mcpServer.fs.command: npx
              mcpServer.fs.args: "-y,@modelcontextprotocol/server-filesystem,/tmp"
```

#### SSE Transport

-   Java
    
-   XML
    
-   YAML
    

```java
// Connect to MCP server via SSE
from("direct:chat")
    .to("spring-ai-chat:chat?chatModel=#chatModel"
        + "&mcpServer.weather.transportType=sse"
        + "&mcpServer.weather.url=http://mcp-server:3001/sse");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="spring-ai-chat:chat?chatModel=#chatModel&amp;mcpServer.weather.transportType=sse&amp;mcpServer.weather.url=http://mcp-server:3001/sse"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: spring-ai-chat:chat
            parameters:
              chatModel: "#chatModel"
              mcpServer.weather.transportType: sse
              mcpServer.weather.url: "http://mcp-server:3001/sse"
```

#### Multiple MCP Servers

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("spring-ai-chat:chat?chatModel=#chatModel"
        + "&mcpServer.fs.transportType=stdio"
        + "&mcpServer.fs.command=npx"
        + "&mcpServer.fs.args=-y,@modelcontextprotocol/server-filesystem,/tmp"
        + "&mcpServer.weather.transportType=sse"
        + "&mcpServer.weather.url=http://weather-mcp:3001/sse");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="spring-ai-chat:chat?chatModel=#chatModel&amp;mcpServer.fs.transportType=stdio&amp;mcpServer.fs.command=npx&amp;mcpServer.fs.args=-y,@modelcontextprotocol/server-filesystem,/tmp&amp;mcpServer.weather.transportType=sse&amp;mcpServer.weather.url=http://weather-mcp:3001/sse"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: spring-ai-chat:chat
            parameters:
              chatModel: "#chatModel"
              mcpServer.fs.transportType: stdio
              mcpServer.fs.command: npx
              mcpServer.fs.args: "-y,@modelcontextprotocol/server-filesystem,/tmp"
              mcpServer.weather.transportType: sse
              mcpServer.weather.url: "http://weather-mcp:3001/sse"
```

#### OAuth Authentication for MCP Servers

For MCP servers requiring authentication, configure an OAuth profile per server. This requires `camel-oauth` on the classpath:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("spring-ai-chat:chat?chatModel=#chatModel"
        + "&mcpServer.api.transportType=sse"
        + "&mcpServer.api.url=http://secure-mcp:3001/sse"
        + "&mcpServer.api.oauthProfile=keycloak");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="spring-ai-chat:chat?chatModel=#chatModel&amp;mcpServer.api.transportType=sse&amp;mcpServer.api.url=http://secure-mcp:3001/sse&amp;mcpServer.api.oauthProfile=keycloak"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: spring-ai-chat:chat
            parameters:
              chatModel: "#chatModel"
              mcpServer.api.transportType: sse
              mcpServer.api.url: "http://secure-mcp:3001/sse"
              mcpServer.api.oauthProfile: keycloak
```

With corresponding properties:

```properties
camel.oauth.keycloak.client-id=my-client
camel.oauth.keycloak.client-secret=my-secret
camel.oauth.keycloak.token-endpoint=https://keycloak/realms/myrealm/protocol/openid-connect/token
```

> **Important**
> The Spring AI chat component uses the MCP SDK version managed by the Spring AI BOM. Using this component’s MCP support alongside `camel-openai` MCP support in the same application may cause version conflicts. Choose one approach per application.

### Observability

When using Camel Spring Boot with `spring-boot-starter-actuator`, Spring AI’s built-in observability support is automatically enabled. No additional Camel-side configuration is needed — the `ChatModel` and `ChatClient` calls are instrumented by Spring AI through Micrometer.

Add the actuator dependency to your Spring Boot application:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

This works automatically because the Camel component delegates to Spring AI’s `ChatClient` and `ChatModel`, which are already instrumented. The component itself does not need to add any observation code — Spring AI’s auto-configuration handles everything when actuator is on the classpath.

Refer to the [Spring AI Observability documentation](https://docs.spring.io/spring-ai/reference/observability/index.md) for details on available metrics, tracing, and prompt/completion logging configuration.

### Request/Response Logging

The component automatically adds Spring AI’s `SimpleLoggerAdvisor` to log requests and responses for debugging. Enable it by setting the logger `org.springframework.ai.chat.client.advisor` to DEBUG level:

```properties
logging.level.org.springframework.ai.chat.client.advisor=DEBUG
```

## See Also

-   [Spring AI Documentation](https://docs.spring.io/spring-ai/reference/)
    
-   [Spring AI Function Calling](https://docs.spring.io/spring-ai/reference/api/tools.md)
    
-   [Spring AI Tools Component](spring-ai-tools-component.md)
    
-   [Spring AI Embeddings Component](spring-ai-embeddings-component.md)
    
-   [Spring AI VectorStore Component](spring-ai-vector-store-component.md)
    
-   [Spring AI Image Component](spring-ai-image-component.md)
    

## Spring Boot Auto-Configuration

When using spring-ai-chat with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-spring-ai-chat-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.spring-ai-chat.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.spring-ai-chat.chat-model** | The ChatModel instance to use for chat operations. The option is a org.springframework.ai.chat.model.ChatModel type. |  | ChatModel |
| **camel.component.spring-ai-chat.enabled** | Whether to enable auto configuration of the spring-ai-chat component. This is enabled by default. |  | Boolean |
| **camel.component.spring-ai-chat.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |