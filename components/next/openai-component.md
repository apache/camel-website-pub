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

The OpenAI component supports the following options which are listed below.

   
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

### Path Parameters

   
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

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalBodyProperty** (producer) | Additional JSON properties to include in the request body (e.g. additionalBodyProperty.traceId=123). This is a multi-value option with prefix: additionalBodyProperty. |  | Map |
| **additionalResponseHeader** (producer) | Map additional fields from the response message to Camel headers. The key is the field name in the API response, the value is the Camel header name (e.g. additionalResponseHeader.reasoning\_content=CamelMyReasoningHeader). This is a multi-value option with prefix: additionalResponseHeader. |  | Map |
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
| **mcpServer** (producer) | MCP (Model Context Protocol) server configurations. Define servers using prefix notation: mcpServer..transportType=stdiossestreamableHttp, (Note that sse is deprecated) mcpServer..command= (stdio), mcpServer..args= (stdio), mcpServer..url= (sse/streamableHttp), mcpServer..oauthProfile= (OAuth profile for HTTP auth, requires camel-oauth). This is a multi-value option with prefix: mcpServer. |  | Map |
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

The OpenAI component supports the following message header(s), which is/are listed below:

   
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
| **CamelOpenAIMediaType** (producer) Constant: [`MEDIA_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MEDIA_TYPE) | The MIME type of the message body when sending a file or binary content (File, WrappedFile, byte or InputStream) to the model. Takes precedence over component content-type headers and automatic MIME type detection. |  | String |
| **CamelOpenAIThinkingContent** (producer) Constant: [`THINKING_CONTENT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#THINKING_CONTENT) | The thinking content extracted from …​ blocks in the model response. |  | String |
| **CamelOpenAIReasoningContent** (producer) Constant: [`REASONING_CONTENT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#REASONING_CONTENT) | The reasoning content from the model response reasoning\_content field, used by thinking models like Qwen3 and DeepSeek-R1. |  | String |
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

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4&oauthProfile=azure");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="openai:chat-completion?model=gpt-4&amp;oauthProfile=azure"/>
</route>
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
              oauthProfile: azure
```

MCP servers can also use OAuth independently via per-server `oauthProfile`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&oauthProfile=azure"
        + "&mcpServer.tools.transportType=streamableHttp"
        + "&mcpServer.tools.url=https://mcp.internal/mcp"
        + "&mcpServer.tools.oauthProfile=keycloak");
```

```xml
<route>
    <from uri="direct:chat"/>
    <to uri="openai:chat-completion?model=gpt-4&amp;oauthProfile=azure&amp;mcpServer.tools.transportType=streamableHttp&amp;mcpServer.tools.url=https://mcp.internal/mcp&amp;mcpServer.tools.oauthProfile=keycloak"/>
</route>
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
              oauthProfile: azure
              mcpServer.tools.transportType: streamableHttp
              mcpServer.tools.url: https://mcp.internal/mcp
              mcpServer.tools.oauthProfile: keycloak
```

### Basic Chat Completion with String Input

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .setBody(constant("What is Apache Camel?"))
    .to("openai:chat-completion")
    .log("Response: ${body}");
```

```xml
<route>
  <from uri="direct:chat"/>
  <setBody>
    <constant>What is Apache Camel?</constant>
  </setBody>
  <to uri="openai:chat-completion"/>
  <log message="Response: ${body}"/>
</route>
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
        - log:
            message: "Response: ${body}"
```

### File-Backed Prompt with Text File

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:prompts?noop=true")
    .to("openai:chat-completion")
    .log("Response: ${body}");
```

```xml
<route>
  <from uri="file:prompts?noop=true"/>
  <to uri="openai:chat-completion"/>
  <log message="Response: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: file:prompts?noop=true
      steps:
        - to:
            uri: openai:chat-completion
        - log:
            message: "Response: ${body}"
```

### Image File Input with Vision Model

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:images?noop=true")
    .to("openai:chat-completion?model=gpt-4.1-mini&userMessage=Describe what you see in this image")
    .log("Response: ${body}");
```

```xml
<route>
  <from uri="file:images?noop=true"/>
  <to uri="openai:chat-completion?model=gpt-4.1-mini&amp;userMessage=Describe what you see in this image"/>
  <log message="Response: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: file:images?noop=true
      steps:
        - to:
            uri: openai:chat-completion
            parameters:
              model: gpt-4.1-mini
              userMessage: Describe what you see in this image
        - log:
            message: "Response: ${body}"
```

Image input also works with bodies produced by remote file and cloud storage components, such as FTP/SFTP (`WrappedFile`), AWS S3, Azure Blob Storage or MinIO (`byte[]` or `InputStream`). The MIME type is detected from the component’s content-type header or the file name:

-   Java
    
-   XML
    
-   YAML
    

```java
from("aws2-s3:my-bucket")
    .to("openai:chat-completion?model=gpt-4.1-mini&userMessage=Describe what you see in this image")
    .log("Response: ${body}");
```

```xml
<route>
  <from uri="aws2-s3:my-bucket"/>
  <to uri="openai:chat-completion?model=gpt-4.1-mini&amp;userMessage=Describe what you see in this image"/>
  <log message="Response: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: aws2-s3:my-bucket
      steps:
        - to:
            uri: openai:chat-completion
            parameters:
              model: gpt-4.1-mini
              userMessage: Describe what you see in this image
        - log:
            message: "Response: ${body}"
```

When no content-type header is available, set the `CamelOpenAIMediaType` header explicitly:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:image")
    .setHeader("CamelOpenAIMediaType", constant("image/png"))
    .setHeader("CamelOpenAIUserMessage", constant("Describe what you see in this image"))
    .to("openai:chat-completion?model=gpt-4.1-mini")
    .log("Response: ${body}");
```

```xml
<route>
  <from uri="direct:image"/>
  <setHeader name="CamelOpenAIMediaType">
    <constant>image/png</constant>
  </setHeader>
  <setHeader name="CamelOpenAIUserMessage">
    <constant>Describe what you see in this image</constant>
  </setHeader>
  <to uri="openai:chat-completion?model=gpt-4.1-mini"/>
  <log message="Response: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:image
      steps:
        - setHeader:
            name: CamelOpenAIMediaType
            constant: "image/png"
        - setHeader:
            name: CamelOpenAIUserMessage
            constant: "Describe what you see in this image"
        - to:
            uri: openai:chat-completion
            parameters:
              model: gpt-4.1-mini
        - log:
            message: "Response: ${body}"
```

> **Note**
> When using image input, the userMessage is required. Supported image formats are detected by MIME type (e.g., `image/png`, `image/jpeg`, `image/gif`, `image/webp`).

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
            expression:
              simple:
                expression: ${body}
            streaming: true
```

### Structured Output with outputClass

_Java-only: uses Java class definition for `outputClass` schema_

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

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:json-schema")
    .setBody(constant("Create a product description"))
    .setHeader("CamelOpenAIJsonSchema", constant("{\"type\":\"object\",\"properties\":{\"name\":{\"type\":\"string\"},\"price\":{\"type\":\"number\"}}}"))
    .to("openai:chat-completion")
    .log("JSON response: ${body}");
```

```xml
<route>
  <from uri="direct:json-schema"/>
  <setBody>
    <constant>Create a product description</constant>
  </setBody>
  <setHeader name="CamelOpenAIJsonSchema">
    <constant>{"type":"object","properties":{"name":{"type":"string"},"price":{"type":"number"}}}</constant>
  </setHeader>
  <to uri="openai:chat-completion"/>
  <log message="JSON response: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:json-schema
      steps:
        - setBody:
            constant: "Create a product description"
        - setHeader:
            name: CamelOpenAIJsonSchema
            constant: '{"type":"object","properties":{"name":{"type":"string"},"price":{"type":"number"}}}'
        - to:
            uri: openai:chat-completion
        - log:
            message: "JSON response: ${body}"
```

You can also load the schema from a resource file:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:json-schema-resource")
    .setBody(constant("Create a product description"))
    .to("openai:chat-completion?jsonSchema=resource:classpath:schemas/product.schema.json")
    .log("JSON response: ${body}");
```

```xml
<route>
  <from uri="direct:json-schema-resource"/>
  <setBody>
    <constant>Create a product description</constant>
  </setBody>
  <to uri="openai:chat-completion?jsonSchema=resource:classpath:schemas/product.schema.json"/>
  <log message="JSON response: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:json-schema-resource
      steps:
        - setBody:
            constant: "Create a product description"
        - to:
            uri: openai:chat-completion
            parameters:
              jsonSchema: "resource:classpath:schemas/product.schema.json"
        - log:
            message: "JSON response: ${body}"
```

> **Note**
> For full schema validation, integrate with the `camel-json-validator` component after receiving the response.

### Conversation Memory (Per Exchange)

Usage example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:conversation")
    .setBody(constant("My name is Alice"))
    .to("openai:chat-completion?conversationMemory=true")
    .log("First response: ${body}")
    .setBody(constant("What is my name?"))
    .to("openai:chat-completion?conversationMemory=true")
    .log("Second response: ${body}"); // Will remember "Alice"
```

```xml
<route>
  <from uri="direct:conversation"/>
  <setBody>
    <constant>My name is Alice</constant>
  </setBody>
  <to uri="openai:chat-completion?conversationMemory=true"/>
  <log message="First response: ${body}"/>
  <setBody>
    <constant>What is my name?</constant>
  </setBody>
  <to uri="openai:chat-completion?conversationMemory=true"/>
  <log message="Second response: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:conversation
      steps:
        - setBody:
            constant: "My name is Alice"
        - to:
            uri: openai:chat-completion
            parameters:
              conversationMemory: true
        - log:
            message: "First response: ${body}"
        - setBody:
            constant: "What is my name?"
        - to:
            uri: openai:chat-completion
            parameters:
              conversationMemory: true
        - log:
            message: "Second response: ${body}"
```

## Input Handling

The component accepts the following types of input in the message body:

1.  **String**: The prompt text is taken directly from the body
    
2.  **File**, **Path** or **WrappedFile** (the body type produced by the file, FTP, SFTP and SMB components): Used for file-based prompts. The component handles two types of files:
    
    -   **Text files** (MIME type starting with `text/`, plus `application/xml` and `application/json`): The file content is read and used as the prompt. If userMessage endpoint option or `CamelOpenAIUserMessage` is set, it overrides the file content
        
    -   **Image files** (MIME type starting with `image/`): The file is encoded as a base64 data URL and sent to vision-capable models. The userMessage is **required** when using image files
        
    
3.  **byte\[\]** or **InputStream** (the body types produced by cloud storage components such as AWS S3, Azure Blob Storage, Google Cloud Storage and MinIO): When the detected MIME type is an image, the content is encoded as a base64 data URL and sent to vision-capable models (userMessage is **required**). Otherwise, the content is converted to a String and used as the prompt
    

### MIME Type Detection

For `File`, `Path` and locally backed `WrappedFile` bodies, the MIME type is resolved in the following order:

1.  The `CamelOpenAIMediaType` header
    
2.  The `CamelFileContentType` header
    
3.  The file name extension, using the Camel built-in MIME type table (e.g., `.png`, `.jpg`, `.gif`, `.webp`, `.txt`, `.csv`, `.md`, `.xml`, `.json`)
    

For `byte[]`, `InputStream` and remote `WrappedFile` bodies, the MIME type is resolved in the following order:

1.  The `CamelOpenAIMediaType` header
    
2.  Cloud storage content-type headers: `CamelAwsS3ContentType`, `CamelAzureStorageBlobContentType`, `CamelAzureStorageDataLakeContentType`, `CamelGoogleCloudStorageContentType`, `CamelMinioContentType`, `CamelIBMCOSContentType`
    
3.  The `Content-Type` header
    
4.  The `CamelFileContentType` header
    
5.  The extension of the file name in the `CamelFileName` header
    

> **Note**
> Set the `CamelOpenAIMediaType` header to override the MIME type detection, for example when the payload has no content-type metadata or the detection picks the wrong type.

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

_Java-only: uses OpenAI SDK `ChatCompletionMessageParam` types_

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

_Java-only: programmatic `SSLContextParameters` configuration_

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

_Java-only: programmatic component configuration_

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

-   Java
    
-   XML
    
-   YAML
    

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

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="openai:chat-completion?model=gpt-4&amp;baseUrl=https://my-llm-server:8443/v1&amp;sslTruststoreLocation=/path/to/truststore.jks&amp;sslTruststorePassword=changeit&amp;sslKeystoreLocation=/path/to/keystore.jks&amp;sslKeystorePassword=changeit&amp;sslKeyPassword=keypass"/>
</route>
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
              sslKeystoreLocation: /path/to/keystore.jks
              sslKeystorePassword: changeit
              sslKeyPassword: keypass
```

### Disabling Hostname Verification

In development or test environments, hostname verification can be disabled by setting `sslEndpointAlgorithm` to an empty string or `none`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?model=gpt-4"
        + "&baseUrl=https://localhost:8443/v1"
        + "&sslTruststoreLocation=/path/to/truststore.jks"
        + "&sslTruststorePassword=changeit"
        + "&sslEndpointAlgorithm=none");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="openai:chat-completion?model=gpt-4&amp;baseUrl=https://localhost:8443/v1&amp;sslTruststoreLocation=/path/to/truststore.jks&amp;sslTruststorePassword=changeit&amp;sslEndpointAlgorithm=none"/>
