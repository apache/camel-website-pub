# OpenAI

**Since Camel 4.17**

**Only producer is supported**

The OpenAI component provides integration with OpenAI and OpenAI-compatible APIs for chat completion and text embeddings using the official openai-java SDK.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-openai</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

```none
openai:operation[?options]
```

Supported operations:

-   `chat-completion` - Generate chat completions using language models
    
-   `embeddings` - Generate vector embeddings from text for semantic search and RAG applications
    

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

The OpenAI component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiKey** (producer) | Default API key for all endpoints. |  | String |
| **baseUrl** (producer) | Default base URL for all endpoints. | [https://api.openai.com/v1](https://api.openai.com/v1) | String |
| **embeddingModel** (producer) | Default model for embeddings endpoints. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **model** (producer) | Default model for chat completion endpoints. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The OpenAI endpoint is configured using URI syntax:

openai:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform: 'chat-completion' or 'embeddings'.

Enum values:

-   chat-completion
    
-   embeddings
    





 |  | OpenAIOperations |

### Query Parameters (20 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalBodyProperty** (producer) | Additional JSON properties to include in the request body (e.g. additionalBodyProperty.traceId=123). This is a multi-value option with prefix: additionalBodyProperty. |  | Map |
| **apiKey** (producer) | OpenAI API key. Can also be set via OPENAI\_API\_KEY environment variable. |  | String |
| **baseUrl** (producer) | Base URL for OpenAI API. Defaults to OpenAI’s official endpoint. Can be used for local or third-party providers. | [https://api.openai.com/v1](https://api.openai.com/v1) | String |
| **conversationHistoryProperty** (producer) | Exchange property name for storing conversation history. | CamelOpenAIConversationHistory | String |
| **conversationMemory** (producer) | Enable conversation memory per Exchange. | false | boolean |
| **developerMessage** (producer) | Developer message to prepend before user messages. |  | String |
| **dimensions** (producer) | Number of dimensions for the embedding output. Only supported by text-embedding-3 models. Reducing dimensions can lower costs and improve performance without significant quality loss. |  | Integer |
| **embeddingModel** (producer) | The model to use for embeddings. |  | String |
| **encodingFormat** (producer) | 
The format for embedding output: 'float' for list of floats, 'base64' for compressed format.

Enum values:

-   float
    
-   base64
    





 | base64 | String |
| **jsonSchema** (producer) | JSON schema for structured output validation. |  | String |
| **maxTokens** (producer) | Maximum number of tokens to generate. |  | Integer |
| **model** (producer) | The model to use for chat completion. |  | String |
| **outputClass** (producer) | Fully qualified class name for structured output using response format. |  | String |
| **storeFullResponse** (producer) | Store the full response in the exchange property 'CamelOpenAIResponse' in non-streaming mode. | false | boolean |
| **streaming** (producer) | Enable streaming responses. | false | boolean |
| **systemMessage** (producer) | System message to prepend. When set and conversationMemory is enabled, the conversation history is reset. |  | String |
| **temperature** (producer) | Temperature for response generation (0.0 to 2.0). |  | Double |
| **topP** (producer) | Top P for response generation (0.0 to 1.0). |  | Double |
| **userMessage** (producer) | Default user message text to use when no prompt is provided. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The OpenAI component supports 25 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelOpenAIUserMessage** (producer) Constant: [`USER_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#USER_MESSAGE) | The user message to send to the OpenAI chat completion API. |  | String |
| **CamelOpenAISystemMessage** (producer) Constant: [`SYSTEM_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#SYSTEM_MESSAGE) | The system message to provide context and instructions to the model. |  | String |
| **CamelOpenAIDeveloperMessage** (producer) Constant: [`DEVELOPER_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#DEVELOPER_MESSAGE) | The developer message to provide additional instructions to the model. |  | String |
| **CamelOpenAIModel** (producer) Constant: [`MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MODEL) | The model to use for chat completion. |  | String |
| **CamelOpenAITemperature** (producer) Constant: [`TEMPERATURE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#TEMPERATURE) | Controls randomness in the response. Higher values (e.g., 0.8) make output more random, lower values (e.g., 0.2) make it more deterministic. |  | Double |
| **CamelOpenAITopP** (producer) Constant: [`TOP_P`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#TOP_P) | An alternative to temperature for controlling randomness. Uses nucleus sampling where the model considers tokens with top\_p probability mass. |  | Double |
| **CamelOpenAIMaxTokens** (producer) Constant: [`MAX_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MAX_TOKENS) | The maximum number of tokens to generate in the completion. |  | Integer |
| **CamelOpenAIStreaming** (producer) Constant: [`STREAMING`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#STREAMING) | Whether to stream the response back incrementally. |  | Boolean |
| **CamelOpenAIOutputClass** (producer) Constant: [`OUTPUT_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#OUTPUT_CLASS) | The Java class to use for structured output parsing. |  | Class |
| **CamelOpenAIJsonSchema** (producer) Constant: [`JSON_SCHEMA`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#JSON_SCHEMA) | The JSON schema to use for structured output validation. |  | String |
| **CamelOpenAIResponseModel** (producer) Constant: [`RESPONSE_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#RESPONSE_MODEL) | The model used for the completion response. |  | String |
| **CamelOpenAIResponseId** (producer) Constant: [`RESPONSE_ID`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#RESPONSE_ID) | The unique identifier for the completion response. |  | String |
| **CamelOpenAIFinishReason** (producer) Constant: [`FINISH_REASON`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#FINISH_REASON) | The reason the completion finished (e.g., stop, length, content\_filter). |  | String |
| **CamelOpenAIPromptTokens** (producer) Constant: [`PROMPT_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#PROMPT_TOKENS) | The number of tokens used in the prompt. |  | Integer |
| **CamelOpenAICompletionTokens** (producer) Constant: [`COMPLETION_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#COMPLETION_TOKENS) | The number of tokens used in the completion. |  | Integer |
| **CamelOpenAITotalTokens** (producer) Constant: [`TOTAL_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#TOTAL_TOKENS) | The total number of tokens used (prompt completion). |  | Integer |
| **CamelOpenAIResponse** (producer) Constant: [`RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#RESPONSE) | The complete OpenAI response object. |  | ChatCompletion |
| **CamelOpenAIEmbeddingModel** (producer) Constant: [`EMBEDDING_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_MODEL) | The model to use for embeddings. |  | String |
| **CamelOpenAIEmbeddingDimensions** (producer) Constant: [`EMBEDDING_DIMENSIONS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_DIMENSIONS) | Number of output dimensions. |  | Integer |
| **CamelOpenAIEmbeddingResponseModel** (producer) Constant: [`EMBEDDING_RESPONSE_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_RESPONSE_MODEL) | The embedding model used in the response. |  | String |
| **CamelOpenAIEmbeddingCount** (producer) Constant: [`EMBEDDING_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_COUNT) | Number of embeddings returned. |  | Integer |
| **CamelOpenAIEmbeddingVectorSize** (producer) Constant: [`EMBEDDING_VECTOR_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_VECTOR_SIZE) | Vector dimensions of the embeddings. |  | Integer |
| **CamelOpenAIReferenceEmbedding** (producer) Constant: [`REFERENCE_EMBEDDING`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#REFERENCE_EMBEDDING) | Reference embedding vector for similarity comparison. |  | List |
| **CamelOpenAISimilarityScore** (producer) Constant: [`SIMILARITY_SCORE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#SIMILARITY_SCORE) | Calculated cosine similarity score (0.0 to 1.0). |  | Double |
| **CamelOpenAIOriginalText** (producer) Constant: [`ORIGINAL_TEXT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#ORIGINAL_TEXT) | Original text content when embeddings operation is used. |  | String or List |

## Usage

### Authentication

Set `baseUrl` to your providers endpoint (default: `[https://api.openai.com/v1](https://api.openai.com/v1)`).

API key resolution order:

-   Endpoint `apiKey`
    
-   Component `apiKey`
    
-   Environment variable `OPENAI_API_KEY`
    
-   System property `openai.api.key`
    

> **Note**
> The API key can be omitted if using OpenAI-compatible providers that don’t require authentication (e.g., some local LLM servers).

### Basic Chat Completion with String Input

-   Java
    
-   YAML
    

```java
from("direct:chat")
    .setBody(constant("What is Apache Camel?"))
    .to("openai:chat-completion")
    .log("Response: ${body}");
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: openai:chat-completion
            parameters:
              userMessage: What is Apache Camel?
        - log: "Response: ${body}"
```

### File-Backed Prompt with Text File

Usage example:

```java
from("file:prompts?noop=true")
    .to("openai:chat-completion")
    .log("Response: ${body}");
```

### Image File Input with Vision Model

Usage example:

```java
from("file:images?noop=true")
    .to("openai:chat-completion?model=gpt-4.1-mini?userMessage=Describe what you see in this image")
    .log("Response: ${body}");
```

> **Note**
> When using image files, the userMessage is required. Supported image formats are detected by MIME type (e.g., `image/png`, `image/jpeg`, `image/gif`, `image/webp`).

### Streaming Response

When `streaming=true`, the component returns an `Iterator<ChatCompletionChunk>` in the message body. You can consume this iterator using Camel’s streaming EIPs or process it directly:

Usage example:

```yaml
- route:
    id: route-1145
    from:
      id: from-1972
      uri: timer
      parameters:
        repeatCount: 1
        timerName: timer
      steps:
        - to:
            id: to-1301
            uri: openai:chat-completion
            parameters:
              userMessage: In one sentence, what is Apache Camel?
              streaming: true
        - split:
            id: split-3196
            steps:
              - marshal:
                  id: marshal-3773
                  json:
                    library: Jackson
              - log:
                  id: log-6722
                  message: ${body}
            simple:
              expression: ${body}
            streaming: true
```

### Structured Output with outputClass

Usage example:

```java
public class Person {
    public String name;
    public int age;
    public String occupation;
}

from("direct:structured")
    .setBody(constant("Generate a person profile for a software engineer"))
    .to("openai:chat-completion?baseUrl=https://api.openai.com/v1&outputClass=com.example.Person")
    .log("Structured response: ${body}");
```

### Structured Output with JSON Schema

The `jsonSchema` option instructs the model to return JSON that conforms to the provided schema. The response will be valid JSON but is not automatically validated against the schema:

Usage example:

```java
from("direct:json-schema")
    .setBody(constant("Create a product description"))
    .setHeader("CamelOpenAIJsonSchema", constant("{\"type\":\"object\",\"properties\":{\"name\":{\"type\":\"string\"},\"price\":{\"type\":\"number\"}}}"))
    .to("openai:chat-completion")
    .log("JSON response: ${body}");
```

You can also load the schema from a resource file:

Usage example:

```java
from("direct:json-schema-resource")
    .setBody(constant("Create a product description"))
    .to("openai:chat-completion?jsonSchema=resource:classpath:schemas/product.schema.json")
    .log("JSON response: ${body}");
```

> **Note**
> For full schema validation, integrate with the `camel-json-validator` component after receiving the response.

### Conversation Memory (Per Exchange)

Usage example:

```java
from("direct:conversation")
    .setBody(constant("My name is Alice"))
    .to("openai:chat-completion?conversationMemory=true")
    .log("First response: ${body}")
    .setBody(constant("What is my name?"))
    .to("openai:chat-completion?conversationMemory=true")
    .log("Second response: ${body}"); // Will remember "Alice"
```

### Using Third-Party or Local OpenAI-Compatible Endpoint

Usage example:

```java
from("direct:local")
    .setBody(constant("Hello from local LLM"))
    .to("openai:chat-completion?baseUrl=http://localhost:1234/v1&model=local-model")
    .log("${body}");
```

## Input Handling

The component accepts the following types of input in the message body:

1.  **String**: The prompt text is taken directly from the body
    
2.  **File**: Used for file-based prompts. The component handles two types of files:
    
    -   **Text files** (MIME type starting with `text/`): The file content is read and used as the prompt. If userMessage endpoint option or `CamelOpenAIUserMessage` is set, it overrides the file content
        
    -   **Image files** (MIME type starting with `image/`): The file is encoded as a base64 data URL and sent to vision-capable models. The userMessage is **required** when using image files
        
    

> **Note**
> When using `File` input, the component uses `Files.probeContentType()` to detect the file type. Ensure your system has proper MIME type detection configured.

## Output Handling

### Default Mode

The full model response is returned as a String in the message body.

### Streaming Mode

When `streaming=true`, the message body contains an `Iterator<ChatCompletionChunk>` suitable for Camel streaming EIPs (such as `split()` with `streaming()`).

IMPORTANT:

-   Conversation memory is **not** automatically updated for streaming responses (only for non-streaming responses)
    

### Structured Outputs

#### Using outputClass

The model is instructed to return JSON matching the specified class, but the response body remains a String.

#### Using jsonSchema

The `jsonSchema` option instructs the model to return JSON conforming to the provided schema. The response will be valid JSON but is not automatically validated against the schema. For full schema validation, integrate with the `camel-json-validator` component after receiving the response.

The JSON schema must be a valid JSON object. Invalid schema strings will result in an `IllegalArgumentException`.

## Conversation Memory

When `conversationMemory=true`, the component maintains conversation history in the `CamelOpenAIConversationHistory` exchange property (configurable via `conversationHistoryProperty` option). This history is scoped to a single Exchange and allows multi-turn conversations within a route.

IMPORTANT:

-   Conversation history is automatically updated with each assistant response for **non-streaming** responses only
    
-   The history is stored as a `List<ChatCompletionMessageParam>` in the Exchange property
    
-   The history persists across multiple calls to the endpoint within the same Exchange
    
-   You can manually set the `CamelOpenAIConversationHistory` exchange property to provide custom conversation context
    

Example of manual conversation history:

Usage example:

```java
List<ChatCompletionMessageParam> history = new ArrayList<>();
history.add(ChatCompletionMessageParam.ofUser(/* ... */));
history.add(ChatCompletionMessageParam.ofAssistant(/* ... */));

from("direct:with-history")
    .setBody(constant("Continue the conversation"))
    .setProperty("CamelOpenAIConversationHistory", constant(history))
    .to("openai:chat-completion?conversationMemory=true")
    .log("${body}");
```

## Compatibility

This component works with any OpenAI API-compatible endpoint by setting the `baseUrl` parameter. This includes:

-   OpenAI official API (`[https://api.openai.com/v1](https://api.openai.com/v1)`)
    
-   Local LLM servers (e.g., Ollama, LM Studio, LocalAI)
    
-   Third-party OpenAI-compatible providers
    

> **Note**
> When using local or third-party providers, ensure they support the chat completions and/or embeddings API endpoint format. Some providers may have different authentication requirements or API variations.

### Embedding Models by Provider

  
| Provider | Recommended Model | Dimensions |
| --- | --- | --- |
| OpenAI | `text-embedding-3-small` | 1536 (reducible to 256, 512, 1024) |
| OpenAI | `text-embedding-3-large` | 3072 (reducible) |
| Ollama | `nomic-embed-text` | 768 |
| Ollama | `mxbai-embed-large` | 1024 |
| Mistral | `mistral-embed` | 1024 |

Example using Ollama for local embeddings:

```yaml
- to:
    uri: openai:embeddings
    parameters:
      baseUrl: http://localhost:11434/v1
      embeddingModel: nomic-embed-text
```

## Embeddings Operation

The `embeddings` operation generates vector embeddings from text, which can be used for semantic search, similarity comparison, and RAG (Retrieval-Augmented Generation) applications.

### Basic Embedding

-   Java
    
-   YAML
    

```java
from("direct:embed")
    .setBody(constant("What is Apache Camel?"))
    .to("openai:embeddings?embeddingModel=nomic-embed-text")
```

```yaml
- route:
    from:
      uri: direct:embed
      steps:
        - to:
            uri: openai:embeddings
            parameters:
              embeddingModel: nomic-embed-text
```

The response body is the embedding vector data:

-   Single input: `List<Float>` (a single embedding vector)
    
-   Batch input: `List<List<Float>>` (one embedding vector per input string)
    

Additional metadata (model, token usage, vector size, count) is exposed via headers (see `OpenAIConstants`).

### Batch Embedding

You can embed multiple texts in a single request by passing a `List<String>`:

```java
from("direct:batch-embed")
    .setBody(constant(List.of("First text", "Second text", "Third text")))
    .to("openai:embeddings?embeddingModel=nomic-embed-text")
    .log("Generated ${header.CamelOpenAIEmbeddingCount} embeddings");
```

### Direct Vector Database Integration

For single-input requests, the component returns a raw `List<Float>` embedding vector, enabling direct chaining to vector database components.

#### PostgreSQL + pgvector (Recommended)

```yaml
# Index documents in PostgreSQL with pgvector
- route:
    from:
      uri: direct:index
      steps:
        - setVariable:
            name: text
            simple: "${body}"
        - to:
            uri: openai:embeddings
            parameters:
              embeddingModel: nomic-embed-text
        - setVariable:
            name: embedding
            simple: "${body.toString()}"
        - to:
            uri: sql:INSERT INTO documents (content, embedding) VALUES (:#text, :#embedding::vector)
```

#### Alternative: Dedicated Vector Databases

For specialized vector workloads, you can also use `camel-qdrant`, `camel-weaviate`, `camel-milvus`, or `camel-pinecone`:

### Similarity Calculation

The component can automatically calculate cosine similarity when a reference embedding is provided:

```java
List<Float> referenceEmbedding = /* previously computed embedding */;

from("direct:compare")
    .setBody(constant("New text to compare"))
    .setHeader("CamelOpenAIReferenceEmbedding", constant(referenceEmbedding))
    .to("openai:embeddings?embeddingModel=nomic-embed-text")
    .log("Similarity score: ${header.CamelOpenAISimilarityScore}");
```

You can also use `SimilarityUtils` directly for manual calculations:

```java
import org.apache.camel.component.openai.SimilarityUtils;

double similarity = SimilarityUtils.cosineSimilarity(embedding1, embedding2);
double distance = SimilarityUtils.euclideanDistance(embedding1, embedding2);
List<Float> normalized = SimilarityUtils.normalize(embedding);
```

### Embeddings Output Headers

The following headers are set after an embeddings request:

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelOpenAIEmbeddingResponseModel` | String | The model used for embedding |
| `CamelOpenAIEmbeddingCount` | Integer | Number of embeddings returned |
| `CamelOpenAIEmbeddingVectorSize` | Integer | Dimension of each embedding vector |
| `CamelOpenAIPromptTokens` | Integer | Tokens used in the input |
| `CamelOpenAITotalTokens` | Integer | Total tokens used |
| `CamelOpenAIOriginalText` | String/List | Original input text(s) |
| `CamelOpenAISimilarityScore` | Double | Cosine similarity (if reference embedding provided) |

## Error Handling

The component may throw the following exceptions:

-   `IllegalArgumentException`:
    
    -   When an invalid operation is specified (supported: `chat-completion`, `embeddings`)
        
    -   When message body or user message is missing
        
    -   When image file is provided without userMessage (chat-completion)
        
    -   When unsupported file type is provided (only text and image files are supported)
        
    -   When invalid JSON schema string is provided
        
    
-   API-specific exceptions from the OpenAI SDK for network errors, authentication failures, rate limiting, etc.
    

## Spring Boot Auto-Configuration

When using openai with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-openai-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.openai.api-key** | Default API key for all endpoints. |  | String |
| **camel.component.openai.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openai.base-url** | Default base URL for all endpoints. | [https://api.openai.com/v1](https://api.openai.com/v1) | String |
| **camel.component.openai.embedding-model** | Default model for embeddings endpoints. |  | String |
| **camel.component.openai.enabled** | Whether to enable auto configuration of the openai component. This is enabled by default. |  | Boolean |
| **camel.component.openai.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openai.model** | Default model for chat completion endpoints. |  | String |