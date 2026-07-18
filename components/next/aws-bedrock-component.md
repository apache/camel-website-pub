# AWS Bedrock

**Since Camel 4.5**

**Only producer is supported**

The AWS2 Bedrock component supports invoking a supported LLM model from [AWS Bedrock](https://aws.amazon.com/bedrock/) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Bedrock. More information is available at [Amazon Bedrock](https://aws.amazon.com/bedrock/).

## URI Format

aws-bedrock://label\[?options\]

You can append query options to the URI in the following format:

`?options=value&option2=value&…​`

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

The AWS Bedrock component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | BedrockConfiguration |
| **guardrailIdentifier** (producer) | The identifier (ID or ARN) for the guardrail to apply to the model invocation. |  | String |
| **guardrailTrace** (producer) | Whether to return trace information from the guardrail. | false | boolean |
| **guardrailVersion** (producer) | The version of the guardrail to use. Defaults to DRAFT. | DRAFT | String |
| **includeStreamingMetadata** (producer) | Whether to include streaming metadata in the response headers (completion reason, token count, chunk count). | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **modelId** (producer) | 
**Required** Define the model Id we are going to use.

Enum values:

-   amazon.titan-text-express-v1
    
-   amazon.titan-text-lite-v1
    
-   amazon.titan-image-generator-v1
    
-   amazon.titan-embed-text-v1
    
-   amazon.titan-embed-image-v1
    
-   amazon.titan-text-premier-v1:0
    
-   amazon.titan-embed-text-v2:0
    
-   amazon.titan-image-generator-v2:0
    
-   amazon.nova-canvas-v1:0
    
-   amazon.nova-lite-v1:0
    
-   amazon.nova-micro-v1:0
    
-   amazon.nova-premier-v1:0
    
-   amazon.nova-pro-v1:0
    
-   amazon.nova-reel-v1:0
    
-   amazon.nova-reel-v1:1
    
-   amazon.nova-sonic-v1:0
    
-   amazon.rerank-v1:0
    
-   ai21.jamba-1-5-large-v1:0
    
-   ai21.jamba-1-5-mini-v1:0
    
-   anthropic.claude-3-sonnet-20240229-v1:0
    
-   anthropic.claude-3-5-sonnet-20240620-v1:0
    
-   anthropic.claude-3-5-sonnet-20241022-v2:0
    
-   anthropic.claude-3-haiku-20240307-v1:0
    
-   anthropic.claude-3-5-haiku-20241022-v1:0
    
-   anthropic.claude-3-opus-20240229-v1:0
    
-   anthropic.claude-3-7-sonnet-20250219-v1:0
    
-   anthropic.claude-opus-4-20250514-v1:0
    
-   anthropic.claude-sonnet-4-20250514-v1:0
    
-   cohere.command-r-plus-v1:0
    
-   cohere.command-r-v1:0
    
-   cohere.embed-english-v3
    
-   cohere.embed-multilingual-v3
    
-   cohere.rerank-v3-5:0
    
-   meta.llama3-8b-instruct-v1:0
    
-   meta.llama3-70b-instruct-v1:0
    
-   meta.llama3-1-8b-instruct-v1:0
    
-   meta.llama3-1-70b-instruct-v1:0
    
-   meta.llama3-1-405b-instruct-v1:0
    
-   meta.llama3-2-1b-instruct-v1:0
    
-   meta.llama3-2-3b-instruct-v1:0
    
-   meta.llama3-2-11b-instruct-v1:0
    
-   meta.llama3-2-90b-instruct-v1:0
    
-   meta.llama3-3-70b-instruct-v1:0
    
-   meta.llama4-maverick-17b-instruct-v1:0
    
-   meta.llama4-scout-17b-instruct-v1:0
    
-   mistral.mistral-7b-instruct-v0:2
    
-   mistral.mixtral-8x7b-instruct-v0:1
    
-   mistral.mistral-large-2402-v1:0
    
-   mistral.mistral-large-2407-v1:0
    
-   mistral.mistral-small-2402-v1:0
    
-   mistral.pixtral-large-2502-v1:0
    
-   stability.sd3-5-large-v1:0
    
-   stability.stable-image-control-sketch-v1:0
    
-   stability.stable-image-control-structure-v1:0
    
-   stability.stable-image-core-v1:1
    





 |  | String |
| **operation** (producer) | 

**Required** The operation to perform.

Enum values:

-   invokeTextModel
    
-   invokeImageModel
    
-   invokeEmbeddingsModel
    
-   invokeTextModelStreaming
    
-   invokeImageModelStreaming
    
-   invokeEmbeddingsModelStreaming
    
-   converse
    
-   converseStream
    
-   applyGuardrail
    





 |  | BedrockOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (producer) | 

The region in which Bedrock client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   us-east-1
    
-   us-east-2
    
-   us-west-2
    
-   us-gov-west-1
    
-   ap-northeast-1
    
-   ap-northeast-2
    
-   ap-south-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   ca-central-1
    
-   eu-central-1
    
-   eu-central-2
    
-   eu-west-1
    
-   eu-west-2
    
-   eu-west-3
    
-   sa-east-1
    





 |  | String |
| **streamOutputMode** (producer) | 

The streaming output mode (complete or chunks). In complete mode, the full response is accumulated and returned as a single message. In chunks mode, each chunk is emitted as a separate exchange.

Enum values:

-   complete
    
-   chunks
    





 | complete | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Bedrock client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Bedrock client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **bedrockRuntimeAsyncClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Runtime Async client for streaming operations. |  | BedrockRuntimeAsyncClient |
| **bedrockRuntimeClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Runtime client. |  | BedrockRuntimeClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Bedrock client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Bedrock client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Bedrock client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Bedrock client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | boolean |

## Endpoint Options

The AWS Bedrock endpoint is configured using URI syntax:

aws-bedrock:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **guardrailIdentifier** (producer) | The identifier (ID or ARN) for the guardrail to apply to the model invocation. |  | String |
| **guardrailTrace** (producer) | Whether to return trace information from the guardrail. | false | boolean |
| **guardrailVersion** (producer) | The version of the guardrail to use. Defaults to DRAFT. | DRAFT | String |
| **includeStreamingMetadata** (producer) | Whether to include streaming metadata in the response headers (completion reason, token count, chunk count). | true | boolean |
| **modelId** (producer) | 
**Required** Define the model Id we are going to use.

Enum values:

-   amazon.titan-text-express-v1
    
-   amazon.titan-text-lite-v1
    
-   amazon.titan-image-generator-v1
    
-   amazon.titan-embed-text-v1
    
-   amazon.titan-embed-image-v1
    
-   amazon.titan-text-premier-v1:0
    
-   amazon.titan-embed-text-v2:0
    
-   amazon.titan-image-generator-v2:0
    
-   amazon.nova-canvas-v1:0
    
-   amazon.nova-lite-v1:0
    
-   amazon.nova-micro-v1:0
    
-   amazon.nova-premier-v1:0
    
-   amazon.nova-pro-v1:0
    
-   amazon.nova-reel-v1:0
    
-   amazon.nova-reel-v1:1
    
-   amazon.nova-sonic-v1:0
    
-   amazon.rerank-v1:0
    
-   ai21.jamba-1-5-large-v1:0
    
-   ai21.jamba-1-5-mini-v1:0
    
-   anthropic.claude-3-sonnet-20240229-v1:0
    
-   anthropic.claude-3-5-sonnet-20240620-v1:0
    
-   anthropic.claude-3-5-sonnet-20241022-v2:0
    
-   anthropic.claude-3-haiku-20240307-v1:0
    
-   anthropic.claude-3-5-haiku-20241022-v1:0
    
-   anthropic.claude-3-opus-20240229-v1:0
    
-   anthropic.claude-3-7-sonnet-20250219-v1:0
    
-   anthropic.claude-opus-4-20250514-v1:0
    
-   anthropic.claude-sonnet-4-20250514-v1:0
    
-   cohere.command-r-plus-v1:0
    
-   cohere.command-r-v1:0
    
-   cohere.embed-english-v3
    
-   cohere.embed-multilingual-v3
    
-   cohere.rerank-v3-5:0
    
-   meta.llama3-8b-instruct-v1:0
    
-   meta.llama3-70b-instruct-v1:0
    
-   meta.llama3-1-8b-instruct-v1:0
    
-   meta.llama3-1-70b-instruct-v1:0
    
-   meta.llama3-1-405b-instruct-v1:0
    
-   meta.llama3-2-1b-instruct-v1:0
    
-   meta.llama3-2-3b-instruct-v1:0
    
-   meta.llama3-2-11b-instruct-v1:0
    
-   meta.llama3-2-90b-instruct-v1:0
    
-   meta.llama3-3-70b-instruct-v1:0
    
-   meta.llama4-maverick-17b-instruct-v1:0
    
-   meta.llama4-scout-17b-instruct-v1:0
    
-   mistral.mistral-7b-instruct-v0:2
    
-   mistral.mixtral-8x7b-instruct-v0:1
    
-   mistral.mistral-large-2402-v1:0
    
-   mistral.mistral-large-2407-v1:0
    
-   mistral.mistral-small-2402-v1:0
    
-   mistral.pixtral-large-2502-v1:0
    
-   stability.sd3-5-large-v1:0
    
-   stability.stable-image-control-sketch-v1:0
    
-   stability.stable-image-control-structure-v1:0
    
-   stability.stable-image-core-v1:1
    





 |  | String |
| **operation** (producer) | 

**Required** The operation to perform.

Enum values:

-   invokeTextModel
    
-   invokeImageModel
    
-   invokeEmbeddingsModel
    
-   invokeTextModelStreaming
    
-   invokeImageModelStreaming
    
-   invokeEmbeddingsModelStreaming
    
-   converse
    
-   converseStream
    
-   applyGuardrail
    





 |  | BedrockOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (producer) | 

The region in which Bedrock client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   us-east-1
    
-   us-east-2
    
-   us-west-2
    
-   us-gov-west-1
    
-   ap-northeast-1
    
-   ap-northeast-2
    
-   ap-south-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   ca-central-1
    
-   eu-central-1
    
-   eu-central-2
    
-   eu-west-1
    
-   eu-west-2
    
-   eu-west-3
    
-   sa-east-1
    





 |  | String |
| **streamOutputMode** (producer) | 

The streaming output mode (complete or chunks). In complete mode, the full response is accumulated and returned as a single message. In chunks mode, each chunk is emitted as a separate exchange.

Enum values:

-   complete
    
-   chunks
    





 | complete | String |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Bedrock client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Bedrock client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **bedrockRuntimeAsyncClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Runtime Async client for streaming operations. |  | BedrockRuntimeAsyncClient |
| **bedrockRuntimeClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Runtime client. |  | BedrockRuntimeClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Bedrock client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Bedrock client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Bedrock client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Bedrock client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | boolean |

## Message Headers

The AWS Bedrock component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsBedrockOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsBedrockContentType** (producer) Constant: [`MODEL_CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#MODEL_CONTENT_TYPE) | The model content type. |  | String |
| **CamelAwsBedrockAcceptContentType** (producer) Constant: [`MODEL_ACCEPT_CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#MODEL_ACCEPT_CONTENT_TYPE) | The model accept content type. |  | String |
| **CamelAwsBedrockStreamOutputMode** (producer) Constant: [`STREAM_OUTPUT_MODE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#STREAM_OUTPUT_MODE) | The streaming output mode (complete or chunks). |  | String |
| **CamelAwsBedrockCompletionReason** (producer) Constant: [`STREAMING_COMPLETION_REASON`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#STREAMING_COMPLETION_REASON) | The completion reason for streaming response. |  | String |
| **CamelAwsBedrockTokenCount** (producer) Constant: [`STREAMING_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#STREAMING_TOKEN_COUNT) | The number of tokens generated in streaming response. |  | Integer |
| **CamelAwsBedrockChunkCount** (producer) Constant: [`STREAMING_CHUNK_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#STREAMING_CHUNK_COUNT) | The number of chunks received in streaming response. |  | Integer |
| **CamelAwsBedrockConverseMessages** (producer) Constant: [`CONVERSE_MESSAGES`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#CONVERSE_MESSAGES) | The conversation messages for Converse API. |  | List |
| **CamelAwsBedrockConverseSystem** (producer) Constant: [`CONVERSE_SYSTEM`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#CONVERSE_SYSTEM) | The system prompts for Converse API. |  | List |
| **CamelAwsBedrockConverseInferenceConfig** (producer) Constant: [`CONVERSE_INFERENCE_CONFIG`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#CONVERSE_INFERENCE_CONFIG) | The inference configuration for Converse API. |  | InferenceConfiguration |
| **CamelAwsBedrockConverseToolConfig** (producer) Constant: [`CONVERSE_TOOL_CONFIG`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#CONVERSE_TOOL_CONFIG) | The tool configuration for Converse API. |  | ToolConfiguration |
| **CamelAwsBedrockConverseAdditionalFields** (producer) Constant: [`CONVERSE_ADDITIONAL_MODEL_REQUEST_FIELDS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#CONVERSE_ADDITIONAL_MODEL_REQUEST_FIELDS) | The additional model request fields for Converse API. |  | Document |
| **CamelAwsBedrockConverseStopReason** (producer) Constant: [`CONVERSE_STOP_REASON`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#CONVERSE_STOP_REASON) | The stop reason from Converse API response. |  | String |
| **CamelAwsBedrockConverseUsage** (producer) Constant: [`CONVERSE_USAGE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#CONVERSE_USAGE) | The usage metrics from Converse API response. |  | TokenUsage |
| **CamelAwsBedrockConverseOutputMessage** (producer) Constant: [`CONVERSE_OUTPUT_MESSAGE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#CONVERSE_OUTPUT_MESSAGE) | The output message from Converse API response. |  | Message |
| **CamelAwsBedrockGuardrailConfig** (producer) Constant: [`GUARDRAIL_CONFIG`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#GUARDRAIL_CONFIG) | The guardrail configuration to apply to the request. |  | GuardrailConfiguration |
| **CamelAwsBedrockGuardrailIdentifier** (producer) Constant: [`GUARDRAIL_IDENTIFIER`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#GUARDRAIL_IDENTIFIER) | The guardrail identifier to use for the ApplyGuardrail operation. |  | String |
| **CamelAwsBedrockGuardrailContent** (producer) Constant: [`GUARDRAIL_CONTENT`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#GUARDRAIL_CONTENT) | The content blocks for ApplyGuardrail operation. |  | List |
| **CamelAwsBedrockGuardrailSource** (producer) Constant: [`GUARDRAIL_SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#GUARDRAIL_SOURCE) | The source type for ApplyGuardrail operation (INPUT or OUTPUT). |  | String |
| **CamelAwsBedrockGuardrailOutput** (producer) Constant: [`GUARDRAIL_OUTPUT`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#GUARDRAIL_OUTPUT) | The guardrail assessment output from the response. |  | GuardrailAssessment |
| **CamelAwsBedrockGuardrailTrace** (producer) Constant: [`GUARDRAIL_TRACE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#GUARDRAIL_TRACE) | The trace information from guardrail evaluation. |  | GuardrailTrace |
| **CamelAwsBedrockGuardrailAssessments** (producer) Constant: [`GUARDRAIL_ASSESSMENTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#GUARDRAIL_ASSESSMENTS) | The guardrail assessments from ApplyGuardrail response. |  | List |
| **CamelAwsBedrockGuardrailUsage** (producer) Constant: [`GUARDRAIL_USAGE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/runtime/BedrockConstants.html#GUARDRAIL_USAGE) | The guardrail usage metrics from ApplyGuardrail response. |  | GuardrailUsage |

Required Bedrock component options

You have to provide the bedrockRuntimeClient in the Registry or your accessKey and secretKey to access the [Amazon Bedrock](https://aws.amazon.com/bedrock/) service.

## Usage

### Static credentials, Default Credential Provider and Profile Credentials Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`.
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You have also the possibility of using Profile Credentials Provider, by specifying the useProfileCredentialsProvider option to true and profileCredentialsName to the profile name.

Only one of static, default and profile credentials could be used at the same time.

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Bedrock Producer operations

Camel-AWS Bedrock component provides the following operation on the producer side:

-   invokeTextModel
    
-   invokeImageModel
    
-   invokeEmbeddingsModel
    
-   invokeTextModelStreaming
    
-   invokeImageModelStreaming
    
-   invokeEmbeddingsModelStreaming
    
-   converse
    
-   converseStream
    
-   applyGuardrail
    

The operation must match the model type. Text-generation models are used with `invokeTextModel`, image-generation models (for example `amazon.titan-image-generator-v1`, `amazon.nova-canvas-v1:0`, the `stability.*` models) with `invokeImageModel`, and embedding models (for example `amazon.titan-embed-text-v1`, `cohere.embed-english-v3`) with `invokeEmbeddingsModel`. Invoking `invokeTextModel` with an image, embedding, rerank or video/speech model fails fast with an `IllegalArgumentException` that names the model and points to the operation to use instead.

### Streaming Support

The streaming operations (`invokeTextModelStreaming`, `invokeImageModelStreaming`, `invokeEmbeddingsModelStreaming`) enable real-time streaming of model responses, providing lower latency and better user experience for interactive applications.

#### Streaming Output Modes

Two streaming modes are supported:

**Complete Mode (default)**: Accumulates all chunks and returns the complete response as a single message. This is the simplest mode and behaves similarly to non-streaming operations, but with lower time-to-first-token.

**Chunks Mode**: Emits each chunk as it arrives in a List. Useful for reactive streaming pipelines or when you need to process chunks individually.

#### Streaming Configuration Options

-   `streamOutputMode`: Set to "complete" (default) or "chunks"
    
-   `includeStreamingMetadata`: Whether to include metadata headers (default: true)
    

#### Streaming Metadata Headers

When `includeStreamingMetadata` is true, the following headers are set:

-   `CamelAwsBedrockCompletionReason`: The reason the model stopped generating (e.g., "FINISH", "end\_turn", "stop")
    
-   `CamelAwsBedrockTokenCount`: The number of tokens generated (if provided by the model)
    
-   `CamelAwsBedrockChunkCount`: The number of chunks received
    

#### Supported Models for Streaming

All text generation models support streaming: - Amazon Titan (all text models) - Anthropic Claude (all versions) - Meta Llama (all versions) - Mistral AI (all models) - Cohere Command models - Amazon Nova models

### Converse API Support

The Converse API provides a unified, model-agnostic interface for conversational AI interactions with AWS Bedrock models. It offers several advantages over the legacy InvokeModel API:

-   **Unified Interface**: Single API across all supported models (Claude, Llama, Mistral, etc.)
    
-   **Multi-turn Conversations**: Native support for conversation history with user/assistant roles
    
-   **Tool Use & Function Calling**: Built-in support for tools and function calling
    
-   **System Prompts**: First-class support for system-level instructions
    
-   **Structured Responses**: Consistent response format across all models
    
-   **Streaming Support**: Real-time streaming with the `converseStream` operation
    

#### Converse Operations

Two operations are provided:

**converse**: Standard request-response conversation

```none
aws-bedrock://label?operation=converse&modelId=anthropic.claude-3-sonnet-20240229-v1:0
```

**converseStream**: Streaming conversation with real-time chunk delivery

```none
aws-bedrock://label?operation=converseStream&modelId=anthropic.claude-3-sonnet-20240229-v1:0
```

#### Converse Configuration Options

Converse API uses message headers for configuration:

-   `CamelAwsBedrockConverseMessages` (required): List of Message objects representing the conversation
    
-   `CamelAwsBedrockConverseSystem`: List of SystemContentBlock for system-level instructions
    
-   `CamelAwsBedrockConverseInferenceConfig`: InferenceConfiguration for temperature, maxTokens, etc.
    
-   `CamelAwsBedrockConverseToolConfig`: ToolConfiguration for function calling support
    
-   `CamelAwsBedrockConverseAdditionalFields`: Document for model-specific additional fields
    

For streaming operations, you can also use: - `CamelAwsBedrockStreamOutputMode`: Set to "complete" (default) or "chunks"

#### Converse Response Headers

When a conversation completes, the following headers are set:

-   `CamelAwsBedrockConverseStopReason`: Why the model stopped (e.g., "end\_turn", "max\_tokens")
    
-   `CamelAwsBedrockConverseUsage`: TokenUsage object with input/output token counts
    
-   `CamelAwsBedrockConverseOutputMessage`: The complete Message object from the model
    
-   `CamelAwsBedrockChunkCount`: (streaming only) Number of chunks received
    

#### Supported Models for Converse API

The Converse API supports all modern foundation models on Bedrock:

-   Anthropic Claude 3 family (Haiku, Sonnet, Opus)
    
-   Anthropic Claude 3.5 family (Sonnet v2, Haiku)
    
-   Amazon Nova family (Micro, Lite, Pro)
    
-   Meta Llama 3.x models
    
-   Mistral AI models
    
-   Cohere Command R models
    

> **Note**
> Legacy models (Claude 2.x, Claude Instant) are not supported by the Converse API. Use the `invokeTextModel` operation for those models.

### Guardrails Support

AWS Bedrock Guardrails enable you to implement safeguards for your generative AI applications based on your use cases and responsible AI policies. Guardrails can filter harmful content, block sensitive topics, remove personally identifiable information (PII), and enhance content safety and privacy in generative AI applications.

The Camel AWS Bedrock component provides comprehensive support for guardrails through:

-   **Converse API Integration**: Apply guardrails to conversational interactions
    
-   **Streaming Support**: Use guardrails with real-time streaming responses
    
-   **Standalone Validation**: Check content against guardrails without invoking a model
    
-   **Flexible Configuration**: Configure guardrails at endpoint level or per-message
    

#### Guardrails Configuration Options

**Endpoint-level Configuration** (applies to all requests):

-   `guardrailIdentifier`: The ID or ARN of the guardrail to apply
    
-   `guardrailVersion`: The version of the guardrail (default: "DRAFT")
    
-   `guardrailTrace`: Whether to return trace information (default: false)
    

**Message-level Configuration** (per-message override via headers):

-   `CamelAwsBedrockGuardrailConfig`: GuardrailConfiguration object for converse operations
    
-   `CamelAwsBedrockGuardrailIdentifier`: Guardrail identifier String for the applyGuardrail operation (overrides the endpoint `guardrailIdentifier`)
    
-   `CamelAwsBedrockGuardrailContent`: Content blocks for applyGuardrail operation
    
-   `CamelAwsBedrockGuardrailSource`: Source type - "INPUT" or "OUTPUT" for applyGuardrail
    

#### Guardrails Operations

**converse with Guardrails**: Apply guardrails to conversational model invocations

```none
aws-bedrock://label?operation=converse&modelId=anthropic.claude-3-sonnet-20240229-v1:0
    &guardrailIdentifier=abc123xyz&guardrailVersion=DRAFT&guardrailTrace=true
```

**converseStream with Guardrails**: Apply guardrails to streaming conversations

```none
aws-bedrock://label?operation=converseStream&modelId=anthropic.claude-3-sonnet-20240229-v1:0
    &guardrailIdentifier=abc123xyz&guardrailVersion=DRAFT
```

**applyGuardrail**: Standalone operation to validate content against a guardrail without invoking a model

```none
aws-bedrock://label?operation=applyGuardrail&guardrailIdentifier=abc123xyz
    &guardrailVersion=DRAFT
```

#### Guardrails Response Headers

When using guardrails, the following headers may be set in the response:

-   `CamelAwsBedrockGuardrailTrace`: Trace information from guardrail evaluation (when trace is enabled)
    
-   `CamelAwsBedrockGuardrailOutput`: Output content blocks from applyGuardrail
    
-   `CamelAwsBedrockGuardrailAssessments`: Detailed assessments from applyGuardrail
    
-   `CamelAwsBedrockGuardrailUsage`: Token usage for guardrail evaluation
    

#### Creating a Guardrail in AWS

Before using guardrails, you need to create and configure one in the AWS Bedrock console:

1.  Navigate to AWS Bedrock Console → Guardrails
    
2.  Click "Create guardrail"
    
3.  Configure filters:
    
    -   **Content filters**: Block harmful content (hate, violence, sexual, etc.)
        
    -   **Denied topics**: Block specific topics you define
        
    -   **Word filters**: Block or mask custom words/phrases
        
    -   **PII filters**: Detect and redact personally identifiable information
        
    
4.  Save and note your Guardrail ID (e.g., `abc123xyz`)
    

#### Supported Models for Guardrails

Guardrails work with all models that support the Converse API:

-   Anthropic Claude 3 family (Haiku, Sonnet, Opus)
    
-   Anthropic Claude 3.5 family (Sonnet v2, Haiku)
    
-   Amazon Nova family (Micro, Lite, Pro)
    
-   Meta Llama 3.x models
    
-   Mistral AI models
    
-   Cohere Command R models
    

## Sub-Pages

For more details on specific features, see:

-   [Supported Models](others/aws-bedrock-models.md) - Complete list of supported AWS Bedrock models with JSON request schemas
    
-   [Examples](others/aws-bedrock-examples.md) - Producer examples for text, image, embeddings, streaming, conversation, and guardrails
    

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws-bedrock</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.