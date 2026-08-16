# LangChain4j Agent

**Since Camel 4.14**

**Only producer is supported**

The LangChain4j Agent component provides comprehensive AI agent capabilities by integrating with the [LangChain4j library](https://github.com/langchain4j/langchain4j). This component supports advanced AI agent patterns including tool calling, MCP (Model Context Protocol) integration, conversation memory, retrieval-augmented generation (RAG), and input/output guardrails.

## Features

The LangChain4j Agent component offers the following key features:

-   **Agent-Based Architecture**: Flexible agent creation using the `Agent` API interface
    
-   **Tool Integration**: Seamless integration with Camel routes via the `ai-tool` component
    
-   **MCP Tools**: Integration with Model Context Protocol (MCP) tools for external system access
    
-   **Conversation Memory**: Persistent chat memory for maintaining conversation context
    
-   **RAG Support**: Integration with retrieval systems for naive and advanced RAG
    
-   **Guardrails**: Input and output validation and transformation
    
-   **Configuration Flexibility**: Centralized agent configuration using `AgentConfiguration`
    
-   **Multimodal Content**: Support for images, PDFs, audio, video, and text files from file-based Camel components
    

## Component Options

The component has been simplified to use only two main options:

-   **agent**: Reference to an `Agent` implementation registered in the Camel registry
    
-   **tags**: Tags for discovering and calling Camel route tools (optional)
    

All other configuration (chat models, memory, RAG, guardrails, custom tools, MCP clients) is now handled through the `AgentConfiguration` when creating agents.

## URI format

```none
langchain4j-agent:agentId[?options]
```

Where **agentId** is a unique identifier for the agent instance.

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

The LangChain4j Agent component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **agent** (producer) | **Autowired** The agent to use for the component. |  | Agent |
| **agentConfiguration** (producer) | **Autowired** AgentConfiguration used by Camel to create the agent internally. When set, Camel creates an AgentWithMemory if a ChatMemoryProvider is configured, otherwise an AgentWithoutMemory. If an agentFactory is also configured, the factory takes precedence. |  | AgentConfiguration |
| **agentFactory** (producer) | **Autowired** The agent factory to use for creating agents if no Agent is provided. |  | AgentFactory |
| **configuration** (producer) | The configuration. |  | LangChain4jAgentConfiguration |
| **jsonSchema** (producer) | JSON schema for structured output validation. Only supported in inline agent creation mode: agentConfiguration must be set and neither agent nor agentFactory may be configured. Mutually exclusive with outputClass. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **outputClass** (producer) | Java class to use for structured output. Camel derives the JSON schema from the class and instructs the model to produce matching JSON; the response body is left as a raw JSON string. Only supported in inline agent creation mode: agentConfiguration must be set and neither agent nor agentFactory may be configured. The class must be a POJO with public fields or getters; simple types, enums, and collections are not supported. Mutually exclusive with jsonSchema. |  | Class |
| **tags** (producer) | Tags for discovering and calling Camel route tools. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **mcpClients** (advanced) | Pre-built MCP (Model Context Protocol) client instances for external tool integration. Reference beans from the registry, e.g., #myMcpClient1,#myMcpClient2. |  | List |
| **mcpServer** (advanced) | MCP server definitions in the form of mcpServer..=. Supported properties: transportType (stdio, http, streamableHttp, or sse, default: stdio), command (comma-separated, for stdio), url (for http/sse), environment.= (for stdio), timeout (in seconds, default: 60), logRequests, logResponses, oauthProfile (OAuth profile for HTTP auth, requires camel-oauth). This is a multi-value option with prefix: mcpServer. |  | Map |

## Endpoint Options

The LangChain4j Agent endpoint is configured using URI syntax:

langchain4j-agent:agentId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **agentId** (producer) | **Required** The Agent id. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **agent** (producer) | **Autowired** The agent to use for the component. |  | Agent |
| **agentConfiguration** (producer) | **Autowired** AgentConfiguration used by Camel to create the agent internally. When set, Camel creates an AgentWithMemory if a ChatMemoryProvider is configured, otherwise an AgentWithoutMemory. If an agentFactory is also configured, the factory takes precedence. |  | AgentConfiguration |
| **agentFactory** (producer) | **Autowired** The agent factory to use for creating agents if no Agent is provided. |  | AgentFactory |
| **jsonSchema** (producer) | JSON schema for structured output validation. Only supported in inline agent creation mode: agentConfiguration must be set and neither agent nor agentFactory may be configured. Mutually exclusive with outputClass. |  | String |
| **outputClass** (producer) | Java class to use for structured output. Camel derives the JSON schema from the class and instructs the model to produce matching JSON; the response body is left as a raw JSON string. Only supported in inline agent creation mode: agentConfiguration must be set and neither agent nor agentFactory may be configured. The class must be a POJO with public fields or getters; simple types, enums, and collections are not supported. Mutually exclusive with jsonSchema. |  | Class |
| **tags** (producer) | Tags for discovering and calling Camel route tools. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **mcpClients** (advanced) | Pre-built MCP (Model Context Protocol) client instances for external tool integration. Reference beans from the registry, e.g., #myMcpClient1,#myMcpClient2. |  | List |
| **mcpServer** (advanced) | MCP server definitions in the form of mcpServer..=. Supported properties: transportType (stdio, http, streamableHttp, or sse, default: stdio), command (comma-separated, for stdio), url (for http/sse), environment.= (for stdio), timeout (in seconds, default: 60), logRequests, logResponses, oauthProfile (OAuth profile for HTTP auth, requires camel-oauth). This is a multi-value option with prefix: mcpServer. |  | Map |

## Message Headers

The LangChain4j Agent component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelLangChain4jAgentSystemMessage** (producer) Constant: [`SYSTEM_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#SYSTEM_MESSAGE) | The system prompt. |  | String |
| **CamelLangChain4jAgentMemoryId** (producer) Constant: [`MEMORY_ID`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#MEMORY_ID) | Memory ID. |  | Object |
| **CamelLangChain4jAgentUserMessage** (producer) Constant: [`USER_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#USER_MESSAGE) | The user message to accompany file content when using WrappedFile as input. |  | String |
| **CamelLangChain4jAgentMediaType** (producer) Constant: [`MEDIA_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#MEDIA_TYPE) | The media type (MIME type) of the file content. Overrides auto-detection from file extension. |  | String |
| **CamelLangChain4jAgentExcludeTags** (producer) Constant: [`EXCLUDE_TAGS`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#EXCLUDE_TAGS) | Comma-separated list of Camel tool tags to exclude from this agent invocation. |  | String |
| **CamelLangChain4jAgentExcludeMcpServers** (producer) Constant: [`EXCLUDE_MCP_SERVERS`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#EXCLUDE_MCP_SERVERS) | Comma-separated list of MCP server names (keys) to exclude from this agent invocation. |  | String |
| **CamelLangChain4jAgentFinishReason** (producer) Constant: [`FINISH_REASON`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#FINISH_REASON) | 
The Finish Reason.

Enum values:

-   STOP
    
-   LENGTH
    
-   TOOL\_EXECUTION
    
-   CONTENT\_FILTER
    
-   OTHER
    





 |  | FinishReason |
| **CamelLangChain4jAgentInputTokenCount** (producer) Constant: [`INPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#INPUT_TOKEN_COUNT) | The Input Token Count. |  | int |
| **CamelLangChain4jAgentOutputTokenCount** (producer) Constant: [`OUTPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#OUTPUT_TOKEN_COUNT) | The Output Token Count. |  | int |
| **CamelLangChain4jAgentTotalTokenCount** (producer) Constant: [`TOTAL_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#TOTAL_TOKEN_COUNT) | The Total Token Count. |  | int |
| **CamelLangChain4jAgentRequestModel** (producer) Constant: [`REQUEST_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#REQUEST_MODEL) | The request model name. |  | String |
| **CamelLangChain4jAgentResponseModel** (producer) Constant: [`RESPONSE_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#RESPONSE_MODEL) | The response model name. Not set by the agent producer when langchain4j Result does not expose it. |  | String |
| **CamelLangChain4jAgentSources** (producer) Constant: [`SOURCES`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#SOURCES) | RAG sources retrieved during agent invocation. |  | List |
| **CamelLangChain4jAgentToolExecutions** (producer) Constant: [`TOOL_EXECUTIONS`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#TOOL_EXECUTIONS) | Tool executions performed during agent invocation. |  | List |

## OAuth Authentication

### Quarkus Runtime

When running in Quarkus, use the [quarkus-langchain4j-oidc-mcp-auth-provider](https://quarkus.io/extensions/io.quarkiverse.langchain4j/quarkus-langchain4j-oidc-mcp-auth-provider/) extension for MCP server authentication. This is the recommended approach as it integrates natively with Quarkus OIDC, supports automatic token propagation, and follows Quarkus security best practices.

```xml
<dependency>
    <groupId>io.quarkiverse.langchain4j</groupId>
    <artifactId>quarkus-langchain4j-oidc-mcp-auth-provider</artifactId>
</dependency>
```

With this extension, the authenticated user’s OIDC access token is automatically propagated to MCP servers. MCP clients are configured via `quarkus.langchain4j.mcp.*` properties and are injected as pre-built beans. Camel picks them up via the `mcpClients` parameter — no `oauthProfile` or `camel-oauth` is needed.

### camel-main and manual MCP server configuration

When running outside Quarkus (e.g., camel-main) or when manually configuring MCP servers via inline `mcpServer.<name>.*` parameters, use the `oauthProfile` option to acquire an access token via the OAuth 2.0 Client Credentials grant. The token is injected as an `Authorization: Bearer` header on HTTP-based MCP transports. This requires `camel-oauth` on the classpath.

```properties
camel.oauth.keycloak.client-id=camel-client
camel.oauth.keycloak.client-secret=camel-client-secret
camel.oauth.keycloak.token-endpoint=https://keycloak.example.com/realms/camel/protocol/openid-connect/token
```

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:agent")
    .to("langchain4j-agent:myAgent?mcpServer.tools.transportType=http&mcpServer.tools.url=https://mcp.internal/mcp&mcpServer.tools.oauthProfile=keycloak");
```

```xml
<route>
  <from uri="direct:agent"/>
  <to uri="langchain4j-agent:myAgent?mcpServer.tools.transportType=http&amp;mcpServer.tools.url=https://mcp.internal/mcp&amp;mcpServer.tools.oauthProfile=keycloak"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:agent
      steps:
        - to:
            uri: langchain4j-agent:myAgent
            parameters:
              mcpServer.tools.transportType: http
              mcpServer.tools.url: "https://mcp.internal/mcp"
              mcpServer.tools.oauthProfile: keycloak
```

### LLM Provider Authentication

The langchain4j-agent component accepts a pre-built `Agent` or `ChatModel` bean — it does not create the LLM client itself. For LLM providers that require OAuth authentication (e.g., Azure OpenAI), use `OAuthHelper` when building the bean programmatically:

_Java-only: programmatic `ChatModel` bean registration with \`OAuthHelper\`_

```java
String token = OAuthHelper.resolveOAuthToken(getContext(), "azure");

ChatModel chatModel = OpenAiChatModel.builder()
        .apiKey(token)
        .modelName("gpt-4")
        .build();

getContext().getRegistry().bind("myChatModel", chatModel);

from("direct:agent")
    .to("langchain4j-agent:myAgent");
```

> **Note**
> In Quarkus or Spring Boot, configure the ChatModel via the framework’s own properties and dependency injection instead of programmatic bean registration.

## Usage

### Creating Custom Agents

Starting from Camel 4.14, the LangChain4j Agent component uses an agent-based architecture where agents are created by implementing the `org.apache.camel.component.langchain4j.agent.api.Agent` interface. The component provides two built-in agent implementations:

-   `AgentWithMemory` - For chat interactions with conversation history
    
-   `AgentWithoutMemory` - For stateless chat interactions
    

#### Agent Configuration

Agents are configured using the `AgentConfiguration` class which provides a fluent API for setting up:

-   Chat Model
    
-   Chat Memory Provider (for memory-enabled agents)
    
-   Retrieval Augmentor (for RAG functionality)
    
-   Input and Output Guardrails
    
-   Concurrent tool execution (`withExecuteToolsConcurrently`) for parallel Camel route tools and MCP tools within one LLM round trip
    

#### Concurrent tool execution

When the LLM requests multiple tools in a single turn, LangChain4j can invoke them in parallel via `AgentConfiguration.withExecuteToolsConcurrently()`. Camel route tools (`ai-tool:` consumers discovered through `tags`) run each invocation on an isolated exchange copy, so concurrent execution does not corrupt the producer exchange.

_Java-only: enable parallel tool calls with a managed Camel executor_

```java
AgentConfiguration configuration = new AgentConfiguration()
    .withChatModel(chatModel)
    .withExecuteToolsConcurrently();

// When created through langchain4j-agent (agentConfiguration on the endpoint),
// Camel registers a managed thread pool from ExecutorServiceManager automatically.
// Pass your own Executor with withExecuteToolsConcurrently(executor) to override.
```

Tool-route header side-effects are not merged back onto the main exchange when tools run concurrently; only the tool result text is returned to the LLM.

#### Creating an Agent without Memory

_Java-only: LangChain4j `AgentConfiguration` and programmatic bean registration_

```java
// Create and configure the chat model
ChatModel chatModel = OpenAiChatModel.builder()
    .apiKey(openApiKey)
    .modelName(GPT_3_5_TURBO)
    .temperature(0.3)
    .timeout(ofSeconds(3000))
    .build();

// Create agent configuration
AgentConfiguration configuration = new AgentConfiguration()
    .withChatModel(chatModel)
    .withInputGuardrailClasses(List.of())
    .withOutputGuardrailClasses(List.of());

// Create the agent
Agent simpleAgent = new AgentWithoutMemory(configuration);

// Register the agent in the Camel context
context.getRegistry().bind("simpleAgent", simpleAgent);
```

Use the agent in your Camel route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-agent:test?agent=#simpleAgent")
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-agent:test?agent=#simpleAgent"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-agent:test
            parameters:
              agent: "#simpleAgent"
```

#### Creating an Agent with Memory

_Java-only: LangChain4j `ChatMemoryProvider` and `AgentConfiguration` setup_

```java
// Create chat model (same as above)
ChatModel chatModel = OpenAiChatModel.builder()...

// Create memory provider
ChatMemoryProvider memoryProvider = memoryId -> MessageWindowChatMemory.builder()
    .id(memoryId)
    .maxMessages(10)
    .chatMemoryStore(persistentStore) // Your persistent store implementation
    .build();

// Create agent configuration with memory
AgentConfiguration configuration = new AgentConfiguration()
    .withChatModel(chatModel)
    .withChatMemoryProvider(memoryProvider)
    .withInputGuardrailClasses(List.of())
    .withOutputGuardrailClasses(List.of());

// Create the agent
Agent memoryAgent = new AgentWithMemory(configuration);

// Register the agent
context.getRegistry().bind("memoryAgent", memoryAgent);
```

> **Note**
> Add the `camel-langchain4j-agent-api` dependency to access the Agent API classes in your application:
>
> ```xml
> <dependency>
>     <groupId>org.apache.camel</groupId>
>     <artifactId>camel-langchain4j-agent-api</artifactId>
>     <version>x.x.x</version>
> </dependency>
> ```

### Using AgentConfiguration Directly

Instead of manually instantiating `AgentWithoutMemory` or `AgentWithMemory`, you can register an `AgentConfiguration` bean and let Camel create the right agent implementation automatically. Camel creates an `AgentWithMemory` when a `ChatMemoryProvider` is present, or an `AgentWithoutMemory` otherwise.

#### Stateless agent

_Java-only: `AgentConfiguration` bean registration_

```java
AgentConfiguration config = new AgentConfiguration()
    .withChatModel(chatModel);

context.getRegistry().bind("myConfig", config);
```

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-agent:assistant?agentConfiguration=#myConfig");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-agent:assistant?agentConfiguration=#myConfig"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-agent:assistant
            parameters:
              agentConfiguration: "#myConfig"
```

#### Stateful agent (with memory)

_Java-only: `ChatMemoryProvider` and `AgentConfiguration` bean registration_

```java
ChatMemoryProvider memoryProvider = memoryId -> MessageWindowChatMemory.builder()
    .id(memoryId)
    .maxMessages(10)
    .chatMemoryStore(persistentStore)
    .build();

AgentConfiguration config = new AgentConfiguration()
    .withChatModel(chatModel)
    .withChatMemoryProvider(memoryProvider);

context.getRegistry().bind("myConfig", config);
```

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-agent:assistant?agentConfiguration=#myConfig");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-agent:assistant?agentConfiguration=#myConfig"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-agent:assistant
            parameters:
              agentConfiguration: "#myConfig"
```

If an `agentFactory` is also configured on the endpoint, the factory takes precedence over `agentConfiguration`.

### Basic Chat with only a userMessage

For simple chat interactions, you can use an agent without memory.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-agent:simple?agent=#simpleAgent")
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-agent:simple?agent=#simpleAgent"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-agent:simple
            parameters:
              agent: "#simpleAgent"
```

The body can either contain the prompt as a String, or you can create an object of type **org.apache.camel.component.langchain4j.agent.api.AiAgentBody** containing the userMessage.

_Java-only: ProducerTemplate test API_

```java
var prompt = "What is Apache Camel";

String response = template.requestBody("direct:chat", prompt, String.class);
```

_Java-only: ProducerTemplate test API with \`AiAgentBody\`_

```java
var prompt = "What is Apache Camel";
AiAgentBody body = new AiAgentBody(prompt);

String response = template.requestBody("direct:chat", body, String.class);
```

### Basic Chat with user and system messages

For chat interactions with system prompts, you can use an agent without memory.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-agent:simple?agent=#simpleAgent")
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-agent:simple?agent=#simpleAgent"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-agent:simple
            parameters:
              agent: "#simpleAgent"
```

The body can either contain the user prompt as a String and specifying the **CamelLangChain4jAgentSystemMessage** header for the system prompt, or you can create an object of type **org.apache.camel.component.langchain4j.agent.api.AiAgentBody** containing both **userMessage** and **systemMessage**.

_Java-only: ProducerTemplate test API_

```java
var userPrompt = "Write a short story about a lost cat.";
var systemPrompt = "You are a whimsical storyteller. Your responses should be imaginative, descriptive, and always include a touch of magic. Start every story with 'Once upon a starlit night...";

String response = template.requestBodyAndHeader("direct:chat",
                userPrompt, "CamelLangChain4jAgentSystemMessage", systemPrompt , String.class);
```

_Java-only: ProducerTemplate test API with \`AiAgentBody\`_

```java
var userPrompt = "Write a short story about a lost cat.";
var systemPrompt = "You are a whimsical storyteller. Your responses should be imaginative, descriptive, and always include a touch of magic. Start every story with 'Once upon a starlit night...";

AiAgentBody body = new AiAgentBody()
                .withUserMessage(userPrompt)
                .withSystemMessage(systemPrompt);

String response = template.requestBody("direct:chat", body, String.class);
```

### Chat with Tools

Integrate with Camel routes as tools. The LangChain4j Agent component integrates with Camel Routes defined using the `ai-tool` component via the `tags` parameter.

-   Java
    
-   XML
    
-   YAML
    

```java
// Define tool routes
from("ai-tool:userDb?tags=users&description=Query user database&parameter.userId=string")
    .setBody(constant("{\"name\": \"John Doe\", \"id\": \"123\"}"));

from("ai-tool:weather?tags=weather&description=Get weather information&parameter.city=string")
    .setBody(constant("{\"weather\": \"sunny\", \"temperature\": \"22°C\"}"));

// Agent with tools (using the created agent)
from("direct:chat")
    .to("langchain4j-agent:tools?agent=#simpleAgent&tags=users,weather");
```

```xml
<!-- Define tool routes -->
<route>
  <from uri="ai-tool:userDb?tags=users&amp;description=Query user database&amp;parameter.userId=string"/>
  <setBody>
    <constant>{"name": "John Doe", "id": "123"}</constant>
  </setBody>
</route>

<route>
  <from uri="ai-tool:weather?tags=weather&amp;description=Get weather information&amp;parameter.city=string"/>
  <setBody>
    <constant>{"weather": "sunny", "temperature": "22°C"}</constant>
  </setBody>
</route>

<!-- Agent with tools -->
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-agent:tools?agent=#simpleAgent&amp;tags=users,weather"/>
</route>
```

```yaml
# Define tool routes
- route:
    from:
      uri: ai-tool:userDb
      parameters:
        tags: users
        description: Query user database
        parameter.userId: string
      steps:
        - setBody:
            constant: '{"name": "John Doe", "id": "123"}'

- route:
    from:
      uri: ai-tool:weather
      parameters:
        tags: weather
        description: Get weather information
        parameter.city: string
      steps:
        - setBody:
            constant: '{"weather": "sunny", "temperature": "22°C"}'

# Agent with tools
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-agent:tools
            parameters:
              agent: "#simpleAgent"
              tags: users,weather
```

_Java-only: ProducerTemplate test API_

```java
var userPrompt = "Can you tell me the name of user 123 and the weather in New York?";
var systemPrompt = "You are a helpful assistant that can access user database and weather information. Use the available tools to provide accurate information.";

String response = template.requestBodyAndHeader("direct:chat",
                userPrompt, "CamelLangChain4jAgentSystemMessage", systemPrompt , String.class);
```

> **Note**
> Add the `camel-ai-tool` dependency to use Camel route tools with the LangChain4j Agent component:
>
> ```xml
> <dependency>
>     <groupId>org.apache.camel</groupId>
>     <artifactId>camel-ai-tool</artifactId>
> </dependency>
> ```

### Custom LangChain4j Tools

You can also add custom LangChain4j tools using the `@Tool` annotation. These tools are passed directly to the agent via the `customTools` configuration parameter.

#### Creating Custom LangChain4j Tools

Create a class with methods annotated with `@Tool`:

_Java-only: LangChain4j `@Tool` annotated class_

```java
import dev.langchain4j.agent.tool.P;
import dev.langchain4j.agent.tool.Tool;

public class CalculatorTool {

    @Tool("Adds two numbers")
    public int add(@P("First number") int a, @P("Second number") int b) {
        return a + b;
    }

    @Tool("Multiplies two numbers")
    public int multiply(@P("First number") int a, @P("Second number") int b) {
        return a * b;
    }

    @Tool("Gets the square root of a number")
    public double sqrt(@P("Number") double x) {
        return Math.sqrt(x);
    }
}
```

#### Using Custom LangChain4j Tools with Agent

Pass your custom tool instances to the agent configuration:

_Java-only: LangChain4j `@Tool` instances and `AgentConfiguration` setup_

```java
// Create tool instances
CalculatorTool calculator = new CalculatorTool();
WeatherTool weather = new WeatherTool();

// Create agent configuration with custom tools
AgentConfiguration config = new AgentConfiguration()
    .withChatModel(chatModel)
    .withCustomTools(Arrays.asList(calculator, weather));

// Create agent
Agent agent = new AgentWithoutMemory(config);

// Register agent in Camel context
context.getRegistry().bind("customToolsAgent", agent);
```

#### Route Configuration

Use the agent with custom tools in your routes:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-agent:assistant?agent=#customToolsAgent")
    .to("mock:agent-response");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-agent:assistant?agent=#customToolsAgent"/>
  <to uri="mock:agent-response"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-agent:assistant
            parameters:
              agent: "#customToolsAgent"
        - to:
            uri: mock:agent-response
```

#### Usage Example

_Java-only: ProducerTemplate test API_

```java
String response = template.requestBody("direct:chat",
    "Calculate 10 * 5 and tell me the weather in Paris", String.class);
```

> **Note**
> Custom LangChain4j tools are executed directly by the LangChain4j framework. No additional configuration or tool Executor is needed for tool execution.

### Mixed Tools (Camel Routes + Custom LangChain4j Tools)

You can combine both Camel route tools (via `tags`) and custom LangChain4j tools (via `customTools`) in the same agent:

_Java-only: LangChain4j `@Tool` instances, `AgentConfiguration`, and bean registration_

```java
// Define Camel route tools
from("ai-tool:weatherService?tags=weather&description=Get current weather information&parameter.location=string")
    .setBody(constant("{\"weather\": \"sunny\", \"location\": \"Current Location\"}"));

// Create custom tool instances
CalculatorTool calculator = new CalculatorTool();
StringTool stringTool = new StringTool();

// Create agent configuration with both types of tools
AgentConfiguration config = new AgentConfiguration()
    .withChatModel(chatModel)
    .withCustomTools(Arrays.asList(calculator, stringTool));

// Create agent
Agent agent = new AgentWithMemory(config);

// Register agent in Camel context
context.getRegistry().bind("mixedToolsAgent", agent);
```

#### Route Configuration with Mixed Tools

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-agent:assistant?agent=#mixedToolsAgent&tags=weather")
    .to("mock:agent-response");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-agent:assistant?agent=#mixedToolsAgent&amp;tags=weather"/>
  <to uri="mock:agent-response"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-agent:assistant
            parameters:
              agent: "#mixedToolsAgent"
              tags: weather
        - to:
            uri: mock:agent-response
```

#### Usage Example

_Java-only: ProducerTemplate test API_

```java
String response = template.requestBody("direct:chat",
    "Calculate 10 * 5 and tell me the weather in London", String.class);
```

> **Note**
> When using mixed tools, Camel route tools are discovered dynamically via the `tags` parameter, while custom LangChain4j tools are provided statically via the `customTools` configuration.

### RAG Integration

RAG (Retrieval-Augmented Generation) is supported by configuring a `RetrievalAugmentor` in the `AgentConfiguration`. Create an agent with RAG capabilities:

_Java-only: LangChain4j `RetrievalAugmentor` and `AgentConfiguration` setup_

```java
// Create the retrieval augmentor (shown below)
RetrievalAugmentor retrievalAugmentor = createRetrievalAugmentor();

// Create agent configuration with RAG
AgentConfiguration configuration = new AgentConfiguration()
    .withChatModel(chatModel)
    .withRetrievalAugmentor(retrievalAugmentor)
    .withInputGuardrailClasses(List.of())
    .withOutputGuardrailClasses(List.of());

Agent ragAgent = new AgentWithoutMemory(configuration);
context.getRegistry().bind("ragAgent", ragAgent);
```

Use the RAG agent:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-agent:rag?agent=#ragAgent")
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-agent:rag?agent=#ragAgent"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-agent:rag
            parameters:
              agent: "#ragAgent"
```

_Java-only: LangChain4j `EmbeddingStoreContentRetriever` and ProducerTemplate test API_

```java
// creating the retrieval Augmentor
EmbeddingStoreContentRetriever contentRetriever = EmbeddingStoreContentRetriever.builder()
                .embeddingStore(embeddingStore) // the embedding store should be defined
                .embeddingModel(embeddingModel) // the embedding model should be defined
                .maxResults(3)
                .minScore(0.6)
                .build();

RetrievalAugmentor retrievalAugmentor = DefaultRetrievalAugmentor.builder()
                .contentRetriever(contentRetriever)
                // other options or steps can be included for Advanced RAG
                .build();

// bind the retrievalAugmentor in the context
context.getRegistry().bind("retrievalAugmentor", retrievalAugmentor);

// using the producer
String response = template.requestBody("direct:chat", body, String.class);
```

### Chat with Memory

Memory functionality is supported by using `AgentWithMemory` and configuring a `ChatMemoryProvider` in the `AgentConfiguration`. The memory works for multiple users/sessions.

> **Note**
> The component requires using a Chat Memory Provider that uses a [persistent memory store](https://docs.langchain4j.dev/tutorials/chat-memory#persistence).

The memory works for multiple users/sessions. For each context window, the users needs to set the memory ID: - By setting the Header CamelLangChain4jAgentMemoryId. This supposes that user is using a body as String. - By setting the AiAgentBody.memoryId field. This supposes that that user is using a body as AiAgentBody.

Example of Route with Memory Agent

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("langchain4j-agent:memory?agent=#memoryAgent")
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="langchain4j-agent:memory?agent=#memoryAgent"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:chat
      steps:
        - to:
            uri: langchain4j-agent:memory
            parameters:
              agent: "#memoryAgent"
```

_Java-only: `ChatMemoryProvider`, `AiAgentBody`, and ProducerTemplate test API_

```java
// Example of creating a Chat Memory Provider : Create a message window memory that keeps the last 10 messages
        ChatMemoryProvider chatMemoryProvider = memoryId -> MessageWindowChatMemory.builder()
                .id(memoryId)
                .maxMessages(10)
                .chatMemoryStore(store) // the Chat Memory store is previously created
                .build();

// bind the chat memory provider in the context
context.getRegistry().bind("chatMemoryProvider", chatMemoryProvider);


AiAgentBody request = new AiAgentBody("Hello!", null, "session-123");
String response = template.requestBody("direct:chat", request, String.class);
```

### Structured Outputs with JSON Schema

The LangChain4j Agent component supports structured outputs by enforcing a JSON schema on LLM responses. This feature is available for providers that support structured outputs including Amazon Bedrock, Azure OpenAI, Google AI Gemini, Mistral, Ollama, and OpenAI.

#### Using the jsonSchema endpoint option

The simplest way to enable structured output is to use the `jsonSchema` endpoint option. This works when using `agentConfiguration` (inline agent creation mode). The option supports classpath references, file paths, and inline JSON, the same way as the `camel-openai` component.

##### Example with classpath resource

Create a JSON schema file, for example `src/main/resources/person-schema.json`:

```json
{
    "type": "object",
    "properties": {
        "name": {"type": "string", "description": "The person's full name"},
        "age": {"type": "integer", "description": "The person's age in years"},
        "occupation": {"type": "string", "description": "The person's job"}
    },
    "required": ["name", "age", "occupation"],
    "additionalProperties": false
}
```

Then use it in a route:

_Java-only: `AgentConfiguration` bean registration_

```java
AgentConfiguration agentConfiguration = new AgentConfiguration()
        .withChatModel(chatModel);

context.getRegistry().bind("myAgentConfig", agentConfiguration);
```

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:extract-person-info")
    .setBody(constant("Extract information about John Smith, a 35-year-old software engineer"))
    .to("langchain4j-agent:structured?agentConfiguration=#myAgentConfig&jsonSchema=classpath:person-schema.json")
    .unmarshal().json()
    .log("Extracted person: ${body}");
```

```xml
<route>
  <from uri="direct:extract-person-info"/>
  <setBody>
    <constant>Extract information about John Smith, a 35-year-old software engineer</constant>
  </setBody>
  <to uri="langchain4j-agent:structured?agentConfiguration=#myAgentConfig&amp;jsonSchema=classpath:person-schema.json"/>
  <unmarshal>
    <json/>
  </unmarshal>
  <log message="Extracted person: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:extract-person-info
      steps:
        - setBody:
            constant: "Extract information about John Smith, a 35-year-old software engineer"
        - to:
            uri: langchain4j-agent:structured
            parameters:
              agentConfiguration: "#myAgentConfig"
              jsonSchema: "classpath:person-schema.json"
        - unmarshal:
            json: {}
        - log:
            message: "Extracted person: ${body}"
```

The `jsonSchema` option accepts:

-   Classpath resources: `jsonSchema=classpath:schemas/person.json`
    
-   File paths: `jsonSchema=file:///path/to/schema.json`
    
-   Inline JSON: `jsonSchema={"type":"object","properties":{"name":{"type":"string"}}}`
    
-   Property placeholders: `jsonSchema=resource:classpath:${schema.location}`
    

#### Using the outputClass endpoint option (Java Class-based Schema)

As an alternative to providing a JSON schema directly, you can use the `outputClass` endpoint option to specify a Java class. The Camel LangChain4j agent will automatically:

1.  Derive the JSON schema from the class structure
    
2.  Configure the AI model to return JSON matching that schema
    

The response body is left as a raw JSON string, consistent with the `camel-openai` component. Use Camel’s `.unmarshal().json()` in your route to convert it to a POJO.

This approach is mutually exclusive with `jsonSchema` — you can use one or the other, but not both.

##### Example with Java POJO

First, define your response class. Annotate required fields with `@JsonProperty(required = true)` so they appear in the `required` array of the generated JSON schema, ensuring the model always populates them. Use `@Description` to add semantic hints:

_Java-only: Java POJO with `@JsonProperty` and `@Description` annotations_

```java
import com.fasterxml.jackson.annotation.JsonProperty;
import dev.langchain4j.model.output.structured.Description;

public class PersonInfo {
    @JsonProperty(required = true)
    @Description("The person's full name")
    private String name;

    @JsonProperty(required = true)
    @Description("The person's age in years")
    private int age;

    @JsonProperty(required = true)
    @Description("The person's job or profession")
    private String occupation;

    // Getters and setters...
}
```

Then configure the endpoint to use this class. Use the fully qualified class name (FQCN) directly — no registry binding needed. Add `.unmarshal().json()` to convert the raw JSON response to a POJO:

_Java-only: `AgentConfiguration` bean setup, `unmarshal` with POJO class, and `process` lambda_

```java
AgentConfiguration agentConfiguration = new AgentConfiguration()
        .withChatModel(chatModel);

context.getRegistry().bind("myAgentConfig", agentConfiguration);

from("direct:extract-person-info")
    .setBody(constant("Extract information about John Smith, a 35-year-old software engineer"))
    .to("langchain4j-agent:structured?agentConfiguration=#myAgentConfig&outputClass=com.example.PersonInfo")
    .unmarshal().json(PersonInfo.class)
    .process(exchange -> {
        PersonInfo person = exchange.getIn().getBody(PersonInfo.class);
        log.info("Name: {}, Age: {}, Occupation: {}",
            person.getName(), person.getAge(), person.getOccupation());
    });
```

> **Note**
> -   Both `jsonSchema` and `outputClass` only work when using `agentConfiguration` (inline agent creation mode), without `agent` or `agentFactory` configured
>     
> -   You cannot use both options simultaneously — they are mutually exclusive
>     
> -   The AI model must support structured outputs (e.g., OpenAI GPT-4o, GPT-4o-mini, or Ollama models with JSON mode)
>     
> -   Complex nested objects and collections are fully supported with `outputClass`

#### Alternative: configuring ResponseFormat on the ChatModel

You can also define the `ResponseFormat` at the `ChatModel` level. See the [LangChain4j Structured Outputs documentation](https://docs.langchain4j.dev/tutorials/structured-outputs#using-json-schema-with-chatmodel) for details.

> **Note**
> -   The LLM response will be guaranteed to conform to the provided schema
>     
> -   No prompt engineering is needed for output formatting
>     
> -   The same schema file can be shared across `camel-openai` and `camel-langchain4j-agent` components

## Sub-Pages

For more details on specific features, see:

-   [Input and Output Guardrails](others/langchain4j-agent-guardrails.md) - Custom and built-in guardrails, presets, advanced configuration, and Spring Boot integration
    
-   [MCP Tools Integration](others/langchain4j-agent-mcp.md) - Model Context Protocol client configuration, tool filtering, and endpoint-level MCP setup
    
-   [Multimodal Content Support](others/langchain4j-agent-multimodal.md) - Image, PDF, audio, and video processing with automatic file conversion