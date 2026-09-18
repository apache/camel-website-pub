# LLM Integration Guide

This guide helps you choose the right Camel AI component and apply common LLM integration patterns in production routes. It addresses practical gaps reported by users building document-processing and chat pipelines — structured extraction, streaming to browsers, dynamic prompts, and prompt management at scale.

> **Tip**
> For a catalog of all AI components, start at [AI Components](ai-summary.md). For coding-agent context about Camel itself, see [llms.txt](/llms.txt).

## Choosing an AI component

Camel ships several AI components. Each documents itself well in isolation, but picking the wrong one early leads to provider lock-in or missing features you need later.

### Decision matrix

  
| Use case | Recommended component | Why |
| --- | --- | --- |
| OpenAI or OpenAI-compatible chat (Ollama, vLLM, LM Studio, OpenRouter, Azure OpenAI) | [OpenAI](openai-component.md) | Native OpenAI SDK integration, MCP tool calling, agentic loops, embeddings, audio, structured JSON output via `jsonSchema` / `outputClass` |
| Multi-provider chat without tying routes to one vendor | [LangChain4j Chat](langchain4j-chat-component.md) | Provider-agnostic `ChatModel` beans (OpenAI, Anthropic, Ollama, Vertex, and more via LangChain4j). Strong fit for RAG pipelines with [Embedding Store](langchain4j-embeddingstore-component.md) and content enricher |
| Autonomous agents with Camel route tools and/or MCP servers | [LangChain4j Agent](langchain4j-agent-component.md) | Multi-turn tool calling, guardrails, memory, concurrent tool execution. Complements [MCP Tool Calling](others/openai-mcp.md) for OpenAI-native agentic loops |
| Spring Boot + Spring AI stack | [Spring AI Chat](spring-ai-chat-component.md) | When the application already standardizes on Spring AI beans |
| Vector search / semantic retrieval only | [OpenAI embeddings](others/openai-operations.md) or [LangChain4j Embeddings](langchain4j-embeddings-component.md) | Generate embeddings, then store/query via [PGVector](pgvector-component.md), [Milvus](milvus-component.md), etc. |

### OpenAI vs LangChain4j Chat — quick comparison

**Choose [OpenAI](openai-component.md) when:**

-   You target the OpenAI API (or a compatible proxy) and want first-class MCP, Responses API, embeddings, and audio in one component
    
-   You need built-in conversation memory on the exchange, agentic tool loops, or OpenAI-specific response headers
    
-   Your team prefers configuring everything through Camel URI options and headers
    

**Choose [LangChain4j Chat](langchain4j-chat-component.md) when:**

-   You may switch LLM providers (OpenAI today, Anthropic or local Ollama tomorrow) without rewriting routes
    
-   You orchestrate RAG with Camel EIPs (content enricher, split, aggregate) and LangChain4j `ChatModel` / `EmbeddingModel` beans
    
-   You use prompt templates with \`{{variable}}\` substitution (see [Prompt templates and management at scale](#prompt-templates))
    

Both components can call the same underlying models. The difference is abstraction level and which advanced features (MCP, agent guardrails, Spring Boot starters) you need around the chat call.

## Structured output (recommended for extraction)

For tasks like resume parsing, invoice extraction, or classification, **do not hand-roll JSON parsing** in a follow-up processor unless you have a specific reason. The OpenAI component can constrain the model to return JSON matching a schema.

### JSON Schema (works in Java, XML, and YAML routes)

```yaml
- route:
    from:
      uri: direct:extract-resume
      steps:
        - setBody:
            simple: "${body}"
        - to:
            uri: openai:chat-completion
            parameters:
              model: gpt-4o-mini
              temperature: 0.1
              jsonSchema: resource:classpath:schemas/resume.schema.json
        - unmarshal:
            json:
              library: Jackson
              unmarshalType: com.example.Resume
```

The `jsonSchema` option (or `CamelOpenAIJsonSchema` header) tells the model to emit JSON conforming to your schema. The response body is a JSON **string** — use Camel’s Jackson data format or `json-validator` if you need typed objects or strict validation.

See [Structured Output with JSON Schema](openai-component.html#_structured_output_with_json_schema) for header-based and inline schema examples.

### Java classes (Java DSL only)

When running Java routes, `outputClass` derives the schema from a POJO:

```java
from("direct:extract-person")
    .setBody(constant("Generate a software engineer profile"))
    .to("openai:chat-completion?outputClass=com.example.Person")
    .unmarshal().json(JsonLibrary.Jackson, Person.class);
