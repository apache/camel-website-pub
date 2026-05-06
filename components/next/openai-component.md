# OpenAI

**Since Camel 4.17**

**Only producer is supported**

The OpenAI component provides integration with OpenAI and OpenAI-compatible APIs for chat completion, text embeddings, and audio transcription using the official openai-java SDK.

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
    
-   `tool-execution` - Execute MCP tool calls from a stored chat completion response (used in manual tool loops)
    
-   `audio-transcription` - Transcribe audio files to text using speech-to-text models (e.g., Whisper, GPT-4o Transcribe)
    

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

The OpenAI component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiKey** (producer) | Default API key for all endpoints. |  | String |
| **audioModel** (producer) | Default model for audio transcription endpoints. |  | String |
| **baseUrl** (producer) | Default base URL for all endpoints. | [https://api.openai.com/v1](https://api.openai.com/v1) | String |
| **embeddingModel** (producer) | Default model for embeddings endpoints. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **model** (producer) | Default model for chat completion endpoints. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The OpenAI endpoint is configured using URI syntax:

openai:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The operation to perform: 'chat-completion', 'embeddings', 'tool-execution', or 'audio-transcription'.

Enum values:

-   chat-completion
    
-   embeddings
    
-   tool-execution
    
-   audio-transcription
    





 |  | OpenAIOperations |

### Query Parameters (46 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalBodyProperty** (producer) | Additional JSON properties to include in the request body (e.g. additionalBodyProperty.traceId=123). This is a multi-value option with prefix: additionalBodyProperty. |  | Map |
| **apiKey** (producer) | OpenAI API key. Can also be set via OPENAI\_API\_KEY environment variable. |  | String |
| **audioLanguage** (producer) | The language of the input audio in ISO-639-1 format (e.g., 'en'). Improves accuracy and latency. |  | String |
| **audioModel** (producer) | The model to use for audio transcription (e.g., whisper-1, gpt-4o-transcribe). |  | String |
| **audioPrompt** (producer) | Optional text to guide the model’s style or continue a previous audio segment. |  | String |
| **audioResponseFormat** (producer) | 
The format of the transcription output.

Enum values:

-   json
    
-   text
    
-   srt
    
-   verbose\_json
    
-   vtt
    





 | json | String |
| **audioTemperature** (producer) | Sampling temperature for transcription (0.0 to 1.0). |  | Double |
| **audioTimestampGranularities** (producer) | Comma-separated timestamp granularities: 'word', 'segment', or 'word,segment'. Only applicable with verbose\_json response format. |  | String |
| **autoToolExecution** (producer) | When true and MCP servers are configured, automatically execute tool calls and loop back to the model. When false, tool calls are returned as the message body for manual handling. | true | boolean |
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
| **maxToolIterations** (producer) | Maximum number of tool call loop iterations to prevent infinite loops. | 50 | int |
| **mcpProtocolVersions** (producer) | Comma-separated list of MCP protocol versions to advertise when connecting to MCP servers using Streamable HTTP transport. When not set, the SDK default is used. Example: 2024-11-05,2025-03-26,2025-06-18. |  | String |
| **mcpReconnect** (producer) | Automatically reconnect to MCP servers when a tool call fails due to a transport error, and retry the call once. | true | boolean |
| **mcpServer** (producer) | MCP (Model Context Protocol) server configurations. Define servers using prefix notation: mcpServer..transportType=stdiossestreamableHttp, mcpServer..command= (stdio), mcpServer..args= (stdio), mcpServer..url= (sse/streamableHttp), mcpServer..oauthProfile= (OAuth profile for HTTP auth, requires camel-oauth). This is a multi-value option with prefix: mcpServer. |  | Map |
| **mcpTimeout** (producer) | Timeout in seconds for MCP tool call requests. Applies to all MCP operations including tool execution and initialization. | 20 | int |
| **model** (producer) | The model to use for chat completion. |  | String |
| **outputClass** (producer) | Fully qualified class name for structured output using response format. |  | String |
| **storeFullResponse** (producer) | Store the full response in the exchange property 'CamelOpenAIResponse' in non-streaming mode. | false | boolean |
| **streaming** (producer) | Enable streaming responses. | false | boolean |
| **stripThinking** (producer) | Strip …​ blocks from model responses (used by reasoning models like Qwen3, DeepSeek-R1). The thinking content is stored in the CamelOpenAIThinkingContent header. | false | boolean |
| **systemMessage** (producer) | System message to prepend. When set and conversationMemory is enabled, the conversation history is reset. |  | String |
| **temperature** (producer) | Temperature for response generation (0.0 to 2.0). |  | Double |
| **topP** (producer) | Top P for response generation (0.0 to 1.0). |  | Double |
| **userMessage** (producer) | Default user message text to use when no prompt is provided. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used instead of apiKey. Requires camel-oauth on the classpath. The profile properties are resolved from camel.oauth..client-id, camel.oauth..client-secret, and camel.oauth..token-endpoint. |  | String |
| **sslContextParameters** (security) | SSLContextParameters to use for configuring SSL/TLS. When set, takes precedence over the individual sslTruststore, sslKeystore, and sslProtocol options. |  | SSLContextParameters |
| **sslEndpointAlgorithm** (security) | The endpoint identification algorithm to validate the server hostname using the server certificate. Set to an empty string or 'none' to disable hostname verification. | https | String |
| **sslKeymanagerAlgorithm** (security) | The algorithm used by the key manager factory for SSL connections. | SunX509 | String |
| **sslKeyPassword** (security) | The password of the private key in the key store file. |  | String |
| **sslKeystoreLocation** (security) | The location of the key store file. This is optional and can be used for two-way authentication for the OpenAI API. |  | String |
| **sslKeystorePassword** (security) | The store password for the key store file. |  | String |
| **sslKeystoreType** (security) | The file format of the key store file. | JKS | String |
| **sslProtocol** (security) | The SSL protocol used to generate the SSLContext. | TLSv1.3 | String |
| **sslTrustmanagerAlgorithm** (security) | The algorithm used by the trust manager factory for SSL connections. | PKIX | String |
| **sslTruststoreLocation** (security) | The location of the trust store file, used to validate the server’s certificate. |  | String |
| **sslTruststorePassword** (security) | The password for the trust store file. If a password is not set, the configured trust store can still be used, but integrity checking is disabled. |  | String |
| **sslTruststoreType** (security) | The file format of the trust store file. | JKS | String |

## Message Headers

The OpenAI component supports 38 message header(s), which is/are listed below:

   
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
| **CamelOpenAIStripThinking** (producer) Constant: [`STRIP_THINKING`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#STRIP_THINKING) | Whether to strip …​ blocks from the response body. |  | Boolean |
| **CamelOpenAIThinkingContent** (producer) Constant: [`THINKING_CONTENT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#THINKING_CONTENT) | The thinking content extracted from …​ blocks in the model response. |  | String |
| **CamelOpenAIResponseModel** (producer) Constant: [`RESPONSE_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#RESPONSE_MODEL) | The model used for the completion response. |  | String |
| **CamelOpenAIResponseId** (producer) Constant: [`RESPONSE_ID`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#RESPONSE_ID) | The unique identifier for the completion response. |  | String |
| **CamelOpenAIFinishReason** (producer) Constant: [`FINISH_REASON`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#FINISH_REASON) | The reason the completion finished (e.g., stop, length, content\_filter). |  | String |
| **CamelOpenAIPromptTokens** (producer) Constant: [`PROMPT_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#PROMPT_TOKENS) | The number of tokens used in the prompt. |  | Integer |
| **CamelOpenAICompletionTokens** (producer) Constant: [`COMPLETION_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#COMPLETION_TOKENS) | The number of tokens used in the completion. |  | Integer |
| **CamelOpenAITotalTokens** (producer) Constant: [`TOTAL_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#TOTAL_TOKENS) | The total number of tokens used (prompt completion). |  | Integer |
| **CamelOpenAIToolIterations** (producer) Constant: [`TOOL_ITERATIONS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#TOOL_ITERATIONS) | Number of tool call iterations performed in the agentic loop. |  | Integer |
| **CamelOpenAIMcpToolCalls** (producer) Constant: [`MCP_TOOL_CALLS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MCP_TOOL_CALLS) | List of tool names called during the agentic loop. |  | List |
| **CamelOpenAIMcpReturnDirect** (producer) Constant: [`MCP_RETURN_DIRECT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MCP_RETURN_DIRECT) | Whether the response came directly from a tool with returnDirect=true, rather than from the LLM. |  | Boolean |
| **CamelOpenAIResponse** (producer) Constant: [`RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#RESPONSE) | The complete OpenAI response object. |  | ChatCompletion |
| **CamelOpenAIEmbeddingModel** (producer) Constant: [`EMBEDDING_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_MODEL) | The model to use for embeddings. |  | String |
| **CamelOpenAIEmbeddingDimensions** (producer) Constant: [`EMBEDDING_DIMENSIONS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_DIMENSIONS) | Number of output dimensions. |  | Integer |
| **CamelOpenAIEmbeddingResponseModel** (producer) Constant: [`EMBEDDING_RESPONSE_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_RESPONSE_MODEL) | The embedding model used in the response. |  | String |
| **CamelOpenAIEmbeddingCount** (producer) Constant: [`EMBEDDING_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_COUNT) | Number of embeddings returned. |  | Integer |
| **CamelOpenAIEmbeddingVectorSize** (producer) Constant: [`EMBEDDING_VECTOR_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_VECTOR_SIZE) | Vector dimensions of the embeddings. |  | Integer |
| **CamelOpenAIReferenceEmbedding** (producer) Constant: [`REFERENCE_EMBEDDING`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#REFERENCE_EMBEDDING) | Reference embedding vector for similarity comparison. |  | List |
| **CamelOpenAISimilarityScore** (producer) Constant: [`SIMILARITY_SCORE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#SIMILARITY_SCORE) | Calculated cosine similarity score (0.0 to 1.0). |  | Double |
| **CamelOpenAIOriginalText** (producer) Constant: [`ORIGINAL_TEXT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#ORIGINAL_TEXT) | Original text content when embeddings operation is used. |  | String or List |
| **CamelOpenAIAudioModel** (producer) Constant: [`AUDIO_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_MODEL) | The model to use for audio transcription. |  | String |
| **CamelOpenAIAudioLanguage** (producer) Constant: [`AUDIO_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_LANGUAGE) | The language of the input audio (ISO-639-1). |  | String |
| **CamelOpenAIAudioResponseFormat** (producer) Constant: [`AUDIO_RESPONSE_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_RESPONSE_FORMAT) | The response format for audio transcription (json, text, srt, verbose\_json, vtt). |  | String |
| **CamelOpenAIAudioTemperature** (producer) Constant: [`AUDIO_TEMPERATURE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_TEMPERATURE) | Sampling temperature for audio transcription (0.0 to 1.0). |  | Double |
| **CamelOpenAIAudioPrompt** (producer) Constant: [`AUDIO_PROMPT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_PROMPT) | Optional text to guide the model’s style or continue a previous audio segment. |  | String |
| **CamelOpenAIAudioTimestampGranularities** (producer) Constant: [`AUDIO_TIMESTAMP_GRANULARITIES`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_TIMESTAMP_GRANULARITIES) | Comma-separated timestamp granularities: word, segment, or word,segment (verbose\_json only). |  | String |
| **CamelOpenAIAudioDuration** (producer) Constant: [`AUDIO_DURATION`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_DURATION) | Duration of the audio in seconds (verbose\_json only). |  | Double |
| **CamelOpenAIAudioDetectedLanguage** (producer) Constant: [`AUDIO_DETECTED_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_DETECTED_LANGUAGE) | Language detected in the audio (verbose\_json only). |  | String |

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

#### OAuth Authentication

When using an identity provider (e.g., Azure AD for Azure OpenAI), set the `oauthProfile` parameter to acquire an access token via the OAuth 2.0 Client Credentials grant. The token is used in place of the API key. This requires `camel-oauth` on the classpath.

```properties
camel.oauth.azure.client-id=my-client
camel.oauth.azure.client-secret=my-secret
camel.oauth.azure.token-endpoint=https://login.microsoftonline.com/tenant/oauth2/v2.0/token
camel.oauth.azure.scope=https://cognitiveservices.azure.com/.default
```

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4&oauthProfile=azure");
```

MCP servers can also use OAuth independently via per-server `oauthProfile`:

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&oauthProfile=azure"
        + "&mcpServer.tools.transportType=streamableHttp"
        + "&mcpServer.tools.url=https://mcp.internal/mcp"
        + "&mcpServer.tools.oauthProfile=keycloak");
```

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

## SSL Configuration

The component supports custom SSL/TLS configuration for connecting to OpenAI or OpenAI-compatible endpoints that use self-signed certificates, private CAs, or require mutual TLS (mTLS) authentication.

When no SSL parameters are set, the default JVM trust store is used.

### Using SSLContextParameters

The component implements `SSLContextParametersAware` and supports Camel’s standard `SSLContextParameters` for SSL configuration. When set, `SSLContextParameters` takes precedence over the individual `ssl*` properties (same pattern as `camel-kafka`).

```java
KeyStoreParameters trustStoreParams = new KeyStoreParameters();
trustStoreParams.setResource("/path/to/truststore.jks");
trustStoreParams.setPassword("changeit");

TrustManagersParameters trustManagers = new TrustManagersParameters();
trustManagers.setKeyStore(trustStoreParams);

SSLContextParameters sslContextParameters = new SSLContextParameters();
sslContextParameters.setTrustManagers(trustManagers);

from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&baseUrl=https://my-llm-server:8443/v1"
        + "&sslContextParameters=#sslContextParameters");
```

To use global SSL context parameters for all OpenAI endpoints:

```java
OpenAIComponent openai = context.getComponent("openai", OpenAIComponent.class);
openai.setUseGlobalSslContextParameters(true);
```

### Custom Trust Store

To trust a server using a self-signed or private CA certificate:

-   Java
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&baseUrl=https://my-llm-server:8443/v1"
        + "&sslTruststoreLocation=/path/to/truststore.jks"
        + "&sslTruststorePassword=changeit");
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: openai:chat-completion
            parameters:
              model: gpt-4
              baseUrl: https://my-llm-server:8443/v1
              sslTruststoreLocation: /path/to/truststore.jks
              sslTruststorePassword: changeit
```

### Mutual TLS (mTLS)

For two-way authentication, configure both trust store and key store:

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&baseUrl=https://my-llm-server:8443/v1"
        + "&sslTruststoreLocation=/path/to/truststore.jks"
        + "&sslTruststorePassword=changeit"
        + "&sslKeystoreLocation=/path/to/keystore.jks"
        + "&sslKeystorePassword=changeit"
        + "&sslKeyPassword=keypass");
```

### Disabling Hostname Verification

In development or test environments, hostname verification can be disabled by setting `sslEndpointAlgorithm` to an empty string or `none`:

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&baseUrl=https://localhost:8443/v1"
        + "&sslTruststoreLocation=/path/to/truststore.jks"
        + "&sslTruststorePassword=changeit"
        + "&sslEndpointAlgorithm=none");
```

> **Warning**
> Disabling hostname verification is insecure and should only be used in non-production environments.

### SSL Parameters

   
| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `sslContextParameters` | SSLContextParameters |  | Camel SSL context parameters. When set, takes precedence over the individual `ssl*` options below |
| `sslTruststoreLocation` | String |  | Location of the trust store file |
| `sslTruststorePassword` | String |  | Trust store password |
| `sslTruststoreType` | String | `JKS` | Trust store format (e.g., `JKS`, `PKCS12`) |
| `sslKeystoreLocation` | String |  | Location of the key store file (for mTLS) |
| `sslKeystorePassword` | String |  | Key store password |
| `sslKeystoreType` | String | `JKS` | Key store format (e.g., `JKS`, `PKCS12`) |
| `sslKeyPassword` | String |  | Private key password in the key store |
| `sslProtocol` | String | `TLSv1.3` | SSL protocol for generating the SSLContext |
| `sslKeymanagerAlgorithm` | String | `SunX509` | Algorithm for the key manager factory |
| `sslTrustmanagerAlgorithm` | String | `PKIX` | Algorithm for the trust manager factory |
| `sslEndpointAlgorithm` | String | `https` | Hostname verification algorithm; set to empty or `none` to disable |

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

Using the [PGVector](pgvector-component.md) component:

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
        - setHeader:
            name: CamelPgVectorAction
            constant: UPSERT
        - setHeader:
            name: CamelPgVectorTextContent
            simple: "${variable.text}"
        - to:
            uri: pgvector:documents

# Similarity search
- route:
    from:
      uri: direct:search
      steps:
        - to:
            uri: openai:embeddings
            parameters:
              embeddingModel: nomic-embed-text
        - setHeader:
            name: CamelPgVectorAction
            constant: SIMILARITY_SEARCH
        - setHeader:
            name: CamelPgVectorQueryTopK
            constant: 5
        - to:
            uri: pgvector:documents
```

The pgvector component handles table creation, HNSW indexing, upsert with conflict resolution, and similarity search with configurable distance types (cosine, euclidean, inner product). See the [PGVector component documentation](pgvector-component.md) for details.

For custom table schemas, complex queries (joins, CTEs), or integration with existing PostgreSQL tables, you can use `camel-sql` directly with the pgvector extension:

```yaml
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

## Audio Transcription Operation

The `audio-transcription` operation transcribes audio files to text using OpenAI’s speech-to-text models (Whisper, GPT-4o Transcribe).

### Basic Audio Transcription

-   Java
    
-   YAML
    

```java
from("file:audio?noop=true")
    .to("openai:audio-transcription?audioModel=whisper-1")
    .log("Transcription: ${body}");
```

```yaml
- route:
    from:
      uri: direct:transcribe
      steps:
        - to:
            uri: openai:audio-transcription
            parameters:
              audioModel: whisper-1
        - log: "Transcription: ${body}"
```

### Input Handling

The audio transcription operation accepts the following types in the message body:

-   `java.io.File` - Audio file reference
    
-   `java.nio.file.Path` - Path to an audio file
    
-   `java.io.InputStream` - Audio data stream
    
-   `byte[]` - Raw audio bytes
    

Supported audio formats: flac, mp3, mp4, mpeg, mpga, m4a, ogg, wav, webm.

### Audio Transcription Parameters

   
| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `audioModel` | String |  | The model to use (e.g., `whisper-1`, `gpt-4o-transcribe`). Required. |
| `audioLanguage` | String |  | Input audio language in ISO-639-1 format (e.g., `en`). Improves accuracy. |
| `audioPrompt` | String |  | Optional text to guide the model’s style or continue a previous segment. |
| `audioResponseFormat` | String | `json` | Output format: `json`, `text`, `srt`, `verbose_json`, `vtt`. |
| `audioTemperature` | Double |  | Sampling temperature (0.0 to 1.0). |
| `audioTimestampGranularities` | String |  | Comma-separated: `word`, `segment`, or `word,segment`. Only with `verbose_json`. |

### Audio Transcription Output Headers

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelOpenAIAudioDuration` | Double | Duration of the audio in seconds (verbose\_json only) |
| `CamelOpenAIAudioDetectedLanguage` | String | Language detected in the audio (verbose\_json only) |

### Audio Models by Provider

  
| Provider | Model | Description |
| --- | --- | --- |
| OpenAI | `whisper-1` | General-purpose speech recognition |
| OpenAI | `gpt-4o-transcribe` | High-accuracy transcription based on GPT-4o |
| OpenAI | `gpt-4o-mini-transcribe` | Lighter-weight GPT-4o variant |

### Local Audio Transcription Servers

The audio transcription operation works with any OpenAI-compatible server that implements the `POST /v1/audio/transcriptions` endpoint. It has been tested with:

-   [MLX Audio](https://github.com/ml-explore/mlx-audio) — `python3 -m mlx_audio.server --host 127.0.0.1 --port 8003`
    

Example using MLX Audio for local transcription:

```java
from("direct:transcribe")
    .to("openai:audio-transcription?audioModel=mlx-community/whisper-large-v3-turbo"
        + "&baseUrl=http://localhost:8003/v1");
```

> **Note**
> Some local servers require the model parameter to be a path (e.g., `./models/granite-speech-4.1-2b-8bit`). Refer to your server’s documentation for the expected model identifier format.

## MCP Tool Calling (Agentic Loop)

The component supports automatic tool calling via the [Model Context Protocol (MCP)](https://modelcontextprotocol.io). When MCP servers are configured, the component acts as an MCP client: it lists available tools, converts them to OpenAI function-calling format, and runs an agentic loop — the model requests tool calls, the component executes them via MCP, feeds results back, and repeats until the model produces a final text answer.

### MCP Server Configuration

MCP servers are configured inline on the endpoint URI using the `mcpServer.` prefix pattern. Each server is identified by a name, with sub-properties for transport type, command/URL, and arguments.

#### Streamable HTTP Transport

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&mcpServer.api.transportType=streamableHttp"
        + "&mcpServer.api.url=http://localhost:9090/mcp");
```

#### SSE Transport

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&mcpServer.weather.transportType=sse"
        + "&mcpServer.weather.url=http://localhost:8080");
```

#### Stdio Transport

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&mcpServer.fs.transportType=stdio"
        + "&mcpServer.fs.command=npx"
        + "&mcpServer.fs.args=-y,@modelcontextprotocol/server-filesystem,/tmp");
```

#### Multiple MCP Servers

Multiple servers can be configured on the same endpoint. Tools from all servers are merged and made available to the model:

-   Java
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&mcpServer.fs.transportType=stdio"
        + "&mcpServer.fs.command=npx"
        + "&mcpServer.fs.args=-y,@modelcontextprotocol/server-filesystem,/tmp"
        + "&mcpServer.weather.transportType=sse"
        + "&mcpServer.weather.url=http://localhost:8080");
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: openai:chat-completion
            parameters:
              model: gpt-4
              mcpServer.fs.transportType: stdio
              mcpServer.fs.command: npx
              mcpServer.fs.args: "-y,@modelcontextprotocol/server-filesystem,/tmp"
              mcpServer.weather.transportType: sse
              mcpServer.weather.url: http://localhost:8080
        - log: "${body}"
```

### Agentic Loop Behavior

When the model responds with tool calls, the component automatically:

1.  Executes each tool call via the corresponding MCP server
    
2.  Sends the tool results back to the model
    
3.  Repeats until the model produces a final text response
    

The `maxToolIterations` option (default: 50) prevents infinite loops. If exceeded, an `IllegalStateException` is thrown.

Set `autoToolExecution=false` to disable the agentic loop and receive raw tool calls in the message body instead:

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&autoToolExecution=false"
        + "&mcpServer.api.transportType=streamableHttp"
        + "&mcpServer.api.url=http://localhost:9090/mcp")
    .log("Tool calls: ${body}"); // body is the raw tool calls list
```

### Manual Tool Loop with `tool-execution` Operation

When `autoToolExecution=false`, you can implement your own tool loop using the `openai:tool-execution` operation and Camel’s `loopDoWhile` EIP. This gives you full control to add logging, filtering, retry logic, or custom routing between tool calls — without writing any Java code.

The `tool-execution` operation:

-   Reads the stored `ChatCompletion` response (requires `storeFullResponse=true` on the chat-completion call)
    
-   Extracts tool calls and executes them via MCP
    
-   Rebuilds the conversation history with the proper message chain
    
-   Clears the body for the next chat-completion call
    

-   Java
    
-   YAML
    

```java
from("direct:chat")
    // Save the original prompt for the tool-execution operation
    .setProperty("originalPrompt", body())

    // Initial call: tools are listed but not auto-executed
    .to("openai:chat-completion?autoToolExecution=false"
        + "&conversationMemory=true&storeFullResponse=true"
        + "&mcpServer.api.transportType=streamableHttp"
        + "&mcpServer.api.url=http://localhost:9090/mcp")

    // Loop while the model requests tool calls
    .loopDoWhile(header("CamelOpenAIFinishReason").isEqualTo("tool_calls"))
        // Execute tool calls via MCP
        .to("openai:tool-execution"
            + "?mcpServer.api.transportType=streamableHttp"
            + "&mcpServer.api.url=http://localhost:9090/mcp")
        // Send updated conversation back to the model
        .to("openai:chat-completion?autoToolExecution=false"
            + "&conversationMemory=true&storeFullResponse=true"
            + "&mcpServer.api.transportType=streamableHttp"
            + "&mcpServer.api.url=http://localhost:9090/mcp")
    .end()

    .log("Final answer: ${body}");
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - setProperty:
            name: originalPrompt
            simple: "${body}"
        - to:
            uri: openai:chat-completion
            parameters:
              autoToolExecution: false
              conversationMemory: true
              storeFullResponse: true
              mcpServer.api.transportType: streamableHttp
              mcpServer.api.url: http://localhost:9090/mcp
        - loopDoWhile:
            simple: "${header.CamelOpenAIFinishReason} == 'tool_calls'"
            steps:
              - to:
                  uri: openai:tool-execution
                  parameters:
                    mcpServer.api.transportType: streamableHttp
                    mcpServer.api.url: http://localhost:9090/mcp
              - to:
                  uri: openai:chat-completion
                  parameters:
                    autoToolExecution: false
                    conversationMemory: true
                    storeFullResponse: true
                    mcpServer.api.transportType: streamableHttp
                    mcpServer.api.url: http://localhost:9090/mcp
        - log: "Final answer: ${body}"
```

> **Note**
> The `tool-execution` operation requires the `originalPrompt` exchange property (set via `setProperty` before the first call) and the `CamelOpenAIResponse` exchange property (set by `storeFullResponse=true`).

### returnDirect

MCP tools can declare `returnDirect=true` in their annotations. When **all** tools invoked in a single batch carry this flag, the component short-circuits: it returns the tool result directly as the exchange body without sending it back to the model for further processing.

This is useful for tools whose output is the definitive answer (e.g., a database lookup) and does not need LLM interpretation.

The `CamelOpenAIMcpReturnDirect` header is set to `true` when this occurs, so downstream processors can distinguish tool-direct responses from LLM-generated ones.

> **Note**
> Tool execution errors always bypass `returnDirect` — errors are sent back to the model for graceful handling.

### MCP Tool Call Headers

The following headers are set after the agentic loop completes:

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelOpenAIToolIterations` | Integer | Number of tool call iterations performed |
| `CamelOpenAIMcpToolCalls` | List<String> | Ordered list of tool names called during the loop |
| `CamelOpenAIMcpReturnDirect` | Boolean | `true` if the response came directly from a tool with `returnDirect` |

### Conversation Memory with MCP Tools

When `conversationMemory=true`, the full tool call chain is stored in the conversation history exchange property (`CamelOpenAIConversationHistory`). This includes:

-   Assistant messages containing tool call requests
    
-   Tool result messages with execution outputs
    
-   The final assistant text response
    

This enables multi-turn agentic conversations where the model can reference previous tool interactions across exchanges.

#### Multi-Turn Example

-   Java
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?conversationMemory=true"
        + "&mcpServer.api.transportType=streamableHttp"
        + "&mcpServer.api.url=http://localhost:9090/mcp")
    .to("mock:response");
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: openai:chat-completion
            parameters:
              conversationMemory: true
              mcpServer.api.transportType: streamableHttp
              mcpServer.api.url: http://localhost:9090/mcp
        - log: "${body}"
```

With this route, a multi-turn conversation works as follows:

```java
// Turn 1: the model calls the "add" tool and returns the result
Exchange turn1 = template.request("direct:chat", e ->
    e.getIn().setBody("Use the add tool to add 15 and 27"));
// Response: "The result of adding 15 and 27 is 42."

// Turn 2: carry forward the conversation history
List<?> history = turn1.getProperty("CamelOpenAIConversationHistory", List.class);
Exchange turn2 = template.request("direct:chat", e -> {
    e.getIn().setBody("What numbers did you just add?");
    e.setProperty("CamelOpenAIConversationHistory", history);
});
// Response: "I added 15 and 27." — the model remembers the tool interaction
```

The conversation history includes the full tool call chain from turn 1 (the assistant’s tool call request, the tool result, and the final answer), so in turn 2 the model has complete context of what happened — including which tools were called and what they returned.

> **Note**
> When `systemMessage` is set and `conversationMemory` is enabled, the conversation history is reset. This allows starting fresh conversations within the same route.

### MCP Protocol Version

When using the Streamable HTTP transport, the component advertises MCP protocol versions during initialization. By default, the SDK’s built-in versions are used. If your MCP server does not support the latest protocol version, you can restrict the advertised versions:

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&mcpServer.api.transportType=streamableHttp"
        + "&mcpServer.api.url=http://localhost:9090/mcp"
        + "&mcpProtocolVersions=2024-11-05,2025-03-26,2025-06-18");
```

### MCP Connection Recovery

When `mcpReconnect=true` (the default), the component automatically recovers from MCP server connection failures. If a tool call fails with a transport error, the component:

1.  Closes the failed connection
    
2.  Creates a new transport and client using the original server configuration
    
3.  Re-initializes and re-lists available tools
    
4.  Retries the tool call once on the new connection
    

This handles scenarios where an MCP server restarts, a network connection drops, or a stdio subprocess dies. If reconnection fails, the original transport error is propagated.

Set `mcpReconnect=false` to disable automatic recovery:

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&mcpReconnect=false"
        + "&mcpServer.api.transportType=streamableHttp"
        + "&mcpServer.api.url=http://localhost:9090/mcp");
```

### Error Handling in the Agentic Loop

 
| Scenario | Behavior |
| --- | --- |
| MCP client initialization failure | Route fails to start (`RuntimeException` during `doStart()`) |
| Tool execution throws an exception | Error is caught, logged as WARN, and sent as tool result text to the model |
| MCP transport error (`mcpReconnect=true`) | Automatic reconnection and retry (once). If retry fails, error is sent to the model |
| MCP `CallToolResult.isError()` is true | Error content is sent as tool result text to the model |
| Tool name not found in any server | `IllegalStateException` is thrown |
| Max iterations exceeded | `IllegalStateException` is thrown with the tool call log |
| Streaming + MCP tools with autoToolExecution | Falls back to non-streaming (logged as INFO) |

## Error Handling

The component may throw the following exceptions:

-   `IllegalArgumentException`:
    
    -   When an invalid operation is specified (supported: `chat-completion`, `embeddings`, `tool-execution`, `audio-transcription`)
        
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

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.openai.api-key** | Default API key for all endpoints. |  | String |
| **camel.component.openai.audio-model** | Default model for audio transcription endpoints. |  | String |
| **camel.component.openai.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.openai.base-url** | Default base URL for all endpoints. | [https://api.openai.com/v1](https://api.openai.com/v1) | String |
| **camel.component.openai.embedding-model** | Default model for embeddings endpoints. |  | String |
| **camel.component.openai.enabled** | Whether to enable auto configuration of the openai component. This is enabled by default. |  | Boolean |
| **camel.component.openai.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.openai.model** | Default model for chat completion endpoints. |  | String |
| **camel.component.openai.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |