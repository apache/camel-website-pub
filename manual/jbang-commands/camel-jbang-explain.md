# camel explain

Explain what a Camel route does using AI/LLM

## Usage

```bash
camel explain [options]
```

## Options

   
| Option | Description | Default | Type |
| --- | --- | --- | --- |
| `--api-key` | API key for authentication. Also reads OPENAI\_API\_KEY or LLM\_API\_KEY env vars |  | String |
| `--api-type` | API type: 'ollama' or 'openai' (OpenAI-compatible) | ollama | ApiType |
| `--catalog-context` | Include Camel Catalog descriptions in the prompt |  | boolean |
| `--format` | Output format (text, markdown) | text | String |
| `--model` | Model to use | DEFAULT\_MODEL | String |
| `--show-prompt` | Show the prompt sent to the LLM |  | boolean |
| `--stream` | Stream the response as it’s generated (shows progress) | true | boolean |
| `--system-prompt` | Custom system prompt |  | String |
| `--temperature` | Temperature for response generation (0.0-2.0) | 0.7 | double |
| `--timeout` | Timeout in seconds for LLM response | 120 | int |
| `--url` | LLM API endpoint URL. Auto-detected from 'camel infra' for Ollama if not specified. |  | String |
| `--verbose,-v` | Include detailed technical information |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |

## Examples

The `camel explain` command uses AI/LLM to explain Camel routes in plain English. It supports multiple LLM providers including Ollama (local), OpenAI, Azure OpenAI, vLLM, LM Studio, and LocalAI.

### Prerequisites

Start Ollama locally using Camel infra:

```bash
camel infra run ollama
```

### Basic Usage

Explain a YAML route:

```bash
camel explain my-route.yaml
```

Explain a Java route:

```bash
camel explain OrderRoute.java
```

Explain multiple route files:

```bash
camel explain route1.yaml route2.xml MyRoute.java
```

### Output Options

Use verbose mode for detailed technical information:

```bash
camel explain my-route.yaml --verbose
```

Output as Markdown for documentation:

```bash
camel explain my-route.yaml --format=markdown
```

### Prompt Options

Include Camel Catalog descriptions for more accurate explanations:

```bash
camel explain my-route.yaml --catalog-context
```

Show the prompt sent to the LLM (useful for debugging):

```bash
camel explain my-route.yaml --show-prompt
```

Use a custom system prompt:

```bash
camel explain my-route.yaml --system-prompt="Focus on error handling and security aspects."
```

### LLM Configuration

Use OpenAI or compatible services:

```bash
camel explain my-route.yaml --url=https://api.openai.com --api-type=openai --api-key=sk-...
```

Use environment variables for the API key:

```bash
export OPENAI_API_KEY=sk-...
camel explain my-route.yaml --url=https://api.openai.com --api-type=openai
```

Use a specific model:

```bash
camel explain my-route.yaml --model=llama3.1:70b
```

### Advanced Options

Disable streaming (wait for complete response):

```bash
camel explain my-route.yaml --stream=false
```

Adjust temperature (0.0 = deterministic, 2.0 = creative):

```bash
camel explain my-route.yaml --temperature=0.3
```

Set a custom timeout (in seconds):

```bash
camel explain my-route.yaml --timeout=300
```