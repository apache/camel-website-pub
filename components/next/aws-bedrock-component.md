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

The AWS Bedrock component supports 29 options, which are listed below.

   
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

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (25 parameters)

   
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

The AWS Bedrock component supports 23 message header(s), which is/are listed below:

   
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

### Supported AWS Bedrock Models

-   Titan Text Express V1 with id `amazon.titan-text-express-v1` Express is a large language model for text generation. It is useful for a wide range of advanced, general language tasks such as open-ended text generation and conversational chat, as well as support within Retrieval Augmented Generation (RAG).
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "inputText": {
      "type": "string"
    },
    "textGenerationConfig": {
      "type": "object",
      "properties": {
        "maxTokenCount": {
          "type": "integer"
        },
        "stopSequences": {
          "type": "array",
          "items": [
            {
              "type": "string"
            }
          ]
        },
        "temperature": {
          "type": "integer"
        },
        "topP": {
          "type": "integer"
        }
      },
      "required": [
        "maxTokenCount",
        "stopSequences",
        "temperature",
        "topP"
      ]
    }
  },
  "required": [
    "inputText",
    "textGenerationConfig"
  ]
}
```

-   Titan Text Lite V1 with id `amazon.titan-text-lite-v1` Lite is a light weight efficient model, ideal for fine-tuning of English-language tasks.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "inputText": {
      "type": "string"
    },
    "textGenerationConfig": {
      "type": "object",
      "properties": {
        "maxTokenCount": {
          "type": "integer"
        },
        "stopSequences": {
          "type": "array",
          "items": [
            {
              "type": "string"
            }
          ]
        },
        "temperature": {
          "type": "integer"
        },
        "topP": {
          "type": "integer"
        }
      },
      "required": [
        "maxTokenCount",
        "stopSequences",
        "temperature",
        "topP"
      ]
    }
  },
  "required": [
    "inputText",
    "textGenerationConfig"
  ]
}
```

-   Titan Image Generator G1 with id `amazon.titan-image-generator-v1` It generates images from text, and allows users to upload and edit an existing image. Users can edit an image with a text prompt (without a mask) or parts of an image with an image mask. You can extend the boundaries of an image with outpainting, and fill in an image with inpainting.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "textToImageParams": {
      "type": "object",
      "properties": {
        "text": {
          "type": "string"
        },
        "negativeText": {
          "type": "string"
        }
      },
      "required": [
        "text",
        "negativeText"
      ]
    },
    "taskType": {
      "type": "string"
    },
    "imageGenerationConfig": {
      "type": "object",
      "properties": {
        "cfgScale": {
          "type": "integer"
        },
        "seed": {
          "type": "integer"
        },
        "quality": {
          "type": "string"
        },
        "width": {
          "type": "integer"
        },
        "height": {
          "type": "integer"
        },
        "numberOfImages": {
          "type": "integer"
        }
      },
      "required": [
        "cfgScale",
        "seed",
        "quality",
        "width",
        "height",
        "numberOfImages"
      ]
    }
  },
  "required": [
    "textToImageParams",
    "taskType",
    "imageGenerationConfig"
  ]
}
```

-   Titan Embeddings G1 with id `amazon.titan-embed-text-v1` The Amazon Titan Embeddings G1 - Text – Text v1.2 can intake up to 8k tokens and outputs a vector of 1,536 dimensions. The model also works in 25+ different language
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "inputText": {
      "type": "string"
    }
  },
  "required": [
    "inputText"
  ]
}
```

-   Jurassic2-Ultra with id `ai21.j2-ultra-v1` Jurassic-2 Ultra is AI21’s most powerful model for complex tasks that require advanced text generation and comprehension.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "prompt": {
      "type": "string"
    },
    "maxTokens": {
      "type": "integer"
    },
    "temperature": {
      "type": "integer"
    },
    "topP": {
      "type": "integer"
    },
    "stopSequences": {
      "type": "array",
      "items": [
        {
          "type": "string"
        }
      ]
    },
    "presencePenalty": {
      "type": "object",
      "properties": {
        "scale": {
          "type": "integer"
        }
      },
      "required": [
        "scale"
      ]
    },
    "frequencyPenalty": {
      "type": "object",
      "properties": {
        "scale": {
          "type": "integer"
        }
      },
      "required": [
        "scale"
      ]
    }
  },
  "required": [
    "prompt",
    "maxTokens",
    "temperature",
    "topP",
    "stopSequences",
    "presencePenalty",
    "frequencyPenalty"
  ]
}
```

-   Jurassic2-Mid with id `ai21.j2-mid-v1` Jurassic-2 Mid is less powerful than Ultra, yet carefully designed to strike the right balance between exceptional quality and affordability.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "prompt": {
      "type": "string"
    },
    "maxTokens": {
      "type": "integer"
    },
    "temperature": {
      "type": "integer"
    },
    "topP": {
      "type": "integer"
    },
    "stopSequences": {
      "type": "array",
      "items": [
        {
          "type": "string"
        }
      ]
    },
    "presencePenalty": {
      "type": "object",
      "properties": {
        "scale": {
          "type": "integer"
        }
      },
      "required": [
        "scale"
      ]
    },
    "frequencyPenalty": {
      "type": "object",
      "properties": {
        "scale": {
          "type": "integer"
        }
      },
      "required": [
        "scale"
      ]
    }
  },
  "required": [
    "prompt",
    "maxTokens",
    "temperature",
    "topP",
    "stopSequences",
    "presencePenalty",
    "frequencyPenalty"
  ]
}
```

-   Claude Instant V1.2 with id `anthropic.claude-instant-v1` A fast, affordable yet still very capable model, which can handle a range of tasks including casual dialogue, text analysis, summarization, and document question-answering.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "prompt": {
      "type": "string"
    },
    "max_tokens_to_sample": {
      "type": "integer"
    },
    "stop_sequences": {
      "type": "array",
      "items": [
        {
          "type": "string"
        }
      ]
    },
    "temperature": {
      "type": "number"
    },
    "top_p": {
      "type": "integer"
    },
    "top_k": {
      "type": "integer"
    },
    "anthropic_version": {
      "type": "string"
    }
  },
  "required": [
    "prompt",
    "max_tokens_to_sample",
    "stop_sequences",
    "temperature",
    "top_p",
    "top_k",
    "anthropic_version"
  ]
}
```

-   Claude 2 with id `anthropic.claude-v2` Anthropic’s highly capable model across a wide range of tasks from sophisticated dialogue and creative content generation to detailed instruction following.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "prompt": {
      "type": "string"
    },
    "max_tokens_to_sample": {
      "type": "integer"
    },
    "stop_sequences": {
      "type": "array",
      "items": [
        {
          "type": "string"
        }
      ]
    },
    "temperature": {
      "type": "number"
    },
    "top_p": {
      "type": "integer"
    },
    "top_k": {
      "type": "integer"
    },
    "anthropic_version": {
      "type": "string"
    }
  },
  "required": [
    "prompt",
    "max_tokens_to_sample",
    "stop_sequences",
    "temperature",
    "top_p",
    "top_k",
    "anthropic_version"
  ]
}
```

-   Claude 2.1 with id `anthropic.claude-v2:1` An update to Claude 2 that features double the context window, plus improvements across reliability, hallucination rates, and evidence-based accuracy in long document and RAG contexts.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "prompt": {
      "type": "string"
    },
    "max_tokens_to_sample": {
      "type": "integer"
    },
    "stop_sequences": {
      "type": "array",
      "items": [
        {
          "type": "string"
        }
      ]
    },
    "temperature": {
      "type": "number"
    },
    "top_p": {
      "type": "integer"
    },
    "top_k": {
      "type": "integer"
    },
    "anthropic_version": {
      "type": "string"
    }
  },
  "required": [
    "prompt",
    "max_tokens_to_sample",
    "stop_sequences",
    "temperature",
    "top_p",
    "top_k",
    "anthropic_version"
  ]
}
```

-   Claude 3 Sonnet with id `anthropic.claude-3-sonnet-20240229-v1:0` Claude 3 Sonnet by Anthropic strikes the ideal balance between intelligence and speed—particularly for enterprise workloads.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "messages": {
      "type": "array",
      "items": [
        {
          "type": "object",
          "properties": {
            "role": {
              "type": "string"
            },
            "content": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "type": {
                      "type": "string"
                    },
                    "text": {
                      "type": "string"
                    }
                  },
                  "required": [
                    "type",
                    "text"
                  ]
                }
              ]
            }
          },
          "required": [
            "role",
            "content"
          ]
        }
      ]
    },
    "max_tokens": {
      "type": "integer"
    },
    "anthropic_version": {
      "type": "string"
    }
  },
  "required": [
    "messages",
    "max_tokens",
    "anthropic_version"
  ]
}
```

-   Claude 3 Haiku with id `anthropic.claude-3-haiku-20240307-v1:0` Claude 3 Haiku is Anthropic’s fastest, most compact model for near-instant responsiveness. It answers simple queries and requests with speed.
    

Json schema for request

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "messages": {
      "type": "array",
      "items": [
        {
          "type": "object",
          "properties": {
            "role": {
              "type": "string"
            },
            "content": {
              "type": "array",
              "items": [
                {
                  "type": "object",
                  "properties": {
                    "type": {
                      "type": "string"
                    },
                    "text": {
                      "type": "string"
                    }
                  },
                  "required": [
                    "type",
                    "text"
                  ]
                }
              ]
            }
          },
          "required": [
            "role",
            "content"
          ]
        }
      ]
    },
    "max_tokens": {
      "type": "integer"
    },
    "anthropic_version": {
      "type": "string"
    }
  },
  "required": [
    "messages",
    "max_tokens",
    "anthropic_version"
  ]
}
```

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
    

## Examples

### Producer Examples

-   invokeTextModel: this operation will invoke a model from Bedrock. This is an example for both Titan Express and Titan Lite.
    

```java
from("direct:invoke")
    .to("aws-bedrock://test?bedrockRuntimeClient=#amazonBedrockRuntimeClient&operation=invokeTextModel&modelId="
                            + BedrockModels.TITAN_TEXT_EXPRESS_V1.model))
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:invoke", exchange -> {
            ObjectMapper mapper = new ObjectMapper();
            ObjectNode rootNode = mapper.createObjectNode();
            rootNode.put("inputText",
                    "User: Generate synthetic data for daily product sales in various categories - include row number, product name, category, date of sale and price. Produce output in JSON format. Count records and ensure there are no more than 5.");

            ArrayNode stopSequences = mapper.createArrayNode();
            stopSequences.add("User:");
            ObjectNode childNode = mapper.createObjectNode();
            childNode.put("maxTokenCount", 1024);
            childNode.put("stopSequences", stopSequences);
            childNode.put("temperature", 0).put("topP", 1);

            rootNode.put("textGenerationConfig", childNode);
            exchange.getMessage().setBody(mapper.writer().writeValueAsString(rootNode));
            exchange.getMessage().setHeader(BedrockConstants.MODEL_CONTENT_TYPE, "application/json");
            exchange.getMessage().setHeader(BedrockConstants.MODEL_ACCEPT_CONTENT_TYPE, "application/json");
        });
