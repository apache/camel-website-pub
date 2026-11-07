# AWS Kinesis

**Since Camel 3.2**

**Both producer and consumer are supported**

The AWS2 Kinesis component supports consuming messages from and producing messages to Amazon Kinesis service.

The AWS2 Kinesis component also supports Synchronous and Asynchronous Client, which means you choose what fits best your requirements, so if you need the connection (client) to be async, there’s a property of 'asyncClient' (in DSL also can be found) needs to be turned true.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Kinesis. More information is available at [AWS Kinesis](https://aws.amazon.com/kinesis/)

## URI Format

aws2-kinesis://stream-name\[?options\]

The stream needs to be created prior to it being used.

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

The AWS Kinesis component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cborEnabled** (common) | This option will set the CBOR\_ENABLED property during the execution. | true | boolean |
| **configuration** (common) | Component configuration. |  | Kinesis2Configuration |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **region** (common) | 
The region in which Kinesis Firehose client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   ap-south-2
    
-   ap-south-1
    
-   eu-south-1
    
-   eu-south-2
    
-   us-gov-east-1
    
-   me-central-1
    
-   il-central-1
    
-   ca-central-1
    
-   eu-central-1
    
-   us-iso-west-1
    
-   eu-central-2
    
-   eu-isoe-west-1
    
-   us-west-1
    
-   us-west-2
    
-   af-south-1
    
-   eu-north-1
    
-   eu-west-3
    
-   eu-west-2
    
-   eu-west-1
    
-   ap-northeast-3
    
-   ap-northeast-2
    
-   ap-northeast-1
    
-   me-south-1
    
-   sa-east-1
    
-   ap-east-1
    
-   cn-north-1
    
-   ca-west-1
    
-   us-gov-west-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   us-iso-east-1
    
-   ap-southeast-3
    
-   ap-southeast-4
    
-   us-east-1
    
-   us-east-2
    
-   cn-northwest-1
    
-   us-isob-east-1
    
-   aws-global
    
-   aws-cn-global
    
-   aws-us-gov-global
    
-   aws-iso-global
    
-   aws-iso-b-global
    





 |  | String |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **iteratorType** (consumer) | 

Defines where in the Kinesis stream to start getting records.

Enum values:

-   AT\_SEQUENCE\_NUMBER
    
-   AFTER\_SEQUENCE\_NUMBER
    
-   TRIM\_HORIZON
    
-   LATEST
    
-   AT\_TIMESTAMP
    
-   null
    





 | TRIM\_HORIZON | ShardIteratorType |
| **maxResultsPerRequest** (consumer) | Maximum number of records fetched from each shard in each poll: the Limit of the GetRecords request, from 1 to 10000. Not used by the KCL consumer (useKclConsumers). | 1000 | int |
| **messageTimestamp** (consumer) | The message timestamp to start polling from. Required if iteratorType is set to AT\_TIMESTAMP. |  | String |
| **sequenceNumber** (consumer) | The sequence number to start polling from. Required if iteratorType is set to AFTER\_SEQUENCE\_NUMBER or AT\_SEQUENCE\_NUMBER. |  | String |
| **shardClosed** (consumer) | 

Define what will be the behavior in case of shard closed. Possible value are ignore, silent and fail. In case of ignore a WARN message will be logged once and the consumer will not process new messages until restarted,in case of silent there will be no logging and the consumer will not process new messages until restarted,in case of fail a ReachedClosedStateException will be thrown.

Enum values:

-   ignore
    
-   fail
    
-   silent
    





 | ignore | Kinesis2ShardClosedStrategyEnum |
| **shardId** (consumer) | Defines which shardId in the Kinesis stream to get records from. |  | String |
| **kclStopCheckpointOnFailure** (consumer (advanced)) | If we want to use a KCL Consumer and keep the checkpoint of a shard before the first record whose exchange fails, so the next holder of the lease of the shard (the route started again, or another worker) consumes the records from that one on again. The consumer goes on routing the shard, so these records can be routed twice and out of order. By default a failed record is reported to the exception handler and checkpointed with its batch. See the KCL consumer section of the docs. | false | boolean |
| **shardMonitorInterval** (consumer (advanced)) | The interval in milliseconds to wait between shard polling. | 10000 | long |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **amazonKinesisAsyncClient** (advanced) | **Autowired** Supply a pre-constructed Amazon Kinesis async client to use for the KCL Consumer. |  | KinesisAsyncClient |
| **amazonKinesisClient** (advanced) | **Autowired** Amazon Kinesis client to use for all requests for this endpoint. |  | KinesisClient |
| **applicationName** (advanced) | Name of the KCL application. This defaults to the stream name. |  | String |
| **asyncClient** (advanced) | If we want to a KinesisAsyncClient instance set it to true. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **cloudWatchAsyncClient** (advanced) | If we want to a KCL Consumer, we can pass an instance of CloudWatchAsyncClient. |  | CloudWatchAsyncClient |
| **dynamoDbAsyncClient** (advanced) | If we want to a KCL Consumer, we can pass an instance of DynamoDbAsyncClient. |  | DynamoDbAsyncClient |
| **kclDisableCloudwatchMetricsExport** (advanced) | If we want to use a KCL Consumer and disable the CloudWatch Metrics Export. | false | boolean |
| **useKclConsumers** (advanced) | If we want to a KCL Consumer set it to true. | false | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Kinesis client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Kinesis client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Kinesis client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Kinesis client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Kinesis client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Kinesis client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis. | false | boolean |

## Endpoint Options

The AWS Kinesis endpoint is configured using URI syntax:

aws2-kinesis:streamName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **streamName** (common) | **Required** Name of the stream. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cborEnabled** (common) | This option will set the CBOR\_ENABLED property during the execution. | true | boolean |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **region** (common) | 
The region in which Kinesis Firehose client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

Enum values:

-   ap-south-2
    
-   ap-south-1
    
-   eu-south-1
    
-   eu-south-2
    
-   us-gov-east-1
    
-   me-central-1
    
-   il-central-1
    
-   ca-central-1
    
-   eu-central-1
    
-   us-iso-west-1
    
-   eu-central-2
    
-   eu-isoe-west-1
    
-   us-west-1
    
-   us-west-2
    
-   af-south-1
    
-   eu-north-1
    
-   eu-west-3
    
-   eu-west-2
    
-   eu-west-1
    
-   ap-northeast-3
    
-   ap-northeast-2
    
-   ap-northeast-1
    
-   me-south-1
    
-   sa-east-1
    
-   ap-east-1
    
-   cn-north-1
    
-   ca-west-1
    
-   us-gov-west-1
    
-   ap-southeast-1
    
-   ap-southeast-2
    
-   us-iso-east-1
    
-   ap-southeast-3
    
-   ap-southeast-4
    
-   us-east-1
    
-   us-east-2
    
-   cn-northwest-1
    
-   us-isob-east-1
    
-   aws-global
    
-   aws-cn-global
    
-   aws-us-gov-global
    
-   aws-iso-global
    
-   aws-iso-b-global
    





 |  | String |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **iteratorType** (consumer) | 

Defines where in the Kinesis stream to start getting records.

Enum values:

-   AT\_SEQUENCE\_NUMBER
    
-   AFTER\_SEQUENCE\_NUMBER
    
-   TRIM\_HORIZON
    
-   LATEST
    
-   AT\_TIMESTAMP
    
-   null
    





 | TRIM\_HORIZON | ShardIteratorType |
| **maxResultsPerRequest** (consumer) | Maximum number of records fetched from each shard in each poll: the Limit of the GetRecords request, from 1 to 10000. Not used by the KCL consumer (useKclConsumers). | 1000 | int |
| **messageTimestamp** (consumer) | The message timestamp to start polling from. Required if iteratorType is set to AT\_TIMESTAMP. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **sequenceNumber** (consumer) | The sequence number to start polling from. Required if iteratorType is set to AFTER\_SEQUENCE\_NUMBER or AT\_SEQUENCE\_NUMBER. |  | String |
| **shardClosed** (consumer) | 

Define what will be the behavior in case of shard closed. Possible value are ignore, silent and fail. In case of ignore a WARN message will be logged once and the consumer will not process new messages until restarted,in case of silent there will be no logging and the consumer will not process new messages until restarted,in case of fail a ReachedClosedStateException will be thrown.

Enum values:

-   ignore
    
-   fail
    
-   silent
    





 | ignore | Kinesis2ShardClosedStrategyEnum |
| **shardId** (consumer) | Defines which shardId in the Kinesis stream to get records from. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **kclStopCheckpointOnFailure** (consumer (advanced)) | If we want to use a KCL Consumer and keep the checkpoint of a shard before the first record whose exchange fails, so the next holder of the lease of the shard (the route started again, or another worker) consumes the records from that one on again. The consumer goes on routing the shard, so these records can be routed twice and out of order. By default a failed record is reported to the exception handler and checkpointed with its batch. See the KCL consumer section of the docs. | false | boolean |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **shardMonitorInterval** (consumer (advanced)) | The interval in milliseconds to wait between shard polling. | 10000 | long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **amazonKinesisAsyncClient** (advanced) | **Autowired** Supply a pre-constructed Amazon Kinesis async client to use for the KCL Consumer. |  | KinesisAsyncClient |
| **amazonKinesisClient** (advanced) | **Autowired** Amazon Kinesis client to use for all requests for this endpoint. |  | KinesisClient |
| **applicationName** (advanced) | Name of the KCL application. This defaults to the stream name. |  | String |
| **asyncClient** (advanced) | If we want to a KinesisAsyncClient instance set it to true. | false | boolean |
| **cloudWatchAsyncClient** (advanced) | If we want to a KCL Consumer, we can pass an instance of CloudWatchAsyncClient. |  | CloudWatchAsyncClient |
| **dynamoDbAsyncClient** (advanced) | If we want to a KCL Consumer, we can pass an instance of DynamoDbAsyncClient. |  | DynamoDbAsyncClient |
| **kclDisableCloudwatchMetricsExport** (advanced) | If we want to use a KCL Consumer and disable the CloudWatch Metrics Export. | false | boolean |
| **useKclConsumers** (advanced) | If we want to a KCL Consumer set it to true. | false | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Kinesis client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Kinesis client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Kinesis client.

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
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the Kinesis client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Kinesis client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Kinesis client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis. | false | boolean |

## Message Headers

The AWS Kinesis component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsKinesisSequenceNumber** (common) Constant: [`SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#SEQUENCE_NUMBER) | The sequence number of the record, as defined in [Response Syntax](http://docs.aws.amazon.com/kinesis/latest/APIReference/API_PutRecord.html#API_PutRecord_ResponseSyntax). |  | String |
| **CamelAwsKinesisApproximateArrivalTimestamp** (common) Constant: [`APPROX_ARRIVAL_TIME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#APPROX_ARRIVAL_TIME) | The time AWS assigned as the arrival time of the record. |  | String |
| **CamelAwsKinesisPartitionKey** (common) Constant: [`PARTITION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#PARTITION_KEY) | Identifies which shard in the stream the data record is assigned to. |  | String |
| **CamelMessageTimestamp** (common) Constant: [`MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#MESSAGE_TIMESTAMP) | The timestamp of the message. |  | long |
| **CamelKinesisDbResumeAction** (consumer) Constant: [`RESUME_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#RESUME_ACTION) | The resume action to execute when resuming. |  | String |
| **CamelAwsKinesisShardId** (common) Constant: [`SHARD_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#SHARD_ID) | The shard ID of the shard where the data record was placed. |  | String |
| **CamelAwsKinesisPartitionKeys** (producer) Constant: [`PARTITION_KEYS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#PARTITION_KEYS) | A list of partition keys for batch operations. When set, each record in the batch is assigned the partition key at the corresponding index, allowing records to be routed to different shards. If not set, the single CamelAwsKinesisPartitionKey header is used for all records. |  | List |
| **CamelAwsKinesisFailedRecordCount** (producer) Constant: [`FAILED_RECORD_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#FAILED_RECORD_COUNT) | The number of records that failed in a batch put operation. |  | Integer |
| **CamelAwsKinesisRecordCount** (producer) Constant: [`RECORD_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#RECORD_COUNT) | The total number of records in a batch put operation. |  | Integer |

## Message Body

The message body at each side of the AWS Kinesis component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `bytes` (`byte[]`) | 
The data of the record as a byte array, one message per record, with its partition key, sequence number and shard id in headers. With useKclConsumers=true a java.nio.ByteBuffer: convert it to a String or bytes for the steps that read text.

-   With `useKclConsumers=true`: `pojo` (`java.nio.ByteBuffer`)
    





 |
| **Producer input** | `text`, `bytes`, `stream`, `file` or `list` | The data of the record: text, bytes, a stream or a file. A List or another Iterable is sent as a batch, one record per element, and each element must be text, bytes, a ByteBuffer or a stream. A Map or a POJO fails: marshal it first. |
| **Producer output** | `unchanged` | Unchanged, with the sequence number and the shard id of the record in headers, or the number of records of a batch. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

Required Kinesis component options

You have to provide the KinesisClient in the Registry with proxies and relevant credentials configured.

## Usage

### Batch Consumer

This component implements the Batch Consumer.

This allows you, for instance, to know how many messages exist in this batch and for instance, let the Aggregator aggregate this number of messages.

The consumer is able to consume either from a single specific shard or all available shards (multiple shards consumption) of Amazon Kinesis, therefore, if you leave the 'shardId' property in the DSL configuration empty, then it’ll consume all available shards otherwise only the specified shard corresponding to the shardId will be consumed.

### Consumer throughput and the Kinesis read quotas

In each poll the consumer sends one `GetRecords` request to each shard it reads. The request asks for up to `maxResultsPerRequest` records (1000 by default; Kinesis accepts 1 to 10,000), so a poll routes up to `maxResultsPerRequest` records per shard.

Kinesis limits the reads of each shard:

-   5 `GetRecords` requests per second;
    
-   2 MiB of data per second;
    
-   at most 10,000 records or 10 MiB in one response.
    

A request over these quotas fails with a `ProvisionedThroughputExceededException`. After a response of 10 MiB, the requests of the next 5 seconds to that shard fail too.

The scheduler options decide how often a shard is read:

-   With `greedy=false` (the default), the next poll starts `delay` milliseconds (500 by default) after the previous one ended. A shard then gets at most about 2 requests per second, so up to about twice `maxResultsPerRequest` records per second.
    
-   With `greedy=true`, the next poll starts at once after a poll that routed records, and `delay` applies only after a poll that routed none. With a backlog and a fast route, the consumer can then send more than 5 requests per second to a shard.
    

To keep up with a shard, choose `maxResultsPerRequest` and `delay` so that the records of a poll times the polls per second stay within 2 MiB per second. For example, 1000 records of 1 KiB every 500 ms is about 2 MiB per second. For larger records, lower `maxResultsPerRequest` or raise `delay`. While the records of a response are routed, the consumer holds that response in memory, one for each shard of the poll.

A [graceful shutdown](../../manual/graceful-shutdown.md) waits until the consumer has routed all the records of the poll that is running. Choose `maxResultsPerRequest` so that the route handles the records of a poll within the shutdown timeout (45 seconds by default). Otherwise the shutdown is forced, and the records of the poll that are not routed yet fail with a `RouteStoppingException`.

These options apply to the polling consumer only. The KCL consumer (`useKclConsumers=true`) fetches the records with the settings of the Kinesis Client Library and does not use `maxResultsPerRequest`, `delay` or `greedy`.

### Custom Resume Action

The consumer supports a custom `KinesisResumeAction` for controlling where each shard starts reading (e.g., resuming from a persisted sequence number). Register a subclass in the Camel registry under the key `CamelKinesisDbResumeAction`.

The consumer creates a separate instance per shard via reflection to avoid concurrent mutation when multiple shards are processed in parallel. Because of this, custom subclasses **must** provide a public no-arg constructor. Per-shard state (`builder`, `shardId`, `streamName`) is injected via setters after construction.

When a shard needs a new shard iterator, `evalEntry` is called for every entry of the resume cache, with the shard id as key and the sequence number (a `String`, or the `KinesisOffset` stored by `KinesisResumeStrategy`) as value. The default action starts the shard after the sequence number of its own entry and ignores the entries of the other shards; a subclass should compare the key with `getShardId()` the same way.

### Batch Producer

This component implements the Batch Producer.

This allows you to send multiple messages in a single request to Amazon Kinesis. A batch can have any number of records: the producer splits it into `PutRecords` requests of at most 500 records and 10 MiB, the limits of a request (the size of a record is its data plus its partition key). A record above 10 MiB, the largest record that Kinesis accepts, fails the exchange with an `IllegalArgumentException` before any request is sent. A stream can have a lower limit for the size of its records (1 to 10 MiB), which Kinesis checks.

The batch type needs to implement the `Iterable` interface. For example, it can be a `List`, `Set` or any other collection type. The message type can be one or more of types `byte[]`, `ByteBuffer`, UTF-8 `String`, or `InputStream`. Other types are not supported. A `java.nio.file.Path` body is not a batch: like a `java.io.File`, it is sent as a single record with the content of the file.

A `PutRecords` request can be partly written: Kinesis writes some of its records and returns an error code for the others (for example `ProvisionedThroughputExceededException`). The producer then sends only the records that failed again, up to 3 times, waiting 100, 200 and 400 milliseconds plus a random part of up to a quarter of the delay (so that producers throttled at the same time do not all send again at the same time), and then goes on with the next requests of the batch. When every record fails, for example when the whole stream is throttled, each request waits 700 to 875 milliseconds in total before its records are counted as not written, so a batch of 10,000 records (20 requests of 500 records) can block the caller for 14 to 17.5 seconds, plus the time of the 80 calls and of the retries of the AWS SDK client.

A record that is sent again is written after the next records of its request: if record A fails and record B, with the same partition key, is written, the stream has B before A. `PutRecords` does not guarantee the order of the records either. When the order of the records of a partition key matters, send them one by one, with a body that is not an `Iterable`.

After the last request, the `CamelAwsKinesisRecordCount` header has the number of records of the batch, and the `CamelAwsKinesisFailedRecordCount` header the number of records that are still not written. When that number is not 0, the exchange fails with an exception that gives both numbers and the first error code. When a `PutRecords` call throws, for example an `InvalidArgumentException`, a KMS error, or an error of the AWS SDK client after its own retries, the exchange fails at once with that exception, and the next requests of the batch are not sent. Both headers are set in that case too: the records of that call and of the requests that were not sent are counted as not written, even if the call may have written some of them (for example after a timeout).

A failure does not undo the records that are already written. A redelivery of the exchange, by the error handler of the route or by the source of the message (for example a transacted JMS or an SQS consumer), sends the whole batch again, so the records that were written before the failure are written twice. `PutRecords` has no idempotency token: a request whose outcome is unknown, for example after a timeout, can also write a record twice when it is sent again, for example by the retries of the AWS SDK client. A consumer of the stream that must not process a record twice needs an id in the data of the record to detect a duplicate.

A body that is not an `Iterable` is sent as a single record, converted to a `byte[]`. A body that does not convert to a `byte[]` fails with an `InvalidPayloadException`.

### Static credentials, Default Credential Provider and Profile Credentials Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretAccessKey`.
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You have also the possibility of using Profile Credentials Provider, by specifying the useProfileCredentialsProvider option to true and profileCredentialsName to the profile name.

Only one of static, default and profile credentials could be used at the same time.

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### AmazonKinesis configuration

You then have to reference the KinesisClient in the `amazonKinesisClient` URI option.

-   Java
    
-   XML
    
-   YAML
    

```java
from("aws2-kinesis://mykinesisstream?amazonKinesisClient=#kinesisClient")
    .to("log:out?showAll=true");
```

```xml
<route>
  <from uri="aws2-kinesis://mykinesisstream?amazonKinesisClient=#kinesisClient"/>
  <to uri="log:out?showAll=true"/>
</route>
```

```yaml
- route:
    from:
      uri: aws2-kinesis://mykinesisstream
      parameters:
        amazonKinesisClient: "#kinesisClient"
      steps:
        - to:
            uri: log:out
            parameters:
              showAll: true
```

### Providing AWS Credentials

It is recommended that the credentials are obtained by using the [DefaultAWSCredentialsProviderChain](http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/auth/DefaultAWSCredentialsProviderChain.md) that is the default when creating a new ClientConfiguration instance, however, a different [AWSCredentialsProvider](http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/auth/AWSCredentialsProvider.md) can be specified when calling createClient(…​).

### AWS Kinesis KCL Consumer

The component supports also the KCL (Kinesis Client Library) for consuming from a Kinesis Data Stream.

To enable this feature you’ll need to set three different parameter in your endpoint and set the region:

-   Java
    
-   XML
    
-   YAML
    

```java
from("aws2-kinesis://mykinesisstream?asyncClient=true&useDefaultCredentialsProvider=true&useKclConsumers=true&region=eu-west-1")
    .to("log:out?showAll=true");
```

```xml
<route>
  <from uri="aws2-kinesis://mykinesisstream?asyncClient=true&amp;useDefaultCredentialsProvider=true&amp;useKclConsumers=true&amp;region=eu-west-1"/>
  <to uri="log:out?showAll=true"/>
</route>
```

```yaml
- route:
    from:
      uri: aws2-kinesis://mykinesisstream
      parameters:
        asyncClient: true
        useDefaultCredentialsProvider: true
        useKclConsumers: true
        region: eu-west-1
      steps:
        - to:
            uri: log:out
            parameters:
              showAll: true
```

This feature will make possible to automatically checkpointing the Shard Iterations by combining the usage of KCL, DynamoDB Table and CloudWatch alarms.

Everything will work out of the box, by simply using your AWS Credentials.

> **Note**
> In the beginning the consumer will require 60/70 seconds for preparing everything, listing the shards, creating/querying the Lease table on Dynamo DB. Keep it in mind while working with the KCL consumer.

### Failed records with the KCL consumer

By default, a record whose exchange fails (the route ends with an exception) is reported to the exception handler of the consumer and checkpointed with its batch, so it is not consumed again. Use a dead letter channel or redelivery in the route when a failed record must not be lost.

With `kclStopCheckpointOnFailure=true`, the checkpoint of a shard stays before the first record of it that failed. KCL does not deliver records of a shard again while the consumer holds the lease of the shard, so the consumer goes on routing the next records, but it checkpoints only the records before the failed one, also when the route stops. The next holder of the lease (the route started again, or another worker taking over the lease) consumes the records from the failed one on again. This has a cost:

-   the records after the failed one are routed again, so they can be routed twice and out of order: the route must be idempotent;
    
-   only one WARN, with the sequence number of the first failed record, shows that the checkpoint stays behind: the lag metrics do not, as the consumer still reads the shard. A record that fails each time keeps the checkpoint of its shard before it: each new holder of the lease routes again everything since that record, up to the retention period of the stream;
    
-   at the end of a shard (resharding) the end is still checkpointed, as KCL requires, so the failed records of that shard are not consumed again.
    

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-kinesis</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.