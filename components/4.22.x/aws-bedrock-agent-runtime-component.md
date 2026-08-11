# AWS Bedrock Agent Runtime

**Since Camel 4.5**

**Only producer is supported**

The AWS2 Bedrock component supports invoking a supported LLM model from [AWS Bedrock](https://aws.amazon.com/bedrock/) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Bedrock. More information is available at [Amazon Bedrock](https://aws.amazon.com/bedrock/).

## URI Format

aws-bedrock-agent-runtime://label\[?options\]

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

The AWS Bedrock Agent Runtime component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | BedrockAgentRuntimeConfiguration |
| **knowledgeBaseId** (producer) | **Required** Define the Knowledge Base Id we are going to use. |  | String |
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

-   retrieveAndGenerate
    
-   invokeFlow
    
-   invokeAgent
    
-   invokeInlineAgent
    
-   retrieve
    





 |  | BedrockAgentRuntimeOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (producer) | 

The region in which Bedrock Agent Runtime client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Bedrock Agent Runtime client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Bedrock Agent Runtime client should expect to load credentials through a profile credentials provider. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **bedrockAgentRuntimeAsyncClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Agent Runtime async client (required for invokeFlow which streams events back). |  | BedrockAgentRuntimeAsyncClient |
| **bedrockAgentRuntimeClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Agent Runtime client. |  | BedrockAgentRuntimeClient |
| **agentAliasId** (agent) | The unique identifier of the agent alias to invoke, used by the invokeAgent operation. |  | String |
| **agentId** (agent) | The unique identifier of the agent to invoke, used by the invokeAgent operation. |  | String |
| **enableTrace** (agent) | Enables tracing for the invokeFlow and agent operations. When enabled, the producer collects the trace events and publishes them in the CamelAwsBedrockAgentRuntimeFlowTraces or CamelAwsBedrockAgentRuntimeAgentTraces header. | false | boolean |
| **foundationModel** (agent) | The foundation model used by the invokeInlineAgent operation. |  | String |
| **instruction** (agent) | The instruction given to the agent defined by the invokeInlineAgent operation. |  | String |
| **sessionId** (agent) | The unique identifier of the agent session. Reuse the same value across invocations to continue the same conversation. When not set, a random session id is generated for each invocation. |  | String |
| **streamOutputMode** (agent) | 

The streaming output mode (complete or chunks) used by the agent operations. In complete mode the response chunks are accumulated and the body is the full text. In chunks mode the body is the list of chunks.

Enum values:

-   complete
    
-   chunks
    





 | complete | String |
| **flowAliasIdentifier** (flow) | The unique identifier of the Bedrock flow alias to invoke (used by the invokeFlow operation). Can be overridden per exchange via the CamelAwsBedrockAgentRuntimeFlowAliasIdentifier header. |  | String |
| **flowIdentifier** (flow) | The unique identifier of the Bedrock flow to invoke (used by the invokeFlow operation). Can be overridden per exchange via the CamelAwsBedrockAgentRuntimeFlowIdentifier header. |  | String |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Bedrock Agent Runtime client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Bedrock Agent Runtime client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Bedrock Agent Runtime client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Bedrock Agent Runtime client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | boolean |

## Endpoint Options

The AWS Bedrock Agent Runtime endpoint is configured using URI syntax:

aws-bedrock-agent-runtime:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **knowledgeBaseId** (producer) | **Required** Define the Knowledge Base Id we are going to use. |  | String |
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

-   retrieveAndGenerate
    
-   invokeFlow
    
-   invokeAgent
    
-   invokeInlineAgent
    
-   retrieve
    





 |  | BedrockAgentRuntimeOperations |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (producer) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (producer) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (producer) | 

The region in which Bedrock Agent Runtime client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the Bedrock Agent Runtime client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (producer) | Set whether the Bedrock Agent Runtime client should expect to load credentials through a profile credentials provider. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **bedrockAgentRuntimeAsyncClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Agent Runtime async client (required for invokeFlow which streams events back). |  | BedrockAgentRuntimeAsyncClient |
| **bedrockAgentRuntimeClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Agent Runtime client. |  | BedrockAgentRuntimeClient |
| **agentAliasId** (agent) | The unique identifier of the agent alias to invoke, used by the invokeAgent operation. |  | String |
| **agentId** (agent) | The unique identifier of the agent to invoke, used by the invokeAgent operation. |  | String |
| **enableTrace** (agent) | Enables tracing for the invokeFlow and agent operations. When enabled, the producer collects the trace events and publishes them in the CamelAwsBedrockAgentRuntimeFlowTraces or CamelAwsBedrockAgentRuntimeAgentTraces header. | false | boolean |
| **foundationModel** (agent) | The foundation model used by the invokeInlineAgent operation. |  | String |
| **instruction** (agent) | The instruction given to the agent defined by the invokeInlineAgent operation. |  | String |
| **sessionId** (agent) | The unique identifier of the agent session. Reuse the same value across invocations to continue the same conversation. When not set, a random session id is generated for each invocation. |  | String |
| **streamOutputMode** (agent) | 

The streaming output mode (complete or chunks) used by the agent operations. In complete mode the response chunks are accumulated and the body is the full text. In chunks mode the body is the list of chunks.

Enum values:

-   complete
    
-   chunks
    





 | complete | String |
| **flowAliasIdentifier** (flow) | The unique identifier of the Bedrock flow alias to invoke (used by the invokeFlow operation). Can be overridden per exchange via the CamelAwsBedrockAgentRuntimeFlowAliasIdentifier header. |  | String |
| **flowIdentifier** (flow) | The unique identifier of the Bedrock flow to invoke (used by the invokeFlow operation). Can be overridden per exchange via the CamelAwsBedrockAgentRuntimeFlowIdentifier header. |  | String |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Bedrock Agent Runtime client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Bedrock Agent Runtime client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Bedrock Agent Runtime client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Bedrock Agent Runtime client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | boolean |

## Message Headers

The AWS Bedrock Agent Runtime component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsBedrockAgentRuntimeOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsBedrockAgentRuntimeCitations** (producer) Constant: [`CITATIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#CITATIONS) | When retrieving and generating a response, this header will contain the citations. |  | String |
| **CamelAwsBedrockAgentRuntimeSessionId** (producer) Constant: [`SESSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#SESSION_ID) | When retrieving and generating a response, this header will contain he unique identifier of the session. Reuse the same value to continue the same session with the knowledge base. |  | String |
| **CamelAwsBedrockAgentRuntimeAgentId** (producer) Constant: [`AGENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_ID) | The unique identifier of the agent to invoke. Overrides the agentId configured on the endpoint. |  | String |
| **CamelAwsBedrockAgentRuntimeAgentAliasId** (producer) Constant: [`AGENT_ALIAS_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_ALIAS_ID) | The unique identifier of the agent alias to invoke. Overrides the agentAliasId configured on the endpoint. |  | String |
| **CamelAwsBedrockAgentRuntimeAgentEnableTrace** (producer) Constant: [`AGENT_ENABLE_TRACE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_ENABLE_TRACE) | Enables tracing for the agent invocation. When set, overrides the enableTrace option on the endpoint. |  | Boolean |
| **CamelAwsBedrockAgentRuntimeAgentEndSession** (producer) Constant: [`AGENT_END_SESSION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_END_SESSION) | Ends the agent session after this invocation. |  | Boolean |
| **CamelAwsBedrockAgentRuntimeAgentMemoryId** (producer) Constant: [`AGENT_MEMORY_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_MEMORY_ID) | The unique identifier of the agent memory to use across sessions. |  | String |
| **CamelAwsBedrockAgentRuntimeAgentStreamOutputMode** (producer) Constant: [`AGENT_STREAM_OUTPUT_MODE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_STREAM_OUTPUT_MODE) | The streaming output mode (complete or chunks) for an agent invocation. When set, overrides the streamOutputMode option on the endpoint. |  | String |
| **CamelAwsBedrockAgentRuntimeAgentFoundationModel** (producer) Constant: [`AGENT_FOUNDATION_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_FOUNDATION_MODEL) | The foundation model used by an inline agent. Overrides the foundationModel configured on the endpoint. |  | String |
| **CamelAwsBedrockAgentRuntimeAgentInstruction** (producer) Constant: [`AGENT_INSTRUCTION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_INSTRUCTION) | The instruction given to an inline agent. Overrides the instruction configured on the endpoint. |  | String |
| **CamelAwsBedrockAgentRuntimeAgentTraces** (producer) Constant: [`AGENT_TRACES`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_TRACES) | When invoking an agent with tracing enabled, this header will contain the list of TracePart emitted during the invocation. The elements are TracePart for invokeAgent and InlineAgentTracePart for invokeInlineAgent. |  | List |
| **CamelAwsBedrockAgentRuntimeAgentReturnControl** (producer) Constant: [`AGENT_RETURN_CONTROL`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_RETURN_CONTROL) | When an agent invocation requires the caller to fulfil an action, this header will contain the list of return-control payloads emitted by the agent. The elements are ReturnControlPayload for invokeAgent and InlineAgentReturnControlPayload for invokeInlineAgent. |  | List |
| **CamelAwsBedrockAgentRuntimeAgentFiles** (producer) Constant: [`AGENT_FILES`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#AGENT_FILES) | When an agent invocation returns files, this header will contain the files emitted by the agent. The elements are FilePart for invokeAgent and InlineAgentFilePart for invokeInlineAgent. |  | List |
| **CamelAwsBedrockAgentRuntimeFlowIdentifier** (producer) Constant: [`FLOW_IDENTIFIER`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_IDENTIFIER) | The unique identifier of the flow to invoke. Overrides the flowIdentifier configured on the endpoint. |  | String |
| **CamelAwsBedrockAgentRuntimeFlowAliasIdentifier** (producer) Constant: [`FLOW_ALIAS_IDENTIFIER`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_ALIAS_IDENTIFIER) | The unique identifier of the flow alias to invoke. Overrides the flowAliasIdentifier configured on the endpoint. |  | String |
| **CamelAwsBedrockAgentRuntimeFlowEnableTrace** (producer) Constant: [`FLOW_ENABLE_TRACE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_ENABLE_TRACE) | Enables tracing for the flow invocation. When set, overrides the enableTrace option on the endpoint. |  | Boolean |
| **CamelAwsBedrockAgentRuntimeFlowExecutionId** (producer) Constant: [`FLOW_EXECUTION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_EXECUTION_ID) | The unique identifier of an in-progress flow execution to continue. Used for multi-turn flow conversations. |  | String |
| **CamelAwsBedrockAgentRuntimeFlowOutputs** (producer) Constant: [`FLOW_OUTPUTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_OUTPUTS) | When invoking a flow, this header will contain the list of FlowOutputEvent emitted by the flow. |  | List |
| **CamelAwsBedrockAgentRuntimeFlowTraces** (producer) Constant: [`FLOW_TRACES`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_TRACES) | When invoking a flow with tracing enabled, this header will contain the list of FlowTraceEvent emitted during execution. |  | List |
| **CamelAwsBedrockAgentRuntimeFlowCompletionReason** (producer) Constant: [`FLOW_COMPLETION_REASON`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_COMPLETION_REASON) | When invoking a flow, this header will contain the reason the flow completed (set when a FlowCompletionEvent is received). |  | String |
| **CamelAwsBedrockAgentRuntimeRetrievedResults** (producer) Constant: [`RETRIEVED_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#RETRIEVED_RESULTS) | When performing a retrieve operation, this header will contain the list of KnowledgeBaseRetrievalResult chunks returned by the knowledge base. |  | List |
| **CamelAwsBedrockAgentRuntimeNumberOfResults** (producer) Constant: [`NUMBER_OF_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#NUMBER_OF_RESULTS) | Overrides the maximum number of results returned by the retrieve operation. Must be a positive Integer; when not set the AWS service default is used. |  | Integer |
| **CamelAwsBedrockAgentRuntimeSearchType** (producer) Constant: [`OVERRIDE_SEARCH_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#OVERRIDE_SEARCH_TYPE) | Overrides the search type used by the retrieve operation. Accepts the AWS SearchType enum (HYBRID, SEMANTIC) or its String representation. |  | String |
| **CamelAwsBedrockAgentRuntimeNextToken** (producer) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#NEXT_TOKEN) | Pagination token used by the retrieve operation. Set on the in-message to request the next page; set on the out-message when the response carries one. |  | String |
| **CamelAwsBedrockAgentRuntimeRetrieveGuardrailAction** (producer) Constant: [`RETRIEVE_GUARDRAIL_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#RETRIEVE_GUARDRAIL_ACTION) | When performing a retrieve operation, this header will contain the guardrail action (if any) applied by the knowledge base. |  | String |

Required Bedrock component options

You have to provide the bedrockRuntimeClient in the Registry or your accessKey and secretKey to access the [Amazon Bedrock](https://aws.amazon.com/bedrock/) service.

## Usage

### Supported operations

The component supports the following operations on the `operation` URI option:

-   `retrieveAndGenerate` — Query a Bedrock Knowledge Base and generate a grounded response from the selected model.
    
-   `retrieve` — Run a semantic search against a Bedrock Knowledge Base and return the matched chunks without LLM generation.
    
-   `invokeFlow` — Invoke a Bedrock Flow by id/alias and stream the resulting events back as Camel message headers.
    
-   `invokeAgent` — Invoke a deployed Bedrock Agent by id/alias and stream the response back.
    
-   `invokeInlineAgent` — Invoke an agent defined inline at invocation time (foundation model plus instruction).
    

### Retrieving from a Bedrock Knowledge Base

The `retrieve` operation performs a semantic search against a Bedrock Knowledge Base and returns the matching chunks without invoking an LLM. Use this when you want to plug retrieval into your own generation step, inspect retrieval quality, or build pagination on top of the knowledge base.

Mandatory options:

-   `knowledgeBaseId` — the id of the Bedrock Knowledge Base to query.
    

The body of the in-message must be a `String` containing the search query. When `pojoRequest=true`, the body must be a `RetrieveRequest` (any retrieval-config knobs in that POJO are honored verbatim).

The retrieval configuration can be tuned per exchange via the following headers:

-   `CamelAwsBedrockAgentRuntimeNumberOfResults` (Integer) — maximum number of chunks to return.
    
-   `CamelAwsBedrockAgentRuntimeSearchType` (String) — overrides the search type (`HYBRID` or `SEMANTIC`).
    
-   `CamelAwsBedrockAgentRuntimeNextToken` (String) — pagination token returned by a previous call.
    

The producer surfaces the matched chunks as the out-message body (a `List<KnowledgeBaseRetrievalResult>`) and on the following headers:

-   `CamelAwsBedrockAgentRuntimeRetrievedResults` — the same `List<KnowledgeBaseRetrievalResult>` available on the body.
    
-   `CamelAwsBedrockAgentRuntimeNextToken` — present when the response carries a pagination token.
    
-   `CamelAwsBedrockAgentRuntimeRetrieveGuardrailAction` — present when the knowledge base applies a guardrail action.
    

### Invoking a Bedrock Flow

The `invokeFlow` operation streams flow events using the AWS SDK async client; the producer transparently allocates a `BedrockAgentRuntimeAsyncClient` when the endpoint is configured with `operation=invokeFlow`.

Mandatory options:

-   `flowIdentifier` — the unique id of the flow to invoke (overridable via the `CamelAwsBedrockAgentRuntimeFlowIdentifier` header).
    
-   `flowAliasIdentifier` — the unique id of the flow alias to invoke (overridable via the `CamelAwsBedrockAgentRuntimeFlowAliasIdentifier` header).
    

Optional options:

-   `enableTrace` — when `true`, the producer collects the emitted ``FlowTraceEvent`s into the `CamelAwsBedrockAgentRuntimeFlowTraces`` header (overridable via `CamelAwsBedrockAgentRuntimeFlowEnableTrace`).
    

The body of the in-message can be:

-   a `String` — wrapped in a single `FlowInput` targeting node `FlowInputNode`, output `document`;
    
-   a `FlowInput` instance — used as the sole input to the flow;
    
-   a `List<FlowInput>` — passed verbatim to the request (use this form to chain multiple flow inputs).
    

When `pojoRequest=true`, the body must be an `InvokeFlowRequest` and is sent unchanged.

The producer collects emitted events into headers:

-   `CamelAwsBedrockAgentRuntimeFlowOutputs` — the list of \`FlowOutputEvent\`s emitted by the flow.
    
-   `CamelAwsBedrockAgentRuntimeFlowTraces` — the list of \`FlowTraceEvent\`s (only when tracing is enabled).
    
-   `CamelAwsBedrockAgentRuntimeFlowCompletionReason` — the completion reason reported by the flow (when present).
    

The out-message body is the document of the last `FlowOutputEvent` (decoded as `String` when the document is a string, otherwise the raw `Document`). When the flow emits no outputs, the body is left untouched.

### Invoking a Bedrock Agent

The `invokeAgent` operation invokes a deployed Bedrock Agent. Like `invokeFlow` it uses the AWS SDK async client, and the producer transparently allocates a `BedrockAgentRuntimeAsyncClient` when the endpoint is configured with `operation=invokeAgent`.

Mandatory options:

-   `agentId` — the unique id of the agent to invoke (overridable via the `CamelAwsBedrockAgentRuntimeAgentId` header).
    
-   `agentAliasId` — the unique id of the agent alias (overridable via the `CamelAwsBedrockAgentRuntimeAgentAliasId` header).
    

The in-message body is the input text sent to the agent. When `pojoRequest=true`, the body must be an `InvokeAgentRequest` and is sent unchanged.

The agent APIs are session based. Set `sessionId` on the endpoint, or the `CamelAwsBedrockAgentRuntimeSessionId` header, to continue an existing conversation; when neither is supplied a random session id is generated for the invocation. The session id used is always echoed back on the `CamelAwsBedrockAgentRuntimeSessionId` header of the out-message so a route can reuse it on the next call.

```java
from("direct:agent")
    .to("aws-bedrock-agent-runtime://label?operation=invokeAgent&agentId=RAWAGENTID&agentAliasId=RAWALIASID");
```

### Invoking an inline Bedrock Agent

The `invokeInlineAgent` operation defines the agent at invocation time instead of referencing a deployed one.

Mandatory options:

-   `foundationModel` — the model backing the agent (overridable via the `CamelAwsBedrockAgentRuntimeAgentFoundationModel` header).
    
-   `instruction` — the instruction given to the agent (overridable via the `CamelAwsBedrockAgentRuntimeAgentInstruction` header).
    

For the richer inline options (action groups, knowledge bases, collaborators, guardrails), set `pojoRequest=true` and send an `InvokeInlineAgentRequest` body, which is passed to AWS unchanged.

### Agent response and streaming output

Both agent operations stream their response. The producer collects the emitted events into headers:

-   `CamelAwsBedrockAgentRuntimeAgentTraces` — the trace events (only when tracing is enabled via `enableTrace` or the `CamelAwsBedrockAgentRuntimeAgentEnableTrace` header).
    
-   `CamelAwsBedrockAgentRuntimeAgentReturnControl` — the return-control payloads, emitted when the agent asks the caller to fulfil an action.
    
-   `CamelAwsBedrockAgentRuntimeAgentFiles` — the files emitted by the agent.
    
-   `CamelAwsBedrockAgentRuntimeCitations` — the citations attributed to the response chunks.
    

The out-message body depends on `streamOutputMode`:

-   `complete` (the default) — the response chunks are accumulated and the body is the full text as a `String`.
    
-   `chunks` — the body is the `List<String>` of individual chunks.
    

The mode can be overridden per exchange with the `CamelAwsBedrockAgentRuntimeAgentStreamOutputMode` header.

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