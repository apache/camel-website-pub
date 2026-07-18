# AWS Bedrock Agent

**Since Camel 4.5**

**Both producer and consumer are supported**

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

The AWS Bedrock Agent component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | Component configuration. |  | BedrockAgentConfiguration |
| **dataSourceId** (common) | Define the Data source Id we are going to use. |  | String |
| **knowledgeBaseId** (common) | Define the Knowledge Base Id we are going to use. |  | String |
| **operation** (common) | 
**Required** The operation to perform.

Enum values:

-   startIngestionJob
    
-   listIngestionJobs
    
-   getIngestionJob
    





 |  | BedrockAgentOperations |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (common) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (common) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (common) | 

The region in which Bedrock Agent client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (common) | Set whether the Bedrock Agent client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (common) | Set whether the Bedrock Agent client should expect to load credentials through a profile credentials provider. | false | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **ingestionJobId** (consumer) | Define the Ingestion Job Id we want to track. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **bedrockAgentClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Agent client. |  | BedrockAgentClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Bedrock Agent client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Bedrock Agent client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Bedrock Agent client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Bedrock Agent client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | boolean |

## Endpoint Options

The AWS Bedrock Agent endpoint is configured using URI syntax:

aws-bedrock-agent:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (common) | **Required** Logical name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataSourceId** (common) | Define the Data source Id we are going to use. |  | String |
| **knowledgeBaseId** (common) | Define the Knowledge Base Id we are going to use. |  | String |
| **operation** (common) | 
**Required** The operation to perform.

Enum values:

-   startIngestionJob
    
-   listIngestionJobs
    
-   getIngestionJob
    





 |  | BedrockAgentOperations |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **pojoRequest** (common) | If we want to use a POJO request as body or not. | false | boolean |
| **profileCredentialsName** (common) | If using a profile credentials provider, this parameter will set the profile name. | false | String |
| **region** (common) | 

The region in which Bedrock Agent client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (common) | Set whether the Bedrock Agent client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (common) | Set whether the Bedrock Agent client should expect to load credentials through a profile credentials provider. | false | boolean |
| **ingestionJobId** (consumer) | Define the Ingestion Job Id we want to track. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **bedrockAgentClient** (advanced) | **Autowired** To use an existing configured AWS Bedrock Agent client. |  | BedrockAgentClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Bedrock Agent client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Bedrock Agent client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Bedrock Agent client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Bedrock Agent client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Bedrock. | false | boolean |

## Message Headers

The AWS Bedrock Agent component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsBedrockAgentRuntimeOperation** (common) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsBedrockAgentRuntimeCitations** (common) Constant: [`CITATIONS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#CITATIONS) | When retrieving and generating a response, this header will contain the citations. |  | String |
| **CamelAwsBedrockAgentRuntimeSessionId** (common) Constant: [`SESSION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#SESSION_ID) | When retrieving and generating a response, this header will contain he unique identifier of the session. Reuse the same value to continue the same session with the knowledge base. |  | String |
| **CamelAwsBedrockAgentRuntimeFlowIdentifier** (common) Constant: [`FLOW_IDENTIFIER`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_IDENTIFIER) | The unique identifier of the flow to invoke. Overrides the flowIdentifier configured on the endpoint. |  | String |
| **CamelAwsBedrockAgentRuntimeFlowAliasIdentifier** (common) Constant: [`FLOW_ALIAS_IDENTIFIER`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_ALIAS_IDENTIFIER) | The unique identifier of the flow alias to invoke. Overrides the flowAliasIdentifier configured on the endpoint. |  | String |
| **CamelAwsBedrockAgentRuntimeFlowEnableTrace** (common) Constant: [`FLOW_ENABLE_TRACE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_ENABLE_TRACE) | Enables tracing for the flow invocation. When set, overrides the enableTrace option on the endpoint. |  | Boolean |
| **CamelAwsBedrockAgentRuntimeFlowExecutionId** (common) Constant: [`FLOW_EXECUTION_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_EXECUTION_ID) | The unique identifier of an in-progress flow execution to continue. Used for multi-turn flow conversations. |  | String |
| **CamelAwsBedrockAgentRuntimeFlowOutputs** (common) Constant: [`FLOW_OUTPUTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_OUTPUTS) | When invoking a flow, this header will contain the list of FlowOutputEvent emitted by the flow. |  | List |
| **CamelAwsBedrockAgentRuntimeFlowTraces** (common) Constant: [`FLOW_TRACES`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_TRACES) | When invoking a flow with tracing enabled, this header will contain the list of FlowTraceEvent emitted during execution. |  | List |
| **CamelAwsBedrockAgentRuntimeFlowCompletionReason** (common) Constant: [`FLOW_COMPLETION_REASON`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#FLOW_COMPLETION_REASON) | When invoking a flow, this header will contain the reason the flow completed (set when a FlowCompletionEvent is received). |  | String |
| **CamelAwsBedrockAgentRuntimeRetrievedResults** (common) Constant: [`RETRIEVED_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#RETRIEVED_RESULTS) | When performing a retrieve operation, this header will contain the list of KnowledgeBaseRetrievalResult chunks returned by the knowledge base. |  | List |
| **CamelAwsBedrockAgentRuntimeNumberOfResults** (common) Constant: [`NUMBER_OF_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#NUMBER_OF_RESULTS) | Overrides the maximum number of results returned by the retrieve operation. Must be a positive Integer; when not set the AWS service default is used. |  | Integer |
| **CamelAwsBedrockAgentRuntimeSearchType** (common) Constant: [`OVERRIDE_SEARCH_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#OVERRIDE_SEARCH_TYPE) | Overrides the search type used by the retrieve operation. Accepts the AWS SearchType enum (HYBRID, SEMANTIC) or its String representation. |  | String |
| **CamelAwsBedrockAgentRuntimeNextToken** (common) Constant: [`NEXT_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#NEXT_TOKEN) | Pagination token used by the retrieve operation. Set on the in-message to request the next page; set on the out-message when the response carries one. |  | String |
| **CamelAwsBedrockAgentRuntimeRetrieveGuardrailAction** (common) Constant: [`RETRIEVE_GUARDRAIL_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agentruntime/BedrockAgentRuntimeConstants.html#RETRIEVE_GUARDRAIL_ACTION) | When performing a retrieve operation, this header will contain the guardrail action (if any) applied by the knowledge base. |  | String |

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