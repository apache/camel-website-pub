# OpenAI

**Since Camel 4.17**

**Only producer is supported**

The OpenAI component provides integration with OpenAI and OpenAI-compatible APIs for chat completion, text embeddings, content moderation, audio transcription, audio translation, and text-to-speech using the official openai-java SDK.

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
    
-   `responses` - Call the OpenAI Responses API (hosted tools, server-side conversation state; non-streaming)
    

See [Responses API operation](others/openai-responses.md) for usage (`previousResponseId`, builtin tools, MCP pass-through).

-   `embeddings` - Generate vector embeddings from text for semantic search and RAG applications
    
-   `tool-execution` - Execute MCP tool calls from a stored chat completion response (used in manual tool loops)
    
-   `audio-transcription` - Transcribe audio files to text using speech-to-text models (e.g., Whisper, GPT-4o Transcribe)
    
-   `audio-translation` - Transcribe and translate audio files into English text (e.g., Whisper)
    
-   `audio-speech` - Synthesize spoken audio from text using text-to-speech models (e.g., gpt-4o-mini-tts, tts-1)
    
-   `moderation` - Check text against the OpenAI usage policies before it reaches a model
    

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
**Required** The operation to perform: 'chat-completion', 'responses', 'embeddings', 'tool-execution', 'audio-transcription', 'audio-translation', 'audio-speech', or 'moderation'.

Enum values:

-   chat-completion
    
-   responses
    
-   embeddings
    
-   tool-execution
    
-   audio-transcription
    
-   audio-translation
    
-   audio-speech
    
-   moderation
    





 |  | OpenAIOperations |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalBodyProperty** (producer) | Additional JSON properties to include in the request body (e.g. additionalBodyProperty.traceId=123). This is a multi-value option with prefix: additionalBodyProperty. |  | Map |
| **additionalHeader** (producer) | Additional HTTP request headers to send with every API call (e.g. additionalHeader.OpenAI-Organization=my-org or additionalHeader.api-key=secret). Values may contain secrets. This is a multi-value option with prefix: additionalHeader. |  | Map |
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
| **builtinTools** (producer) | Comma-separated hosted tools for the Responses API: web\_search, file\_search, code\_interpreter. |  | String |
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
| **fileSearchVectorStoreIds** (producer) | Comma-separated vector store ids required when builtinTools includes file\_search. |  | String |
| **hallucinatedToolNameStrategy** (producer) | 

Strategy for handling tool names hallucinated by the model (tool not found in any MCP server). 'failExchange' (default) throws an IllegalStateException, failing the exchange immediately. 'repromptModel' sends a corrective tool result listing the available tools so the model can self-correct and retry. The maxToolIterations option bounds retries.

Enum values:

-   failExchange
    
-   repromptModel
    





 | failExchange | HallucinatedToolNameStrategy |
