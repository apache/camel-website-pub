# ![google vertexai sink](_images/kamelets/google-vertexai-sink.svg) Google Vertex AI Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Sends each message as a prompt to a generative AI model in Google Vertex AI, such as Gemini, and replaces the body with the answer of the model.

Use it to summarize, classify, translate or answer questions about text as it flows, for example to summarize support tickets or extract the topic of an email.

Input: the body is the prompt, as text; bytes and streams are read as text. The optional `CamelGoogleVertexAIPrompt` header gives the prompt instead of the body.

Output: when it is used inside a route, the body afterwards is the answer of the model, as text, for the default `generateText` operation. The `CamelGoogleVertexAIFinishReason` header says why the model stopped, and the token counts are in the `CamelGoogleVertexAIPromptTokenCount`, `CamelGoogleVertexAICandidatesTokenCount` and `CamelGoogleVertexAITotalTokenCount` headers.

## Configuration Options

The following table summarizes the configuration options available for the `google-vertexai-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **modelId** | Model ID | **Required** The ID of the model to use, as listed in the Model Garden of the Vertex AI console. | string |  | gemini-2.5-flash |
| **projectId** | Google Cloud Project ID | **Required** The ID of the Google Cloud project where Vertex AI is enabled, as shown in the Google Cloud console. It is the project ID, not the project name or number. | string |  | my-project-123 |
| **region** | Google Cloud Region | **Required** The Google Cloud region to call the model in, where the model is available. Vertex AI calls it the location. | string |  | us-central1 |
| **maxOutputTokens** | Max Output Tokens | The most tokens (pieces of words) the answer may have, a whole number. When it is not set, 1024 is used. | string |  | 2048 |
| **operation** | Operation | What to ask the model for. `generateText` (the default), `generateChat` and `generateCode` answer the prompt with text, `generateImage` gives a List of images, `generateEmbeddings` gives one vector of numbers per text, and `generateMultimodal` sends media together with the prompt. `rawPredict` fails, as it needs a publisher that this Kamelet cannot set. Enum values: \* generateText \* generateChat \* generateImage \* generateEmbeddings \* generateCode \* generateMultimodal \* rawPredict | string | generateText |  |
| **serviceAccountKey** | Service Account Key | Where to read the JSON key of a service account that may call Vertex AI, such as one with the Vertex AI User role: `file:` followed by the path of the key file, or `base64:` followed by the Base64 encoding of its content. Create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys. When it is not set, the Application Default Credentials are used: the key file named in the `GOOGLE_APPLICATION_CREDENTIALS` environment variable, or the service account of the Google Cloud machine it runs on. | binary |  |  |
| **temperature** | Temperature | How random the answer is, a number from 0.0 to 1.0, such as `0.2`. Lower values give more predictable answers. When it is not set, 0.7 is used. | string |  | 0.2 |
| **topK** | Top K | Only choose each next word among this many most likely ones, a whole number. When it is not set, 40 is used. | string |  | 40 |
| **topP** | Top P | Only choose each next word among the most likely ones whose probabilities add up to this number, from 0.0 to 1.0. When it is not set, 0.95 is used. | string |  | 0.95 |

## Dependencies

At runtime, the `google-vertexai-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:google-vertexai
    

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
            uri: "kamelet:google-vertexai-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Google Vertex AI Sink Kamelet Description

### Authentication

This Kamelet uses Google Cloud service account authentication. The service account key is optional - if not provided, the Kamelet will use Application Default Credentials (ADC).

If you provide a service account key, give its location: `file:` followed by the path of the JSON key file, or `base64:` followed by the Base64 encoding of its content. Ensure that the service account has the `aiplatform.endpoints.predict` permission (typically granted through the `Vertex AI User` role).

### Required Configuration

-   **Project ID**: The Google Cloud Project ID
    
-   **Region**: The Google Cloud region where Vertex AI models are available (e.g., `us-central1`), which Vertex AI calls the location
    
-   **Model ID**: The model identifier to use for predictions (e.g., `gemini-2.5-pro`)
    

### Optional Configuration

-   **Service Account Key**: The location of the service account key, as `file:<path>` or `base64:<Base64 of the key file>`
    
-   **Operation**: The operation to perform (default: `generateText`). Supported operations are `generateText`, `generateChat`, `generateImage`, `generateEmbeddings`, `generateCode`, `generateMultimodal`, and `rawPredict`
    
-   **Temperature**: Controls randomness in generation (0.0 to 1.0)
    
-   **Max Output Tokens**: Maximum number of tokens to generate in the response
    
-   **Top P**: Nucleus sampling parameter (0.0 to 1.0)
    
-   **Top K**: Only sample from the top K options for each subsequent token
    

### Content Generation

The Kamelet sends the message body as a prompt to the specified Google Vertex AI model and returns the generated content. It supports Google native models, such as Gemini and Imagen. The `rawPredict` operation for partner models needs a publisher, which this Kamelet cannot set, so it fails.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-vertexai-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-vertexai-sink.kamelet.yaml)