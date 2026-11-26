# ![openai chat action](_images/kamelets/openai-chat-action.svg) OpenAI Chat Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Sends each message as a question to a chat model of OpenAI, or of any server with the same API such as Ollama, vLLM or LM Studio, and gives back the answer.

Use it to summarize, classify, translate or answer questions about text as it flows, for example to sort support emails by topic or to pull the fields out of an order. Set `jsonSchema` to get the answer as JSON that has the fields you ask for. For a model in Amazon Bedrock or Google Vertex AI, use `aws-bedrock-text-sink` or `google-vertexai-sink`.

Input: the body is the user message, as text; bytes and streams are read as text, whatever their Content-Type.

Output: the body is the answer of the model, as text. With `jsonSchema`, it is the JSON text of the answer. The `CamelOpenAIFinishReason` header says why the model stopped, such as `stop` or `length`, `CamelOpenAIResponseModel` and `CamelOpenAIResponseId` are the model and the id the server gives for the answer, and the token counts are in the `CamelOpenAIPromptTokens`, `CamelOpenAICompletionTokens` and `CamelOpenAITotalTokens` headers.

Good to know: each message is one question on its own: the Kamelet keeps no history of the conversation, and the model cannot call tools, so the text of a message cannot make it act. Headers that start with `CamelOpenAI` are removed from the message first, so a message cannot change the model, the system message or the request. An error answer from the server fails the message with an error of the package `com.openai.errors`, such as `UnauthorizedException` for a wrong API key (status 401) or `InternalServerException` for a status 5xx. A request that gets the status 408, 409, 429 or 5xx is first sent again, `maxRetries` times.

## Configuration Options

The following table summarizes the configuration options available for the `openai-chat-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **model** | Model | **Required** The name of the model to ask, as the server names it. | string |  | gpt-4.1-mini |
| **apiKey** | API Key | The API key to send to the server, as a Bearer token. Create it in the OpenAI platform under API keys. When it is not set, the `OPENAI_API_KEY` environment variable is used. With neither, requests are sent without a key, which suits a local server that checks none, such as Ollama, while OpenAI answers them with the status 401. | string |  |  |
| **baseUrl** | Base URL | The URL of the API of the server, up to and without `/chat/completions`. For a local server, such as `[http://localhost:11434/v1](http://localhost:11434/v1)` for Ollama. | string | [https://api.openai.com/v1](https://api.openai.com/v1) | http://localhost:11434/v1 |
| **jsonSchema** | JSON Schema | The JSON schema of the answer: JSON text, or `resource:file:` followed by the path of a file that holds it. The model is asked to answer with JSON that follows it (the `response_format` of the request), and the body afterwards is that JSON as text. The answer is not checked against the schema. The model and the server must support structured outputs. In a route, two closing braces next to each other are read as the end of a placeholder: write them with a space in between, as `} }`, or use a file. | string |  | resource:file:/etc/camel/ticket-schema.json |
| **jsonSchemaStrict** | JSON Schema Strict | Whether the model must follow `jsonSchema` exactly (`strict` structured outputs), so the answer has all the fields of the schema and no others. OpenAI then only accepts a schema where each object lists all its properties in `required` and sets `additionalProperties` to false, and answers another with the status 400. Not all servers support it. | boolean | false |  |
| **maxRetries** | Max Retries | How many more times a request is sent when the server answers with the status 408, 409, 429 or 5xx, before the message fails. A `Retry-After` of the server is honoured. `0` sends each request once. | integer | 2 |  |
| **maxTokens** | Max Tokens | The most tokens (pieces of words) the answer may have, sent as `max_completion_tokens`. An answer that is cut off has the finish reason `length`. When it is not set, the server chooses. | integer |  | 500 |
| **stripThinking** | Strip Thinking | Whether to remove the `<think>…​</think>` block that reasoning models such as Qwen3 or DeepSeek-R1 put before their answer. The block is then in the `CamelOpenAIThinkingContent` header. | boolean | false |  |
| **systemMessage** | System Message | Instructions for the model, sent before each user message, such as the role it plays, the language or the length of the answer. | string |  | You sort support emails. Answer with one word: billing, technical or other. |
| **temperature** | Temperature | How random the answer is, from 0.0 to 2.0. Lower values give more focused and repeatable answers. When it is not set, the server chooses. | number |  | 0.2 |

## Dependencies

At runtime, the `openai-chat-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:openai
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:openai-chat-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/openai-chat-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/openai-chat-action.kamelet.yaml)