```

### Tips for reliable structured extraction

-   Set a **low temperature** (0.0–0.2) — see [Generation parameters (temperature and more)](#generation-parameters)
    
-   Keep schemas focused; split large documents into steps (extract sections, then merge)
    
-   Validate with [JSON Validator](json-validator-component.md) when compliance matters
    
-   For LangChain4j agents, see [LangChain4j Agent](langchain4j-agent-component.md) — structured output guardrails avoid prompt-engineering response formats
    

## Generation parameters (temperature and more)

### Chat temperature on OpenAI

The OpenAI component exposes `temperature` (0.0–2.0) and `topP` as endpoint options. You can also set them per exchange via headers:

 
| Option / header | Purpose |
| --- | --- |
| `temperature` URI parameter | Default sampling temperature for the endpoint |
| `CamelOpenAITemperature` header | Override temperature for a single exchange |
| `topP` / `CamelOpenAITopP` | Nucleus sampling alternative to temperature |

```yaml
- to:
    uri: openai:chat-completion
    parameters:
      model: gpt-4o-mini
      temperature: 0.1
```

For provider-specific parameters not exposed as first-class options, use `additionalBodyProperty`:

```yaml
- to:
    uri: openai:chat-completion
    parameters:
      model: gpt-4o-mini
      additionalBodyProperty.seed: "42"
```

> **Note**
> Prefer first-class URI options when available — they are clearer and validated by the component. Use `additionalBodyProperty` for vendor-specific knobs without a dedicated option (for example `seed` for reproducible sampling).

### LangChain4j Chat

Configure temperature on the `ChatModel` bean (Spring Boot properties or programmatic builder). See [LangChain4j Chat — Using a specific Chat Model](langchain4j-chat-component.html#_using_a_specific_chat_model).

## Dynamic prompts per exchange

Prompts can change on every message using Camel’s expression languages — no static `userMessage` URI option required.

### Body as prompt

The message body is the user prompt when no header overrides it:

```yaml
- from:
    uri: direct:ask
    steps:
      - to:
          uri: openai:chat-completion
          parameters:
            model: gpt-4o-mini
```

Send `"Summarize this CV: …​"` as the exchange body.

### Header override with Simple

Use `CamelOpenAIUserMessage` to build prompts from exchange data:

```yaml
- route:
    from:
      uri: direct:score-candidate
      steps:
        - setHeader:
            name: CamelOpenAIUserMessage
            simple: "Rate this candidate 1-10 for role ${header.jobTitle}. CV: ${body}"
        - to:
            uri: openai:chat-completion
            parameters:
              model: gpt-4o-mini
              temperature: 0.2
```

This pattern works well when the body carries a document (file, JSON, text) and the header carries instructions.

## Prompt templates and management at scale

Inline prompt strings in every route become hard to maintain. Common patterns:

### External prompt files

Load prompts from the classpath or file system and pass them as the body or via a processor:

```yaml
- from:
    uri: file:prompts/extract-resume.txt?noop=true
    steps:
      - setHeader:
          name: CamelOpenAIUserMessage
          simple: "${body}\n\nDocument to parse:\n${exchangeProperty.documentText}"
      - to: openai:chat-completion?jsonSchema=resource:classpath:schemas/resume.schema.json