```

where template is a ProducerTemplate.

-   invokeImageModel: this operation will invoke a model from Bedrock. This is an example for both Titan Express and Titan Lite.
    

```java
from("direct:invoke")
    .to("aws-bedrock://test?bedrockRuntimeClient=#amazonBedrockRuntimeClient&operation=invokeImageModel&modelId="
                            + BedrockModels.TITAN_IMAGE_GENERATOR_V1.model))
                        .split(body())
                        .unmarshal().base64()
                        .setHeader("CamelFileName", simple("image-${random(128)}.png")).to("file:target/generated_images")
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:send_titan_image", exchange -> {
            ObjectMapper mapper = new ObjectMapper();
            ObjectNode rootNode = mapper.createObjectNode();
            ObjectNode textParameter = mapper.createObjectNode();
            textParameter.putIfAbsent("text",
                    new TextNode("A Sci-fi camel running in the desert"));
            rootNode.putIfAbsent("textToImageParams", textParameter);
            rootNode.putIfAbsent("taskType", new TextNode("TEXT_IMAGE"));
            ObjectNode childNode = mapper.createObjectNode();
            childNode.putIfAbsent("numberOfImages", new IntNode(3));
            childNode.putIfAbsent("quality", new TextNode("standard"));
            childNode.putIfAbsent("cfgScale", new IntNode(8));
            childNode.putIfAbsent("height", new IntNode(512));
            childNode.putIfAbsent("width", new IntNode(512));
            childNode.putIfAbsent("seed", new IntNode(0));

            rootNode.putIfAbsent("imageGenerationConfig", childNode);

            exchange.getMessage().setBody(mapper.writer().writeValueAsString(rootNode));
            exchange.getMessage().setHeader(BedrockConstants.MODEL_CONTENT_TYPE, "application/json");
            exchange.getMessage().setHeader(BedrockConstants.MODEL_ACCEPT_CONTENT_TYPE, "application/json");
        });
```

where template is a ProducerTemplate.

-   invokeEmbeddingsModel: this operation will invoke an Embeddings model from Bedrock. This is an example for Titan Embeddings G1.
    

```java
from("direct:send_titan_embeddings")
    .to("aws-bedrock:label?useDefaultCredentialsProvider=true&region=us-east-1&operation=invokeEmbeddingsModel&modelId="
    + BedrockModels.TITAN_EMBEDDINGS_G1.model)
    .to(result);
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:send_titan_embeddings", exchange -> {
            ObjectMapper mapper = new ObjectMapper();
            ObjectNode rootNode = mapper.createObjectNode();
            rootNode.putIfAbsent("inputText",
                    new TextNode("A Sci-fi camel running in the desert"));

            exchange.getMessage().setBody(mapper.writer().writeValueAsString(rootNode));
            exchange.getMessage().setHeader(BedrockConstants.MODEL_CONTENT_TYPE, "application/json");
            exchange.getMessage().setHeader(BedrockConstants.MODEL_ACCEPT_CONTENT_TYPE, "*/*");
        });
```

where template is a ProducerTemplate.

-   invokeTextModelStreaming (Complete Mode): this operation will invoke a model from Bedrock with streaming, accumulating the complete response.
    

```java
from("direct:stream_complete")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=invokeTextModelStreaming&modelId=" + BedrockModels.TITAN_TEXT_EXPRESS_V1.model
        + "&streamOutputMode=complete")
    .to("log:response");
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:stream_complete", exchange -> {
            ObjectMapper mapper = new ObjectMapper();
            ObjectNode rootNode = mapper.createObjectNode();
            rootNode.put("inputText", "Write a short poem about Apache Camel.");

            ArrayNode stopSequences = mapper.createArrayNode();
            stopSequences.add("User:");
            ObjectNode childNode = mapper.createObjectNode();
            childNode.put("maxTokenCount", 512);
            childNode.put("stopSequences", stopSequences);
            childNode.put("temperature", 0).put("topP", 1);

            rootNode.put("textGenerationConfig", childNode);
            exchange.getMessage().setBody(mapper.writer().writeValueAsString(rootNode));
            exchange.getMessage().setHeader(BedrockConstants.MODEL_CONTENT_TYPE, "application/json");
            exchange.getMessage().setHeader(BedrockConstants.MODEL_ACCEPT_CONTENT_TYPE, "application/json");
        });

        // Get the complete response
        String response = result.getMessage().getBody(String.class);

        // Get streaming metadata
        Integer tokenCount = result.getMessage().getHeader(BedrockConstants.STREAMING_TOKEN_COUNT, Integer.class);
        String completionReason = result.getMessage().getHeader(BedrockConstants.STREAMING_COMPLETION_REASON, String.class);
        Integer chunkCount = result.getMessage().getHeader(BedrockConstants.STREAMING_CHUNK_COUNT, Integer.class);
