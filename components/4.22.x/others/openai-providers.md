# OpenAI - Compatible Providers

[Back to OpenAI Component](../openai-component.md)

## OpenAI-Compatible Providers

Because the component speaks the OpenAI API, you do not need a separate component to use third-party gateways or local model servers that expose an OpenAI-compatible API. Point `baseUrl` at the provider, set `apiKey` if it requires one, and use the same operations and options as with OpenAI.

> **Note**
> Ensure the provider supports the chat completions and/or embeddings endpoint format you use. Authentication requirements and minor API variations differ between providers.

  
| Provider | `baseUrl` | Notes |
| --- | --- | --- |
| OpenAI | `[https://api.openai.com/v1](https://api.openai.com/v1)` | Default; `baseUrl` can be omitted |
| OpenRouter | `[https://openrouter.ai/api/v1](https://openrouter.ai/api/v1)` | Multi-model gateway with provider routing and fallbacks |
| Ollama | `[http://localhost:11434/v1](http://localhost:11434/v1)` | Local LLM server |
| LM Studio | `[http://localhost:1234/v1](http://localhost:1234/v1)` | Local model runner |
| vLLM | `[http://localhost:8000/v1](http://localhost:8000/v1)` | High-throughput, self-hosted serving engine |

### Ollama (local)

[Ollama](https://ollama.com) runs models locally and does not require an API key. Install Ollama and pull the model used in the example below:

```bash
ollama run llama3.2
```

-   Java
    
-   YAML
    

```java
from("direct:chat")
    .setBody(constant("What is Apache Camel?"))
    .to("openai:chat-completion?baseUrl=http://localhost:11434/v1&model=llama3.2");
```

```yaml
- to:
    uri: openai:chat-completion
    parameters:
      baseUrl: http://localhost:11434/v1
      model: llama3.2
      userMessage: What is Apache Camel?
```

For local embeddings, use an embedding model such as `nomic-embed-text` (see the **Embedding Models by Provider** table below).

### LM Studio (local)

[LM Studio](https://lmstudio.ai) serves the model currently loaded in the app. Set `model` to the identifier shown in its UI.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?baseUrl=http://localhost:1234/v1&model=local-model");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="openai:chat-completion?baseUrl=http://localhost:1234/v1&amp;model=local-model"/>
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
              baseUrl: http://localhost:1234/v1
              model: local-model
```

### vLLM (self-hosted)

[vLLM](https://docs.vllm.ai) is a high-throughput LLM serving engine. Install it with `pip install vllm` and start the model used in the example below:

```bash
vllm serve meta-llama/Llama-3.1-8B-Instruct --port 8000
```

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?baseUrl=http://localhost:8000/v1"
        + "&model=meta-llama/Llama-3.1-8B-Instruct");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="openai:chat-completion?baseUrl=http://localhost:8000/v1&amp;model=meta-llama/Llama-3.1-8B-Instruct"/>
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
              baseUrl: http://localhost:8000/v1
              model: meta-llama/Llama-3.1-8B-Instruct
```

If vLLM was started with `--api-key`, pass the same value via the `apiKey` option.

On Apple Silicon, the `vllm-mlx` variant uses Apple’s MLX framework and runs the same way:

```bash
vllm-mlx serve mlx-community/Qwen2.5-7B-Instruct-4bit --port 8000
```

### OpenRouter

[OpenRouter](https://openrouter.ai) is an OpenAI-compatible gateway that routes requests across many model providers. Set `baseUrl` to its endpoint and select a model with a cross-provider identifier:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:chat")
    .to("openai:chat-completion?baseUrl=https://openrouter.ai/api/v1"
        + "&apiKey={{openrouter.api.key}}"
        + "&model=anthropic/claude-sonnet-4-20250514");
```

```xml
<route>
  <from uri="direct:chat"/>
  <to uri="openai:chat-completion?baseUrl=https://openrouter.ai/api/v1&amp;apiKey={{openrouter.api.key}}&amp;model=anthropic/claude-sonnet-4-20250514"/>
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
              baseUrl: https://openrouter.ai/api/v1
              apiKey: "{{openrouter.api.key}}"
              model: anthropic/claude-sonnet-4-20250514
```

#### Provider Routing

OpenRouter accepts a `provider` object in the request body to control routing order and fallbacks. Pass it through the `additionalBodyProperty` option as a JSON value — the component parses JSON-valued properties and adds them to the request body:

```yaml
- to:
    uri: openai:chat-completion
    parameters:
      baseUrl: https://openrouter.ai/api/v1
      apiKey: "{{openrouter.api.key}}"
      model: anthropic/claude-sonnet-4-20250514
      additionalBodyProperty.provider: '{"order":["anthropic","google"],"allow_fallbacks":false}'
```

> **Note**
> OpenRouter’s optional attribution headers (`HTTP-Referer` and `X-Title`, which identify your app on the OpenRouter rankings) are sent as HTTP request headers, not body properties. The component does not currently expose a way to set custom HTTP request headers, so they cannot be configured today. They are optional and do not affect chat completions.

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