```

See [OpenAI — file-based prompts](openai-component.html#_basic_chat_completion_with_string_input).

### Property placeholders

Store reusable prompt fragments in `application.properties` or Kubernetes ConfigMaps:

```properties
resume.system.prompt=You are a recruiter assistant. Extract only facts present in the document.
resume.user.template=Extract structured data from this resume:\n\n{{body}}
```

Reference with Camel property placeholders in URI options or \`{{property.name}}\` in YAML routes.

### LangChain4j template variables

For LangChain4j Chat, use `CHAT_SINGLE_MESSAGE_WITH_PROMPT` with \`{{variable}}\` placeholders — see [Send a prompt with variables](langchain4j-chat-component.html#_send_a_prompt_with_variables).

### Organization tips

-   One schema file + one prompt file per extraction task
    
-   Version prompts alongside routes (Git) or in external config for non-developer edits
    
-   Keep system instructions in `CamelOpenAISystemMessage` (OpenAI) or `AiAgentBody.systemMessage` (LangChain4j Agent) separate from user content
    

## Streaming responses

With `streaming=true`, the OpenAI component returns an `Iterator<ChatCompletionChunk>` in the message body. Process it with Camel streaming EIPs (`split` + `streaming()`).

### In-route streaming (log, transform, aggregate)

```yaml
- from:
    uri: direct:stream-chat
    steps:
      - to:
          uri: openai:chat-completion
          parameters:
            userMessage: Explain Apache Camel in one paragraph
            streaming: true
      - split:
          streaming: true
          simple: ${body}
          steps:
            - log:
                message: "chunk: ${body}"
```

> **Important**
> Conversation memory is **not** updated for streaming responses. Use non-streaming mode when you need multi-turn history on the same exchange.

### Streaming to a browser (SSE)

For web clients, combine OpenAI streaming with [Platform HTTP](platform-http-component.md) and Server-Sent Events. Add `camel-platform-http-vertx` (or another platform-http implementation) to the classpath.

_Java example — extract text deltas and emit SSE frames_

```java
from("platform-http:/chat/stream?httpMethodRestrict=POST")
    .setHeader("CamelOpenAIUserMessage", simple("${body}"))
    .to("openai:chat-completion?streaming=true")
    .setHeader(Exchange.CONTENT_TYPE, constant("text/event-stream"))
    .split(body()).streaming()
        .process(exchange -> {
            ChatCompletionChunk chunk = exchange.getMessage().getBody(ChatCompletionChunk.class);
            String delta = chunk.choices().isEmpty()
                    ? ""
                    : chunk.choices().get(0).delta().content().orElse("");
            exchange.getMessage().setBody("data: " + delta + "\n\n");
        })
    .end();
```

Enable `useStreaming=true` on the platform-http endpoint when passing large streamed bodies (supported on Vert.x).

### When to stream through Camel vs. bypass it

 
| Stream through Camel | Use a dedicated async handler |
| --- | --- |
| You already orchestrate auth, enrichment, logging, and routing in Camel | You need minimum latency token delivery and already have a reactive Web layer |
| You want one integration path for batch and interactive modes | You only proxy an upstream SSE stream verbatim (consider [A2A RAW passthrough](others/a2a-producer.html#_raw_passthrough_raw_mode)) |
| Moderate throughput chat UI backed by integration logic | High-concurrency fan-out where Camel adds little value between HTTP and the LLM SDK |

## End-to-end example: document extraction pipeline

A typical resume-processing pipeline (the use case from community feedback):

```yaml
- route:
    id: resume-extraction
    from:
      uri: direct:process-resume
      steps:
        # 1. Optional: extract text upstream (docling, tika, etc.)
        - setProperty:
            name: documentText
            simple: "${body}"
        # 2. Structured LLM extraction — no manual JSON parsing
        - setHeader:
            name: CamelOpenAIUserMessage
            simple: "Extract candidate fields from this resume:\n\n${exchangeProperty.documentText}"
        - to:
            uri: openai:chat-completion
            parameters:
              model: gpt-4o-mini
              temperature: 0.1
              jsonSchema: resource:classpath:schemas/resume.schema.json
        # 3. Optional: validate then route to HR system
        - to: json-validator:validate?schema=resource:classpath:schemas/resume.schema.json
        - to: direct:store-candidate
```

## Related documentation

-   [OpenAI Component](openai-component.md) — chat, MCP, embeddings, audio, structured output
    
-   [LangChain4j Chat](langchain4j-chat-component.md) — multi-provider chat and RAG
    
-   [LangChain4j Agent](langchain4j-agent-component.md) — agents, tools, guardrails
    
-   [OpenAI-Compatible Providers](others/openai-providers.md) — Ollama, vLLM, local LLMs
    
-   [MCP Tool Calling](others/openai-mcp.md) — agentic tool loops on OpenAI