```

-   invokeTextModelStreaming (Chunks Mode): this operation will invoke a model from Bedrock with streaming, emitting individual chunks.
    

```java
from("direct:stream_chunks")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=invokeTextModelStreaming&modelId=" + BedrockModels.ANTROPHIC_CLAUDE_V35_2.model
        + "&streamOutputMode=chunks")
    .split(body())
        .to("websocket:chat-output");  // Send each chunk to websocket
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:stream_chunks", exchange -> {
            ObjectMapper mapper = new ObjectMapper();
            ObjectNode rootNode = mapper.createObjectNode();

            ArrayNode messages = mapper.createArrayNode();
            ObjectNode message = mapper.createObjectNode();
            message.put("role", "user");

            ArrayNode content = mapper.createArrayNode();
            ObjectNode contentBlock = mapper.createObjectNode();
            contentBlock.put("type", "text");
            contentBlock.put("text", "Explain Apache Camel in one sentence.");
            content.add(contentBlock);

            message.put("content", content);
            messages.add(message);

            rootNode.put("messages", messages);
            rootNode.put("max_tokens", 200);
            rootNode.put("anthropic_version", "bedrock-2023-05-31");

            exchange.getMessage().setBody(mapper.writer().writeValueAsString(rootNode));
            exchange.getMessage().setHeader(BedrockConstants.MODEL_CONTENT_TYPE, "application/json");
            exchange.getMessage().setHeader(BedrockConstants.MODEL_ACCEPT_CONTENT_TYPE, "application/json");
        });

        // Get the list of chunks
        List<String> chunks = result.getMessage().getBody(List.class);

        // Process each chunk
        for (String chunk : chunks) {
            System.out.println("Chunk: " + chunk);
        }
```

-   converse: this operation uses the unified Converse API for model-agnostic conversations.
    

```java
from("direct:converse")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=converse&modelId=" + BedrockModels.ANTROPHIC_CLAUDE_V3.model)
    .to("log:response");
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:converse", exchange -> {
            // Create a conversation message
            List<software.amazon.awssdk.services.bedrockruntime.model.Message> messages = new ArrayList<>();
            messages.add(software.amazon.awssdk.services.bedrockruntime.model.Message.builder()
                    .role(software.amazon.awssdk.services.bedrockruntime.model.ConversationRole.USER)
                    .content(software.amazon.awssdk.services.bedrockruntime.model.ContentBlock
                            .fromText("What is Apache Camel and what are its main features?"))
                    .build());

            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_MESSAGES, messages);

            // Optional: Add inference configuration
            software.amazon.awssdk.services.bedrockruntime.model.InferenceConfiguration inferenceConfig
                    = software.amazon.awssdk.services.bedrockruntime.model.InferenceConfiguration.builder()
                            .maxTokens(500)
                            .temperature(0.7f)
                            .build();
            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_INFERENCE_CONFIG, inferenceConfig);

            // Optional: Add system prompt
            List<software.amazon.awssdk.services.bedrockruntime.model.SystemContentBlock> systemPrompt = new ArrayList<>();
            systemPrompt.add(software.amazon.awssdk.services.bedrockruntime.model.SystemContentBlock
                    .fromText("You are a helpful assistant that explains software concepts clearly and concisely."));
            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_SYSTEM, systemPrompt);
        });

        // Get the response text
        String response = result.getMessage().getBody(String.class);

        // Get metadata from headers
        String stopReason = result.getMessage().getHeader(BedrockConstants.CONVERSE_STOP_REASON, String.class);
        software.amazon.awssdk.services.bedrockruntime.model.TokenUsage usage
                = result.getMessage().getHeader(BedrockConstants.CONVERSE_USAGE,
                        software.amazon.awssdk.services.bedrockruntime.model.TokenUsage.class);

        System.out.println("Response: " + response);
        System.out.println("Stop reason: " + stopReason);
        System.out.println("Input tokens: " + usage.inputTokens());
        System.out.println("Output tokens: " + usage.outputTokens());
```

-   converseStream (Complete Mode): this operation uses the Converse API with streaming, accumulating the complete response.
    

```java
from("direct:converse_stream")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=converseStream&modelId=" + BedrockModels.ANTROPHIC_CLAUDE_V3.model)
    .to("log:response");
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:converse_stream", exchange -> {
            // Create a conversation message
            List<software.amazon.awssdk.services.bedrockruntime.model.Message> messages = new ArrayList<>();
            messages.add(software.amazon.awssdk.services.bedrockruntime.model.Message.builder()
                    .role(software.amazon.awssdk.services.bedrockruntime.model.ConversationRole.USER)
                    .content(software.amazon.awssdk.services.bedrockruntime.model.ContentBlock
                            .fromText("Explain the Enterprise Integration Patterns in three sentences."))
                    .build());

            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_MESSAGES, messages);
            exchange.getMessage().setHeader(BedrockConstants.STREAM_OUTPUT_MODE, "complete");

            // Optional: Add inference configuration
            software.amazon.awssdk.services.bedrockruntime.model.InferenceConfiguration inferenceConfig
                    = software.amazon.awssdk.services.bedrockruntime.model.InferenceConfiguration.builder()
                            .maxTokens(300)
                            .temperature(0.5f)
                            .build();
            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_INFERENCE_CONFIG, inferenceConfig);
        });

        // Get the complete streamed response
        String response = result.getMessage().getBody(String.class);
        Integer chunkCount = result.getMessage().getHeader(BedrockConstants.STREAMING_CHUNK_COUNT, Integer.class);

        System.out.println("Response: " + response);
        System.out.println("Received " + chunkCount + " chunks");
