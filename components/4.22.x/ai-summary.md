# AI

The Camel AI components are a group of components for applying Apache Camel to various AI-related technologies.

## Getting started with LLMs

New to Camel AI? Start with the [LLM Integration Guide](ai-llm-integration-guide.md) — it explains when to use [OpenAI](openai-component.md) vs [LangChain4j Chat](langchain4j-chat-component.md), structured JSON extraction, streaming to browsers, dynamic prompts, and prompt management patterns.

## Choosing the Right AI Component

Camel offers two main paths for integrating Large Language Models (LLMs) into routes:

-   **[OpenAI](openai-component.md)** — talks directly to OpenAI and any OpenAI-compatible API (OpenRouter, Ollama, vLLM, LM Studio). Native support for streaming, structured output (`outputClass` / `jsonSchema`), MCP tool calling, conversation memory, and the Responses API. Best when you are committed to the OpenAI ecosystem or using an OpenAI-compatible gateway.
    
-   **[LangChain4j Chat](langchain4j-chat-component.md)** — abstracts through [LangChain4j](https://github.com/langchain4j/langchain4j) so you can switch LLM providers (OpenAI, Anthropic, Google Gemini, Mistral, Ollama, and others) by swapping a dependency. Also provides prompt templates with variables, RAG integration via the Content Enricher pattern, and multi-message conversation history.
    

  
| Need | camel-openai | camel-langchain4j-chat |
| --- | --- | --- |
| OpenAI or compatible API (OpenRouter, Ollama, vLLM) | Yes | Via LangChain4j provider |
| Switch providers without code changes | No (OpenAI-compatible only) | Yes |
| MCP tool calling / agentic loops | Yes | No (use [langchain4j-tools](langchain4j-tools-component.md) instead) |
| Streaming responses | Yes | Manual (via `StreamingChatLanguageModel`) |
| Structured output (JSON schema) | Yes (`outputClass`, `jsonSchema`) | No |
| Prompt templates with variables | No (use Simple expressions) | Yes (built-in \`{{variable}}\` syntax) |
| RAG pipelines | Manual | Yes (with `LangChain4jRagAggregatorStrategy`) |
| Embeddings | Yes | Via [langchain4j-embeddingstore](langchain4j-embeddingstore-component.md) |
> **Tip**
> If you already use an OpenAI-compatible API and want the richest feature set (streaming, MCP, structured output), start with `camel-openai`. If multi-provider flexibility is a hard requirement, use `camel-langchain4j-chat`. Both can coexist in the same project. For end-to-end pipeline examples, see the [LLM Integration Guide](ai-llm-integration-guide.md).

## AI components

See the following for usage of each component:

[A2A](a2a-component.md)

A2A endpoint for agent-to-agent communication.

[AI Tool](ai-tool-component.md)

Framework-agnostic consumer endpoint that registers a Camel route as an LLM tool in the shared AiToolRegistry.

[ChatScript](chatscript-component.md)

Chat with a ChatScript Server.

[Deep Java Library](djl-component.md)

Infer Deep Learning models from message exchanges data using Deep Java Library (DJL).

[Docling](docling-component.md)

Process documents using Docling library for parsing and conversion.

[KServe](kserve-component.md)

Provide access to AI model servers with the KServe standard to run inference with remote models

[LangChain4j Agent](langchain4j-agent-component.md)

LangChain4j Agent component

[LangChain4j Chat](langchain4j-chat-component.md)

LangChain4j Chat component

[LangChain4j Embedding Store](langchain4j-embeddingstore-component.md)

Perform operations on the LangChain4jEmbeddingStores.

[LangChain4j Embeddings](langchain4j-embeddings-component.md)

LangChain4j Embeddings

[LangChain4j Tools](langchain4j-tools-component.md)

LangChain4j Tools and Function Calling Features

[LangChain4j Web Search](langchain4j-web-search-component.md)

LangChain4j Web Search Engine

[LLM Integration Guide](ai-llm-integration-guide.md)

[Milvus](milvus-component.md)

Perform operations on the Milvus Vector Database.

[Neo4j](neo4j-component.md)

Perform operations on the Neo4j Graph Database

[OpenAI](openai-component.md)

OpenAI endpoint for chat completion, Responses API, embeddings, audio transcription, audio translation, and text-to-speech.

[PGVector](pgvector-component.md)

Perform operations on the PostgreSQL pgvector Vector Database.

[Pinecone](pinecone-component.md)

Perform operations on the Pinecone Vector Database.

[Qdrant](qdrant-component.md)

Perform operations on the Qdrant Vector Database.

[Spring AI Chat](spring-ai-chat-component.md)

Perform chat operations using Spring AI.

[Spring AI Embeddings](spring-ai-embeddings-component.md)

Spring AI Embeddings

[Spring AI Image](spring-ai-image-component.md)

Spring AI Image Generation

[Spring AI Vector Store](spring-ai-vector-store-component.md)

Spring AI Vector Store

[TensorFlow Serving](tensorflow-serving-component.md)

Provide access to TensorFlow Serving model servers to run inference with TensorFlow saved models remotely

[weaviate](weaviate-component.md)

Perform operations on the Weaviate Vector Database.