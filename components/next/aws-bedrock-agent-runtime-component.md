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

The AWS Bedrock Agent Runtime component supports 28 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | BedrockAgentRuntimeConfiguration |
| **knowledgeBaseId** (producer) | **Required** Define the Knowledge Base Id we are going to use. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **modelId** (producer) | 
**Required** Define the model Id we are going to use.

Enum values:

-   anthropic.claude-instant-v1
    
-   anthropic.claude-v2
    
-   anthropic.claude-v2:1
    





 |  | String |
| **operation** (producer) | 

**Required** The operation to perform.

Enum values:

-   retrieveAndGenerate
    
-   invokeFlow
    
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
| **enableTrace** (flow) | Enables tracing for the invokeFlow operation. When enabled, the producer collects FlowTraceEvent entries and publishes them in the CamelAwsBedrockAgentRuntimeFlowTraces header. | false | boolean |
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

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters (24 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **knowledgeBaseId** (producer) | **Required** Define the Knowledge Base Id we are going to use. |  | String |
| **modelId** (producer) | 
**Required** Define the model Id we are going to use.

Enum values:

-   anthropic.claude-instant-v1
    
-   anthropic.claude-v2
    
-   anthropic.claude-v2:1
    





 |  | String |
| **operation** (producer) | 

**Required** The operation to perform.

Enum values:

-   retrieveAndGenerate
    
-   invokeFlow
    
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
| **enableTrace** (flow) | Enables tracing for the invokeFlow operation. When enabled, the producer collects FlowTraceEvent entries and publishes them in the CamelAwsBedrockAgentRuntimeFlowTraces header. | false | boolean |
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

The AWS Bedrock Agent Runtime component supports 15 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsBedrockAgentRuntimeOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsBedrockAgentRuntimeCitations** (producer) Constant: [`CITATIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#CITATIONS) | When retrieving and generating a response, this header will contain the citations. |  | String |
| **CamelAwsBedrockAgentRuntimeSessionId** (producer) Constant: [`SESSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#SESSION_ID) | When retrieving and generating a response, this header will contain he unique identifier of the session. Reuse the same value to continue the same session with the knowledge base. |  | String |
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

## Spring Boot Auto-Configuration

When using aws-bedrock-agent-runtime with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

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