| **hostedMcpTools** (producer) | JSON array of hosted MCP tool definitions (OpenAI Tool.Mcp) passed through to the Responses API. |  | String |
| **jsonSchema** (producer) | JSON schema for structured output validation. |  | String |
| **maxAgenticTokens** (producer) | Maximum cumulative prompt plus completion tokens allowed across the MCP agentic loop. When 0 or negative, no token budget is enforced. Enforcement runs after each API call that requests further tool execution, so actual spend may exceed the configured budget by up to one call (typically the largest, as the prompt grows each iteration). A final text response is returned even when cumulative usage exceeds the budget. | 0 | long |
| **maxHistoryMessages** (producer) | When conversationMemory is enabled, retain at most this many messages in the exchange conversation history. System and developer messages are prepended separately and are not stored in history. Assistant tool-call blocks are kept intact and may retain slightly more than this limit to preserve tool result pairing. When 0, no message limit is applied. | 0 | int |
| **maxHistoryTokens** (producer) | When conversationMemory is enabled, trim conversation history using a token estimate (character count / 4, including image payload size for multi-modal user messages). Oldest segments are dropped first until the estimated tokens are within this limit. Assistant tool-call blocks are removed as a unit with their tool results. The most recent segment is always retained, even when it alone exceeds this limit. When 0, no token limit is applied. | 0 | int |
| **maxRetries** (producer) | Maximum number of times the OpenAI SDK client retries failed requests. The SDK retry is rate-limit aware (honors Retry-After on 429). | 2 | int |
| **maxTokens** (producer) | Maximum number of tokens to generate. |  | Integer |
| **maxToolIterations** (producer) | Maximum number of tool call loop iterations to prevent infinite loops. | 50 | int |
| **mcpProtocolVersions** (producer) | Comma-separated list of MCP protocol versions to advertise when connecting to MCP servers using Streamable HTTP transport. When not set, the SDK default is used. Example: 2024-11-05,2025-03-26,2025-06-18. |  | String |
| **mcpReconnect** (producer) | Automatically reconnect to MCP servers when a tool call fails due to a transport error, and retry the call once. | true | boolean |
| **mcpServer** (producer) | MCP (Model Context Protocol) server configurations. Define servers using prefix notation: mcpServer..transportType=stdiossestreamableHttp, (Note that sse is deprecated) mcpServer..command= (stdio), mcpServer..args= (stdio), mcpServer..url= (sse/streamableHttp), mcpServer..oauthProfile= (OAuth profile for HTTP auth, requires camel-oauth), mcpServer..toolNames= (optional include list to restrict which tools are registered from this server). This is a multi-value option with prefix: mcpServer. |  | Map |
| **mcpTimeout** (producer) | Timeout in seconds for MCP tool call requests. Applies to all MCP operations including tool execution and initialization. | 20 | int |
| **mcpToolRefresh** (producer) | Refresh the advertised tool list when an MCP server notifies that its tools changed. Set to false to keep the tool list fixed to what was listed when the endpoint started, for deployments that require a deterministic set of tools. | true | boolean |
| **model** (producer) | The model to use for chat completion. |  | String |
| **moderationModel** (producer) | The model to use for moderation. | omni-moderation-latest | String |
| **outputClass** (producer) | Fully qualified class name for structured output using response format. |  | String |
| **parallelToolExecution** (producer) | Execute the tool calls returned by the model in a single response concurrently instead of sequentially. Tool calls in the same batch are independent by design, so this reduces the latency of a batch to that of its slowest tool. Results are always fed back to the model in the original tool call order. Note that with toolExecutionErrorStrategy=failExchange the sibling tool calls already dispatched complete before the exchange fails. | false | boolean |
| **parallelToolTimeout** (producer) | Timeout in milliseconds for a batch of parallel tool calls, so that one slow tool cannot block the whole batch. The timeout applies to the batch as a whole, not per tool call. A tool call that exceeds it is cancelled and handled according to toolExecutionErrorStrategy. The default of 0 disables the batch timeout and relies on mcpTimeout, which already bounds each individual MCP request. Only used when parallelToolExecution=true. | 0 | long |
| **previousResponseId** (producer) | Previous response id for OpenAI server-side conversation state (Responses API only). |  | String |
| **requestTimeout** (producer) | HTTP request timeout in milliseconds for the OpenAI SDK client. When 0 or negative, the SDK default (10 minutes) is used. | 0 | long |
| **speechInstructions** (producer) | Optional instructions to control the voice of the generated audio. Does not work with tts-1 or tts-1-hd. |  | String |
| **speechModel** (producer) | The model to use for text-to-speech (e.g., gpt-4o-mini-tts, tts-1, tts-1-hd). |  | String |
| **speechResponseFormat** (producer) | 

The audio format for text-to-speech output.

Enum values:

-   mp3
    
-   opus
    
-   aac
    
-   flac
    
-   wav
    
-   pcm
    





 | mp3 | String |
| **speechSpeed** (producer) | The speed of the generated audio, from 0.25 to 4.0 where 1.0 is normal speed. |  | Double |
| **speechVoice** (producer) | The voice to use for text-to-speech (e.g., alloy, echo, fable, onyx, nova, shimmer). See the OpenAI documentation for the full list of supported voices. | alloy | String |
| **storeFullResponse** (producer) | Store the full SDK response in non-streaming mode: chat-completion uses exchange property 'CamelOpenAIResponse'; responses uses 'CamelOpenAIResponsesResponse'; moderation uses 'CamelOpenAIModerationResponse'. | false | boolean |
| **streaming** (producer) | Enable streaming responses. | false | boolean |
| **stripThinking** (producer) | Strip …​ blocks from model responses (used by reasoning models like Qwen3, DeepSeek-R1). The thinking content is stored in the CamelOpenAIThinkingContent header. | false | boolean |
| **systemMessage** (producer) | System message to prepend. When set and conversationMemory is enabled, the conversation history is reset. |  | String |
| **temperature** (producer) | Temperature for response generation (0.0 to 2.0). |  | Double |
| **toolExecutionErrorStrategy** (producer) | 

