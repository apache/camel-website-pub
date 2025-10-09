# camel harden

Suggest security hardening for Camel routes using AI/LLM

## Usage

```bash
camel harden [options]
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
| `--verbose,-v` | Include detailed security recommendations with code examples |  | boolean |
| `-h,--help` | Display the help and sub-commands |  | boolean |

## Examples

The `camel harden` command uses AI/LLM to analyze Camel routes and provide security hardening recommendations. It supports multiple LLM providers including Ollama (local), OpenAI, Azure OpenAI, vLLM, LM Studio, and LocalAI.

### Prerequisites

Start Ollama locally using Camel infra:

```bash
camel infra run ollama
```

### Basic Usage

Analyze a YAML route for security issues:

```bash
camel harden my-route.yaml
```

Analyze a Java route:

```bash
camel harden OrderRoute.java
```

Analyze multiple route files:

```bash
camel harden route1.yaml route2.xml MyRoute.java
```

### Security Analysis Focus

The harden command analyzes routes for these security concerns:

-   **Authentication & Authorization** - Missing or weak authentication, credential exposure
    
-   **Encryption & Data Protection** - TLS/SSL configuration, data in transit security
    
-   **Secrets Management** - Hardcoded credentials, vault integration recommendations
    
-   **Input Validation & Injection Prevention** - SQL, command, and path traversal vulnerabilities
    
-   **Secure Component Configuration** - Insecure defaults, missing security headers
    
-   **Logging & Monitoring** - Sensitive data in logs, audit trail recommendations
    

### Output Options

Use verbose mode for detailed recommendations with code examples:

```bash
camel harden my-route.yaml --verbose
```

Output as Markdown for documentation:

```bash
camel harden my-route.yaml --format=markdown
```

### Prompt Options

Include Camel Catalog descriptions for component-specific security advice:

```bash
camel harden my-route.yaml --catalog-context
```

Show the prompt sent to the LLM (useful for debugging):

```bash
camel harden my-route.yaml --show-prompt
```

Use a custom system prompt:

```bash
camel harden my-route.yaml --system-prompt="Focus on OWASP Top 10 vulnerabilities."
```

### LLM Configuration

Use OpenAI or compatible services:

```bash
camel harden my-route.yaml --url=https://api.openai.com --api-type=openai --api-key=sk-...
```

Use environment variables for the API key:

```bash
export OPENAI_API_KEY=sk-...
camel harden my-route.yaml --url=https://api.openai.com --api-type=openai
```

Use a specific model:

```bash
camel harden my-route.yaml --model=llama3.1:70b
```

### Advanced Options

Disable streaming (wait for complete response):

```bash
camel harden my-route.yaml --stream=false
```

Adjust temperature (0.0 = deterministic, 2.0 = creative):

```bash
camel harden my-route.yaml --temperature=0.3
```

Set a custom timeout (in seconds):

```bash
camel harden my-route.yaml --timeout=300
```

### Security Findings Severity Levels

The harden command categorizes findings by severity:

-   **Critical** - Immediate security risks (command injection, hardcoded credentials, disabled TLS)
    
-   **High** - Significant security concerns (HTTP instead of HTTPS, SQL injection risk, plain FTP)
    
-   **Medium** - Moderate security issues (missing authentication hints, path validation concerns)
    
-   **Low** - Minor security improvements (missing optional security headers)
    

### Example Workflow

A typical security review workflow:

```bash
# 1. First, understand what the route does
camel explain my-route.yaml

# 2. Perform security analysis
camel harden my-route.yaml

# 3. Get detailed recommendations with code examples
camel harden my-route.yaml --verbose --format=markdown

# 4. Full analysis with catalog context
camel harden my-route.yaml --catalog-context --verbose
```