```

-   converseStream (Chunks Mode): this operation uses the Converse API with streaming, emitting individual chunks.
    

```java
from("direct:converse_stream_chunks")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=converseStream&modelId=" + BedrockModels.ANTROPHIC_CLAUDE_V3.model)
    .split(body())
        .to("websocket:chat-output");  // Send each chunk to websocket
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:converse_stream_chunks", exchange -> {
            // Create a conversation message
            List<software.amazon.awssdk.services.bedrockruntime.model.Message> messages = new ArrayList<>();
            messages.add(software.amazon.awssdk.services.bedrockruntime.model.Message.builder()
                    .role(software.amazon.awssdk.services.bedrockruntime.model.ConversationRole.USER)
                    .content(software.amazon.awssdk.services.bedrockruntime.model.ContentBlock
                            .fromText("Write a haiku about software integration."))
                    .build());

            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_MESSAGES, messages);
            exchange.getMessage().setHeader(BedrockConstants.STREAM_OUTPUT_MODE, "chunks");
        });

        // Get the list of chunks
        List<String> chunks = result.getMessage().getBody(List.class);

        // Process each chunk as it was received
        for (String chunk : chunks) {
            System.out.println("Chunk: " + chunk);
        }
```

-   Multi-turn Conversation with Converse API: demonstrates maintaining conversation history.
    

```java
from("direct:conversation")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=converse&modelId=" + BedrockModels.ANTROPHIC_CLAUDE_V3.model)
    .to("log:response");
```

and you can then send to the direct endpoint something like

```java
        // Maintain conversation history
        List<software.amazon.awssdk.services.bedrockruntime.model.Message> conversationHistory = new ArrayList<>();

        // First turn
        conversationHistory.add(software.amazon.awssdk.services.bedrockruntime.model.Message.builder()
                .role(software.amazon.awssdk.services.bedrockruntime.model.ConversationRole.USER)
                .content(software.amazon.awssdk.services.bedrockruntime.model.ContentBlock
                        .fromText("What is Apache Camel?"))
                .build());

        Exchange result1 = template.send("direct:conversation", exchange -> {
            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_MESSAGES,
                    new ArrayList<>(conversationHistory));
        });

        // Add assistant's response to history
        software.amazon.awssdk.services.bedrockruntime.model.Message assistantMessage
                = result1.getMessage().getHeader(BedrockConstants.CONVERSE_OUTPUT_MESSAGE,
                        software.amazon.awssdk.services.bedrockruntime.model.Message.class);
        conversationHistory.add(assistantMessage);

        // Second turn - follow-up question
        conversationHistory.add(software.amazon.awssdk.services.bedrockruntime.model.Message.builder()
                .role(software.amazon.awssdk.services.bedrockruntime.model.ConversationRole.USER)
                .content(software.amazon.awssdk.services.bedrockruntime.model.ContentBlock
                        .fromText("Can you give me a simple example?"))
                .build());

        Exchange result2 = template.send("direct:conversation", exchange -> {
            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_MESSAGES,
                    new ArrayList<>(conversationHistory));
        });

        String followUpResponse = result2.getMessage().getBody(String.class);
        System.out.println("Follow-up response: " + followUpResponse);
```

### Guardrails Examples

-   Converse with Guardrails (Endpoint Configuration): Apply guardrails configured at the endpoint level.
    

```java
from("direct:converse_with_guardrails")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=converse&modelId=" + BedrockModels.ANTROPHIC_CLAUDE_V3.model
        + "&guardrailIdentifier=abc123xyz&guardrailVersion=DRAFT&guardrailTrace=true")
    .to("log:response");
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:converse_with_guardrails", exchange -> {
            // Create a conversation message
            List<software.amazon.awssdk.services.bedrockruntime.model.Message> messages = new ArrayList<>();
            messages.add(software.amazon.awssdk.services.bedrockruntime.model.Message.builder()
                    .role(software.amazon.awssdk.services.bedrockruntime.model.ConversationRole.USER)
                    .content(software.amazon.awssdk.services.bedrockruntime.model.ContentBlock
                            .fromText("Tell me about Paris"))
                    .build());

            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_MESSAGES, messages);

            // Optional: Add inference configuration
            software.amazon.awssdk.services.bedrockruntime.model.InferenceConfiguration inferenceConfig
                    = software.amazon.awssdk.services.bedrockruntime.model.InferenceConfiguration.builder()
                            .maxTokens(200)
                            .temperature(0.7f)
                            .build();
            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_INFERENCE_CONFIG, inferenceConfig);
        });

        // Get the response
        String response = result.getMessage().getBody(String.class);

        // Check if guardrail trace is available
        software.amazon.awssdk.services.bedrockruntime.model.GuardrailTrace trace
                = result.getMessage().getHeader(BedrockConstants.GUARDRAIL_TRACE,
                        software.amazon.awssdk.services.bedrockruntime.model.GuardrailTrace.class);

        if (trace != null) {
            System.out.println("Guardrail evaluation: " + trace);
        }
