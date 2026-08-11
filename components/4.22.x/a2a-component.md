# A2A

**Since Camel 4.21**

**Both producer and consumer are supported**

The A2A component implements the [Agent-to-Agent (A2A) v1.0 protocol](https://a2a-protocol.org/latest/specification/), enabling Camel routes to both expose and call A2A-compliant agents.

As a **consumer**, it turns a Camel route into an A2A agent — automatically serving an agent card at `/.well-known/agent-card.json`, exposing all A2A operations via HTTP, and managing task state. As a **producer**, it calls remote A2A agents with automatic agent card discovery, protocol wrapping, and credential management.

The component follows the same design philosophy as [REST OpenAPI](rest-openapi-component.md): it handles protocol plumbing and delegates business logic entirely to the route.

> **Note**
> **A2A Protocol**
>
> The [A2A protocol](https://a2a-protocol.org) is an open standard for communication between AI agents. It defines how agents discover each other (via agent cards), exchange messages, manage long-running tasks, stream progress updates, and deliver push notifications. The protocol supports both REST (HTTP+JSON) and JSON-RPC 2.0 bindings over HTTP.

## Preview Limitations

The A2A component is Preview in Camel 4.21. It targets the A2A v1.0 protocol, but endpoint options, model classes, generated metadata, and the task-store SPI may still change before the component reaches stable support.

Current Preview limitations:

-   Extended Agent Card / `GetExtendedAgentCard` is not implemented in this first release.
    
-   Consumers validate operation requests by default. Local-only examples in this page set `validateAuth=false`; network-exposed agents should use an agent card with `securitySchemes` and `securityRequirements` plus `apiKey`, `bearerToken`, or `oauthProfile` endpoint configuration.
    
-   The REST binding uses A2A custom-method paths containing colons, such as `/message:send`. These paths collide on Vert.x/platform-http. Use `protocolBinding=JSONRPC` with platform-http, or use `httpServerComponent=undertow` or `httpServerComponent=jetty` for REST custom-method routes.
    
-   Real-time SSE streaming is verified with Vert.x/platform-http, Undertow, and Jetty.
    
-   The default task store is in-memory and single-JVM. Register a custom `A2ATaskStore` for durable or cross-node task state.
    

Maven users will need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-a2a</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

Consumer routes also need an HTTP server component at runtime. For example, add `camel-platform-http-vertx` for JSON-RPC agents (including SSE streaming), or `camel-undertow` / `camel-jetty` for REST custom-method routes. See [Dependencies](#_dependencies) and [HTTP Server Component Discovery](#_http_server_component_discovery).

## URI Format

a2a:agentCardSource\[?options\]

How **agentCardSource** determines where the agent card is loaded from:

 
| Source | Example |
| --- | --- |
| Remote URL (partial) | `a2a:\https://agent.example.com` — auto-expands to `https://agent.example.com/.well-known/agent-card.json` |
| Remote URL (full) | `a2a:\https://agent.example.com/.well-known/agent-card.json` |
| Classpath | `a2a:classpath:cards/weather.json` |
| File | `a2a:file:/etc/agents/weather.json` |
| Plain name | `a2a:weather-agent?name=Weather&description=…​` — card built from params |

The same URI works in both `from()` (consumer: "I am this agent") and `to()` (producer: "I am calling this agent").

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

The A2A component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The A2A endpoint is configured using URI syntax:

a2a:agentCardSource

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **agentCardSource** (common) | **Required** The agent card source (classpath:, file:, http://, https://, or plain name). |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **agentCard** (common) | Agent card bean reference or inline configuration. |  | AgentCard |
| **basePath** (common) | The base path for HTTP requests. |  | String |
| **dataFormat** (common) | 
The data format for the exchange body, following the CXF DataFormat convention. PAYLOAD (default) extracts text content from message parts as a String backward compatible, simple for chatbot routes. POJO sets the body to the full Java model object (Message on consumer, Task or Message on producer) preserving all parts, metadata, and file content. RAW passes the raw JSON string without deserialization useful for forwarding, logging, or compliance.

Enum values:

-   PAYLOAD
    
-   POJO
    
-   RAW
    





 | PAYLOAD | A2ADataFormat |
| **description** (common) | The agent description (overrides agent card). |  | String |
| **historyLength** (common) | Maximum number of history messages to include in the context. |  | Integer |
| **host** (common) | The host to connect to for producers. |  | String |
| **name** (common) | The agent name (overrides agent card). |  | String |
| **port** (common) | The port to connect to for producers. |  | Integer |
| **protocolBinding** (common) | 

The protocol binding to use for communication. Legacy aliases rest and jsonrpc are also accepted.

Enum values:

-   HTTP+JSON
    
-   JSONRPC
    





 | HTTP+JSON | String |
| **returnImmediately** (common) | Whether to return immediately without waiting for task completion. | false | boolean |
| **validateAuth** (common) | Whether to validate authentication on incoming consumer operation requests. Disable explicitly only for unauthenticated A2A operation serving. | true | boolean |
| **version** (common) | The agent version (overrides agent card). |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **httpServerComponent** (consumer (advanced)) | The Camel HTTP component to use for serving incoming A2A requests (consumer side). Must implement RestConsumerFactory (e.g., platform-http, jetty, netty-http, undertow, servlet). When not set, the component is auto-discovered from the classpath or falls back to the global camel.rest.component setting. |  | String |
| **maxConcurrentTasks** (consumer (advanced)) | Maximum number of tasks the agent can process concurrently. When the limit is reached, new requests are rejected with ServerBusyError (HTTP 429). Set to 0 (default) for unlimited concurrency. | 0 | int |
| **sseHeartbeatInterval** (consumer (advanced)) | Interval in milliseconds for SSE keep-alive heartbeat comments. Sent as ':' comment lines to prevent proxies from closing idle connections. Independent from asyncTimeout which controls task processing timeout. | 15000 | long |
| **sseQueueCapacity** (consumer (advanced)) | Maximum number of SSE events that can be buffered per streaming connection. When the queue is full, new events are dropped with a warning log. Prevents unbounded memory growth from slow clients. | 1000 | int |
| **taskQueueSize** (consumer (advanced)) | Maximum number of tasks that can wait in the pending queue when all concurrent slots are occupied. Only applies to async requests (returnImmediately=true). Queued tasks receive SUBMITTED status and are processed as capacity becomes available. Set to 0 (default) for no queueing requests are rejected immediately when at capacity. | 0 | int |
| **operation** (producer) | 

The A2A operation to perform.

Enum values:

-   MESSAGE\_SEND
    
-   MESSAGE\_STREAM
    
-   TASK\_GET
    
-   TASK\_LIST
    
-   TASK\_CANCEL
    
-   TASK\_SUBSCRIBE
    
-   PUSH\_CONFIG\_CREATE
    
-   PUSH\_CONFIG\_GET
    
-   PUSH\_CONFIG\_LIST
    
-   PUSH\_CONFIG\_DELETE
    





 | MESSAGE\_SEND | A2AOperations |
| **connectTimeout** (producer (advanced)) | Connect timeout in milliseconds for the HTTP client used by the producer. | 30000 | long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **streamingReadTimeout** (producer (advanced)) | Read timeout in milliseconds for the producer’s SSE streaming connection. If no SSE event arrives within this period, the stream is closed with an error. Prevents indefinite blocking when a remote agent stops sending events. | 300000 | long |
| **asyncTimeout** (advanced) | Timeout in milliseconds for asynchronous task operations. | 300000 | long |
| **completedTaskTtl** (advanced) | Time-to-live in milliseconds for completed tasks before cleanup. | 3600000 | long |
| **followRedirects** (advanced) | Whether the HTTP client should follow redirects. Disabled by default to prevent credential leakage on cross-origin redirects. Enable only when the remote agent is known to issue redirects (e.g., behind a load balancer). | false | boolean |
| **maxPayloadSize** (advanced) | Maximum payload size in bytes (default 6MB). | 6291456 | long |
| **pushRetryAttempts** (advanced) | Maximum number of retry attempts for push notification webhook delivery. | 3 | int |
| **pushRetryBackoffMs** (advanced) | Initial backoff in milliseconds for push notification retry. Retries use exponential backoff with this delay multiplied by 2 to the attempt number. | 1000 | long |
| **allowLocalWebhookUrls** (security) | Whether to allow webhook URLs pointing to localhost/loopback addresses. When false (default), push notification webhook URLs targeting 127.0.0.0/8, ::1, or localhost are rejected as SSRF protection. Enable for local development only. | false | boolean |
| **apiKey** (security) | API key for authentication. |  | String |
| **apiKeyHeader** (security) | HTTP header name for API key authentication (e.g., X-API-Key, Authorization). | Authorization | String |
| **bearerToken** (security) | Bearer token for authentication. |  | String |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used for authentication. Requires camel-oauth on the classpath. The profile properties are resolved from camel.oauth.profile-name.client-id, camel.oauth.profile-name.client-secret, and camel.oauth.profile-name.token-endpoint. |  | String |

## Message Headers

The A2A component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelA2AOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#OPERATION) | A2A operation to invoke. |  | String |
| **CamelA2ATaskId** (common) Constant: [`TASK_ID`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#TASK_ID) | Task ID. |  | String |
| **CamelA2APushConfigId** (common) Constant: [`PUSH_CONFIG_ID`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#PUSH_CONFIG_ID) | Push notification config ID. |  | String |
| **CamelA2AContextId** (common) Constant: [`CONTEXT_ID`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#CONTEXT_ID) | Context ID for multi-turn conversations. |  | String |
| **CamelA2AMessageId** (common) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#MESSAGE_ID) | Message ID. |  | String |
| **CamelA2ATaskState** (common) Constant: [`TASK_STATE`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#TASK_STATE) | Task state. |  | String |
| **CamelA2AMethod** (producer) Constant: [`METHOD`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#METHOD) | A2A method name invoked. |  | String |
| **CamelA2AResponseType** (common) Constant: [`RESPONSE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#RESPONSE_TYPE) | Response type: task or message. |  | String |
| **CamelA2AReturnImmediately** (common) Constant: [`RETURN_IMMEDIATELY`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#RETURN_IMMEDIATELY) | Return immediately flag. |  | Boolean |
| **CamelA2AHistoryLength** (common) Constant: [`HISTORY_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#HISTORY_LENGTH) | Max history messages. |  | Integer |
| **CamelA2AStreamEmitter** (consumer) Constant: [`STREAM_EMITTER`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#STREAM_EMITTER) | SSE stream emitter for route processors. |  | A2AStreamEmitter |
| **CamelA2AListContextId** (common) Constant: [`LIST_CONTEXT_ID`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#LIST_CONTEXT_ID) | Context ID filter for task listing. |  | String |
| **CamelA2AListPageSize** (common) Constant: [`LIST_PAGE_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#LIST_PAGE_SIZE) | Page size for task listing. |  | Integer |
| **CamelA2AListPageToken** (common) Constant: [`LIST_PAGE_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#LIST_PAGE_TOKEN) | Page token for task listing pagination. |  | String |
| **CamelA2AListIncludeArtifacts** (common) Constant: [`LIST_INCLUDE_ARTIFACTS`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#LIST_INCLUDE_ARTIFACTS) | Whether to include artifacts in task listing. |  | Boolean |
| **CamelA2AListHistoryLength** (common) Constant: [`LIST_HISTORY_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#LIST_HISTORY_LENGTH) | History length for task listing. |  | Integer |
| **CamelA2AListStatusTimestampAfter** (common) Constant: [`LIST_STATUS_TIMESTAMP_AFTER`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#LIST_STATUS_TIMESTAMP_AFTER) | Filter tasks by status timestamp after this value. |  | String |
| **CamelA2AListStatus** (common) Constant: [`LIST_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#LIST_STATUS) | Comma-separated status filter for task listing. |  | String |
| **CamelA2AExtensions** (consumer) Constant: [`EXTENSIONS`](https://javadoc.io/doc/org.apache.camel/camel-a2a/latest/org/apache/camel/component/a2a/A2AConstants.html#EXTENSIONS) | Negotiated A2A extension URIs requested by the client. |  | List |

## Sub-Pages

For more details on consumer and producer usage, see:

-   [Consumer Guide](others/a2a-consumer.md) - Exposing an A2A agent with authentication, SSE streaming, async tasks, push notifications, and capacity limiting
    
-   [Producer Guide](others/a2a-producer.md) - Calling remote agents with streaming, async task lifecycle, push notifications, and parallel multicast
    

## Simple Language Functions

The component registers custom Simple language functions under the `a2a:` namespace:

 
| Function | Description |
| --- | --- |
| `${a2a:emit('message')}` | Emit a status update with `WORKING` state. Used in `script` EIP for SSE streaming side effects. |
| `${a2a:emit(STATE, 'message')}` | Emit a status update with an explicit `TaskState` (e.g., `INPUT_REQUIRED`). |
| `${a2a:text}` | Extract `TextPart` content from the body (`Task` or `Message`). If the body is a `Task`, extracts from the last history message. |
| `${a2a:text(expression)}` | Extract `TextPart` content from the result of a Simple expression. |
| `${a2a:data}` | Extract `DataPart` content as a JSON string from the body. |
| `${a2a:data(expression)}` | Extract `DataPart` content from the result of a Simple expression. |
| `${a2a:file}` | Extract `FilePart` content — the `url` value for URL file parts, or a binary-size description for inline base64 `raw` content. |
| `${a2a:file(expression)}` | Extract `FilePart` content from the result of a Simple expression. |
| `${a2a:card}` | Full agent card as JSON string. Resolves the card from the A2A endpoint (consumer’s own card, or the cached remote card on the producer). |
| `${a2a:card.name}` | Agent card name. |
| `${a2a:card.description}` | Agent card description. |
| `${a2a:card.url}` | Agent card URL. |
| `${a2a:card.version}` | Agent card version. |
| `${a2a:card.skills}` | Skills formatted as human-readable text, one per line: `* Skill Name: description`. |
| `${a2a:card.skills.json}` | Skills as a JSON array string. |
| `${a2a:card.iconUrl}` | Agent card icon URL. |
| `${a2a:card.documentationUrl}` | Agent card documentation URL. |
| `${a2a:card.provider}` | Agent provider as JSON string. |
| `${a2a:card.capabilities}` | Agent capabilities as JSON string. |
| `${a2a:card.supportedInterfaces}` | Supported interfaces as JSON array string. |
| `${a2a:card.securitySchemes}` | Security schemes as JSON object string. |
| `${a2a:card.securityRequirements}` | A2A v1.0 security requirements as JSON array string. |
| `${a2a:card.security}` | Legacy draft `security` field as JSON array string. |

The `${a2a:card}` functions resolve the agent card from the exchange context. On a consumer route, `exchange.getFromEndpoint()` provides the agent’s own card. On a producer route, the component scans registered endpoints for a cached remote card. Returns an empty string if no card is available.

> **Note**
> The card functions support flat field access only — nested property access like `${a2a:card.skills[0].name}` or `${a2a:card.provider.organization}` is not supported. For structured data, use `${a2a:card.skills.json}` or `${a2a:card}` (full JSON) and parse downstream.

Example — including remote agent skills in an LLM prompt:

```yaml
- setBody:
    simple: |
      Generate a plan using these available skills:
      ${a2a:card.skills}
```

For the full text of all parts combined, use the TypeConverter:

```yaml
- convertBodyTo:
    type: String
```

## Exchange Headers

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelA2AOperation` | `String` | A2A operation to invoke. Accepts both enum names (`TASK_GET`, `PUSH_CONFIG_CREATE`) and PascalCase method names (`GetTask`, `CreateTaskPushNotificationConfig`). |
| `CamelA2ATaskId` | `String` | Task ID for `GetTask`, `CancelTask`, `SubscribeToTask`, and push notification operations. |
| `CamelA2APushConfigId` | `String` | Push notification config ID for get/delete operations. |
| `CamelA2AContextId` | `String` | Context ID for multi-turn conversations. Set automatically on consumer inbound and producer response. |
| `CamelA2AMessageId` | `String` | Message ID from the request/response. |
| `CamelA2ATaskState` | `String` | Task state from the response (e.g., `TASK_STATE_COMPLETED`, `TASK_STATE_WORKING`). |
| `CamelA2AMethod` | `String` | A2A method name invoked (set on producer response). |
| `CamelA2AResponseType` | `String` | Response type after a producer call (`task`, `message`, `taskList`, `pushConfigList`, or `stream`). On consumer routes, set this header to `message` to return a message-only `SendMessage` response; the default is a task response. |
| `CamelA2AReturnImmediately` | `Boolean` | Override `returnImmediately` per-request. Takes precedence over endpoint-level config. |
| `CamelA2AHistoryLength` | `Integer` | Producer request field for `GetTask` and `SubscribeToTask`. |
| `CamelA2AUserProfile` | `Map<String, Object>` | Authenticated user profile (set as exchange **property**, not a header). Populated when `validateAuth=true` and authentication succeeds. Access via `$\{exchangeProperty.CamelA2AUserProfile}` in Simple expressions. |
| `CamelA2AListContextId` | `String` | Context ID filter for `ListTasks`. |
| `CamelA2AListPageSize` | `Integer` | Page size for `ListTasks`. |
| `CamelA2AListPageToken` | `String` | Pagination token for `ListTasks`. |
| `CamelA2AListStatus` | `String` | Comma-separated status filter for `ListTasks`. |
| `CamelA2AListIncludeArtifacts` | `Boolean` | Whether `ListTasks` responses include artifacts. |
| `CamelA2AListHistoryLength` | `Integer` | Maximum history messages to include per task in `ListTasks` responses. |
| `CamelA2AListStatusTimestampAfter` | `String` | Status timestamp filter for `ListTasks`. Use an ISO-8601 offset date-time. |
| `CamelA2AExtensions` | `List<String>` | Consumer-side negotiated A2A extension URIs from the `A2A-Extensions` request header. Set as both an exchange property and a route header after validation. |
| `CamelA2AStreamEmitter` | `A2AStreamEmitter` | Consumer-side: the stream emitter injected for streaming routes. Available for advanced use cases — prefer `${a2a:emit()}` or `A2AProgress` API for most agents. |
> **Note**
> `CamelA2AResponseTask` and `CamelA2AUserProfile` are exchange **properties**, not headers. Access them via `$\{exchangeProperty.CamelA2AResponseTask}` and `$\{exchangeProperty.CamelA2AUserProfile}` in Simple expressions. `CamelA2AResponseTask` contains the full `Task` object from the producer response, useful in polling workflows. `CamelA2AUserProfile` contains the authenticated user’s profile map, available when `validateAuth=true`.

## Supported Operations

   
| Operation (enum) | Method Name | Producer | Consumer |
| --- | --- | --- | --- |
| `MESSAGE_SEND` | `SendMessage` | Send message, receive Task or Message | Route processes message |
| `MESSAGE_STREAM` | `SendStreamingMessage` | Lazy `Iterator<StreamResponse>` (`PAYLOAD`/`POJO`), or raw `InputStream` (`RAW`) | Route emits via `${a2a:emit()}` |
| `TASK_GET` | `GetTask` | Retrieve task from remote | Read from task store |
| `TASK_LIST` | `ListTasks` | List tasks from remote | Query task store |
| `TASK_CANCEL` | `CancelTask` | Cancel remote task | Update store + cancel in-flight async |
| `TASK_SUBSCRIBE` | `SubscribeToTask` | Lazy `Iterator<StreamResponse>` of task updates | Event-to-Stream Bridge (real-time SSE) for REST and JSON-RPC bindings |
| `PUSH_CONFIG_CREATE` | `CreateTaskPushNotificationConfig` | Register webhook | Store config + SSRF validation |
| `PUSH_CONFIG_GET` | `GetTaskPushNotificationConfig` | Retrieve config | Read from store |
| `PUSH_CONFIG_LIST` | `ListTaskPushNotificationConfigs` | List configs | Read from store |
| `PUSH_CONFIG_DELETE` | `DeleteTaskPushNotificationConfig` | Delete config | Remove from store |

The `CamelA2AOperation` header accepts both the enum name (left column) and the PascalCase method name (second column).

The built-in JSON-RPC consumer dispatches `SendMessage`, `SendStreamingMessage`, `GetTask`, `ListTasks`, `CancelTask`, `SubscribeToTask`, and the push notification config operations.

## Pluggable Authentication

Authentication uses a strategy-per-scheme pattern via the `A2ASecuritySchemeHandler` SPI. One handler covers both producer (apply credentials) and consumer (validate credentials) for a given security scheme type.

Default handlers:

  
| Scheme Type | Handler | Description |
| --- | --- | --- |
| `http` (bearer) | `HttpBearerSchemeHandler` | OAuth profile or static bearer token |
| `apiKey` | `ApiKeySchemeHandler` | API key in `header`, `query`, or `cookie` location. If the security scheme declares `location=header` and `name`, that header is used; otherwise `apiKeyHeader` is used. |
| `oauth2` | `OAuth2SchemeHandler` | Token via `camel-oauth` SPI |
| `openIdConnect` | `OpenIdConnectSchemeHandler` | Same as OAuth2, stores OIDC discovery URL |

Override or extend by registering a custom handler bean:

_Java-only: implementing a custom A2ASecuritySchemeHandler_

```java
@BindToRegistry("myCustomAuth")
public class MutualTlsHandler implements A2ASecuritySchemeHandler {
    public String schemeType() { return "mutualTls"; }

    public void applyCredentials(Exchange exchange, SecurityScheme scheme,
            A2AConfiguration config, CamelContext context) {
        // producer: configure mTLS
    }

    public A2AUserProfile validateCredentials(Exchange exchange,
            SecurityScheme scheme, A2AConfiguration config) {
        // consumer: extract client certificate
        return A2AUserProfile.fromMap(Map.of(
                "scheme", "mutualTls",
                "subject", "CN=client"));
    }
}
```

### Security Scheme Priority

When the agent card declares multiple security schemes, selection is based on configuration hints:

-   `oauthProfile` configured → OAuth2 / OpenID Connect schemes tried first
    
-   `bearerToken` configured → HTTP bearer schemes tried first
    
-   `apiKey` configured → API key schemes tried first
    
-   No hint → schemes tried in agent card declaration order
    

On the producer, the first matching handler applies credentials. On the consumer, all declared schemes are tried until one succeeds (or all fail with 401).

## Task State Machine

A2A tasks follow this state machine:

                    +--> COMPLETED
                    |
SUBMITTED --> WORKING +--> FAILED
                    |
                    +--> CANCELED
                    |
                    +--> INPUT\_REQUIRED --> WORKING (resumed)
                    |
                    +--> AUTH\_REQUIRED --> WORKING (after re-auth)
                    |
                    +--> REJECTED

All valid task states (wire values use the A2A v1.0 proto names shown below; the `$\{a2a:emit()}` function uses the short Java enum names — e.g., `INPUT_REQUIRED`, not `TASK_STATE_INPUT_REQUIRED`):

 
| State | Description |
| --- | --- |
| `TASK_STATE_UNSPECIFIED` | Unknown or missing task state fallback |
| `TASK_STATE_SUBMITTED` | Task accepted, not yet processing |
| `TASK_STATE_WORKING` | Task is actively being processed |
| `TASK_STATE_COMPLETED` | Task completed successfully (terminal) |
| `TASK_STATE_FAILED` | Task failed due to error or timeout (terminal) |
| `TASK_STATE_CANCELED` | Task was canceled by the client (terminal) |
| `TASK_STATE_INPUT_REQUIRED` | Agent needs additional input from the client before proceeding |
| `TASK_STATE_AUTH_REQUIRED` | Agent needs the client to re-authenticate before proceeding |
| `TASK_STATE_REJECTED` | Agent rejected the task (terminal) |

The consumer manages transitions automatically:

-   `SUBMITTED` — when `returnImmediately=true` and the task is accepted
    
-   `WORKING` — when the route starts processing (async tasks)
    
-   `COMPLETED` — when `setBody` produces a non-null response
    
-   `FAILED` — when the route throws an exception or `asyncTimeout` expires
    

Routes can emit any state explicitly via `${a2a:emit(INPUT_REQUIRED, 'Please provide your address')}` or `A2AProgress.emit(exchange, TaskState.AUTH_REQUIRED, "Re-authentication needed")`.

## Unified Body-as-Response

Both streaming and async agents use the same route pattern — `setBody` is always the final response:

```yaml
steps:
  - script:
      simple: "${a2a:emit('progress...')}"    # optional status events
  - setBody:
      constant: "final response"              # consumer handles delivery
```

The consumer handles delivery regardless of mechanism:

-   **Synchronous**: returned directly in the HTTP response
    
-   **Streaming**: emitted as an SSE message event
    
-   **Async + polling**: stored in the task’s history and status message, returned via `GetTask`
    
-   **Push notifications**: included in the `COMPLETED` status webhook payload
    

## Agent Card Resolution

Card fields are resolved with layered precedence (lowest to highest):

1.  **Agent card JSON file** — loaded from the URI source (base)
    
2.  **Bean reference** — `agentCard=#myBean` fills/overrides fields from a programmatic object
    
3.  **URI parameters** — `name`, `description`, `version` override everything
    

Bean reference example — useful when the card needs programmatic construction (e.g., dynamic skills):

```yaml
- route:
    from:
      uri: a2a:classpath:agent-card.json
      parameters:
        agentCard: "#myCardBean"
```

URI parameter overrides — customize base cards per environment via properties:

```yaml
- route:
    from:
      uri: a2a:classpath:agent-card.json
      parameters:
        name: "{{agent.name}}"
        version: "{{agent.version}}"
```

Security schemes from the card drive auth handler selection. Config parameters (`oauthProfile`, `bearerToken`, `apiKey`) provide the runtime credentials and influence scheme priority.

The resolver currently merges these card fields from file and bean cards: `name`, `description`, `url`, `version`, `provider`, `capabilities`, `skills`, `supportedInterfaces`, `securitySchemes`, `securityRequirements`, `iconUrl`, `documentationUrl`, `defaultInputModes`, `defaultOutputModes`, `supportsAuthenticatedExtendedCard`, and unknown extension properties. Legacy input cards using `security` are converted to `securityRequirements`. URI parameters can override only `name`, `description`, and `version`.

> **Note**
> The card is loaded once at endpoint startup and cached. Periodic card refresh is not yet implemented.

## HTTP Server Component Discovery

The consumer needs an HTTP server to register A2A endpoints. The discovery order is:

1.  **Explicit `httpServerComponent`** parameter (e.g., `undertow`, `jetty`)
    
2.  **Global `camel.rest.component`** / REST DSL component configuration
    
3.  **Already registered `platform-http` component**
    
4.  Exactly one already registered Camel component implementing `RestConsumerFactory`
    
5.  Exactly one registry bean implementing `RestConsumerFactory`
    

The preview component does not auto-create arbitrary HTTP server components and does not choose between multiple discovered server factories. Add and register one of the tested server components, or set `httpServerComponent` explicitly.

Tested behavior in this Preview release:

-   `camel-platform-http` / Vert.x - suitable for JSON-RPC agents (including SSE streaming) and serving the public agent card. REST custom-method paths containing colons can collide.
    
-   `camel-undertow` and `camel-jetty` - suitable for REST custom-method paths and real-time SSE streaming.
    

## Data Format

The `dataFormat` parameter controls what the exchange body contains, following the same convention as the [CXF component](cxf-component.md). It applies to both consumer (inbound request) and producer (response) sides.

  
| Value | Default | Description |
| --- | --- | --- |
| `PAYLOAD` | Yes | Extracts text content from message parts as a `String`. On the consumer, incoming `Message` parts are flattened via `messageToString()`. On the producer, response `Task` or `Message` objects are converted to text. Backward compatible — simple routes using `${body}` get clean text. Streaming: same as POJO (lazy iterator on producer, emitter-based on consumer). |
| `POJO` | No | Full Java model objects. On the consumer, the body is the `Message` record with all parts, metadata, and files intact — access individual parts via `$\{body.parts()[0]}`. On the producer, the body is the `Task` or `Message` response object. Streaming: body is a lazy `Iterator<StreamResponse>` parsed on demand (use with Split EIP). |
| `RAW` | No | Raw JSON string with no deserialization. On the consumer, the body is the JSON representation of the incoming `Message`. On the producer, the body is the raw JSON response string. Useful for forwarding, logging, or compliance where byte-exact fidelity matters. Streaming: body is the raw `InputStream` — true SSE passthrough with no buffering. |

Example — consumer in POJO mode for multimodal processing:

```yaml
- route:
    from:
      uri: a2a:classpath:agent-card.json?dataFormat=POJO
      steps:
        - log:
            message: "Received ${body.parts().size()} parts"
        - setBody:
            simple: "Processed ${body.parts()[0]}"
```

Example — producer in RAW mode for proxying:

```yaml
- route:
    from:
      uri: direct:proxy
      steps:
        - to: a2a:http://remote-agent:8080?dataFormat=RAW
        - log:
            message: "Raw JSON: ${body}"
```

## Task Store

The default `InMemoryTaskStore` manages task state with lazy cleanup. It is thread-safe, using concurrent maps for storage and lock-protected eviction for task-associated data such as message-id mappings, subscribers, and push configs.

The `completedTaskTtl` URI parameter (default 3,600,000 ms / 1 hour) controls the TTL for terminal tasks. Expired tasks are evicted on read or during periodic cleanup.

The following settings are configurable programmatically on the `InMemoryTaskStore` bean, not via URI parameters:

  
| Property | Default | Description |
| --- | --- | --- |
| `maxStoredTasks` | `10000` | Maximum tasks in the store. When exceeded, the oldest terminal task is evicted; if no terminal task exists, no task is evicted. Set to 0 for unlimited. |
| `cleanupInterval` | `100` | Number of `put()` calls between periodic bulk cleanup runs. |
| `stuckTaskTtlMs` | `0` (disabled) | TTL for non-terminal stuck tasks (`SUBMITTED`, `WORKING`). When set to a positive value, tasks older than this duration are marked `FAILED` on read or periodic cleanup, and subscribers are notified. This preview safety net is disabled by default; prefer `asyncTimeout` on the endpoint for normal timeout handling. |

To customize, register a bean implementing `A2ATaskStore` in the Camel registry. The preview SPI is also split into narrower parent contracts (`A2ATaskRepository`, `A2ATaskSubscriptions`, `A2APushConfigStore`, and `A2ATaskCleanup`) so custom stores can keep storage, subscription, push-config, and cleanup responsibilities separate. Registry-provided stores are wrapped by a guard that enforces terminal-state protection, delegates subscriber registration and notification to the custom store, tracks endpoint subscribers for terminal-event cleanup, validates push webhook URLs, and normalizes push config IDs/task IDs on the endpoint path. Custom stores still need to preserve durable storage and any cross-node notification semantics inside their own implementation; the dispatcher revalidates webhook URLs before delivery.

Custom subscribers can be registered on a task-store bean for audit logging, metrics, or custom delivery:

_Java-only: registering a custom A2ATaskStore with a global subscriber_

```java
@BindToRegistry
public A2ATaskStore taskStore() {
    MyAuditingTaskStore store = new MyAuditingTaskStore();
    store.addGlobalSubscriber((taskId, event) -> auditLog.record(taskId, event));
    return store;
}
```

## Model Classes

The component uses Java model classes aligned with A2A v1.0:

 
| Class | Description |
| --- | --- |
| `Task` | Task with `id`, `contextId`, `status` (`TaskStatus`), `history` (`List<Message>`), `artifacts` (`List<Artifact>`), and `metadata` (`Map<String, Object>`). `contextId` is the key for multi-turn conversations (maps to `CamelA2AContextId` header). `Task.latest()` returns the last message in history. |
| `Message` | Agent or user message with `role`, `parts`, `messageId`, `contextId`, `taskId`, `referenceTaskIds`, `metadata`, and `extensions`. The `Role` enum uses `ROLE_USER`, `ROLE_AGENT`, and `ROLE_UNSPECIFIED`; `ROLE_UNSPECIFIED` is the fallback for unknown role values during deserialization. |
| `SendMessageRequest` | Operation request wrapper with `message`, `configuration`, and `metadata`. The consumer requires `message.role` and at least one message part. |
| `SendMessageConfiguration` | Send-message runtime options with `returnImmediately`, `blocking`, `historyLength`, and retained extension properties. `returnImmediately` wins over `blocking`; `blocking=false` is treated as immediate return. |
| `SendMessageResponse` | Response wrapper containing exactly one of `task` or `message`. |
| `TaskListRequest` | List-tasks request with `contextId`, `status`, `statusTimestampAfter`, `includeArtifacts`, `historyLength`, `pageSize`, and `pageToken`. |
| `ListTasksResponse` | List-tasks response with `tasks`, `nextPageToken`, `pageSize`, and `totalSize`. |
| `StreamResponse` | SSE event wrapper containing exactly one of `task`, `message`, `statusUpdate`, or `artifactUpdate`. |
| `TextPart` | Text content part implementing `Part<String>`. |
| `DataPart` | Structured data part implementing `Part<Object>`. |
| `FilePart` | File content with `raw` for inline base64 data, `url` for referenced content, plus optional `mediaType`, `filename`, and `metadata`. |
| `TaskStatus` | Status snapshot with `state` (`TaskState`), optional `message` (`Message`), and `timestamp` (`OffsetDateTime`). |
| `Artifact` | Named output with `artifactId`, `name`, `description`, `parts` (`List<Part<?>>`), `metadata`, and `extensions`. |
| `TaskPushNotificationConfig` | Push notification webhook config with `id`, `taskId`, `url`, `token` (simple bearer token), and `authentication` (`AuthenticationInfo` with `scheme` + `credentials`). The `token` field provides a simpler alternative to full `authentication` for webhook auth. |
| `ListPushNotificationConfigsResponse` | Push notification config list response with `configs`. |

Core immutable model types such as `Task`, `Message`, `Artifact`, and `AgentCard` provide builders, for example: `Task.builder().id("t1").contextId("ctx-1").status(new TaskStatus(TaskState.WORKING)).build()`. Mutable request/configuration classes use standard getters and setters.

## Preview API and SPI Boundaries

The stable user-facing surface for this Preview release is the endpoint URI/options, exchange headers, documented model classes, type converters, and these registry SPIs: `A2ATaskStore`, `A2AExtensionHandler`, and `A2ASecuritySchemeHandler`.

The protocol and operation implementation classes under `org.apache.camel.component.a2a.protocol` and `org.apache.camel.component.a2a.operation` are public so the component can share implementation code across packages and tests, but they are not extension SPIs. `A2AProtocol` is sealed deliberately to the built-in REST and JSON-RPC bindings; select a binding with `protocolBinding` rather than implementing a custom protocol class.

The JSON mapper helper returns configured mapper copies. Customizing the returned `ObjectMapper` does not change component-wide serialization behavior.

## Dependencies

The component has zero compile-time coupling to any HTTP library. Transport is discovered at runtime:

  
| Role | SPI | Examples |
| --- | --- | --- |
| Consumer HTTP server | `RestConsumerFactory` | `camel-platform-http`, `camel-undertow`, `camel-jetty` |
| Producer HTTP client | Built-in `java.net.http.HttpClient` | No additional dependency |
| OAuth tokens | `OAuthClientAuthenticationFactory` | `camel-oauth` (optional, discovered via FactoryFinder) |
| Task state | `A2ATaskStore` | Built-in `InMemoryTaskStore` (default), custom implementations via registry |

Add the HTTP server component you want as a runtime dependency. Consumer routes require one of these dependencies; producer-only routes do not.

```xml
<!-- Consumer: JSON-RPC or non-streaming HTTP endpoint serving -->
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-platform-http-vertx</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>

<!-- Consumer: REST custom-method routes and real-time SSE streaming -->
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-undertow</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>

<!-- Alternative consumer transport for REST custom-method routes and real-time SSE streaming -->
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jetty</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>

<!-- Optional: OAuth authentication -->
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-oauth</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## See Also

-   [Camel 4.21 upgrade notes for A2A](../../manual/camel-4x-upgrade-guide-4_21.md)
    
-   [A2A v1.0 Protocol Specification](https://a2a-protocol.org/latest/specification/)
    
-   [A2A Protocol Definitions](https://a2a-protocol.org/latest/definitions/)
    
-   [A2A Protocol GitHub](https://github.com/a2aproject/A2A)