</route>
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
              baseUrl: https://localhost:8443/v1
              sslTruststoreLocation: /path/to/truststore.jks
              sslTruststorePassword: changeit
              sslEndpointAlgorithm: none
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

## Reasoning Models

Some OpenAI-compatible models (e.g., Qwen3, DeepSeek-R1) return chain-of-thought reasoning in a separate `reasoning_content` field alongside the regular `content` in the API response. The component automatically extracts this field and sets it as the `CamelOpenAIReasoningContent` message header.

This is independent from the inline `<think>…​</think>` tag stripping controlled by `stripThinking`. A response can populate both headers simultaneously:

-   `CamelOpenAIReasoningContent` — from the API-level `reasoning_content` field
    
-   `CamelOpenAIThinkingContent` — from inline `<think>` tags in the `content` field (requires `stripThinking=true`)
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?model=qwen3&stripThinking=true")
    .log("Answer: ${body}")
    .log("Reasoning: ${header.CamelOpenAIReasoningContent}")
    .log("Thinking: ${header.CamelOpenAIThinkingContent}");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="openai:chat-completion?model=qwen3&amp;stripThinking=true"/>
  <log message="Answer: ${body}"/>
  <log message="Reasoning: ${header.CamelOpenAIReasoningContent}"/>
  <log message="Thinking: ${header.CamelOpenAIThinkingContent}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: openai:chat-completion
            parameters:
              model: qwen3
              stripThinking: true
        - log:
            message: "Answer: ${body}"
        - log:
            message: "Reasoning: ${header.CamelOpenAIReasoningContent}"
        - log:
            message: "Thinking: ${header.CamelOpenAIThinkingContent}"