```

-   Converse with Guardrails (Header Configuration): Apply guardrails configured per-message via headers.
    

```java
from("direct:converse_dynamic_guardrails")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=converse&modelId=" + BedrockModels.ANTROPHIC_CLAUDE_V3.model)
    .to("log:response");
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:converse_dynamic_guardrails", exchange -> {
            // Create a conversation message
            List<software.amazon.awssdk.services.bedrockruntime.model.Message> messages = new ArrayList<>();
            messages.add(software.amazon.awssdk.services.bedrockruntime.model.Message.builder()
                    .role(software.amazon.awssdk.services.bedrockruntime.model.ConversationRole.USER)
                    .content(software.amazon.awssdk.services.bedrockruntime.model.ContentBlock
                            .fromText("What is the capital of France?"))
                    .build());

            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_MESSAGES, messages);

            // Configure guardrail via header (can be dynamic per message)
            software.amazon.awssdk.services.bedrockruntime.model.GuardrailConfiguration guardrailConfig
                    = software.amazon.awssdk.services.bedrockruntime.model.GuardrailConfiguration.builder()
                            .guardrailIdentifier("abc123xyz")  // Can be determined at runtime
                            .guardrailVersion("DRAFT")
                            .trace(software.amazon.awssdk.services.bedrockruntime.model.GuardrailTrace.ENABLED)
                            .build();
            exchange.getMessage().setHeader(BedrockConstants.GUARDRAIL_CONFIG, guardrailConfig);
        });

        String response = result.getMessage().getBody(String.class);
        System.out.println("Protected response: " + response);
```

-   Converse Stream with Guardrails: Apply guardrails to streaming conversations.
    

```java
from("direct:stream_with_guardrails")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=converseStream&modelId=" + BedrockModels.ANTROPHIC_CLAUDE_V3.model
        + "&guardrailIdentifier=abc123xyz&guardrailVersion=DRAFT")
    .to("log:response");
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:stream_with_guardrails", exchange -> {
            List<software.amazon.awssdk.services.bedrockruntime.model.Message> messages = new ArrayList<>();
            messages.add(software.amazon.awssdk.services.bedrockruntime.model.Message.builder()
                    .role(software.amazon.awssdk.services.bedrockruntime.model.ConversationRole.USER)
                    .content(software.amazon.awssdk.services.bedrockruntime.model.ContentBlock
                            .fromText("Tell me a story about space exploration"))
                    .build());

            exchange.getMessage().setHeader(BedrockConstants.CONVERSE_MESSAGES, messages);
            exchange.getMessage().setHeader(BedrockConstants.STREAM_OUTPUT_MODE, "complete");
        });

        String streamedResponse = result.getMessage().getBody(String.class);
        System.out.println("Guardrail-protected stream response: " + streamedResponse);
```

-   Apply Guardrail: Validate content against a guardrail without invoking a model.
    

```java
from("direct:validate_content")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=applyGuardrail&guardrailIdentifier=abc123xyz&guardrailVersion=DRAFT")
    .to("log:validation_result");
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:validate_content", exchange -> {
            // Create content blocks to check
            List<software.amazon.awssdk.services.bedrockruntime.model.GuardrailContentBlock> content
                    = new ArrayList<>();
            content.add(software.amazon.awssdk.services.bedrockruntime.model.GuardrailContentBlock.builder()
                    .text(software.amazon.awssdk.services.bedrockruntime.model.GuardrailTextBlock.builder()
                            .text("This is the content I want to validate before sending to the model.")
                            .build())
                    .build());

            exchange.getMessage().setHeader(BedrockConstants.GUARDRAIL_CONTENT, content);
            exchange.getMessage().setHeader(BedrockConstants.GUARDRAIL_SOURCE, "INPUT");
        });

        // Get the action result (GUARDRAIL_INTERVENED or NONE)
        String action = result.getMessage().getBody(String.class);

        if ("GUARDRAIL_INTERVENED".equals(action)) {
            System.out.println("Content was blocked by guardrail!");

            // Get the assessments to see why it was blocked
            List<?> assessments = result.getMessage().getHeader(BedrockConstants.GUARDRAIL_ASSESSMENTS, List.class);
            System.out.println("Reasons: " + assessments);

            // Get the filtered output
            List<?> outputs = result.getMessage().getHeader(BedrockConstants.GUARDRAIL_OUTPUT, List.class);
            System.out.println("Filtered content: " + outputs);
        } else {
            System.out.println("Content passed guardrail validation");
        }
```

-   Apply Guardrail with POJO Request: Use the SDK request object directly for maximum control.
    

```java
from("direct:validate_pojo")
    .to("aws-bedrock://test?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=applyGuardrail&pojoRequest=true")
    .to("log:validation_result");