Strategy for handling exceptions thrown during MCP tool execution. 'failExchange' (default) propagates the exception to the Camel exchange so that standard Camel error handling (onException, dead-letter channel) can process it. This is the safer default because 'repromptModel' sends raw exception messages (which may contain connection strings, hostnames, or internal paths) to a third-party LLM provider. 'repromptModel' catches the error and sends it back to the model as a tool result so the model can attempt to recover.

Enum values:

-   failExchange
    
-   repromptModel
    





 | failExchange | ToolExecutionErrorStrategy |
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
| **CamelOpenAIPreviousResponseId** (producer) Constant: [`PREVIOUS_RESPONSE_ID`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#PREVIOUS_RESPONSE_ID) | Previous response id for server-side conversation state on the Responses API. |  | String |
| **CamelOpenAIStreaming** (producer) Constant: [`STREAMING`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#STREAMING) | Whether to stream the response back incrementally. |  | Boolean |
| **CamelOpenAIOutputClass** (producer) Constant: [`OUTPUT_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#OUTPUT_CLASS) | The Java class name (FQCN) to use for structured output parsing. |  | String |
| **CamelOpenAIJsonSchema** (producer) Constant: [`JSON_SCHEMA`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#JSON_SCHEMA) | The JSON schema to use for structured output validation. |  | String |
| **CamelOpenAIStripThinking** (producer) Constant: [`STRIP_THINKING`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#STRIP_THINKING) | Whether to strip …​ blocks from the response body. |  | Boolean |
| **CamelOpenAIMediaType** (producer) Constant: [`MEDIA_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MEDIA_TYPE) | The MIME type of the message body when sending a file or binary content (File, WrappedFile, byte or InputStream) to the model. Takes precedence over component content-type headers and automatic MIME type detection. |  | String |
| **CamelOpenAIThinkingContent** (producer) Constant: [`THINKING_CONTENT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#THINKING_CONTENT) | The thinking content extracted from …​ blocks in the model response. |  | String |
| **CamelOpenAIReasoningContent** (producer) Constant: [`REASONING_CONTENT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#REASONING_CONTENT) | The reasoning content from the model response reasoning\_content field, used by thinking models like Qwen3 and DeepSeek-R1. |  | String |
| **CamelOpenAIResponseModel** (producer) Constant: [`RESPONSE_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#RESPONSE_MODEL) | The model used for the completion response. |  | String |
| **CamelOpenAIResponseId** (producer) Constant: [`RESPONSE_ID`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#RESPONSE_ID) | The unique identifier for the completion response. |  | String |
| **CamelOpenAIFinishReason** (producer) Constant: [`FINISH_REASON`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#FINISH_REASON) | The reason the completion finished (e.g., stop, length, content\_filter). |  | String |
| **CamelOpenAIPromptTokens** (producer) Constant: [`PROMPT_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#PROMPT_TOKENS) | The number of tokens used in the prompt for the latest API call. |  | Long |
| **CamelOpenAICompletionTokens** (producer) Constant: [`COMPLETION_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#COMPLETION_TOKENS) | The number of tokens used in the completion for the latest API call. |  | Long |
| **CamelOpenAITotalTokens** (producer) Constant: [`TOTAL_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#TOTAL_TOKENS) | The total number of tokens used (prompt completion) for the latest API call. |  | Long |
| **CamelOpenAIToolIterations** (producer) Constant: [`TOOL_ITERATIONS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#TOOL_ITERATIONS) | Number of tool call iterations performed in the agentic loop. |  | Integer |
| **CamelOpenAIMcpToolCalls** (producer) Constant: [`MCP_TOOL_CALLS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MCP_TOOL_CALLS) | List of tool names called during the agentic loop. |  | List |
| **CamelOpenAIMcpReturnDirect** (producer) Constant: [`MCP_RETURN_DIRECT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MCP_RETURN_DIRECT) | Whether the response came directly from a tool with returnDirect=true, rather than from the LLM. |  | Boolean |
| **CamelOpenAIAgenticPromptTokens** (producer) Constant: [`AGENTIC_PROMPT_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AGENTIC_PROMPT_TOKENS) | Cumulative prompt tokens consumed across all agentic loop iterations. |  | Long |
| **CamelOpenAIAgenticCompletionTokens** (producer) Constant: [`AGENTIC_COMPLETION_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AGENTIC_COMPLETION_TOKENS) | Cumulative completion tokens consumed across all agentic loop iterations. |  | Long |
| **CamelOpenAIAgenticTotalTokens** (producer) Constant: [`AGENTIC_TOTAL_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AGENTIC_TOTAL_TOKENS) | Cumulative total tokens consumed across all agentic loop iterations. |  | Long |
| **CamelOpenAIResponse** (producer) Constant: [`RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#RESPONSE) | The complete OpenAI chat completion response object. |  | ChatCompletion |
| **CamelOpenAIResponsesResponse** (producer) Constant: [`RESPONSES_RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#RESPONSES_RESPONSE) | The complete OpenAI Responses API response object. |  | Response |
| **CamelOpenAIModerationResponse** (producer) Constant: [`MODERATION_RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MODERATION_RESPONSE) | The complete OpenAI moderation response object. |  | ModerationCreateResponse |
| **CamelOpenAIEmbeddingModel** (producer) Constant: [`EMBEDDING_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_MODEL) | The model to use for embeddings. |  | String |
| **CamelOpenAIEmbeddingDimensions** (producer) Constant: [`EMBEDDING_DIMENSIONS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_DIMENSIONS) | Number of output dimensions. |  | Integer |
| **CamelOpenAIEmbeddingResponseModel** (producer) Constant: [`EMBEDDING_RESPONSE_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_RESPONSE_MODEL) | The embedding model used in the response. |  | String |
| **CamelOpenAIEmbeddingCount** (producer) Constant: [`EMBEDDING_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_COUNT) | Number of embeddings returned. |  | Integer |
| **CamelOpenAIEmbeddingVectorSize** (producer) Constant: [`EMBEDDING_VECTOR_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#EMBEDDING_VECTOR_SIZE) | Vector dimensions of the embeddings. |  | Integer |
| **CamelOpenAIReferenceEmbedding** (producer) Constant: [`REFERENCE_EMBEDDING`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#REFERENCE_EMBEDDING) | Reference embedding vector for similarity comparison. |  | List |
| **CamelOpenAISimilarityScore** (producer) Constant: [`SIMILARITY_SCORE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#SIMILARITY_SCORE) | Calculated cosine similarity score (0.0 to 1.0). |  | Double |
| **CamelOpenAIOriginalText** (producer) Constant: [`ORIGINAL_TEXT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#ORIGINAL_TEXT) | Original text content when embeddings operation is used. |  | String or List |
| **CamelOpenAIModerationModel** (producer) Constant: [`MODERATION_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MODERATION_MODEL) | The model to use for moderation (e.g., omni-moderation-latest). |  | String |
| **CamelOpenAIModerationFlagged** (producer) Constant: [`MODERATION_FLAGGED`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MODERATION_FLAGGED) | Whether the moderation API flagged the input as violating the usage policies. For a batch of inputs this is true when at least one input was flagged. |  | Boolean |
| **CamelOpenAIModerationResults** (producer) Constant: [`MODERATION_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MODERATION_RESULTS) | One verdict per moderated input, in the order of the inputs. Each entry holds the keys 'input', 'flagged', 'categories' and 'categoryScores', so a batch can be split and routed per item. |  | List |
| **CamelOpenAIModerationCategories** (producer) Constant: [`MODERATION_CATEGORIES`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MODERATION_CATEGORIES) | The moderation categories and whether each one was violated, for a single input. Not set for a list body, where 'CamelOpenAIModerationResults' carries the verdicts. |  | Map |
| **CamelOpenAIModerationCategoryScores** (producer) Constant: [`MODERATION_CATEGORY_SCORES`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MODERATION_CATEGORY_SCORES) | The moderation confidence score per category, for a single input. Not set for a list body, where 'CamelOpenAIModerationResults' carries the verdicts. |  | Map |
| **CamelOpenAIModerationResponseModel** (producer) Constant: [`MODERATION_RESPONSE_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#MODERATION_RESPONSE_MODEL) | The moderation model used in the response. |  | String |
| **CamelOpenAIAudioModel** (producer) Constant: [`AUDIO_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_MODEL) | The model to use for audio transcription. |  | String |
| **CamelOpenAIAudioLanguage** (producer) Constant: [`AUDIO_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_LANGUAGE) | The language of the input audio (ISO-639-1). |  | String |
| **CamelOpenAIAudioResponseFormat** (producer) Constant: [`AUDIO_RESPONSE_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_RESPONSE_FORMAT) | The response format for audio transcription (json, text, srt, verbose\_json, vtt). |  | String |
| **CamelOpenAIAudioTemperature** (producer) Constant: [`AUDIO_TEMPERATURE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_TEMPERATURE) | Sampling temperature for audio transcription (0.0 to 1.0). |  | Double |
| **CamelOpenAIAudioPrompt** (producer) Constant: [`AUDIO_PROMPT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_PROMPT) | Optional text to guide the model’s style or continue a previous audio segment. |  | String |
| **CamelOpenAIAudioTimestampGranularities** (producer) Constant: [`AUDIO_TIMESTAMP_GRANULARITIES`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_TIMESTAMP_GRANULARITIES) | Comma-separated timestamp granularities: word, segment, or word,segment (verbose\_json only). |  | String |
| **CamelOpenAIAudioDuration** (producer) Constant: [`AUDIO_DURATION`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_DURATION) | Duration of the audio in seconds (verbose\_json only). |  | Double |
| **CamelOpenAIAudioDetectedLanguage** (producer) Constant: [`AUDIO_DETECTED_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#AUDIO_DETECTED_LANGUAGE) | Language detected in the audio (verbose\_json only). |  | String |
| **CamelOpenAISpeechModel** (producer) Constant: [`SPEECH_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#SPEECH_MODEL) | The model to use for text-to-speech (e.g., gpt-4o-mini-tts, tts-1, tts-1-hd). |  | String |
| **CamelOpenAISpeechVoice** (producer) Constant: [`SPEECH_VOICE`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#SPEECH_VOICE) | The voice to use for the generated audio (e.g., alloy, echo, fable, onyx, nova, shimmer). |  | String |
| **CamelOpenAISpeechResponseFormat** (producer) Constant: [`SPEECH_RESPONSE_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#SPEECH_RESPONSE_FORMAT) | The audio format for text-to-speech output (mp3, opus, aac, flac, wav, pcm). |  | String |
| **CamelOpenAISpeechSpeed** (producer) Constant: [`SPEECH_SPEED`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#SPEECH_SPEED) | The speed of the generated audio (0.25 to 4.0, where 1.0 is normal speed). |  | Double |
| **CamelOpenAISpeechInstructions** (producer) Constant: [`SPEECH_INSTRUCTIONS`](https://javadoc.io/doc/org.apache.camel/camel-openai/latest/org/apache/camel/component/openai/OpenAIConstants.html#SPEECH_INSTRUCTIONS) | Optional instructions to control the voice of the generated audio (does not work with tts-1 or tts-1-hd). |  | String |

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

> **Tip**
> For component selection, structured extraction, streaming, and prompt management patterns, see the [LLM Integration Guide](ai-llm-integration-guide.md).

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

### Dynamic prompts per exchange

The user prompt can change on every exchange. Set the body to the prompt text, or override with the `CamelOpenAIUserMessage` header (Simple expressions work):

-   Java
    
-   YAML
    

```java
from("direct:score")
    .setHeader("CamelOpenAIUserMessage", simple("Rate 1-10 for ${header.role}: ${body}"))
    .to("openai:chat-completion?model=gpt-4o-mini&temperature=0.2")
    .log("${body}");
```

```yaml
- route:
    from:
      uri: direct:score
      steps:
        - setHeader:
            name: CamelOpenAIUserMessage
            simple: "Rate 1-10 for ${header.role}: ${body}"
        - to:
            uri: openai:chat-completion
            parameters:
              model: gpt-4o-mini
              temperature: 0.2
```

### Chat generation parameters

Control randomness for chat completions with `temperature` (0.0–2.0) and `topP` (0.0–1.0). Low temperature (for example `0.1`) is recommended for structured JSON extraction.

-   YAML
    
-   Java
    

```yaml
- to:
    uri: openai:chat-completion
    parameters:
      model: gpt-4o-mini
      temperature: 0.1
      topP: 1.0
```

```java
.to("openai:chat-completion?model=gpt-4o-mini&temperature=0.1")
```

Per-exchange overrides use headers: `CamelOpenAITemperature`, `CamelOpenAITopP`.

For provider-specific request fields not exposed as URI options, use `additionalBodyProperty` (see [OpenAI-Compatible Providers](others/openai-providers.md)).

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

When `streaming=true`, the component returns an `Iterator<ChatCompletionChunk>` in the message body. You can consume this iterator using Camel’s streaming EIPs or process it directly.

For Server-Sent Events to web clients (platform-http), structured extraction pipelines, and when to stream through Camel vs. a dedicated handler, see [LLM Integration Guide — Streaming responses](ai-llm-integration-guide.html#_streaming_responses).

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

> **Tip**
> For extraction tasks (resumes, invoices, classification), prefer `jsonSchema` or `outputClass` instead of hand-written JSON parsing. Use low `temperature` (0.0–0.2). See [LLM Integration Guide — Structured output](ai-llm-integration-guide.html#_structured_output_recommended_for_extraction).

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

Use `maxHistoryMessages` and `maxHistoryTokens` to bound how much history is retained in that property. Oldest conversation segments are dropped first; assistant tool-call blocks are always removed together with their tool results. The most recent segment is always kept, even when it alone exceeds `maxHistoryMessages` or `maxHistoryTokens`. Token limits use a character-count / 4 estimate (including image payload size for multi-modal user messages).

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

## Tips for Production Use

This section covers practical advice for production routes. For component selection, streaming to browsers, and prompt management at scale, see the [LLM Integration Guide](ai-llm-integration-guide.md).

### Temperature and Model Parameters

The `temperature` endpoint option controls how deterministic the model’s output is. Lower values produce more consistent, predictable responses; higher values produce more varied, creative output.

For structured extraction tasks (JSON parsing, data extraction, classification), use a low temperature such as `0.1` to reduce the chance of the model adding unexpected commentary or formatting around the structured output:

-   Java
    
-   YAML
    

```java
from("direct:extract-skills")
    .to("openai:chat-completion?temperature=0.1&outputClass=com.example.SkillList")
    .log("Extracted: ${body}");
```

```yaml
- route:
    from:
      uri: direct:extract-skills
      steps:
        - to:
            uri: openai:chat-completion
            parameters:
              temperature: 0.1
              outputClass: com.example.SkillList
        - log:
            message: "Extracted: ${body}"
```

Temperature can also be set per-exchange via the `CamelOpenAITemperature` header. Other tuning options include `topP` (nucleus sampling) and `maxTokens` (response length limit).

### Dynamic Prompts

The `CamelOpenAIUserMessage` header is evaluated per-exchange, so you can construct prompts dynamically using Camel’s Simple language or any other expression:

-   Java
    
-   YAML
    

```java
from("direct:summarize")
    .setHeader("CamelOpenAIUserMessage",
        simple("Summarize this ${header.documentType} in 3 bullet points: ${body}"))
    .to("openai:chat-completion")
    .log("Summary: ${body}");
```

```yaml
- route:
    from:
      uri: direct:summarize
      steps:
        - setHeader:
            name: CamelOpenAIUserMessage
            simple: "Summarize this ${header.documentType} in 3 bullet points: ${body}"
        - to:
            uri: openai:chat-completion
        - log:
            message: "Summary: ${body}"
```

This is useful when chaining multiple enrichment steps where each step needs a different instruction based on the current exchange state.

### Use Structured Output for JSON Extraction

When you need the model to return structured data (JSON objects, arrays, typed fields), prefer the built-in `outputClass` or `jsonSchema` options over manually parsing the model’s text output. These options instruct the model to produce valid JSON matching your schema, which significantly reduces parsing failures:

```java
// Recommended — structured output handles JSON formatting:
from("direct:extract")
    .to("openai:chat-completion?outputClass=com.example.Skills")
    .log("${body}");

// Avoid — manual JSON parsing is fragile:
from("direct:extract")
    .setHeader("CamelOpenAIUserMessage",
        constant("Extract skills as a JSON array. Respond with valid JSON only."))
    .to("openai:chat-completion")
    .process(exchange -> {
        // This breaks when the model adds commentary around the JSON
        String json = exchange.getIn().getBody(String.class);
        List<String> skills = objectMapper.readValue(json, new TypeReference<>() {});
        exchange.getIn().setBody(skills);
    });
```

See [Structured Output with outputClass](#_structured_output_with_outputclass) and [Structured Output with JSON Schema](#_structured_output_with_json_schema) above for full examples. For additional validation, pipe the response through the [JSON Validator](json-validator-component.md) component.

### Handling Model Output Errors

A successful HTTP 200 response from the model does not guarantee the content is usable. The model may ignore formatting instructions, return truncated output, or produce content that does not match your expected shape. These are not Camel exceptions — they appear as downstream parsing failures in your own processors.

For production routes, add a lightweight validation step after the model call:

```java
from("direct:extract")
    .to("openai:chat-completion?outputClass=com.example.Result")
    .process(exchange -> {
        String response = exchange.getIn().getBody(String.class);
        if (response == null || response.isBlank()) {
            throw new IllegalStateException("Empty model response");
        }
    })
    .to("direct:downstream");
```

Using `outputClass` or `jsonSchema` already reduces this risk substantially by constraining the model’s output format at the API level.

### Prompt Management

When your project grows beyond a few routes, keeping prompt strings inline in route definitions becomes hard to maintain. Consider these approaches:

**Load prompts from resource files:**

```java
from("direct:analyze")
    .setHeader("CamelOpenAISystemMessage",
        constant("resource:classpath:prompts/system-analyst.txt"))
    .to("openai:chat-completion");
```

**Use Camel property placeholders for reusable fragments:**

```properties
# application.properties
prompt.system.analyst=You are a technical analyst. Be concise and factual.
prompt.output.json=Respond with valid JSON only, no commentary.
```

```java
from("direct:analyze")
    .setHeader("CamelOpenAISystemMessage", constant("{{prompt.system.analyst}}"))
    .setHeader("CamelOpenAIUserMessage",
        simple("{{prompt.output.json}} Analyze: ${body}"))
    .to("openai:chat-completion");
```

> **Tip**
> For prompt templates with named variables (e.g., \`{{dishType}}\`), the [LangChain4j Chat](langchain4j-chat-component.md) component offers built-in template support via the `CHAT_SINGLE_MESSAGE_WITH_PROMPT` operation.

### Streaming Considerations

The `streaming=true` option returns an `Iterator<ChatCompletionChunk>` that can be consumed with Camel’s Split EIP (see [Streaming Response](#_streaming_response) above). This works well for pipeline-style processing where each chunk is handled as part of a longer integration flow.

For user-facing scenarios that require Server-Sent Events (SSE) or WebSocket delivery to a browser, see [LLM Integration Guide — Streaming responses](ai-llm-integration-guide.html#_streaming_responses) for platform-http patterns and when to stream through Camel vs. a dedicated handler.

> **Note**
> When MCP tools with `autoToolExecution` are active, streaming automatically falls back to non-streaming to allow the agentic tool-calling loop to function. See [MCP Tool Calling](others/openai-mcp.md) for details.

## Sub-Pages

For more details on specific features, see:

-   [LLM Integration Guide](ai-llm-integration-guide.md) - Choosing components, structured output, streaming, dynamic prompts
    
-   [Responses API operation](others/openai-responses.md) - OpenAI Responses API, hosted tools, and server-side conversation state
    
-   [MCP Tool Calling](others/openai-mcp.md) - Model Context Protocol server configuration, agentic loop, streaming, and connection recovery
    
-   [OpenAI-Compatible Providers](others/openai-providers.md) - Using Ollama, LM Studio, vLLM, and OpenRouter as alternative backends
    
-   [Embeddings, Moderation and Audio Operations](others/openai-operations.md) - Text embeddings, vector database integration, content moderation, and audio transcription
    

## Error Handling

The component may throw the following exceptions:

-   `IllegalArgumentException`:
    
    -   When an invalid operation is specified (supported: `chat-completion`, `responses`, `embeddings`, `tool-execution`, `audio-transcription`, `audio-translation`, `audio-speech`, `moderation`)
        
    -   When message body or user message is missing
        
    -   When the audio model is missing (audio-transcription, audio-translation) or the speech model is missing (audio-speech)
        
    -   When image file is provided without userMessage (chat-completion)
        
    -   When unsupported file type is provided (only text and image files are supported)
        
    -   When invalid JSON schema string is provided
        
    -   When the moderation input list is empty or contains null elements (moderation)
        
    
-   `CamelExchangeException`:
    
    -   When moderation returns a number of results that does not match the number of inputs (moderation)
        
    
-   API-specific exceptions from the OpenAI SDK for network errors, authentication failures, rate limiting, etc.