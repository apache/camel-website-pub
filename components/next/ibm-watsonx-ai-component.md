# IBM watsonx.ai

**Since Camel 4.18**

**Only producer is supported**

The IBM watsonx.ai component allows you to interact with IBM watsonx.ai foundation models for text generation, chat, embeddings, reranking, content detection (PII/HAP), document processing, and other AI capabilities using the [IBM watsonx.ai API](https://cloud.ibm.com/apidocs/watsonx-ai).

This component is built on top of the [IBM watsonx.ai Java SDK](https://github.com/IBM/watsonx-ai-java-sdk).

## Prerequisites

You must have a valid IBM Cloud account with access to watsonx.ai services. More information is available at [IBM watsonx.ai](https://www.ibm.com/products/watsonx-ai).

To use this component, you need:

1.  An IBM Cloud account
    
2.  Access to watsonx.ai services
    
3.  An API key from IBM Cloud IAM
    
4.  A project ID or deployment space ID
    
5.  (optional) IBM Content Object Storage connection to watsonx
    

## URI Format

ibm-watsonx-ai:label\[?options\]

You can append query options to the URI in the following format:

`?option=value&option2=value&…​`

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

The IBM watsonx.ai component supports 35 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **baseUrl** (common) | **Required** The watsonx.ai base URL (e.g., [https://us-south.ml.cloud.ibm.com](https://us-south.ml.cloud.ibm.com)). |  | String |
| **configuration** (producer) | The component configuration. |  | WatsonxAiConfiguration |
| **projectId** (common) | IBM Cloud project ID. |  | String |
| **spaceId** (common) | IBM Cloud deployment space ID (alternative to projectId). |  | String |
| **wxUrl** (common) | The watsonx.ai WX platform URL for tool operations (e.g., [https://api.dataplatform.cloud.ibm.com/wx](https://api.dataplatform.cloud.ibm.com/wx)). |  | String |
| **cosUrl** (producer) | Cloud Object Storage URL. |  | String |
| **deploymentId** (producer) | Deployed model ID (for deployment operations). |  | String |
| **detectHap** (producer) | Whether to detect HAP (Harmful, Abusive, Profane content). | false | Boolean |
| **detectionThreshold** (producer) | Detection threshold (0.0 to 1.0). |  | Double |
| **detectPii** (producer) | Whether to detect PII (Personal Identifiable Information). | false | Boolean |
| **documentBucket** (producer) | COS bucket for document storage. |  | String |
| **documentConnectionId** (producer) | COS connection ID for document storage. |  | String |
| **frequencyPenalty** (producer) | Frequency penalty for chat. |  | Double |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxCompletionTokens** (producer) | Maximum completion tokens for chat. |  | Integer |
| **maxNewTokens** (producer) | Maximum new tokens to generate. |  | Integer |
| **modelId** (producer) | Foundation model ID (e.g., ibm/granite-13b-instruct-v2). |  | String |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   textGeneration
    
-   textGenerationStreaming
    
-   chat
    
-   chatStreaming
    
-   embedding
    
-   rerank
    
-   tokenize
    
-   textExtraction
    
-   textExtractionFetch
    
-   textExtractionUpload
    
-   textExtractionUploadAndFetch
    
-   textExtractionUploadFile
    
-   textExtractionReadFile
    
-   textExtractionDeleteFile
    
-   textExtractionDeleteRequest
    
-   textClassification
    
-   textClassificationFetch
    
-   textClassificationUpload
    
-   textClassificationUploadAndFetch
    
-   textClassificationUploadFile
    
-   textClassificationDeleteFile
    
-   textClassificationDeleteRequest
    
-   detect
    
-   forecast
    
-   listModels
    
-   listTasks
    
-   deploymentInfo
    
-   deploymentGenerate
    
-   deploymentChat
    
-   deploymentForecast
    
-   runTool
    
-   listTools
    
-   processToolCalls
    





 |  | WatsonxAiOperations |
| **presencePenalty** (producer) | Presence penalty for chat. |  | Double |
| **repetitionPenalty** (producer) | Repetition penalty. |  | Double |
| **rerankTopN** (producer) | Number of top results to return for reranking. |  | Integer |
| **resultBucket** (producer) | COS bucket for result storage. |  | String |
| **resultConnectionId** (producer) | COS connection ID for result storage. |  | String |
| **returnDocuments** (producer) | Whether to return documents in rerank response. | false | Boolean |
| **temperature** (producer) | Temperature for randomness (0.0 to 2.0). |  | Double |
| **topK** (producer) | Top K (top-k sampling). |  | Integer |
| **topP** (producer) | Top P (nucleus sampling). |  | Double |
| **truncateInputTokens** (producer) | Maximum number of tokens accepted per input for embeddings. Truncates from the end if exceeded. |  | Integer |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **logRequests** (advanced) | Whether to log HTTP requests to the watsonx.ai API. | false | Boolean |
| **logResponses** (advanced) | Whether to log HTTP responses from the watsonx.ai API. | false | Boolean |
| **timeout** (advanced) | Request timeout in milliseconds. |  | Long |
| **verifySsl** (advanced) | Whether to verify SSL certificates. | true | Boolean |
| **apiKey** (security) | **Required** IBM Cloud API key for authentication. |  | String |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used as apiKey. Requires camel-oauth on the classpath. |  | String |

## Endpoint Options

The IBM watsonx.ai endpoint is configured using URI syntax:

ibm-watsonx-ai:label

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name for the endpoint. |  | String |

### Query Parameters (33 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **baseUrl** (common) | **Required** The watsonx.ai base URL (e.g., [https://us-south.ml.cloud.ibm.com](https://us-south.ml.cloud.ibm.com)). |  | String |
| **projectId** (common) | IBM Cloud project ID. |  | String |
| **spaceId** (common) | IBM Cloud deployment space ID (alternative to projectId). |  | String |
| **wxUrl** (common) | The watsonx.ai WX platform URL for tool operations (e.g., [https://api.dataplatform.cloud.ibm.com/wx](https://api.dataplatform.cloud.ibm.com/wx)). |  | String |
| **cosUrl** (producer) | Cloud Object Storage URL. |  | String |
| **deploymentId** (producer) | Deployed model ID (for deployment operations). |  | String |
| **detectHap** (producer) | Whether to detect HAP (Harmful, Abusive, Profane content). | false | Boolean |
| **detectionThreshold** (producer) | Detection threshold (0.0 to 1.0). |  | Double |
| **detectPii** (producer) | Whether to detect PII (Personal Identifiable Information). | false | Boolean |
| **documentBucket** (producer) | COS bucket for document storage. |  | String |
| **documentConnectionId** (producer) | COS connection ID for document storage. |  | String |
| **frequencyPenalty** (producer) | Frequency penalty for chat. |  | Double |
| **maxCompletionTokens** (producer) | Maximum completion tokens for chat. |  | Integer |
| **maxNewTokens** (producer) | Maximum new tokens to generate. |  | Integer |
| **modelId** (producer) | Foundation model ID (e.g., ibm/granite-13b-instruct-v2). |  | String |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   textGeneration
    
-   textGenerationStreaming
    
-   chat
    
-   chatStreaming
    
-   embedding
    
-   rerank
    
-   tokenize
    
-   textExtraction
    
-   textExtractionFetch
    
-   textExtractionUpload
    
-   textExtractionUploadAndFetch
    
-   textExtractionUploadFile
    
-   textExtractionReadFile
    
-   textExtractionDeleteFile
    
-   textExtractionDeleteRequest
    
-   textClassification
    
-   textClassificationFetch
    
-   textClassificationUpload
    
-   textClassificationUploadAndFetch
    
-   textClassificationUploadFile
    
-   textClassificationDeleteFile
    
-   textClassificationDeleteRequest
    
-   detect
    
-   forecast
    
-   listModels
    
-   listTasks
    
-   deploymentInfo
    
-   deploymentGenerate
    
-   deploymentChat
    
-   deploymentForecast
    
-   runTool
    
-   listTools
    
-   processToolCalls
    





 |  | WatsonxAiOperations |
| **presencePenalty** (producer) | Presence penalty for chat. |  | Double |
| **repetitionPenalty** (producer) | Repetition penalty. |  | Double |
| **rerankTopN** (producer) | Number of top results to return for reranking. |  | Integer |
| **resultBucket** (producer) | COS bucket for result storage. |  | String |
| **resultConnectionId** (producer) | COS connection ID for result storage. |  | String |
| **returnDocuments** (producer) | Whether to return documents in rerank response. | false | Boolean |
| **temperature** (producer) | Temperature for randomness (0.0 to 2.0). |  | Double |
| **topK** (producer) | Top K (top-k sampling). |  | Integer |
| **topP** (producer) | Top P (nucleus sampling). |  | Double |
| **truncateInputTokens** (producer) | Maximum number of tokens accepted per input for embeddings. Truncates from the end if exceeded. |  | Integer |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **logRequests** (advanced) | Whether to log HTTP requests to the watsonx.ai API. | false | Boolean |
| **logResponses** (advanced) | Whether to log HTTP responses from the watsonx.ai API. | false | Boolean |
| **timeout** (advanced) | Request timeout in milliseconds. |  | Long |
| **verifySsl** (advanced) | Whether to verify SSL certificates. | true | Boolean |
| **apiKey** (security) | **Required** IBM Cloud API key for authentication. |  | String |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used as apiKey. Requires camel-oauth on the classpath. |  | String |

## Message Headers

The IBM watsonx.ai component supports 65 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIBMWatsonxAiOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#OPERATION) | The operation to perform. |  | WatsonxAiOperations |
| **CamelIBMWatsonxAiInput** (producer) Constant: [`INPUT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#INPUT) | The input text/prompt for generation. |  | String |
| **CamelIBMWatsonxAiInputs** (producer) Constant: [`INPUTS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#INPUTS) | The list of inputs for batch operations. |  | List |
| **CamelIBMWatsonxAiGeneratedText** (producer) Constant: [`GENERATED_TEXT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#GENERATED_TEXT) | The generated text output. |  | String |
| **CamelIBMWatsonxAiModelId** (producer) Constant: [`MODEL_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#MODEL_ID) | The model ID to use. |  | String |
| **CamelIBMWatsonxAiDeploymentId** (producer) Constant: [`DEPLOYMENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#DEPLOYMENT_ID) | The deployment ID to use. |  | String |
| **CamelIBMWatsonxAiSpaceId** (producer) Constant: [`SPACE_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#SPACE_ID) | The space ID for deployment operations. |  | String |
| **CamelIBMWatsonxAiDeploymentName** (producer) Constant: [`DEPLOYMENT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#DEPLOYMENT_NAME) | The deployment name. |  | String |
| **CamelIBMWatsonxAiDeploymentAssetType** (producer) Constant: [`DEPLOYMENT_ASSET_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#DEPLOYMENT_ASSET_TYPE) | The deployed asset type. |  | String |
| **CamelIBMWatsonxAiDeploymentStatus** (producer) Constant: [`DEPLOYMENT_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#DEPLOYMENT_STATUS) | The deployment status state. |  | String |
| **CamelIBMWatsonxAiTemperature** (producer) Constant: [`TEMPERATURE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TEMPERATURE) | Temperature for randomness (0.0 to 2.0). |  | Double |
| **CamelIBMWatsonxAiMaxNewTokens** (producer) Constant: [`MAX_NEW_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#MAX_NEW_TOKENS) | Maximum new tokens to generate. |  | Integer |
| **CamelIBMWatsonxAiTopP** (producer) Constant: [`TOP_P`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOP_P) | Top P (nucleus sampling). |  | Double |
| **CamelIBMWatsonxAiTopK** (producer) Constant: [`TOP_K`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOP_K) | Top K (top-k sampling). |  | Integer |
| **CamelIBMWatsonxAiRepetitionPenalty** (producer) Constant: [`REPETITION_PENALTY`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#REPETITION_PENALTY) | Repetition penalty. |  | Double |
| **CamelIBMWatsonxAiMessages** (producer) Constant: [`MESSAGES`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#MESSAGES) | The chat messages. |  | List |
| **CamelIBMWatsonxAiSystemMessage** (producer) Constant: [`SYSTEM_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#SYSTEM_MESSAGE) | The system message for chat (used to build messages if MESSAGES header is not set). |  | String |
| **CamelIBMWatsonxAiUserMessage** (producer) Constant: [`USER_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#USER_MESSAGE) | The user message for chat (used to build messages if MESSAGES header is not set, alternative to body). |  | String |
| **CamelIBMWatsonxAiTools** (producer) Constant: [`TOOLS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOOLS) | The tools available for function calling. |  | List |
| **CamelIBMWatsonxAiToolChoice** (producer) Constant: [`TOOL_CHOICE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOOL_CHOICE) | Tool choice option (auto, required, none). |  | String |
| **CamelIBMWatsonxAiEmbeddings** (producer) Constant: [`EMBEDDINGS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#EMBEDDINGS) | The embedding vectors result. |  | List |
| **CamelIBMWatsonxAiRerankQuery** (producer) Constant: [`RERANK_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#RERANK_QUERY) | The query for reranking. |  | String |
| **CamelIBMWatsonxAiRerankTopN** (producer) Constant: [`RERANK_TOP_N`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#RERANK_TOP_N) | Number of top results to return for reranking. |  | Integer |
| **CamelIBMWatsonxAiTokenCount** (producer) Constant: [`TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOKEN_COUNT) | The token count. |  | Integer |
| **CamelIBMWatsonxAiTokens** (producer) Constant: [`TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOKENS) | The token IDs. |  | List |
| **CamelIBMWatsonxAiFile** (producer) Constant: [`FILE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FILE) | The file to upload. |  | File |
| **CamelIBMWatsonxAiFileName** (producer) Constant: [`FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FILE_NAME) | The file name when using InputStream input. |  | String |
| **CamelIBMWatsonxAiFilePath** (producer) Constant: [`FILE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FILE_PATH) | The file path for extraction or classification (for files already in COS). |  | String |
| **CamelIBMWatsonxAiExtractionId** (producer) Constant: [`EXTRACTION_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#EXTRACTION_ID) | The extraction request ID. |  | String |
| **CamelIBMWatsonxAiExtractionStatus** (producer) Constant: [`EXTRACTION_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#EXTRACTION_STATUS) | The extraction status. |  | String |
| **CamelIBMWatsonxAiExtractedText** (producer) Constant: [`EXTRACTED_TEXT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#EXTRACTED_TEXT) | The extracted text content. |  | String |
| **CamelIBMWatsonxAiBucketName** (producer) Constant: [`BUCKET_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#BUCKET_NAME) | The COS bucket name for file operations. |  | String |
| **CamelIBMWatsonxAiUploadSuccess** (producer) Constant: [`UPLOAD_SUCCESS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#UPLOAD_SUCCESS) | Whether the upload operation was successful. |  | Boolean |
| **CamelIBMWatsonxAiDeleteSuccess** (producer) Constant: [`DELETE_SUCCESS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#DELETE_SUCCESS) | Whether the delete operation was successful. |  | Boolean |
| **CamelIBMWatsonxAiClassificationId** (producer) Constant: [`CLASSIFICATION_ID`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#CLASSIFICATION_ID) | The classification request ID. |  | String |
| **CamelIBMWatsonxAiClassificationStatus** (producer) Constant: [`CLASSIFICATION_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#CLASSIFICATION_STATUS) | The classification status. |  | String |
| **CamelIBMWatsonxAiClassificationResult** (producer) Constant: [`CLASSIFICATION_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#CLASSIFICATION_RESULT) | The classification result (document type). |  | String |
| **CamelIBMWatsonxAiDocumentClassified** (producer) Constant: [`DOCUMENT_CLASSIFIED`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#DOCUMENT_CLASSIFIED) | Whether the document was classified. |  | Boolean |
| **CamelIBMWatsonxAiErrorMessage** (producer) Constant: [`ERROR_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#ERROR_MESSAGE) | Error message when classification or extraction fails. |  | String |
| **CamelIBMWatsonxAiErrorCode** (producer) Constant: [`ERROR_CODE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#ERROR_CODE) | Error code when classification or extraction fails. |  | String |
| **CamelIBMWatsonxAiDetectors** (producer) Constant: [`DETECTORS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#DETECTORS) | List of detectors to use. |  | List |
| **CamelIBMWatsonxAiDetected** (producer) Constant: [`DETECTED`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#DETECTED) | Whether harmful content was detected. |  | Boolean |
| **CamelIBMWatsonxAiDetectionResults** (producer) Constant: [`DETECTION_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#DETECTION_RESULTS) | Detection results grouped by type. |  | Map |
| **CamelIBMWatsonxAiDetectionCount** (producer) Constant: [`DETECTION_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#DETECTION_COUNT) | Count of detections found. |  | Integer |
| **CamelIBMWatsonxAiStreamConsumer** (producer) Constant: [`STREAM_CONSUMER`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#STREAM_CONSUMER) | Consumer for streaming text. |  | Consumer |
| **CamelIBMWatsonxAiInputTokenCount** (producer) Constant: [`INPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#INPUT_TOKEN_COUNT) | Input token count. |  | Integer |
| **CamelIBMWatsonxAiOutputTokenCount** (producer) Constant: [`OUTPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#OUTPUT_TOKEN_COUNT) | Output token count. |  | Integer |
| **CamelIBMWatsonxAiStopReason** (producer) Constant: [`STOP_REASON`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#STOP_REASON) | Stop reason for generation. |  | String |
| **CamelIBMWatsonxAiForecastInputSchema** (producer) Constant: [`FORECAST_INPUT_SCHEMA`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FORECAST_INPUT_SCHEMA) | The input schema for time series forecast. |  | InputSchema |
| **CamelIBMWatsonxAiForecastData** (producer) Constant: [`FORECAST_DATA`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FORECAST_DATA) | The forecast data. |  | ForecastData |
| **CamelIBMWatsonxAiForecastResults** (producer) Constant: [`FORECAST_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FORECAST_RESULTS) | The forecast results. |  | List |
| **CamelIBMWatsonxAiForecastInputDataPoints** (producer) Constant: [`FORECAST_INPUT_DATA_POINTS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FORECAST_INPUT_DATA_POINTS) | Number of input data points. |  | Integer |
| **CamelIBMWatsonxAiForecastOutputDataPoints** (producer) Constant: [`FORECAST_OUTPUT_DATA_POINTS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FORECAST_OUTPUT_DATA_POINTS) | Number of output data points. |  | Integer |
| **CamelIBMWatsonxAiFoundationModels** (producer) Constant: [`FOUNDATION_MODELS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FOUNDATION_MODELS) | List of foundation models. |  | List |
| **CamelIBMWatsonxAiFoundationModelTasks** (producer) Constant: [`FOUNDATION_MODEL_TASKS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FOUNDATION_MODEL_TASKS) | List of foundation model tasks. |  | List |
| **CamelIBMWatsonxAiFoundationModelFilter** (producer) Constant: [`FOUNDATION_MODEL_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FOUNDATION_MODEL_FILTER) | Filter for foundation models or tasks. |  | String |
| **CamelIBMWatsonxAiFoundationModelTechPreview** (producer) Constant: [`FOUNDATION_MODEL_TECH_PREVIEW`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#FOUNDATION_MODEL_TECH_PREVIEW) | Include tech preview models. |  | Boolean |
| **CamelIBMWatsonxAiToolName** (producer) Constant: [`TOOL_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOOL_NAME) | The tool name to run. |  | String |
| **CamelIBMWatsonxAiToolRequest** (producer) Constant: [`TOOL_REQUEST`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOOL_REQUEST) | The tool request object. |  | ToolRequest |
| **CamelIBMWatsonxAiToolConfig** (producer) Constant: [`TOOL_CONFIG`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOOL_CONFIG) | The tool configuration. |  | Map |
| **CamelIBMWatsonxAiUtilityTools** (producer) Constant: [`UTILITY_TOOLS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#UTILITY_TOOLS) | List of available utility tools. |  | List |
| **CamelIBMWatsonxAiToolRegistry** (producer) Constant: [`TOOL_REGISTRY`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOOL_REGISTRY) | Tool registry for chat with tool calling capabilities. |  | ToolRegistry |
| **CamelIBMWatsonxAiToolCalls** (producer) Constant: [`TOOL_CALLS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#TOOL_CALLS) | List of tool calls requested by the assistant. |  | List |
| **CamelIBMWatsonxAiHasToolCalls** (producer) Constant: [`HAS_TOOL_CALLS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#HAS_TOOL_CALLS) | Whether the assistant response contains tool calls. |  | Boolean |
| **CamelIBMWatsonxAiAssistantMessage** (producer) Constant: [`ASSISTANT_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watsonx-ai/latest/org/apache/camel/component/ibm/watsonx/ai/WatsonxAiConstants.html#ASSISTANT_MESSAGE) | The full assistant message from chat response. |  | AssistantMessage |

## Required watsonx.ai component options

You must provide the following options to use this component:

-   `apiKey` - Your IBM Cloud API key for authentication
    
-   `baseUrl` - The watsonx.ai endpoint URL (e.g., [https://us-south.ml.cloud.ibm.com](https://us-south.ml.cloud.ibm.com))
    
-   `projectId` or `spaceId` - Your IBM Cloud project or deployment space ID
    
-   `modelId` - The foundation model ID (for model-specific operations)
    
-   (optional) `documentConnectionId`, `documentBucket`, `cosUrl` - needed by services like `textExtraction` or `textClassification`
    
-   (optional) `wxUrl` - For hosted IBM tools
    

## OAuth Authentication

When using an identity provider for service-to-service authentication instead of a static API key, set the `oauthProfile` parameter to acquire an access token via the OAuth 2.0 Client Credentials grant. The token is used as the `apiKey`. This requires `camel-oauth` on the classpath.

```properties
camel.oauth.ibm.client-id=my-client
camel.oauth.ibm.client-secret=my-secret
camel.oauth.ibm.token-endpoint=https://iam.cloud.ibm.com/identity/token
```

```java
from("direct:generate")
    .to("ibm-watsonx-ai:myLabel?oauthProfile=ibm&baseUrl=https://us-south.ml.cloud.ibm.com&projectId=my-project&modelId=ibm/granite-13b-instruct-v2");
```

## Security Considerations

### Sensitive Data Logging

> **Warning**
> When the `logRequests` option is enabled, HTTP requests to the watsonx.ai API may be logged, which can expose sensitive data including your API key. Only enable request logging in development or debugging scenarios, and ensure logs are properly secured. Never enable request logging in production environments where logs might be accessible to unauthorized parties.

## Usage

### Supported Operations

The IBM watsonx.ai component provides the following operations:

#### Text Generation (Deprecated, use chat instead)

-   `textGeneration` - Generate text from a prompt
    
-   `textGenerationStreaming` - Generate text with streaming responses
    

#### Chat

-   `chat` - Chat with conversation history supporting system, user, and assistant messages
    
-   `chatStreaming` - Chat with streaming responses via callback consumer
    

#### Embeddings

-   `embedding` - Generate embeddings for text inputs (single or batch)
    

#### Reranking

-   `rerank` - Rerank documents by relevance to a query
    

#### Tokenization

-   `tokenize` - Count and retrieve tokens for text
    

#### Content Detection

-   `detect` - Detect PII (Personal Identifiable Information) and HAP (Harmful, Abusive, Profane) content in text
    

#### Document Processing

Text Extraction operations:

-   `textExtraction` - Start text extraction from documents stored in Cloud Object Storage
    
-   `textExtractionFetch` - Fetch text extraction results by job ID
    
-   `textExtractionUpload` - Upload a local file and start extraction
    
-   `textExtractionUploadAndFetch` - Upload, extract, and return text synchronously
    
-   `textExtractionUploadFile` - Upload file to COS without starting extraction
    
-   `textExtractionReadFile` - Read file from COS result bucket
    
-   `textExtractionDeleteFile` - Delete file from COS
    
-   `textExtractionDeleteRequest` - Delete extraction job
    

Text Classification operations:

-   `textClassification` - Start document classification for documents in Cloud Object Storage
    
-   `textClassificationFetch` - Fetch classification results by job ID
    
-   `textClassificationUpload` - Upload a local file and start classification
    
-   `textClassificationUploadAndFetch` - Upload, classify, and return result synchronously
    
-   `textClassificationUploadFile` - Upload file to COS without starting classification
    
-   `textClassificationDeleteFile` - Delete file from COS
    
-   `textClassificationDeleteRequest` - Delete classification job
    

> **Note**
> Document processing operations require Cloud Object Storage (COS) configuration with HMAC credentials. See [Cloud Object Storage Connection Setup](#cos-connection-setup) for details.

#### Time Series

-   `forecast` - Generate time series forecasts using foundation models
    

#### Model Discovery

-   `listModels` - List available foundation models
    
-   `listTasks` - List supported tasks
    

#### Deployment Operations

-   `deploymentGenerate` - Generate text using deployed models
    
-   `deploymentChat` - Chat using deployed models
    
-   `deploymentForecast` - Forecast using deployed time series models
    

#### Utility Tools (Experimental)

-   `runTool` - Run utility tools (GoogleSearch, Weather, WebCrawler, Wikipedia, etc.)
    
-   `listTools` - List available utility tools
    
-   `processToolCalls` - Execute tool calls from an assistant message and update the conversation
    

If you don’t specify an operation explicitly, you must set it via the `operation` parameter.

### Common Use Cases

  
| Use Case | Recommended Operation | Models |
| --- | --- | --- |
| Conversational AI, chatbots, Text summarization, Q&A, translation | `chat`, `chatStreaming` | ibm/granite-4-h-small, meta-llama/llama-3-8b-instruct |
| Semantic search, similarity matching | `embedding` | ibm/granite-embedding-278m-multilingual |
| RAG document retrieval ranking | `rerank` | cross-encoder/ms-marco-minilm-l-12-v2 |
| Token counting, context management | `tokenize` | Any text generation model |
| Content moderation, compliance | `detect` | N/A (uses built-in detectors) |
| Document text extraction | `textExtraction`, `textExtractionFetch` | N/A (uses document processing pipeline) |
| Document classification | `textClassification`, `textClassificationFetch` | N/A (uses document processing pipeline) |
| Time series forecasting | `forecast`, `deploymentForecast` | ibm/granite-ttm-1536-96-r2 |
| Model catalog exploration | `listModels`, `listTasks` | N/A |
| Deployed model inference | `deploymentGenerate`, `deploymentChat` | Deployed models |
| Web search, weather, web crawling | `runTool`, `listTools` | N/A (uses utility tools) |
| Chat with tool calling (agentic) | `chat`, `processToolCalls` | ibm/granite-3-8b-instruct, ibm/granite-4-h-small |

## Examples

### Simple Chat

Chat with a simple string message (automatically converted to a user message):

```java
from("direct:simpleChat")
  .setBody(constant("What is the capital of France?"))
  .to("ibm-watsonx-ai:chat?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=ibm/granite-4-h-small" +
      "&operation=chat")
  .log("Response: ${body}");
```

### Chat with System Message

Use a system message to control the assistant’s behavior:

```java
from("direct:chatWithSystem")
  .setHeader("CamelIBMWatsonxAiSystemMessage",
      constant("You are a helpful assistant. Keep your answers brief."))
  .setBody(constant("What is the capital of Italy?"))
  .to("ibm-watsonx-ai:chat?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=ibm/granite-4-h-small" +
      "&operation=chat")
  .log("Response: ${body}");
```

### Streaming Chat

Stream chat responses with a callback consumer:

```java
import com.ibm.watsonx.ai.chat.model.UserMessage;

from("direct:streamChat")
  .process(exchange -> {
      // Set up a consumer to handle streamed chunks
      Consumer<String> streamHandler = chunk -> {
          System.out.print(chunk);
      };
      exchange.getIn().setHeader("CamelIBMWatsonxAiStreamConsumer", streamHandler);
      exchange.getIn().setHeader("CamelIBMWatsonxAiMessages", List.of(
          UserMessage.text("Tell me a joke about programming")
      ));
  })
  .to("ibm-watsonx-ai:chat?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=ibm/granite-4-h-small" +
      "&operation=chatStreaming")
  .log("Full response: ${body}");
```

### Streaming Chat with WebSocket

Stream chat responses to WebSocket clients in real-time, similar to ChatGPT’s streaming UI. This example uses the `camel-vertx-websocket` component to receive messages from clients and stream responses back token-by-token:

-   Java
    

```java
from("vertx-websocket:localhost:8080/chat")
    // Store connection key for sending responses back to this specific client
    .setProperty("connectionKey", header(VertxWebsocketConstants.CONNECTION_KEY))
    .process(exchange -> {
        String connectionKey = exchange.getProperty("connectionKey", String.class);
        ProducerTemplate producer = exchange.getContext().createProducerTemplate();

        // Stream consumer that sends each token as a WebSocket message
        Consumer<String> streamHandler = chunk -> {
            producer.sendBodyAndHeader(
                "vertx-websocket:localhost:8080/chat",
                chunk,
                VertxWebsocketConstants.CONNECTION_KEY, connectionKey
            );
        };
        exchange.getIn().setHeader(WatsonxAiConstants.STREAM_CONSUMER, streamHandler);
    })
    .setHeader(WatsonxAiConstants.SYSTEM_MESSAGE, constant("You are a helpful assistant."))
    // The WebSocket message body becomes the user question
    .to("ibm-watsonx-ai:chat?apiKey=RAW(yourApiKey)" +
        "&baseUrl=https://us-south.ml.cloud.ibm.com" +
        "&projectId=yourProjectId" +
        "&modelId=ibm/granite-4-h-small" +
        "&operation=chatStreaming")
    // Send completion marker to client
    .process(exchange -> {
        String connectionKey = exchange.getProperty("connectionKey", String.class);
        exchange.getContext().createProducerTemplate().sendBodyAndHeader(
            "vertx-websocket:localhost:8080/chat",
            "[DONE]",
            VertxWebsocketConstants.CONNECTION_KEY, connectionKey
        );
    });
```

This pattern enables building real-time chat applications where:

-   WebSocket clients connect and send messages
    
-   Each token from the LLM is streamed back immediately
    
-   Clients receive a `[DONE]` marker when the response is complete
    

> **Note**
> Requires the `camel-vertx-websocket` dependency. See the [Vert.x WebSocket component documentation](vertx-websocket-component.md) for more details.

### Chat with Tool Calling

Enable the LLM to call external tools (like Wikipedia search) and incorporate results into the conversation. This example shows a fully declarative route with no processors required:

-   Java
    
-   YAML
    

```java
import com.ibm.watsonx.ai.chat.ToolRegistry;
import com.ibm.watsonx.ai.chat.model.Tool;
import com.ibm.watsonx.ai.tool.ToolService;
import com.ibm.watsonx.ai.tool.builtin.WikipediaTool;

// Create ToolService for utility tools (requires wxUrl)
ToolService toolService = ToolService.builder()
    .apiKey(apiKey)
    .baseUrl("https://api.dataplatform.cloud.ibm.com/wx")
    .build();

// Create ToolRegistry with Wikipedia tool
ToolRegistry toolRegistry = ToolRegistry.builder()
    .register(new WikipediaTool(toolService))
    .build();

// Get tool schemas for chat
List<Tool> tools = toolRegistry.tools();

from("direct:chatWithTools")
    // Set system message, tools, and registry via headers (body is the user question)
    .setHeader("CamelIBMWatsonxAiSystemMessage",
        constant("You are a helpful assistant. Use available tools when needed."))
    .setHeader("CamelIBMWatsonxAiTools", constant(tools))
    .setHeader("CamelIBMWatsonxAiToolRegistry", constant(toolRegistry))
    // Send to chat
    .to("ibm-watsonx-ai:chat?apiKey=RAW(yourApiKey)" +
        "&baseUrl=https://us-south.ml.cloud.ibm.com" +
        "&projectId=yourProjectId" +
        "&modelId=ibm/granite-3-8b-instruct" +
        "&operation=chat")
    // Loop while LLM requests tool calls
    .loopDoWhile(simple("${header.CamelIBMWatsonxAiHasToolCalls} == true"))
        .log("Executing tool calls...")
        // Process tool calls using the dedicated operation
        .to("ibm-watsonx-ai:tools?operation=processToolCalls")
        // Continue conversation with tool results
        .to("ibm-watsonx-ai:chat?apiKey=RAW(yourApiKey)" +
            "&baseUrl=https://us-south.ml.cloud.ibm.com" +
            "&projectId=yourProjectId" +
            "&modelId=ibm/granite-3-8b-instruct" +
            "&operation=chat")
    .end()
    .log("Final response: ${body}");
```

```yaml
- route:
    from:
      uri: direct:chatWithTools
      steps:
      - setHeader:
          name: CamelIBMWatsonxAiSystemMessage
          constant: "You are a helpful assistant. Use available tools when needed."
      - setHeader:
          name: CamelIBMWatsonxAiTools
          constant: "{{tools}}"
      - setHeader:
          name: CamelIBMWatsonxAiToolRegistry
          constant: "{{toolRegistry}}"
      - to:
          uri: ibm-watsonx-ai:chat
          parameters:
            apiKey: "RAW({{ibm.watsonx.api-key}})"
            baseUrl: "{{ibm.watsonx.base-url}}"
            projectId: "{{ibm.watsonx.project-id}}"
            modelId: ibm/granite-3-8b-instruct
            operation: chat
      - loop:
          id: loop-4459
          doWhile: true
          simple:
            expression: ${header.CamelIBMWatsonxAiHasToolCalls} == true
          steps:
            - log:
                message: Executing tool calls...
            - to:
                uri: ibm-watsonx-ai:tools?operation=processToolCalls
            - to:
                uri: ibm-watsonx-ai:chat
                parameters:
                  apiKey: RAW({{ibm.watsonx.api-key}})
                  baseUrl: "{{ibm.watsonx.base-url}}"
                  modelId: ibm/granite-3-8b-instruct
                  operation: chat
                  projectId: "{{ibm.watsonx.project-id}}"
      - log:
          message: "Final response: ${body}"
```

The above route:

1.  Sets the system message via `CamelIBMWatsonxAiSystemMessage` header
    
2.  The message body becomes the user question automatically
    
3.  Sets tools and registry via headers for function calling
    
4.  Uses `processToolCalls` operation to execute tools and update the conversation
    
5.  Loops until the LLM provides a final answer without tool calls
    

> **Note**
> Tool operations require the `wxUrl` configuration (e.g., `[https://api.dataplatform.cloud.ibm.com/wx](https://api.dataplatform.cloud.ibm.com/wx)`), which is different from the ML `baseUrl`.

### Text Embeddings

Generate embeddings for semantic search and similarity:

```java
from("direct:embed")
  .setBody(constant(List.of(
      "Apache Camel is an integration framework",
      "Quarkus is a Java framework"
  )))
  .to("ibm-watsonx-ai:embed?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=ibm/slate-125m-english-rtrvr" +
      "&operation=embedding")
  .process(exchange -> {
      List<List<Float>> embeddings = exchange.getMessage().getBody(List.class);
      System.out.println("Generated " + embeddings.size() + " embeddings");
      System.out.println("Embedding dimensions: " + embeddings.get(0).size());
  });
```

### Single Text Embedding

Generate embedding for a single text input:

```java
from("direct:embedSingle")
  .setBody(constant("Apache Camel makes integration easy"))
  .to("ibm-watsonx-ai:embed?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=ibm/slate-125m-english-rtrvr" +
      "&operation=embedding")
  .log("Embedding vector size: ${header.CamelIBMWatsonxAiEmbeddings[0].size()}");
```

### Embedding with Vector Database (Qdrant)

Generate an embedding and store it in a Qdrant vector database for semantic search:

```java
import org.apache.camel.component.qdrant.QdrantHeaders;
import org.apache.camel.component.qdrant.QdrantAction;
import io.qdrant.client.PointIdFactory;
import io.qdrant.client.VectorsFactory;
import io.qdrant.client.ValueFactory;
import io.qdrant.client.grpc.Points;

from("direct:embedAndStore")
  .setBody(constant("Apache Camel makes integration easy"))
  .to("ibm-watsonx-ai:embed?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=ibm/slate-125m-english-rtrvr" +
      "&operation=embedding")
  // Transform to Qdrant format and upsert
  .setHeader(QdrantHeaders.ACTION, constant(QdrantAction.UPSERT))
  .process(exchange -> {
      List<Float> embedding = exchange.getMessage().getBody(List.class);
      exchange.getMessage().setBody(
          Points.PointStruct.newBuilder()
              .setId(PointIdFactory.id(UUID.randomUUID()))
              .setVectors(VectorsFactory.vectors(embedding))
              .putPayload("text", ValueFactory.value("Apache Camel makes integration easy"))
              .build());
  })
  .to("qdrant:embeddings?host=localhost&port=6334")
  .log("Embedding stored with ID: ${header.CamelQdrantOperationID}");
```

> **Note**
> This example requires the `camel-qdrant` dependency. See the [Qdrant component documentation](qdrant-component.md) for more details.

### Rerank Documents

Rerank documents by relevance to a query:

```java
from("direct:rerank")
  .process(exchange -> {
      // Set the query to rank against
      exchange.getIn().setHeader("CamelIBMWatsonxAiRerankQuery",
          "What is the best integration framework?");
      // Set documents to rerank
      exchange.getIn().setBody(List.of(
          "Apache Camel provides enterprise integration patterns.",
          "Quarkus is great for microservices.",
          "Kubernetes orchestrates containers.",
          "Apache Kafka handles event streaming."
      ));
  })
  .to("ibm-watsonx-ai:rerank?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=cross-encoder/ms-marco-minilm-l-12-v2" +
      "&operation=rerank")
  .process(exchange -> {
      List results = exchange.getMessage().getBody(List.class);
      System.out.println("Reranked results: " + results);
  });
```

### Rerank with Top N

Return only the top N most relevant documents:

```java
from("direct:rerankTopN")
  .setHeader("CamelIBMWatsonxAiRerankQuery", constant("Cloud computing platform"))
  .setHeader("CamelIBMWatsonxAiRerankTopN", constant(3))
  .setBody(constant(List.of(
      "AWS is a cloud computing platform.",
      "Azure provides cloud services.",
      "IBM Cloud offers cloud solutions.",
      "PostgreSQL is a database.",
      "Infinispan is an in-memory store."
  )))
  .to("ibm-watsonx-ai:rerank?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=cross-encoder/ms-marco-minilm-l-12-v2" +
      "&operation=rerank")
  .log("Top 3 results: ${body}");
```

### Tokenization

Count tokens in text (useful for context window management):

```java
from("direct:tokenize")
  .setBody(constant("Hello, how are you today?"))
  .to("ibm-watsonx-ai:tokenize?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=ibm/granite-4-h-small" +
      "&operation=tokenize")
  .log("Token count: ${header.CamelIBMWatsonxAiTokenCount}")
  .log("Tokens: ${header.CamelIBMWatsonxAiTokens}");
```

### Content Detection (PII/HAP)

Detect personally identifiable information (PII) and harmful/abusive/profane (HAP) content:

```java
from("direct:detect")
  .setBody(constant("Contact John Smith at john.smith@example.com or call 555-123-4567"))
  .to("ibm-watsonx-ai:detect?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&operation=detect" +
      "&detectPii=true")
  .choice()
    .when(header("CamelIBMWatsonxAiDetected").isEqualTo(true))
      .log("PII detected! Count: ${header.CamelIBMWatsonxAiDetectionCount}")
      .log("Detection details: ${header.CamelIBMWatsonxAiDetectionResults}")
    .otherwise()
      .log("No PII detected in content")
  .end();
```

### Content Detection with HAP Threshold

Detect harmful content with a custom threshold:

```java
from("direct:detectHap")
  .setBody(constant("Some text that might contain harmful content"))
  .to("ibm-watsonx-ai:detect?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&operation=detect" +
      "&detectHap=true" +
      "&detectionThreshold=0.5")
  .choice()
    .when(header("CamelIBMWatsonxAiDetected").isEqualTo(true))
      .log("ALERT: Harmful content detected!")
    .otherwise()
      .log("Content is safe")
  .end();
```

### Content Detection with Custom Detectors

Provide custom detectors via header:

```java
import com.ibm.watsonx.ai.detection.detector.Pii;
import com.ibm.watsonx.ai.detection.detector.Hap;

from("direct:detectCustom")
  .process(exchange -> {
      exchange.getIn().setBody("Check this email: user@domain.com");
      exchange.getIn().setHeader("CamelIBMWatsonxAiDetectors", List.of(
          Pii.ofDefaults(),
          Hap.builder().threshold(0.3).build()
      ));
  })
  .to("ibm-watsonx-ai:detect?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&operation=detect")
  .log("Detections: ${body}");
```

### Text Extraction from Cloud Object Storage

Extract text from documents stored in IBM Cloud Object Storage:

> **Note**
> This operation requires COS configuration including cosUrl, documentConnectionId, documentBucket, resultConnectionId, and resultBucket.

```java
from("direct:extract")
  .setBody(constant("documents/report.pdf"))  // Path in COS bucket
  .to("ibm-watsonx-ai:extract?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&operation=textExtraction" +
      "&cosUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud" +
      "&documentConnectionId=your-cos-connection-id" +
      "&documentBucket=your-input-bucket" +
      "&resultConnectionId=your-cos-connection-id" +
      "&resultBucket=your-output-bucket")
  .process(exchange -> {
      String extractionId = exchange.getMessage().getHeader("CamelIBMWatsonxAiExtractionId", String.class);
      String status = exchange.getMessage().getHeader("CamelIBMWatsonxAiExtractionStatus", String.class);
      System.out.println("Extraction job started: " + extractionId);
      System.out.println("Status: " + status);
  });
```

### Fetch Text Extraction Results

Poll for extraction completion and get results:

```java
from("direct:fetchExtraction")
  .setHeader("CamelIBMWatsonxAiExtractionId", constant("your-extraction-job-id"))
  .to("ibm-watsonx-ai:extract?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&operation=textExtractionFetch" +
      "&cosUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud" +
      "&documentConnectionId=your-cos-connection-id" +
      "&documentBucket=your-input-bucket" +
      "&resultConnectionId=your-cos-connection-id" +
      "&resultBucket=your-output-bucket")
  .log("Extraction status: ${header.CamelIBMWatsonxAiExtractionStatus}");
```

### Upload and Extract Local Files (Synchronous)

Upload a local file and get extracted text synchronously using `textExtractionUploadAndFetch`:

```java
from("file:/path/to/documents?noop=true")
  .to("ibm-watsonx-ai:extract?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&operation=textExtractionUploadAndFetch" +
      "&cosUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud" +
      "&documentConnectionId=your-cos-connection-id" +
      "&documentBucket=your-input-bucket" +
      "&resultConnectionId=your-cos-connection-id" +
      "&resultBucket=your-output-bucket")
  .log("Extracted text: ${body}")
  .log("File processed: ${header.CamelFileName}");
```

This operation:

1.  Automatically handles `File`, `GenericFile` (from `file://`, `ftp://`, `sftp://`), `InputStream`, or `byte[]` body types
    
2.  Uploads the file to COS
    
3.  Starts text extraction
    
4.  Polls until completion
    
5.  Returns the extracted text as the message body (also available in `CamelIBMWatsonxAiExtractedText` header)
    

### Text Extraction with File Components

The text extraction operations integrate seamlessly with Camel file components:

```java
// From local file system
from("file:/documents/incoming?noop=true")
  .to("ibm-watsonx-ai:extract?operation=textExtractionUploadAndFetch...")
  .log("Extracted text from ${header.CamelFileName}: ${body}");

// From FTP/SFTP
from("sftp://server/documents?username=xxx&password=xxx")
  .to("ibm-watsonx-ai:extract?operation=textExtractionUploadAndFetch...")
  .log("Extracted: ${header.CamelIBMWatsonxAiExtractedText}");

// From AWS S3
from("aws2-s3://my-bucket?region=us-east-1&prefix=docs/")
  .to("ibm-watsonx-ai:extract?operation=textExtractionUploadAndFetch...")
  .log("Extracted text from S3 object");

// From Azure Blob Storage
from("azure-storage-blob://mycontainer?prefix=documents/")
  .to("ibm-watsonx-ai:extract?operation=textExtractionUploadAndFetch...")
  .log("Extracted text from blob");
```

### Document Classification

Text classification operations allow you to classify documents using IBM watsonx.ai’s document processing capabilities. These operations require Cloud Object Storage (COS) configuration.

> **Important**
> The COS connection in your watsonx.ai project must be configured with HMAC credentials (access\_key\_id and secret\_access\_key), not just IAM Service Credentials. See [Cloud Object Storage Connection Setup](#cos-connection-setup) for details.

#### Classify Documents from Cloud Object Storage

Classify documents already stored in Cloud Object Storage:

```java
from("direct:classify")
  .setBody(constant("documents/contract.pdf"))
  .to("ibm-watsonx-ai:classify?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&operation=textClassification" +
      "&cosUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud" +
      "&documentConnectionId=your-cos-connection-id" +
      "&documentBucket=your-input-bucket")
  .process(exchange -> {
      String classificationId = exchange.getMessage().getHeader("CamelIBMWatsonxAiClassificationId", String.class);
      System.out.println("Classification job started: " + classificationId);
  });
```

#### Upload and Classify Local Files (Synchronous)

Upload a local file and get classification results synchronously using `textClassificationUploadAndFetch`:

```java
from("file:/path/to/documents?noop=true")
  .to("ibm-watsonx-ai:classify?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&operation=textClassificationUploadAndFetch" +
      "&cosUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud" +
      "&documentConnectionId=your-cos-connection-id" +
      "&documentBucket=your-input-bucket")
  .log("Document type: ${header.CamelIBMWatsonxAiClassificationResult}")
  .log("Document classified: ${header.CamelIBMWatsonxAiDocumentClassified}");
```

This operation:

1.  Automatically handles `File`, `GenericFile` (from `file://`, `ftp://`, `sftp://`), `InputStream`, or `byte[]` body types
    
2.  Uploads the file to COS
    
3.  Starts classification
    
4.  Polls until completion
    
5.  Returns the classification result
    

#### Upload and Classify (Asynchronous with Polling)

For more control, use the async flow with `textClassificationUpload` and `textClassificationFetch` in a single route with polling loop:

```java
// Start classification and poll until complete
from("direct:startClassification")
  .to("ibm-watsonx-ai:classify?operation=textClassificationUpload" +
      "&apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&cosUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud" +
      "&documentConnectionId=your-cos-connection-id" +
      "&documentBucket=your-input-bucket")
  .log("Classification started - ID: ${header.CamelIBMWatsonxAiClassificationId}")
  .setProperty("classificationId", header("CamelIBMWatsonxAiClassificationId"))
  // Poll until complete or failed
  .loopDoWhile(simple("${header.CamelIBMWatsonxAiClassificationStatus} != 'completed' && ${header.CamelIBMWatsonxAiClassificationStatus} != 'failed'"))
    .delay(2000)
    .setHeader("CamelIBMWatsonxAiClassificationId", exchangeProperty("classificationId"))
    .to("ibm-watsonx-ai:classify?operation=textClassificationFetch" +
        "&apiKey=RAW(yourApiKey)" +
        "&baseUrl=https://us-south.ml.cloud.ibm.com" +
        "&projectId=yourProjectId" +
        "&cosUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud" +
        "&documentConnectionId=your-cos-connection-id" +
        "&documentBucket=your-input-bucket")
    .log("Status: ${header.CamelIBMWatsonxAiClassificationStatus}")
  .end()
  .choice()
    .when(header("CamelIBMWatsonxAiClassificationStatus").isEqualTo("completed"))
      .log("Classification result: ${header.CamelIBMWatsonxAiClassificationResult}")
    .otherwise()
      .log("Classification failed: ${header.CamelIBMWatsonxAiErrorMessage}")
  .end();
```

#### Classification with File Components

The classification operations integrate seamlessly with Camel file components:

```java
// From local file system
from("file:/documents/incoming?noop=true")
  .to("ibm-watsonx-ai:classify?operation=textClassificationUploadAndFetch...")
  .log("Classified ${header.CamelFileName} as ${header.CamelIBMWatsonxAiClassificationResult}");

// From FTP/SFTP
from("sftp://server/documents?username=xxx&password=xxx")
  .to("ibm-watsonx-ai:classify?operation=textClassificationUploadAndFetch...")
  .log("Classified: ${header.CamelIBMWatsonxAiClassificationResult}");

// From AWS S3
from("aws2-s3://my-bucket?region=us-east-1&prefix=docs/")
  .to("ibm-watsonx-ai:classify?operation=textClassificationUploadAndFetch...")
  .log("Classified S3 object: ${header.CamelIBMWatsonxAiClassificationResult}");

// From Azure Blob Storage
from("azure-storage-blob://mycontainer?prefix=documents/")
  .to("ibm-watsonx-ai:classify?operation=textClassificationUploadAndFetch...")
  .log("Classified blob: ${header.CamelIBMWatsonxAiClassificationResult}");
```

#### Delete Classification Request

Clean up a classification job:

```java
from("direct:deleteClassification")
  .setBody(constant("classification-job-id"))
  .to("ibm-watsonx-ai:classify?operation=textClassificationDeleteRequest" +
      "&apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&cosUrl=https://s3.us-south.cloud-object-storage.appdomain.cloud" +
      "&documentConnectionId=your-cos-connection-id" +
      "&documentBucket=your-input-bucket")
  .log("Delete success: ${header.CamelIBMWatsonxAiDeleteSuccess}");
```

#### Supported File Types

Text classification supports the following input file types:

-   Documents: PDF, DOC, DOCX, PPT, PPTX, XLSX
    
-   Images: BMP, GIF, JFIF, JPG, PNG, TIFF
    
-   Text: HTML, Markdown
    

For complete details on supported file formats, see:

-   [Text Extraction API Reference](https://cloud.ibm.com/apidocs/watsonx-ai#text-extraction)
    
-   [Text Classification API Reference](https://cloud.ibm.com/apidocs/watsonx-ai#text-classification)
    

#### Supported Foundation Models for Classification

-   `mistral-small-3-1-24b-instruct-2503` (certified for key-value pair classification)
    
-   `llama-4-maverick-17b-128e-instruct-fp8`
    
-   `mistral-medium-2505`
    

For the latest list of supported models, see the [IBM watsonx.ai Text Classification documentation](https://cloud.ibm.com/apidocs/watsonx-ai#text-classification).

### Using Input Header

Provide input via header instead of body:

```java
from("direct:headerInput")
  .setHeader("CamelIBMWatsonxAiInput", constant("What is machine learning?"))
  .to("ibm-watsonx-ai:gen?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=ibm/granite-13b-instruct-v2" +
      "&operation=textGeneration")
  .log("Generated text: ${body}");
```

### Accessing Response Metadata

Access token counts and stop reason from response headers:

```java
from("direct:metadata")
  .setBody(constant("Summarize the benefits of cloud computing"))
  .to("ibm-watsonx-ai:gen?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=ibm/granite-13b-instruct-v2" +
      "&operation=textGeneration")
  .log("Generated: ${body}")
  .log("Input tokens: ${header.CamelIBMWatsonxAiInputTokenCount}")
  .log("Output tokens: ${header.CamelIBMWatsonxAiOutputTokenCount}")
  .log("Stop reason: ${header.CamelIBMWatsonxAiStopReason}");
```

### Time Series Forecasting

Generate time series forecasts:

```java
import com.ibm.watsonx.ai.timeseries.InputSchema;
import com.ibm.watsonx.ai.timeseries.ForecastData;

from("direct:forecast")
  .process(exchange -> {
      // Define the schema
      InputSchema schema = InputSchema.builder()
          .timestampColumn("date")
          .addIdColumn("series_id")
          .build();

      // Create forecast data
      ForecastData data = ForecastData.create()
          .addAll("date", "2024-01-01T00:00:00", "2024-01-02T00:00:00", "2024-01-03T00:00:00")
          .add("series_id", "S1", 3)
          .addAll("value", 10.5, 12.3, 11.8);

      exchange.getIn().setHeader("CamelIBMWatsonxAiForecastInputSchema", schema);
      exchange.getIn().setHeader("CamelIBMWatsonxAiForecastData", data);
  })
  .to("ibm-watsonx-ai:forecast?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&projectId=yourProjectId" +
      "&modelId=ibm/granite-ttm-1536-96-r2" +
      "&operation=forecast")
  .log("Forecast results: ${body}");
```

### List Available Models

Explore the model catalog:

```java
from("direct:listModels")
  .to("ibm-watsonx-ai:models?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&operation=listModels")
  .process(exchange -> {
      List models = exchange.getMessage().getBody(List.class);
      models.forEach(model -> System.out.println("Model: " + model));
  });
```

### List Supported Tasks

Discover available tasks:

```java
from("direct:listTasks")
  .to("ibm-watsonx-ai:tasks?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&operation=listTasks")
  .log("Available tasks: ${body}");
```

### Deployment Chat

Chat using a deployed model:

```java
import com.ibm.watsonx.ai.chat.model.UserMessage;

from("direct:deploymentChat")
  .setBody(constant("What is the capital of France?"))
  .to("ibm-watsonx-ai:deploy?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&deploymentId=your-deployment-id" +
      "&operation=deploymentChat")
  .log("Response: ${body}");
```

### Run Utility Tool

Use watsonx.ai utility tools (experimental):

```java
from("direct:runTool")
  .process(exchange -> {
      // Set tool name
      exchange.getIn().setHeader("CamelIBMWatsonxAiToolName", "GoogleSearch");
      // Set structured input
      exchange.getIn().setBody(Map.of("q", "Apache Camel integration framework"));
      // Optional: set config
      exchange.getIn().setHeader("CamelIBMWatsonxAiToolConfig", Map.of("maxResults", 5));
  })
  .to("ibm-watsonx-ai:tool?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&operation=runTool")
  .log("Tool result: ${body}");
```

### List Available Tools

Discover available utility tools:

```java
from("direct:listTools")
  .to("ibm-watsonx-ai:tools?apiKey=RAW(yourApiKey)" +
      "&baseUrl=https://us-south.ml.cloud.ibm.com" +
      "&operation=listTools")
  .process(exchange -> {
      List tools = exchange.getMessage().getBody(List.class);
      System.out.println("Available tools: " + tools.size());
  });
```

## Spring Boot and Camel Main Configuration

When using Spring Boot or Camel Main, you can configure the component in `application.properties`:

> **Note**
> This configuration approach works with both Spring Boot (`camel-ibm-watsonx-ai-starter`) and Camel Main runtimes.

```properties
# watsonx.ai configuration
camel.component.ibm-watsonx-ai.configuration.api-key=${IBM_WATSONX_API_KEY}
camel.component.ibm-watsonx-ai.configuration.base-url=https://us-south.ml.cloud.ibm.com
camel.component.ibm-watsonx-ai.configuration.project-id=${IBM_WATSONX_PROJECT_ID}
camel.component.ibm-watsonx-ai.configuration.model-id=ibm/granite-13b-instruct-v2
camel.component.ibm-watsonx-ai.configuration.temperature=0.7
camel.component.ibm-watsonx-ai.configuration.max-new-tokens=200
```

Then use the component in routes without repeating configuration:

```java
from("direct:generate")
  .setBody(constant("Explain microservices architecture"))
  .to("ibm-watsonx-ai:gen?operation=textGeneration")
  .log("Generated: ${body}");
```

## watsonx.ai Authentication

IBM watsonx.ai uses IBM Cloud IAM (Identity and Access Management) for authentication. You need to provide your IBM Cloud API key.

You can create API keys in the IBM Cloud console:

1.  Go to [https://cloud.ibm.com/iam/apikeys](https://cloud.ibm.com/iam/apikeys)
    
2.  Click "Create an IBM Cloud API key"
    
3.  Copy the API key and use it in your Camel routes
    

For more information about authentication, see the [IBM Cloud IAM documentation](https://cloud.ibm.com/docs/watson?topic=watson-iam).

## Cloud Object Storage Connection Setup

Document processing operations (text extraction and classification) require a properly configured IBM Cloud Object Storage (COS) connection in your watsonx.ai project.

> **Important**
> The COS connection must include HMAC credentials (access\_key\_id and secret\_access\_key), not just IAM Service Credentials. Without HMAC credentials, you will encounter errors like "EmptyStaticCreds: static credentials are empty".

### Creating COS Credentials with HMAC

1.  Go to your IBM Cloud console
    
2.  Navigate to your Cloud Object Storage instance
    
3.  Go to **Service credentials** tab
    
4.  Click **New credential**
    
5.  **Important**: Expand "Advanced options" and enable **Include HMAC Credential**
    
6.  Create the credential
    
7.  The credential will include both IAM and HMAC keys:
    
    ```json
    {
      "apikey": "...",
      "cos_hmac_keys": {
        "access_key_id": "...",
        "secret_access_key": "..."
      },
      ...
    }
    ```
    

### Creating the COS Connection in watsonx.ai

1.  In your watsonx.ai project, go to **Manage** → **Connections**
    
2.  Click **New connection**
    
3.  Select **IBM Cloud Object Storage**
    
4.  Enter the HMAC credentials (access\_key\_id and secret\_access\_key)
    
5.  Save the connection and note the **Connection ID**
    

The Connection ID is what you use for the `documentConnectionId` and `resultConnectionId` parameters.

### Additional Resources

-   For more information about how to create the **IBM Cloud Object Storage connection**, see the [IBM watsonx.ai COS connection documentation](https://dataplatform.cloud.ibm.com/docs/content/wsj/manage-data/conn-cos.html?context=wx&locale=en).
    
-   To find the **bucket name** and COS endpoint for your region, see the [IBM Cloud Object Storage buckets documentation](https://cloud.ibm.com/docs/cloud-object-storage?topic=cloud-object-storage-endpoints).
    

## Dependencies

Maven users will need to add the following dependency to their `pom.xml`.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ibm-watsonx-ai</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

where `x.x.x` is the version number of Camel.