```

> **Note**
> Reasoning content extraction is supported in non-streaming mode only (both simple and agentic/MCP tool loop paths). Streaming responses do not extract reasoning content.

### Mapping Additional Response Fields to Headers

The `additionalResponseHeader` option allows mapping any extra field from the API response message into a named Camel header. This is useful for provider-specific fields that are not part of the standard OpenAI response schema.

The key is the field name in the API response, and the value is the Camel header name to set:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?model=qwen3"
        + "&additionalResponseHeader.reasoning_content=CamelMyReasoning"
        + "&additionalResponseHeader.custom_field=CamelMyCustomField")
    .log("Custom reasoning: ${header.CamelMyReasoning}");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="openai:chat-completion?model=qwen3&amp;additionalResponseHeader.reasoning_content=CamelMyReasoning&amp;additionalResponseHeader.custom_field=CamelMyCustomField"/>
  <log message="Custom reasoning: ${header.CamelMyReasoning}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: openai:chat-completion
            parameters:
              model: qwen3
              additionalResponseHeader.reasoning_content: CamelMyReasoning
              additionalResponseHeader.custom_field: CamelMyCustomField
        - log:
            message: "Custom reasoning: ${header.CamelMyReasoning}"
```

String-valued fields are set directly. Non-string fields (numbers, booleans, objects) are converted using `toString()`.

> **Note**
> This maps fields from the response message’s additional properties (fields not part of the standard schema). Standard response fields like `content`, `role`, and `tool_calls` are not accessible through this option.

## Sub-Pages

For more details on specific features, see:

-   [MCP Tool Calling](others/openai-mcp.md) - Model Context Protocol server configuration, agentic loop, streaming, and connection recovery
    
-   [OpenAI-Compatible Providers](others/openai-providers.md) - Using Ollama, LM Studio, vLLM, and OpenRouter as alternative backends
    
-   [Embeddings and Audio Operations](others/openai-operations.md) - Text embeddings, vector database integration, and audio transcription
    

## Error Handling

The component may throw the following exceptions:

-   `IllegalArgumentException`:
    
    -   When an invalid operation is specified (supported: `chat-completion`, `embeddings`, `tool-execution`, `audio-transcription`)
        
    -   When message body or user message is missing
        
    -   When image file is provided without userMessage (chat-completion)
        
    -   When unsupported file type is provided (only text and image files are supported)
        
    -   When invalid JSON schema string is provided
        
    
-   API-specific exceptions from the OpenAI SDK for network errors, authentication failures, rate limiting, etc.