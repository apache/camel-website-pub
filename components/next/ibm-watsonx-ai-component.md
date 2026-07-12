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
| **apiKey** (security) | **Required** IBM Cloud API key for authentication. |  | String |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used as apiKey. Requires camel-oauth on the classpath. |  | String |
| **verifySsl** (security) | Whether to verify SSL certificates. | true | Boolean |

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
| **apiKey** (security) | **Required** IBM Cloud API key for authentication. |  | String |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used as apiKey. Requires camel-oauth on the classpath. |  | String |
| **verifySsl** (security) | Whether to verify SSL certificates. | true | Boolean |

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

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:generate")
    .to("ibm-watsonx-ai:myLabel?oauthProfile=ibm&baseUrl=https://us-south.ml.cloud.ibm.com&projectId=my-project&modelId=ibm/granite-13b-instruct-v2");
```

```xml
<route>
  <from uri="direct:generate"/>
  <to uri="ibm-watsonx-ai:myLabel?oauthProfile=ibm&amp;baseUrl=https://us-south.ml.cloud.ibm.com&amp;projectId=my-project&amp;modelId=ibm/granite-13b-instruct-v2"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:generate
      steps:
        - to:
            uri: ibm-watsonx-ai:myLabel
            parameters:
              oauthProfile: ibm
              baseUrl: "https://us-south.ml.cloud.ibm.com"
              projectId: my-project
              modelId: ibm/granite-13b-instruct-v2
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

## Sub-Pages

For more details, see:

-   [Examples](others/ibm-watsonx-ai-examples.md) - Comprehensive examples for chat, embeddings, reranking, content detection, document processing, forecasting, and model operations
    

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

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:generate")
    .setBody(constant("Explain microservices architecture"))
    .to("ibm-watsonx-ai:gen?operation=textGeneration")
    .log("Generated: ${body}");
```

```xml
<route>
  <from uri="direct:generate"/>
  <setBody>
    <constant>Explain microservices architecture</constant>
  </setBody>
  <to uri="ibm-watsonx-ai:gen?operation=textGeneration"/>
  <log message="Generated: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:generate
      steps:
        - setBody:
            constant: "Explain microservices architecture"
        - to:
            uri: ibm-watsonx-ai:gen
            parameters:
              operation: textGeneration
        - log:
            message: "Generated: ${body}"
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