```

and you can then send to the direct endpoint something like

```java
        final Exchange result = template.send("direct:validate_pojo", exchange -> {
            // Create content blocks
            List<software.amazon.awssdk.services.bedrockruntime.model.GuardrailContentBlock> content
                    = new ArrayList<>();
            content.add(software.amazon.awssdk.services.bedrockruntime.model.GuardrailContentBlock.builder()
                    .text(software.amazon.awssdk.services.bedrockruntime.model.GuardrailTextBlock.builder()
                            .text("User-generated content to validate")
                            .build())
                    .build());

            // Build the complete request object
            software.amazon.awssdk.services.bedrockruntime.model.ApplyGuardrailRequest request
                    = software.amazon.awssdk.services.bedrockruntime.model.ApplyGuardrailRequest.builder()
                            .guardrailIdentifier("abc123xyz")
                            .guardrailVersion("DRAFT")
                            .source(software.amazon.awssdk.services.bedrockruntime.model.GuardrailContentSource.INPUT)
                            .content(content)
                            .build();

            exchange.getMessage().setBody(request);
        });

        String action = result.getMessage().getBody(String.class);
        System.out.println("Validation result: " + action);
```

-   Content Moderation Pipeline: Combine guardrails with model invocation in a pipeline.
    

```java
from("direct:moderated_conversation")
    // First, validate input with guardrail
    .to("aws-bedrock://validate?useDefaultCredentialsProvider=true&region=us-east-1"
        + "&operation=applyGuardrail&guardrailIdentifier=abc123xyz")
    .choice()
        .when(simple("${body} == 'GUARDRAIL_INTERVENED'"))
            .log("Input blocked by guardrail")
            .setBody(constant("Sorry, I cannot process this request."))
        .otherwise()
            // Input passed, proceed with model invocation
            .to("aws-bedrock://converse?useDefaultCredentialsProvider=true&region=us-east-1"
                + "&operation=converse&modelId=" + BedrockModels.ANTROPHIC_CLAUDE_V3.model
                + "&guardrailIdentifier=abc123xyz")
            .log("Model response: ${body}")
    .end()
    .to("mock:result");
