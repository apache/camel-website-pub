# Hugging Face

**Since Camel 4.19**

**Only producer is supported**

The **Hugging Face** (HF) component provides an opinionated integration with Hugging Face models for various AI tasks, such as text classification, generation, and audio processing. It uses [Deep Java Library](https://djl.ai/)'s Python engine to run Hugging Face’s Transformers library in a Python subprocess, allowing easy access to HF pipelines. The Python environment needs to be setup before using the component.

This component is made to allow users to hit the ground running with HF models. If high-throughput/low-latency or the Python subprocess is an issue, users are encouraged to use the **camel-djl** for a more Java native approach.

To use the HF component, Maven users will need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-huggingface</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

huggingface:task?modelId=model

Where _model_ is the model name hosted on Hugging Face and _task_ is one of the supported HF task listed below. For example, to use the [Qwen2.5-3B-Instruct](https://huggingface.co/Qwen/Qwen2.5-3B-Instruct) model with the _chat_ task:

Object detection

```java
from("direct:start-chat")
    .to("huggingface:chat?modelId=Qwen/Qwen2.5-3B-Instruct");
```

### Supported Tasks

The component supports the following tasks:

    
| Task | Input Type | Output Type | Options | Models |
| --- | --- | --- | --- | --- |
| text-classification | String (text to classify) | _ai.djl.modality.Classifications_ | revision, device | Classification-tuned models (e.g., distilbert-base-uncased-finetuned-sst-2-english for sentiment, roberta-large for multi-label) |
| text-generation | String (prompt) | String (generated text) | revision, device, maxTokens, temperature | Generative models (e.g., gpt2 for completion, mistralai/Mistral-7B-Instruct-v0.2 for instruct-tuned generation) |
| question-answering | QAInput | String (extracted answer) | revision, device | QA-tuned models (e.g., distilbert-base-cased-distilled-squad for extractive QA, deepset/roberta-base-squad2 for robust Q&A) |
| summarization | String (text to summarize) | String (summary text) | revision, device, minLength, maxTokens, temperature | Summarization-tuned models (e.g., facebook/bart-large-cnn for abstractive summarization, t5-small for translation-like summarization) |
| zero-shot-classification | String\[\] or List<String> \[text, label1, label2, …​\] | String (best label) | revision, device, multiLabel, autoSelect | NLI-based zero-shot models (e.g., facebook/bart-large-mnli for general zero-shot, joeddav/deberta-v3-large-zeroshot-v1 for multi-label) |
| sentence-embeddings | String\[\], List<String> or String (sentences to embed) | float\[\]\[\] (2D embedding tensor: batch × dimension) | revision, device | Embedding-tuned models (e.g., sentence-transformers/all-MiniLM-L6-v2) |
| text-to-image | String (prompt) | byte\[\] (PNG image bytes) | revision, device | Diffusion-based generation models (e.g., CompVis/stable-diffusion-v1-4 for general images, runwayml/stable-diffusion-v1-5 for improved quality) |
| automatic-speech-recognition | Audio or byte\[\] (audio bytes) | String (transcribed text) | revision, device | ASR-tuned models (e.g., facebook/wav2vec2-base-960h) |
| text-to-speech | String (text prompt) | _ai.djl.modality.audio_ | revision, device | TTS-tuned models (e.g., facebook/mms-tts-eng for English TTS, microsoft/speecht5\_tts for multi-speaker) |
| chat | String (user message) | String (LLM response) | revision, device, maxTokens, temperature, systemPrompt, userRole, memoryIdHeader | Instruct-tuned/chat models (e.g., mistralai/Mistral-7B-Instruct-v0.2 for conversational, microsoft/Phi-3-mini-4k-instruct for efficient chat) |
| custom | TBD | TBD | predictorBean (required), revision, device | Any HF model compatible with the custom predictor bean (e.g., Helsinki-NLP/opus-mt-en-fr for translation, distilgpt2 for custom generation) |

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

The Hugging Face component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **authToken** (producer) | HF API token for private models. |  | String |
| **autoSelect** (producer) | If true, auto-select the best label (highest score) for zero-shot classification. | true | boolean |
| **configuration** (producer) | The configuration. |  | HuggingFaceConfiguration |
| **device** (producer) | Device for inference (cpu, gpu, auto). |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxTokens** (producer) | Max tokens for generation tasks. |  | int |
| **memoryIdHeader** (producer) | Header name for conversation memory ID (for multi-user chats). | CamelChatMemoryId | String |
| **minLength** (producer) | Min tokens for summarization tasks. |  | int |
| **modelId** (producer) | **Required** Hugging Face model ID (e.g., distilbert-base-uncased-finetuned-sst-2-english). |  | String |
| **modelLoadingTimeout** (producer) | Model loading timeout in seconds, if negative then use default (240 seconds). |  | int |
| **multiLabel** (producer) | Allow multi-label classifications for zero-shot tasks. | false | boolean |
| **pooling** (producer) | Whether to pool the predictor (keep the Python process alive) or create a new one for each request. | true | boolean |
| **predictorBean** (producer) | Bean name of a custom TaskPredictor implementation (for tasks not covered by built-in predictors). |  | String |
| **predictTimeout** (producer) | Predict timeout in seconds, if negative then use default (120 seconds). |  | int |
| **revision** (producer) | Model revision or branch (default: main). |  | String |
| **systemPrompt** (producer) | Initial system prompt for chat tasks (e.g., 'You are a helpful assistant named Alan.'). |  | String |
| **temperature** (producer) | Temperature for sampling (0.0-1.0). |  | float |
| **topK** (producer) | Top-k parameter for classification tasks. | 5 | int |
| **userRole** (producer) | Role for user messages in chat history (e.g., 'user' or 'human'). | user | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used as authToken. Requires camel-oauth on the classpath. |  | String |

## Endpoint Options

The Hugging Face endpoint is configured using URI syntax:

huggingface:task

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **task** (producer) | 
**Required** The Hugging Face task to perform (e.g., TEXT\_CLASSIFICATION).

Enum values:

-   TEXT\_CLASSIFICATION
    
-   TEXT\_GENERATION
    
-   QUESTION\_ANSWERING
    
-   SUMMARIZATION
    
-   ZERO\_SHOT\_CLASSIFICATION
    
-   SENTENCE\_EMBEDDINGS
    
-   TEXT\_TO\_IMAGE
    
-   AUTOMATIC\_SPEECH\_RECOGNITION
    
-   TEXT\_TO\_SPEECH
    
-   CHAT
    





 |  | HuggingFaceTask |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **authToken** (producer) | HF API token for private models. |  | String |
| **autoSelect** (producer) | If true, auto-select the best label (highest score) for zero-shot classification. | true | boolean |
| **device** (producer) | Device for inference (cpu, gpu, auto). |  | String |
| **maxTokens** (producer) | Max tokens for generation tasks. |  | int |
| **memoryIdHeader** (producer) | Header name for conversation memory ID (for multi-user chats). | CamelChatMemoryId | String |
| **minLength** (producer) | Min tokens for summarization tasks. |  | int |
| **modelId** (producer) | **Required** Hugging Face model ID (e.g., distilbert-base-uncased-finetuned-sst-2-english). |  | String |
| **modelLoadingTimeout** (producer) | Model loading timeout in seconds, if negative then use default (240 seconds). |  | int |
| **multiLabel** (producer) | Allow multi-label classifications for zero-shot tasks. | false | boolean |
| **pooling** (producer) | Whether to pool the predictor (keep the Python process alive) or create a new one for each request. | true | boolean |
| **predictorBean** (producer) | Bean name of a custom TaskPredictor implementation (for tasks not covered by built-in predictors). |  | String |
| **predictTimeout** (producer) | Predict timeout in seconds, if negative then use default (120 seconds). |  | int |
| **revision** (producer) | Model revision or branch (default: main). |  | String |
| **systemPrompt** (producer) | Initial system prompt for chat tasks (e.g., 'You are a helpful assistant named Alan.'). |  | String |
| **temperature** (producer) | Temperature for sampling (0.0-1.0). |  | float |
| **topK** (producer) | Top-k parameter for classification tasks. | 5 | int |
| **userRole** (producer) | Role for user messages in chat history (e.g., 'user' or 'human'). | user | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used as authToken. Requires camel-oauth on the classpath. |  | String |

## Message Headers

The Hugging Face component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHuggingFaceOutput** (producer) Constant: [`OUTPUT`](https://javadoc.io/doc/org.apache.camel/camel-huggingface/latest/org/apache/camel/component/huggingface/HuggingFaceConstants.html#OUTPUT) | The output from the model. |  | String |

## OAuth Authentication

When accessing private or gated models behind an OAuth-protected endpoint, set the `oauthProfile` parameter to acquire an access token via the OAuth 2.0 Client Credentials grant. The token is used as the `authToken`. This requires `camel-oauth` on the classpath.

```properties
camel.oauth.hf.client-id=my-client
camel.oauth.hf.client-secret=my-secret
camel.oauth.hf.token-endpoint=https://idp.example.com/token
```

```java
from("direct:chat")
    .to("huggingface:chat?modelId=mistralai/Mistral-7B-Instruct-v0.2&oauthProfile=hf");
```

## Examples

Classify sentiment of text:

```java
from("direct:start")
    .to("huggingface:text-classification?modelId=modelId=cardiffnlp/twitter-roberta-base-sentiment-latest&topK=2")
    .to("log:result");
```

```cmd
Input : "I love this movie!"
Output : DJL Classifications [{"className" : "positive","probability" : 0.9847}, {"className" : "neutral", "probability" : 0.01182}]
```

Chat Example

Simple chat route with automatic history:

```java
from("direct:start-chat")
    .to("huggingface:chat?modelId=mistralai/Mistral-7B-Instruct-v0.2&systemPrompt=You are a helpful assistant&maxTokens=100&temperature=0.7")
    .to("log:response");
```

Send multiple messages to "direct:start-chat" — history is maintained automatically.

Custom Task

For a custom task (e.g., _translation_): Define a custom predictor bean in your application or test:

```java
public class TranslationPredictor extends AbstractTaskPredictor {
    // Implement
}

@Bean
public TranslationPredictor myCustomPredictor() {
    return new TranslationPredictor();
}
```

Route:

```java
from("direct:start-custom")
    .to("huggingface:custom?modelId=Helsinki-NLP/opus-mt-en-fr&predictorBean=myCustomPredictor")
    .to("log:translated");
```

This allows extending the component for most HF tasks.

When using a large model for the first time, downloading can take some time so make sure to set the _modelLoadingTimeout_ option (in seconds, default is 240).

When performing a computationally expensive task, make sure to set the _predictTimeout_ option (in seconds, default is 120).

For more examples, see the tests in the source code. For questions or contributions, checkout the Apache Camel community.