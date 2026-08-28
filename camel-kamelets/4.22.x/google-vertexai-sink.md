# ![google vertexai sink](_images/kamelets/google-vertexai-sink.svg) Google Vertex AI Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Send data to Google Vertex AI for generating content with generative AI models.

## Configuration Options

The following table summarizes the configuration options available for the `google-vertexai-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **location** | Google Cloud Location | **Required** The Google Cloud region (e.g., us-central1). | string |  |  |
| **modelId** | Model Id | **Required** The Model ID to use for predictions (e.g., gemini-2.5-pro). | string |  |  |
| **projectId** | Google Cloud Project Id | **Required** The Google Cloud Project ID. | string |  |  |
| **maxOutputTokens** | Max Output Tokens | Maximum number of tokens to generate in the response. | string |  |  |
| **operation** | Operation | The operation to perform. Enum values: \* generateText \* generateChat \* generateImage \* generateEmbeddings \* generateCode \* generateMultimodal \* rawPredict | string | generateText |  |
| **serviceAccountKey** | Service Account Key | The service account key to use as credentials for the Vertex AI client. You must encode this value in base64. | binary |  |  |
| **temperature** | Temperature | Controls randomness in generation. Lower values make output more deterministic. Range 0.0 to 1.0. | string |  |  |
| **topK** | Top K | Only sample from the top K options for each subsequent token. | string |  |  |
| **topP** | Top P | Nucleus sampling parameter. Considers tokens with top\_p probability mass. Range 0.0 to 1.0. | string |  |  |

## Dependencies

At runtime, the `google-vertexai-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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

If you provide a service account key, it must be base64-encoded. Ensure that the service account has the `aiplatform.endpoints.predict` permission (typically granted through the `Vertex AI User` role).

### Required Configuration

-   **Project ID**: The Google Cloud Project ID
    
-   **Location**: The Google Cloud region where Vertex AI models are available (e.g., `us-central1`)
    
-   **Model ID**: The model identifier to use for predictions (e.g., `gemini-2.5-pro`)
    

### Optional Configuration

-   **Service Account Key**: Base64-encoded service account credentials
    
-   **Operation**: The operation to perform (default: `generateText`). Supported operations are `generateText`, `generateChat`, `generateImage`, `generateEmbeddings`, `generateCode`, `generateMultimodal`, and `rawPredict`
    
-   **Temperature**: Controls randomness in generation (0.0 to 1.0)
    
-   **Max Output Tokens**: Maximum number of tokens to generate in the response
    
-   **Top P**: Nucleus sampling parameter (0.0 to 1.0)
    
-   **Top K**: Only sample from the top K options for each subsequent token
    

### Content Generation

The Kamelet sends the message body as a prompt to the specified Google Vertex AI model and returns the generated content. It supports Google native models (Gemini, Imagen) as well as partner models (Claude, Llama, Mistral) through the `rawPredict` operation.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-vertexai-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-vertexai-sink.kamelet.yaml)