```

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

## Spring Boot Auto-Configuration

When using aws-bedrock with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws-bedrock-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 87 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws-bedrock-agent-runtime.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws-bedrock-agent-runtime.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws-bedrock-agent-runtime.bedrock-agent-runtime-async-client** | To use an existing configured AWS Bedrock Agent Runtime async client (required for invokeFlow which streams events back). The option is a software.amazon.awssdk.services.bedrockagentruntime.BedrockAgentRuntimeAsyncClient type. |  | BedrockAgentRuntimeAsyncClient |
| **camel.component.aws-bedrock-agent-runtime.bedrock-agent-runtime-client** | To use an existing configured AWS Bedrock Agent Runtime client. The option is a software.amazon.awssdk.services.bedrockagentruntime.BedrockAgentRuntimeClient type. |  | BedrockAgentRuntimeClient |
| **camel.component.aws-bedrock-agent-runtime.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.bedrock.agentruntime.BedrockAgentRuntimeConfiguration type. |  | BedrockAgentRuntimeConfiguration |
| **camel.component.aws-bedrock-agent-runtime.enable-trace** | Enables tracing for the invokeFlow operation. When enabled, the producer collects FlowTraceEvent entries and publishes them in the CamelAwsBedrockAgentRuntimeFlowTraces header. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.enabled** | Whether to enable auto configuration of the aws-bedrock-agent-runtime component. This is enabled by default. |  | Boolean |
| **camel.component.aws-bedrock-agent-runtime.flow-alias-identifier** | The unique identifier of the Bedrock flow alias to invoke (used by the invokeFlow operation). Can be overridden per exchange via the CamelAwsBedrockAgentRuntimeFlowAliasIdentifier header. |  | String |
| **camel.component.aws-bedrock-agent-runtime.flow-identifier** | The unique identifier of the Bedrock flow to invoke (used by the invokeFlow operation). Can be overridden per exchange via the CamelAwsBedrockAgentRuntimeFlowIdentifier header. |  | String |
| **camel.component.aws-bedrock-agent-runtime.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws-bedrock-agent-runtime.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws-bedrock-agent-runtime.knowledge-base-id** | Define the Knowledge Base Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent-runtime.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.model-id** | Define the model Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent-runtime.operation** | The operation to perform. |  | BedrockAgentRuntimeOperations |
| **camel.component.aws-bedrock-agent-runtime.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **camel.component.aws-bedrock-agent-runtime.proxy-host** | To define a proxy host when instantiating the Bedrock Agent Runtime client. |  | String |
| **camel.component.aws-bedrock-agent-runtime.proxy-port** | To define a proxy port when instantiating the Bedrock Agent Runtime client. |  | Integer |
| **camel.component.aws-bedrock-agent-runtime.proxy-protocol** | To define a proxy protocol when instantiating the Bedrock Agent Runtime client. | https | Protocol |
| **camel.component.aws-bedrock-agent-runtime.region** | The region in which Bedrock Agent Runtime client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws-bedrock-agent-runtime.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws-bedrock-agent-runtime.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws-bedrock-agent-runtime.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws-bedrock-agent-runtime.use-default-credentials-provider** | Set whether the Bedrock Agent Runtime client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.use-profile-credentials-provider** | Set whether the Bedrock Agent Runtime client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws-bedrock-agent-runtime.use-session-credentials** | Set whether the Bedrock Agent Runtime client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | Boolean |
| **camel.component.aws-bedrock-agent.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws-bedrock-agent.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws-bedrock-agent.bedrock-agent-client** | To use an existing configured AWS Bedrock Agent client. The option is a software.amazon.awssdk.services.bedrockagent.BedrockAgentClient type. |  | BedrockAgentClient |
| **camel.component.aws-bedrock-agent.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.aws-bedrock-agent.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.bedrock.agent.BedrockAgentConfiguration type. |  | BedrockAgentConfiguration |
| **camel.component.aws-bedrock-agent.data-source-id** | Define the Data source Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent.enabled** | Whether to enable auto configuration of the aws-bedrock-agent component. This is enabled by default. |  | Boolean |
| **camel.component.aws-bedrock-agent.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws-bedrock-agent.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws-bedrock-agent.ingestion-job-id** | Define the Ingestion Job Id we want to track. |  | String |
| **camel.component.aws-bedrock-agent.knowledge-base-id** | Define the Knowledge Base Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws-bedrock-agent.model-id** | Define the model Id we are going to use. |  | String |
| **camel.component.aws-bedrock-agent.operation** | The operation to perform. |  | BedrockAgentOperations |
| **camel.component.aws-bedrock-agent.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws-bedrock-agent.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws-bedrock-agent.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **camel.component.aws-bedrock-agent.proxy-host** | To define a proxy host when instantiating the Bedrock Agent client. |  | String |
| **camel.component.aws-bedrock-agent.proxy-port** | To define a proxy port when instantiating the Bedrock Agent client. |  | Integer |
| **camel.component.aws-bedrock-agent.proxy-protocol** | To define a proxy protocol when instantiating the Bedrock Agent client. | https | Protocol |
| **camel.component.aws-bedrock-agent.region** | The region in which Bedrock Agent client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws-bedrock-agent.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws-bedrock-agent.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws-bedrock-agent.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws-bedrock-agent.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws-bedrock-agent.use-default-credentials-provider** | Set whether the Bedrock Agent client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws-bedrock-agent.use-profile-credentials-provider** | Set whether the Bedrock Agent client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws-bedrock-agent.use-session-credentials** | Set whether the Bedrock Agent client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | Boolean |
| **camel.component.aws-bedrock.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws-bedrock.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws-bedrock.bedrock-runtime-async-client** | To use an existing configured AWS Bedrock Runtime Async client for streaming operations. The option is a software.amazon.awssdk.services.bedrockruntime.BedrockRuntimeAsyncClient type. |  | BedrockRuntimeAsyncClient |
| **camel.component.aws-bedrock.bedrock-runtime-client** | To use an existing configured AWS Bedrock Runtime client. The option is a software.amazon.awssdk.services.bedrockruntime.BedrockRuntimeClient type. |  | BedrockRuntimeClient |
| **camel.component.aws-bedrock.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.bedrock.runtime.BedrockConfiguration type. |  | BedrockConfiguration |
| **camel.component.aws-bedrock.enabled** | Whether to enable auto configuration of the aws-bedrock component. This is enabled by default. |  | Boolean |
| **camel.component.aws-bedrock.guardrail-identifier** | The identifier (ID or ARN) for the guardrail to apply to the model invocation. |  | String |
| **camel.component.aws-bedrock.guardrail-trace** | Whether to return trace information from the guardrail. | false | Boolean |
| **camel.component.aws-bedrock.guardrail-version** | The version of the guardrail to use. Defaults to DRAFT. | DRAFT | String |
| **camel.component.aws-bedrock.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws-bedrock.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws-bedrock.include-streaming-metadata** | Whether to include streaming metadata in the response headers (completion reason, token count, chunk count). | true | Boolean |
| **camel.component.aws-bedrock.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws-bedrock.model-id** | Define the model Id we are going to use. |  | String |
| **camel.component.aws-bedrock.operation** | The operation to perform. |  | BedrockOperations |
| **camel.component.aws-bedrock.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | Boolean |
| **camel.component.aws-bedrock.pojo-request** | If we want to use a POJO request as body or not. | false | Boolean |
| **camel.component.aws-bedrock.profile-credentials-name** | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **camel.component.aws-bedrock.proxy-host** | To define a proxy host when instantiating the Bedrock client. |  | String |
| **camel.component.aws-bedrock.proxy-port** | To define a proxy port when instantiating the Bedrock client. |  | Integer |
| **camel.component.aws-bedrock.proxy-protocol** | To define a proxy protocol when instantiating the Bedrock client. | https | Protocol |
| **camel.component.aws-bedrock.region** | The region in which Bedrock client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws-bedrock.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws-bedrock.session-token** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **camel.component.aws-bedrock.stream-output-mode** | The streaming output mode (complete or chunks). In complete mode, the full response is accumulated and returned as a single message. In chunks mode, each chunk is emitted as a separate exchange. | complete | String |
| **camel.component.aws-bedrock.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws-bedrock.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws-bedrock.use-default-credentials-provider** | Set whether the Bedrock client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws-bedrock.use-profile-credentials-provider** | Set whether the Bedrock client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws-bedrock.use-session-credentials** | Set whether the Bedrock client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | Boolean |