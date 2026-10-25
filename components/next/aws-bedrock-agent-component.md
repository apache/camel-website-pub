# AWS Bedrock Agent

**Since Camel 4.5**

**Both producer and consumer are supported**

The AWS Bedrock Agent component works with the ingestion jobs of the knowledge bases of the [AWS Bedrock](https://aws.amazon.com/bedrock/) service: an ingestion job syncs a data source into a knowledge base. The producer starts, lists and gets ingestion jobs, and the consumer polls the state of one ingestion job.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Bedrock. More information is available at [Amazon Bedrock](https://aws.amazon.com/bedrock/).

## URI Format

aws-bedrock-agent://label\[?options\]

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
| **dataSourceId** (common) | Define the Data source Id we are going to use. The consumer and all the operations need it; the CamelAwsBedrockAgentDataSourceId header overrides it for the producer. |  | String |
| **ingestionJobId** (common) | Define the Ingestion Job Id we want to track. The consumer and the getIngestionJob operation need it; the CamelAwsBedrockAgentIngestionJobId header overrides it for the producer. |  | String |
| **knowledgeBaseId** (common) | Define the Knowledge Base Id we are going to use. The consumer and all the operations need it; the CamelAwsBedrockAgentKnowledgeBaseId header overrides it for the producer. |  | String |
| **operation** (common) | 
**Required** The operation to perform. It can be startIngestionJob, listIngestionJobs or getIngestionJob.

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
| **dataSourceId** (common) | Define the Data source Id we are going to use. The consumer and all the operations need it; the CamelAwsBedrockAgentDataSourceId header overrides it for the producer. |  | String |
| **ingestionJobId** (common) | Define the Ingestion Job Id we want to track. The consumer and the getIngestionJob operation need it; the CamelAwsBedrockAgentIngestionJobId header overrides it for the producer. |  | String |
| **knowledgeBaseId** (common) | Define the Knowledge Base Id we are going to use. The consumer and all the operations need it; the CamelAwsBedrockAgentKnowledgeBaseId header overrides it for the producer. |  | String |
| **operation** (common) | 
**Required** The operation to perform. It can be startIngestionJob, listIngestionJobs or getIngestionJob.

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
| **CamelAwsBedrockAgentOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agent/BedrockAgentConstants.html#OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsBedrockAgentDataSourceId** (producer) Constant: [`DATASOURCE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agent/BedrockAgentConstants.html#DATASOURCE_ID) | The data source Id of the operation; it overrides the dataSourceId option. |  | String |
| **CamelAwsBedrockAgentKnowledgeBaseId** (producer) Constant: [`KNOWLEDGE_BASE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agent/BedrockAgentConstants.html#KNOWLEDGE_BASE_ID) | The knowledge base Id of the operation; it overrides the knowledgeBaseId option. |  | String |
| **CamelAwsBedrockAgentIngestionJobId** (producer) Constant: [`INGESTION_JOB_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agent/BedrockAgentConstants.html#INGESTION_JOB_ID) | The id of the ingestion job of the getIngestionJob operation; it overrides the ingestionJobId option. |  | String |
| **CamelAwsBedrockAgentIngestionJobStatus** (common) Constant: [`INGESTION_JOB_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agent/BedrockAgentConstants.html#INGESTION_JOB_STATUS) | 
The status of the ingestion job, set by the consumer and by the getIngestionJob operation.

Enum values:

-   STARTING
    
-   IN\_PROGRESS
    
-   COMPLETE
    
-   FAILED
    
-   STOPPING
    
-   STOPPED
    
-   null
    





 |  | IngestionJobStatus |
| **CamelAwsBedrockAgentIngestionJobFailureReasons** (common) Constant: [`INGESTION_JOB_FAILURE_REASONS`](https://javadoc.io/doc/org.apache.camel/camel-aws-bedrock/latest/org/apache/camel/component/aws2/bedrock/agent/BedrockAgentConstants.html#INGESTION_JOB_FAILURE_REASONS) | The failure reasons of the ingestion job, set by the consumer and by the getIngestionJob operation when the job has failure reasons. |  | List |

## Message Body

The message body at each side of the AWS Bedrock Agent component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `pojo` (`software.amazon.awssdk.services.bedrockagent.model.IngestionJob`) | The ingestion job of the knowledgeBaseId, dataSourceId and ingestionJobId options, one message per poll, also when the job did not change, with its status in the CamelAwsBedrockAgentIngestionJobStatus header. |
| **Producer input** | `any` | 
Not used: the knowledge base, the data source and the ingestion job come from the options, or from headers such as CamelAwsBedrockAgentKnowledgeBaseId, which override the options. With pojoRequest=true the request of the AWS SDK for the operation, such as a StartIngestionJobRequest: another body fails.

-   With `pojoRequest=true`: `pojo`
    





 |
| **Producer output** | `pojo` (`software.amazon.awssdk.services.bedrockagent.model.IngestionJob`) | 

The id of the ingestion job as text for startIngestionJob, a List of IngestionJobSummary for listIngestionJobs, and the IngestionJob for getIngestionJob, with its status in the CamelAwsBedrockAgentIngestionJobStatus header.

-   With `operation=startIngestionJob`: `text` (`java.lang.String`)
    
-   With `operation=listIngestionJobs`: `list` (`java.util.List<software.amazon.awssdk.services.bedrockagent.model.IngestionJobSummary>`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

Required Bedrock Agent component options

You have to provide the bedrockAgentClient in the Registry or your accessKey and secretKey to access the [Amazon Bedrock](https://aws.amazon.com/bedrock/) service.

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

### Bedrock Agent Producer operations

The producer supports the following operations, set with the `operation` option or the `CamelAwsBedrockAgentOperation` header:

-   startIngestionJob: starts an ingestion job of the data source `dataSourceId` into the knowledge base `knowledgeBaseId`. The body is set to the id of the new ingestion job.
    
-   listIngestionJobs: lists the ingestion jobs of the data source `dataSourceId` of the knowledge base `knowledgeBaseId`. The body is set to the list of `IngestionJobSummary` of the AWS SDK.
    
-   getIngestionJob: gets the ingestion job `ingestionJobId` of the data source `dataSourceId` of the knowledge base `knowledgeBaseId`. The body is set to the `IngestionJob` of the AWS SDK, the `CamelAwsBedrockAgentIngestionJobStatus` header to its status, and the `CamelAwsBedrockAgentIngestionJobFailureReasons` header to its failure reasons, if it has any.
    

The knowledge base, data source and ingestion job ids are taken from the `CamelAwsBedrockAgentKnowledgeBaseId`, `CamelAwsBedrockAgentDataSourceId` and `CamelAwsBedrockAgentIngestionJobId` headers, and else from the `knowledgeBaseId`, `dataSourceId` and `ingestionJobId` options. So the options are the defaults of the endpoint, and a header overrides them for one message, for example to get the ingestion job that startIngestionJob returned in the body.

With `pojoRequest=true`, the body is the request of the AWS SDK instead (`StartIngestionJobRequest`, `ListIngestionJobsRequest` or `GetIngestionJobRequest`), and the ids are taken from it.

### Bedrock Agent Consumer

The consumer polls the ingestion job `ingestionJobId` of the data source `dataSourceId` of the knowledge base `knowledgeBaseId`; the three options must be set. On every poll it sends an exchange with the `IngestionJob` of the AWS SDK as the body and the `CamelAwsBedrockAgentIngestionJobStatus` and `CamelAwsBedrockAgentIngestionJobFailureReasons` headers, as the getIngestionJob operation does. It does so on every poll, also when the job did not change since the previous poll, so filter on the status to act once the job is done, and set the poll `delay` to how often the job should be checked.

### Example

The following route starts an ingestion job, which syncs a data source into a knowledge base:

```yaml
- route:
    from:
      uri: direct:ingest
      steps:
        - to:
            uri: aws-bedrock-agent:agent
            parameters:
              operation: startIngestionJob
              knowledgeBaseId: KB12345678
              dataSourceId: DS12345678
              region: us-east-1
              accessKey: "{{aws.access-key}}"
              secretKey: "{{aws.secret-key}}"
        - log:
            message: "${body}"
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