# LangChain4j Agent

**Since Camel 4.14**

**Only producer is supported**

The LangChain4j Agent component provides comprehensive AI agent capabilities by integrating with the [LangChain4j library](https://github.com/langchain4j/langchain4j). This component supports advanced AI agent patterns including tool calling, conversation memory, retrieval-augmented generation (RAG), and input/output guardrails.

## Features

The LangChain4j Agent component offers the following key features:

-   **Agent-Based Architecture**: Flexible agent creation using the `Agent` API interface
    
-   **Tool Integration**: Seamless integration with Camel routes via the `langchain4j-tools` component
    
-   **Conversation Memory**: Persistent chat memory for maintaining conversation context
    
-   **RAG Support**: Integration with retrieval systems for naive and advanced RAG
    
-   **Guardrails**: Input and output validation and transformation
    
-   **Configuration Flexibility**: Centralized agent configuration using `AgentConfiguration`
    

## Component Options

The component has been simplified to use only two main options:

-   **agent**: Reference to an `Agent` implementation registered in the Camel registry
    
-   **tags**: Tags for discovering and calling Camel route tools (optional)
    

All other configuration (chat models, memory, RAG, guardrails) is now handled through the `AgentConfiguration` when creating agents.

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

The LangChain4j Agent component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **agent** (producer) | **Autowired** The agent to use for the component. |  | Agent |
| **agentFactory** (producer) | **Autowired** The agent factory to use for creating agents if no Agent is provided. |  | AgentFactory |
| **configuration** (producer) | The configuration. |  | LangChain4jAgentConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **tags** (producer) | Tags for discovering and calling Camel route tools. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The LangChain4j Agent endpoint is configured using URI syntax:

langchain4j-agent:agentId

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **agentId** (producer) | **Required** The Agent id. |  | String |

### Query Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **agent** (producer) | **Autowired** The agent to use for the component. |  | Agent |
| **agentFactory** (producer) | **Autowired** The agent factory to use for creating agents if no Agent is provided. |  | AgentFactory |
| **tags** (producer) | Tags for discovering and calling Camel route tools. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The LangChain4j Agent component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelLangChain4jAgentSystemMessage** (producer) Constant: [`SYSTEM_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#SYSTEM_MESSAGE) | The system prompt. |  | String |
| **CamelLangChain4jAgentMemoryId** (producer) Constant: [`MEMORY_ID`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-agent/latest/org/apache/camel/component/langchain4j/agent/api/Headers.html#MEMORY_ID) | Memory ID. |  | Object |

## Spring Boot Auto-Configuration

When using langchain4j-agent with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-langchain4j-agent-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.langchain4j-agent.agent** | The agent to use for the component. The option is a org.apache.camel.component.langchain4j.agent.api.Agent type. |  | Agent |
| **camel.component.langchain4j-agent.agent-factory** | The agent factory to use for creating agents if no Agent is provided. The option is a org.apache.camel.component.langchain4j.agent.api.AgentFactory type. |  | AgentFactory |
| **camel.component.langchain4j-agent.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.langchain4j-agent.configuration** | The configuration. The option is a org.apache.camel.component.langchain4j.agent.LangChain4jAgentConfiguration type. |  | LangChain4jAgentConfiguration |
| **camel.component.langchain4j-agent.enabled** | Whether to enable auto configuration of the langchain4j-agent component. This is enabled by default. |  | Boolean |
| **camel.component.langchain4j-agent.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.langchain4j-agent.tags** | Tags for discovering and calling Camel route tools. |  | String |

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
    

#### Creating an Agent without Memory

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

```java
from("direct:chat")
    .to("langchain4j-agent:test?agent=#simpleAgent")
```

#### Creating an Agent with Memory

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

### Basic Chat with only a userMessage

For simple chat interactions, you can use an agent without memory.

```java
from("direct:chat")
    .to("langchain4j-agent:simple?agent=#simpleAgent")
```

The body can either contain the prompt as a String, or you can create an object of type **org.apache.camel.component.langchain4j.agent.api.AiAgentBody** containing the userMessage.

Usage example with a body as String:

```java
var prompt = "What is Apache Camel";

String response = template.requestBody("direct:chat", prompt, String.class);
```

Usage example with a body as AiAgentBody:

```java
var prompt = "What is Apache Camel";
AiAgentBody body = new AiAgentBody(prompt);

String response = template.requestBody("direct:chat", body, String.class);
```

### Basic Chat with user and system messages

For chat interactions with system prompts, you can use an agent without memory.

```java
from("direct:chat")
    .to("langchain4j-agent:simple?agent=#simpleAgent")
```

The body can either contain the user prompt as a String and specifying the **CamelLangChain4jAgentSystemMessage** header for the system prompt, or you can create an object of type **org.apache.camel.component.langchain4j.agent.api.AiAgentBody** containing both **userMessage** and **systemMessage**.

Usage example with a body as String:

```java
var userPrompt = "Write a short story about a lost cat.";
var systemPrompt = "You are a whimsical storyteller. Your responses should be imaginative, descriptive, and always include a touch of magic. Start every story with 'Once upon a starlit night...";

String response = template.requestBodyAndHeader("direct:chat",
                userPrompt, "CamelLangChain4jAgentSystemMessage", systemPrompt , String.class);
```

Usage example with a body as AiAgentBody:

```java
var userPrompt = "Write a short story about a lost cat.";
var systemPrompt = "You are a whimsical storyteller. Your responses should be imaginative, descriptive, and always include a touch of magic. Start every story with 'Once upon a starlit night...";

AiAgentBody body = new AiAgentBody()
                .withUserMessage(userPrompt)
                .withSystemMessage(systemPrompt);

String response = template.requestBody("direct:chat", body, String.class);
```

### Chat with Tools

Integrate with Camel routes as tools. The LangChain4j Agent component integrates with Camel Routes defined using the Camel LangChain4j Tools component via the `tags` parameter.

```java
// Define tool routes
from("langchain4j-tools:userDb?tags=users&description=Query user database&parameter.userId=string")
    .setBody(constant("{\"name\": \"John Doe\", \"id\": \"123\"}"));

from("langchain4j-tools:weather?tags=weather&description=Get weather information&parameter.city=string")
    .setBody(constant("{\"weather\": \"sunny\", \"temperature\": \"22°C\"}"));

// Agent with tools (using the created agent)
from("direct:chat")
    .to("langchain4j-agent:tools?agent=#simpleAgent&tags=users,weather");
```

Usage example :

```java
var userPrompt = "Can you tell me the name of user 123 and the weather in New York?";
var systemPrompt = "You are a helpful assistant that can access user database and weather information. Use the available tools to provide accurate information.";

String response = template.requestBodyAndHeader("direct:chat",
                userPrompt, "CamelLangChain4jAgentSystemMessage", systemPrompt , String.class);
```

> **Note**
> There’s no need to add Camel LangChain4j Tools component as a dependency when using the tools with LangChain4j Agent component.

### RAG Integration

RAG (Retrieval-Augmented Generation) is supported by configuring a `RetrievalAugmentor` in the `AgentConfiguration`. Create an agent with RAG capabilities:

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

// Use the RAG agent
from("direct:chat")
    .to("langchain4j-agent:rag?agent=#ragAgent")
```

Usage example with Retrieval Augmentor serving as naive RAG :

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

```java
from("direct:chat")
    .to("langchain4j-agent:memory?agent=#memoryAgent")
```

Example of usage with AiAgentBody

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

### Input and Output Guardrails

Guardrails are configured in the `AgentConfiguration` using the fluent API methods. Create classes defining InputGuardrails and OutputGuardrails as defined in the [LangChain4j Guardrails documentation](https://docs.langchain4j.dev/tutorials/guardrails) page.

```java
// Create agent configuration with guardrails
AgentConfiguration configuration = new AgentConfiguration()
    .withChatModel(chatModel)
    .withInputGuardrailClassesList("com.example.MyInputGuardrail")
    .withOutputGuardrailClassesList("com.example.MyOutputGuardrail1,com.example.MyOutputGuardrail2");

Agent safeAgent = new AgentWithoutMemory(configuration);
context.getRegistry().bind("safeAgent", safeAgent);

// Use the agent with guardrails
from("direct:agent-with-guardrails")
    .to("langchain4j-agent:safe?agent=#safeAgent")
```

> **Note**
> The current version of the component returns a String as response. If the outputGuardrails extends JsonExtractorOutputGuardrail class, make sure to return a Json in String format.