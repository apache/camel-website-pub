# Google Vertex AI

**Since Camel 4.17**

**Only producer is supported**

This component integrates with Google Cloud Vertex AI, supporting both Google’s native models (Gemini, Imagen) and partner models (Claude, Llama, Mistral) through the rawPredict API.

## Prerequisites

-   A Google Cloud Platform account with Vertex AI API enabled
    
-   A service account with appropriate permissions, or Application Default Credentials configured
    

For setup instructions, see [Vertex AI Documentation](https://cloud.google.com/vertex-ai/docs).

## URI Format

google-vertexai:projectId:location:modelId\[?options\]

-   `projectId` - Your GCP project ID
    
-   `location` - Region where the model is available (e.g., `us-central1`, `us-east5`)
    
-   `modelId` - Model identifier (e.g., `gemini-2.0-flash`, `claude-sonnet-4@20250514`)
    

## Configuring Options

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

The Google Vertex AI component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceAccountKey** (common) | The Service account key that can be used as credentials for the Vertex AI client. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **anthropicVersion** (producer) | Anthropic API version for Claude models. Required when publisher is 'anthropic'. | vertex-2023-10-16 | String |
| **candidateCount** (producer) | Number of candidate responses to generate. | 1 | Integer |
| **configuration** (producer) | The component configuration. |  | GoogleVertexAIConfiguration |
| **jsonMode** (producer) | Whether to use JSON request/response format. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxOutputTokens** (producer) | Maximum number of output tokens. | 1024 | Integer |
| **operation** (producer) | 
Set the operation for the producer.

Enum values:

-   generateText
    
-   generateChat
    
-   generateChatStreaming
    
-   generateImage
    
-   generateEmbeddings
    
-   generateCode
    
-   generateMultimodal
    
-   rawPredict
    
-   streamRawPredict
    





 |  | GoogleVertexAIOperations |
| **publisher** (producer) | Publisher name for partner models (e.g., anthropic, meta, mistralai). Required for rawPredict operations. |  | String |
| **streamOutputMode** (producer) | 

Streaming output mode: complete (default) or chunks.

Enum values:

-   complete
    
-   chunks
    





 | complete | String |
| **temperature** (producer) | Temperature parameter for generation (0.0-1.0). | 0.7 | Float |
| **topK** (producer) | Top-K parameter for generation. | 40 | Integer |
| **topP** (producer) | Top-P parameter for nucleus sampling. | 0.95 | Float |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **client** (advanced) | **Autowired** The Google GenAI client for Vertex AI. |  | Client |
| **predictionServiceClient** (advanced) | **Autowired** The Google Cloud AI Platform Prediction Service client for rawPredict operations. |  | PredictionServiceClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |

## Endpoint Options

The Google Vertex AI endpoint is configured using URI syntax:

google-vertexai:projectId:location:modelId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **projectId** (common) | **Required** Google Cloud Project ID. |  | String |
| **location** (common) | **Required** Google Cloud location/region (e.g., us-central1). |  | String |
| **modelId** (common) | **Required** Model ID to use for predictions. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceAccountKey** (common) | The Service account key that can be used as credentials for the Vertex AI client. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **anthropicVersion** (producer) | Anthropic API version for Claude models. Required when publisher is 'anthropic'. | vertex-2023-10-16 | String |
| **candidateCount** (producer) | Number of candidate responses to generate. | 1 | Integer |
| **jsonMode** (producer) | Whether to use JSON request/response format. | false | boolean |
| **maxOutputTokens** (producer) | Maximum number of output tokens. | 1024 | Integer |
| **operation** (producer) | 
Set the operation for the producer.

Enum values:

-   generateText
    
-   generateChat
    
-   generateChatStreaming
    
-   generateImage
    
-   generateEmbeddings
    
-   generateCode
    
-   generateMultimodal
    
-   rawPredict
    
-   streamRawPredict
    





 |  | GoogleVertexAIOperations |
| **publisher** (producer) | Publisher name for partner models (e.g., anthropic, meta, mistralai). Required for rawPredict operations. |  | String |
| **streamOutputMode** (producer) | 

Streaming output mode: complete (default) or chunks.

Enum values:

-   complete
    
-   chunks
    





 | complete | String |
| **temperature** (producer) | Temperature parameter for generation (0.0-1.0). | 0.7 | Float |
| **topK** (producer) | Top-K parameter for generation. | 40 | Integer |
| **topP** (producer) | Top-P parameter for nucleus sampling. | 0.95 | Float |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **client** (advanced) | **Autowired** The Google GenAI client for Vertex AI. |  | Client |
| **predictionServiceClient** (advanced) | **Autowired** The Google Cloud AI Platform Prediction Service client for rawPredict operations. |  | PredictionServiceClient |

## Message Headers

The Google Vertex AI component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGoogleVertexAIOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   generateText
    
-   generateChat
    
-   generateChatStreaming
    
-   generateImage
    
-   generateEmbeddings
    
-   generateCode
    
-   generateMultimodal
    
-   rawPredict
    
-   streamRawPredict
    





 |  | GoogleVertexAIOperations |
| **CamelGoogleVertexAIModelId** (producer) Constant: [`MODEL_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#MODEL_ID) | The model ID to use for generation. |  | String |
| **CamelGoogleVertexAIProjectId** (producer) Constant: [`PROJECT_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#PROJECT_ID) | The project ID to use for the request. |  | String |
| **CamelGoogleVertexAILocation** (producer) Constant: [`LOCATION`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#LOCATION) | The location/region to use for the request. |  | String |
| **CamelGoogleVertexAITemperature** (producer) Constant: [`TEMPERATURE`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#TEMPERATURE) | The temperature parameter for generation (0.0-1.0). |  | Float |
| **CamelGoogleVertexAITopP** (producer) Constant: [`TOP_P`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#TOP_P) | The top-p parameter for generation. |  | Float |
| **CamelGoogleVertexAITopK** (producer) Constant: [`TOP_K`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#TOP_K) | The top-k parameter for generation. |  | Integer |
| **CamelGoogleVertexAIMaxOutputTokens** (producer) Constant: [`MAX_OUTPUT_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#MAX_OUTPUT_TOKENS) | The maximum number of output tokens. |  | Integer |
| **CamelGoogleVertexAIcandidateCount** (producer) Constant: [`CANDIDATE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#CANDIDATE_COUNT) | The number of candidate responses to generate. |  | Integer |
| **CamelGoogleVertexAIStreamOutputMode** (producer) Constant: [`STREAM_OUTPUT_MODE`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#STREAM_OUTPUT_MODE) | The streaming output mode (complete or chunks). |  | String |
| **CamelGoogleVertexAIPrompt** (producer) Constant: [`PROMPT`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#PROMPT) | The prompt text for text generation. |  | String |
| **CamelGoogleVertexAIChatMessages** (producer) Constant: [`CHAT_MESSAGES`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#CHAT_MESSAGES) | The chat messages for chat generation. |  | List |
| **CamelGoogleVertexAISystemInstruction** (producer) Constant: [`SYSTEM_INSTRUCTION`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#SYSTEM_INSTRUCTION) | The system instruction for the model. |  | String |
| **CamelGoogleVertexAISafetySettings** (producer) Constant: [`SAFETY_SETTINGS`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#SAFETY_SETTINGS) | The safety settings for content filtering. |  | List |
| **CamelGoogleVertexAIFinishReason** (producer) Constant: [`FINISH_REASON`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#FINISH_REASON) | The finish reason from the response. |  | String |
| **CamelGoogleVertexAIPromptTokenCount** (producer) Constant: [`PROMPT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#PROMPT_TOKEN_COUNT) | The number of tokens in the prompt. |  | Integer |
| **CamelGoogleVertexAICandidatesTokenCount** (producer) Constant: [`CANDIDATES_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#CANDIDATES_TOKEN_COUNT) | The number of tokens in the response. |  | Integer |
| **CamelGoogleVertexAITotalTokenCount** (producer) Constant: [`TOTAL_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#TOTAL_TOKEN_COUNT) | The total token count (prompt response). |  | Integer |
| **CamelGoogleVertexAISafetyRatings** (producer) Constant: [`SAFETY_RATINGS`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#SAFETY_RATINGS) | The safety ratings from the response. |  | List |
| **CamelGoogleVertexAIContentBlocked** (producer) Constant: [`CONTENT_BLOCKED`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#CONTENT_BLOCKED) | Whether the content was blocked by safety filters. |  | Boolean |
| **CamelGoogleVertexAIChunkCount** (producer generateChatStreaming streamRawPredict) Constant: [`CHUNK_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#CHUNK_COUNT) | The number of streaming chunks received. |  | Integer |
| **CamelGoogleVertexAIImageNumberOfImages** (producer generateImage) Constant: [`IMAGE_NUMBER_OF_IMAGES`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#IMAGE_NUMBER_OF_IMAGES) | The number of images to generate. |  | Integer |
| **CamelGoogleVertexAIImageAspectRatio** (producer generateImage) Constant: [`IMAGE_ASPECT_RATIO`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#IMAGE_ASPECT_RATIO) | The aspect ratio for generated images (e.g., 1:1, 16:9, 9:16, 3:4, 4:3). |  | String |
| **CamelGoogleVertexAIGeneratedImages** (producer generateImage) Constant: [`GENERATED_IMAGES`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#GENERATED_IMAGES) | The generated images from an image generation operation. |  | List |
| **CamelGoogleVertexAIEmbeddingTaskType** (producer generateEmbeddings) Constant: [`EMBEDDING_TASK_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#EMBEDDING_TASK_TYPE) | The task type for embeddings (e.g., RETRIEVAL\_QUERY, RETRIEVAL\_DOCUMENT, SEMANTIC\_SIMILARITY, CLASSIFICATION, CLUSTERING, QUESTION\_ANSWERING, FACT\_VERIFICATION). |  | String |
| **CamelGoogleVertexAIEmbeddingOutputDimensionality** (producer generateEmbeddings) Constant: [`EMBEDDING_OUTPUT_DIMENSIONALITY`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#EMBEDDING_OUTPUT_DIMENSIONALITY) | The desired output dimensionality for embeddings. |  | Integer |
| **CamelGoogleVertexAIMediaData** (producer generateMultimodal) Constant: [`MEDIA_DATA`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#MEDIA_DATA) | The media data bytes for multimodal input. |  | byte\[\] |
| **CamelGoogleVertexAIMediaMimeType** (producer generateMultimodal) Constant: [`MEDIA_MIME_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#MEDIA_MIME_TYPE) | The MIME type of the media data (e.g., image/png, image/jpeg, video/mp4, audio/mp3). |  | String |
| **CamelGoogleVertexAIMediaGcsUri** (producer generateMultimodal) Constant: [`MEDIA_GCS_URI`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#MEDIA_GCS_URI) | The GCS URI of the media file for multimodal input (e.g., gs://bucket/image.png). |  | String |
| **CamelGoogleVertexAIPublisher** (producer) Constant: [`PUBLISHER`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#PUBLISHER) | Publisher name for partner models (e.g., anthropic, meta, mistralai). |  | String |
| **CamelGoogleVertexAIRawResponse** (producer) Constant: [`RAW_RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#RAW_RESPONSE) | The raw JSON response from rawPredict operation. |  | String |
| **CamelGoogleVertexAIAnthropicVersion** (producer) Constant: [`ANTHROPIC_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-google-vertexai/latest/org/apache/camel/component/google/vertexai/GoogleVertexAIConstants.html#ANTHROPIC_VERSION) | Anthropic API version for Claude models. |  | String |

## Authentication

The component supports two authentication methods:

1.  **Service Account Key File** - Set the `serviceAccountKey` parameter to a file path:
    
    serviceAccountKey=file:/path/to/service-account.json
    
2.  **Application Default Credentials** - If no key is provided, the component uses ADC automatically.
    

## Operations

### Google Models

Use these operations with Gemini, Imagen, and other Google models:

 
| Operation | Description |
| --- | --- |
| `generateText` | Generate text from a prompt |
| `generateChat` | Generate chat responses |
| `generateChatStreaming` | Generate streaming chat responses (accumulated text returned with chunk count) |
| `generateCode` | Generate code from a description |
| `generateImage` | Generate images using Imagen models |
| `generateEmbeddings` | Generate text embeddings using embedding models (single text or batch) |
| `generateMultimodal` | Generate content from multimodal inputs (text + images/video/audio) |

### Partner Models

Use `rawPredict` and `streamRawPredict` for Claude, Llama, and Mistral models:

 
| Operation | Description |
| --- | --- |
| `rawPredict` | Send requests to partner models via the Prediction Service API |
| `streamRawPredict` | Send streaming requests to partner models (accumulated response with chunk count) |

Partner models require the `publisher` parameter: `anthropic`, `meta`, or `mistralai`.

## Examples

### Text Generation with Gemini

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:prompt")
    .setBody(constant("Explain quantum computing briefly"))
    .to("google-vertexai:my-project:us-central1:gemini-2.0-flash")
    .log("${body}");
```

```xml
<route>
  <from uri="direct:prompt"/>
  <setBody>
    <constant>Explain quantum computing briefly</constant>
  </setBody>
  <to uri="google-vertexai:my-project:us-central1:gemini-2.0-flash"/>
  <log message="${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:prompt
      steps:
        - setBody:
            constant: Explain quantum computing briefly
        - to:
            uri: google-vertexai:my-project:us-central1:gemini-2.0-flash
        - log:
            message: "${body}"
```

### Using a Service Account

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:prompt")
    .to("google-vertexai:my-project:us-central1:gemini-2.0-flash?serviceAccountKey=file:/path/to/key.json")
    .log("${body}");
```

```xml
<route>
  <from uri="direct:prompt"/>
  <to uri="google-vertexai:my-project:us-central1:gemini-2.0-flash?serviceAccountKey=file:/path/to/key.json"/>
  <log message="${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:prompt
      steps:
        - to:
            uri: google-vertexai:my-project:us-central1:gemini-2.0-flash
            parameters:
              serviceAccountKey: "file:/path/to/key.json"
        - log:
            message: "${body}"
```

### Calling Claude with rawPredict

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:claude")
    .setBody(constant("What is Apache Camel?"))
    .to("google-vertexai:my-project:us-east5:claude-sonnet-4@20250514?operation=rawPredict&publisher=anthropic")
    .log("${body}");
```

```xml
<route>
  <from uri="direct:claude"/>
  <setBody>
    <constant>What is Apache Camel?</constant>
  </setBody>
  <to uri="google-vertexai:my-project:us-east5:claude-sonnet-4@20250514?operation=rawPredict&amp;publisher=anthropic"/>
  <log message="${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:claude
      steps:
        - setBody:
            constant: What is Apache Camel?
        - to:
            uri: "google-vertexai:my-project:us-east5:claude-sonnet-4@20250514"
            parameters:
              operation: rawPredict
              publisher: anthropic
        - log:
            message: "${body}"
```

The component automatically wraps simple text prompts in the required Anthropic format.

### Streaming Chat with Gemini

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:streaming")
    .setBody(constant("Tell me a story"))
    .to("google-vertexai:my-project:us-central1:gemini-2.0-flash?operation=generateChatStreaming&maxOutputTokens=512")
    .log("Response: ${body}, Chunks: ${header.CamelGoogleVertexAIChunkCount}");
```

```xml
<route>
  <from uri="direct:streaming"/>
  <setBody>
    <constant>Tell me a story</constant>
  </setBody>
  <to uri="google-vertexai:my-project:us-central1:gemini-2.0-flash?operation=generateChatStreaming&amp;maxOutputTokens=512"/>
  <log message="Response: ${body}, Chunks: ${header.CamelGoogleVertexAIChunkCount}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:streaming
      steps:
        - setBody:
            constant: Tell me a story
        - to:
            uri: google-vertexai:my-project:us-central1:gemini-2.0-flash
            parameters:
              operation: generateChatStreaming
              maxOutputTokens: 512
        - log:
            message: "Response: ${body}, Chunks: ${header.CamelGoogleVertexAIChunkCount}"
```

### Image Generation with Imagen

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:image")
    .setBody(constant("A sunset over mountains"))
    .setHeader("CamelGoogleVertexAIImageNumberOfImages", constant(1))
    .to("google-vertexai:my-project:us-central1:imagen-3.0-generate-002?operation=generateImage")
    .log("Generated ${body.size()} image(s)");
```

```xml
<route>
  <from uri="direct:image"/>
  <setBody>
    <constant>A sunset over mountains</constant>
  </setBody>
  <setHeader name="CamelGoogleVertexAIImageNumberOfImages">
    <constant resultType="java.lang.Integer">1</constant>
  </setHeader>
  <to uri="google-vertexai:my-project:us-central1:imagen-3.0-generate-002?operation=generateImage"/>
  <log message="Generated ${body.size()} image(s)"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:image
      steps:
        - setBody:
            constant: A sunset over mountains
        - setHeader:
            name: CamelGoogleVertexAIImageNumberOfImages
            constant: 1
        - to:
            uri: google-vertexai:my-project:us-central1:imagen-3.0-generate-002
            parameters:
              operation: generateImage
        - log:
            message: "Generated ${body.size()} image(s)"
```

The body will contain a `List<Image>` with the generated images. Each `Image` has `imageBytes()` and `mimeType()` methods.

### Text Embeddings

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:embed")
    .setBody(constant("Apache Camel is an integration framework"))
    .to("google-vertexai:my-project:us-central1:text-embedding-005?operation=generateEmbeddings")
    .log("Embedding dimensions: ${body[0].size()}");
```

```xml
<route>
  <from uri="direct:embed"/>
  <setBody>
    <constant>Apache Camel is an integration framework</constant>
  </setBody>
  <to uri="google-vertexai:my-project:us-central1:text-embedding-005?operation=generateEmbeddings"/>
  <log message="Embedding dimensions: ${body[0].size()}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:embed
      steps:
        - setBody:
            constant: Apache Camel is an integration framework
        - to:
            uri: google-vertexai:my-project:us-central1:text-embedding-005
            parameters:
              operation: generateEmbeddings
        - log:
            message: "Embedding dimensions: ${body[0].size()}"
```

The body will contain a `List<List<Float>>` — one embedding vector per input text. For batch embeddings, pass a `List<String>` as the body.

### Multimodal Input (Image + Text)

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:multimodal")
    .setHeader("CamelGoogleVertexAIPrompt", constant("Describe this image"))
    .setHeader("CamelGoogleVertexAIMediaGcsUri", constant("gs://my-bucket/photo.jpg"))
    .setHeader("CamelGoogleVertexAIMediaMimeType", constant("image/jpeg"))
    .to("google-vertexai:my-project:us-central1:gemini-2.0-flash?operation=generateMultimodal")
    .log("${body}");
```

```xml
<route>
  <from uri="direct:multimodal"/>
  <setHeader name="CamelGoogleVertexAIPrompt">
    <constant>Describe this image</constant>
  </setHeader>
  <setHeader name="CamelGoogleVertexAIMediaGcsUri">
    <constant>gs://my-bucket/photo.jpg</constant>
  </setHeader>
  <setHeader name="CamelGoogleVertexAIMediaMimeType">
    <constant>image/jpeg</constant>
  </setHeader>
  <to uri="google-vertexai:my-project:us-central1:gemini-2.0-flash?operation=generateMultimodal"/>
  <log message="${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:multimodal
      steps:
        - setHeader:
            name: CamelGoogleVertexAIPrompt
            constant: Describe this image
        - setHeader:
            name: CamelGoogleVertexAIMediaGcsUri
            constant: "gs://my-bucket/photo.jpg"
        - setHeader:
            name: CamelGoogleVertexAIMediaMimeType
            constant: image/jpeg
        - to:
            uri: google-vertexai:my-project:us-central1:gemini-2.0-flash
            parameters:
              operation: generateMultimodal
        - log:
            message: "${body}"
```

You can also pass inline image bytes via the `CamelGoogleVertexAIMediaData` header instead of a GCS URI.

### Streaming Claude with streamRawPredict

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:stream-claude")
    .setBody(constant("What is Apache Camel?"))
    .to("google-vertexai:my-project:us-east5:claude-sonnet-4@20250514?operation=streamRawPredict&publisher=anthropic")
    .log("${body}");
```

```xml
<route>
  <from uri="direct:stream-claude"/>
  <setBody>
    <constant>What is Apache Camel?</constant>
  </setBody>
  <to uri="google-vertexai:my-project:us-east5:claude-sonnet-4@20250514?operation=streamRawPredict&amp;publisher=anthropic"/>
  <log message="${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:stream-claude
      steps:
        - setBody:
            constant: What is Apache Camel?
        - to:
            uri: "google-vertexai:my-project:us-east5:claude-sonnet-4@20250514"
            parameters:
              operation: streamRawPredict
              publisher: anthropic
        - log:
            message: "${body}"
```

### Claude with Custom Request

For more control, pass a JSON body:

_Java-only: requires Java text block for JSON request body_

```java
from("direct:claude")
    .process(exchange -> {
        String json = """
            {
                "anthropic_version": "vertex-2023-10-16",
                "max_tokens": 512,
                "messages": [{"role": "user", "content": "Write a haiku"}]
            }
            """;
        exchange.getMessage().setBody(json);
    })
    .to("google-vertexai:my-project:us-east5:claude-sonnet-4@20250514?operation=rawPredict&publisher=anthropic")
    .log("${body}");
```

## Supported Models

### Google Models

Use with `generateText`, `generateChat`, `generateChatStreaming`, `generateCode`, `generateImage`, `generateEmbeddings`, or `generateMultimodal`:

-   **Gemini**: `gemini-2.5-pro`, `gemini-2.5-flash`, `gemini-2.0-flash`, `gemini-1.5-pro`, `gemini-1.5-flash`
    
-   **Imagen**: `imagen-4.0-generate-preview-05-20`, `imagen-3.0-generate-002`
    
-   **Gemma**: `gemma-3-27b-it`, `gemma-2-27b-it`, `gemma-2-9b-it`
    
-   **Embeddings**: `text-embedding-005`, `text-embedding-004`
    

### Partner Models

Use with `rawPredict` or `streamRawPredict` and the appropriate `publisher`:

  
| Publisher | Models | Regions |
| --- | --- | --- |
| `anthropic` | `claude-sonnet-4@20250514`, `claude-opus-4@20250514`, `claude-3-5-haiku@20241022` | us-east5, europe-west1 |
| `meta` | `llama-4-maverick-17b-128e-instruct-maas`, `llama-3.3-70b-instruct-maas` | us-central1 |
| `mistralai` | `mistral-medium-3`, `mistral-small-2503`, `codestral-2` | us-central1, europe-west4 |

See `VertexAIModels` for all available model identifiers.

## Dependencies

Add the following dependency:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-vertexai</artifactId>
    <version>x.x.x</version>
</dependency>
```