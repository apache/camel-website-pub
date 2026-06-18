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

The AWS Kinesis component supports 36 options, which are listed below.

   
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
| **maxResultsPerRequest** (consumer) | Maximum number of records that will be fetched in each poll. | 1 | int |
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

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **streamName** (common) | **Required** Name of the stream. |  | String |

### Query Parameters (50 parameters)

   
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
| **maxResultsPerRequest** (consumer) | Maximum number of records that will be fetched in each poll. | 1 | int |
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

The AWS Kinesis component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsKinesisSequenceNumber** (common) Constant: [`SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#SEQUENCE_NUMBER) | The sequence number of the record, as defined in [http://docs.aws.amazon.com/kinesis/latest/APIReference/API\_PutRecord.html#API\_PutRecord\_ResponseSyntaxResponse](http://docs.aws.amazon.com/kinesis/latest/APIReference/API_PutRecord.html#API_PutRecord_ResponseSyntaxResponse) Syntax. |  | String |
| **CamelAwsKinesisApproximateArrivalTimestamp** (common) Constant: [`APPROX_ARRIVAL_TIME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#APPROX_ARRIVAL_TIME) | The time AWS assigned as the arrival time of the record. |  | String |
| **CamelAwsKinesisPartitionKey** (common) Constant: [`PARTITION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#PARTITION_KEY) | Identifies which shard in the stream the data record is assigned to. |  | String |
| **CamelMessageTimestamp** (common) Constant: [`MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#MESSAGE_TIMESTAMP) | The timestamp of the message. |  | long |
| **CamelKinesisDbResumeAction** (consumer) Constant: [`RESUME_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#RESUME_ACTION) | The resume action to execute when resuming. |  | String |
| **CamelAwsKinesisShardId** (common) Constant: [`SHARD_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#SHARD_ID) | The shard ID of the shard where the data record was placed. |  | String |
| **CamelAwsKinesisFailedRecordCount** (producer) Constant: [`FAILED_RECORD_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#FAILED_RECORD_COUNT) | The number of records that failed in a batch put operation. |  | Integer |
| **CamelAwsKinesisRecordCount** (producer) Constant: [`RECORD_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#RECORD_COUNT) | The total number of records in a batch put operation. |  | Integer |

Required Kinesis component options

You have to provide the KinesisClient in the Registry with proxies and relevant credentials configured.

## Usage

### Batch Consumer

This component implements the Batch Consumer.

This allows you, for instance, to know how many messages exist in this batch and for instance, let the Aggregator aggregate this number of messages.

The consumer is able to consume either from a single specific shard or all available shards (multiple shards consumption) of Amazon Kinesis, therefore, if you leave the 'shardId' property in the DSL configuration empty, then it’ll consume all available shards otherwise only the specified shard corresponding to the shardId will be consumed.

### Batch Producer

This component implements the Batch Producer.

This allows you to send multiple messages in a single request to Amazon Kinesis. Messages with batch size more than 500 is allowed. Producer will split them into multiple requests.

The batch type needs to implement the `Iterable` interface. For example, it can be a `List`, `Set` or any other collection type. The message type can be one or more of types `byte[]`, `ByteBuffer`, UTF-8 `String`, or `InputStream`. Other types are not supported.

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
from("aws2-kinesis://mykinesisstream?asyncClient=true&useDefaultCredentialsProvider=true&useKclConsumers=true&region=myregion")
    .to("log:out?showAll=true");
```

```xml
<route>
  <from uri="aws2-kinesis://mykinesisstream?asyncClient=true&amp;useDefaultCredentialsProvider=true&amp;useKclConsumers=true&amp;region=myregion"/>
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
        region: myregion
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

## Spring Boot Auto-Configuration

When using aws2-kinesis with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-kinesis-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 58 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-kinesis-firehose.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-kinesis-firehose.amazon-kinesis-firehose-client** | Amazon Kinesis Firehose client to use for all requests for this endpoint. The option is a software.amazon.awssdk.services.firehose.FirehoseClient type. |  | FirehoseClient |
| **camel.component.aws2-kinesis-firehose.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-kinesis-firehose.cbor-enabled** | This option will set the CBOR\_ENABLED property during the execution. | true | Boolean |
| **camel.component.aws2-kinesis-firehose.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.firehose.KinesisFirehose2Configuration type. |  | KinesisFirehose2Configuration |
| **camel.component.aws2-kinesis-firehose.enabled** | Whether to enable auto configuration of the aws2-kinesis-firehose component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-kinesis-firehose.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-kinesis-firehose.operation** | The operation to do in case the user don’t want to send only a record. |  | KinesisFirehose2Operations |
| **camel.component.aws2-kinesis-firehose.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-kinesis-firehose.profile-credentials-name** | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **camel.component.aws2-kinesis-firehose.proxy-host** | To define a proxy host when instantiating the Kinesis Firehose client. |  | String |
| **camel.component.aws2-kinesis-firehose.proxy-port** | To define a proxy port when instantiating the Kinesis Firehose client. |  | Integer |
| **camel.component.aws2-kinesis-firehose.proxy-protocol** | To define a proxy protocol when instantiating the Kinesis Firehose client. | https | Protocol |
| **camel.component.aws2-kinesis-firehose.region** | The region in which Kinesis Firehose client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-kinesis-firehose.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-kinesis-firehose.session-token** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **camel.component.aws2-kinesis-firehose.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-kinesis-firehose.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-kinesis-firehose.use-default-credentials-provider** | Set whether the Kinesis Firehose client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-kinesis-firehose.use-profile-credentials-provider** | Set whether the Kinesis Firehose client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-kinesis-firehose.use-session-credentials** | Set whether the Kinesis Firehose client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis Firehose. | false | Boolean |
| **camel.component.aws2-kinesis.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-kinesis.amazon-kinesis-async-client** | Supply a pre-constructed Amazon Kinesis async client to use for the KCL Consumer. The option is a software.amazon.awssdk.services.kinesis.KinesisAsyncClient type. |  | KinesisAsyncClient |
| **camel.component.aws2-kinesis.amazon-kinesis-client** | Amazon Kinesis client to use for all requests for this endpoint. The option is a software.amazon.awssdk.services.kinesis.KinesisClient type. |  | KinesisClient |
| **camel.component.aws2-kinesis.application-name** | Name of the KCL application. This defaults to the stream name. |  | String |
| **camel.component.aws2-kinesis.async-client** | If we want to a KinesisAsyncClient instance set it to true. | false | Boolean |
| **camel.component.aws2-kinesis.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-kinesis.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.aws2-kinesis.cbor-enabled** | This option will set the CBOR\_ENABLED property during the execution. | true | Boolean |
| **camel.component.aws2-kinesis.cloud-watch-async-client** | If we want to a KCL Consumer, we can pass an instance of CloudWatchAsyncClient. The option is a software.amazon.awssdk.services.cloudwatch.CloudWatchAsyncClient type. |  | CloudWatchAsyncClient |
| **camel.component.aws2-kinesis.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.kinesis.Kinesis2Configuration type. |  | Kinesis2Configuration |
| **camel.component.aws2-kinesis.dynamo-db-async-client** | If we want to a KCL Consumer, we can pass an instance of DynamoDbAsyncClient. The option is a software.amazon.awssdk.services.dynamodb.DynamoDbAsyncClient type. |  | DynamoDbAsyncClient |
| **camel.component.aws2-kinesis.enabled** | Whether to enable auto configuration of the aws2-kinesis component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-kinesis.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.aws2-kinesis.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.aws2-kinesis.iterator-type** | Defines where in the Kinesis stream to start getting records. | trim-horizon | ShardIteratorType |
| **camel.component.aws2-kinesis.kcl-disable-cloudwatch-metrics-export** | If we want to use a KCL Consumer and disable the CloudWatch Metrics Export. | false | Boolean |
| **camel.component.aws2-kinesis.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-kinesis.max-results-per-request** | Maximum number of records that will be fetched in each poll. | 1 | Integer |
| **camel.component.aws2-kinesis.message-timestamp** | The message timestamp to start polling from. Required if iteratorType is set to AT\_TIMESTAMP. |  | String |
| **camel.component.aws2-kinesis.override-endpoint** | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-kinesis.profile-credentials-name** | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **camel.component.aws2-kinesis.proxy-host** | To define a proxy host when instantiating the Kinesis client. |  | String |
| **camel.component.aws2-kinesis.proxy-port** | To define a proxy port when instantiating the Kinesis client. |  | Integer |
| **camel.component.aws2-kinesis.proxy-protocol** | To define a proxy protocol when instantiating the Kinesis client. | https | Protocol |
| **camel.component.aws2-kinesis.region** | The region in which Kinesis Firehose client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-kinesis.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-kinesis.sequence-number** | The sequence number to start polling from. Required if iteratorType is set to AFTER\_SEQUENCE\_NUMBER or AT\_SEQUENCE\_NUMBER. |  | String |
| **camel.component.aws2-kinesis.session-token** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **camel.component.aws2-kinesis.shard-closed** | Define what will be the behavior in case of shard closed. Possible value are ignore, silent and fail. In case of ignore a WARN message will be logged once and the consumer will not process new messages until restarted,in case of silent there will be no logging and the consumer will not process new messages until restarted,in case of fail a ReachedClosedStateException will be thrown. | ignore | Kinesis2ShardClosedStrategyEnum |
| **camel.component.aws2-kinesis.shard-id** | Defines which shardId in the Kinesis stream to get records from. |  | String |
| **camel.component.aws2-kinesis.shard-monitor-interval** | The interval in milliseconds to wait between shard polling. | 10000 | Long |
| **camel.component.aws2-kinesis.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-kinesis.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-kinesis.use-default-credentials-provider** | Set whether the Kinesis client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-kinesis.use-kcl-consumers** | If we want to a KCL Consumer set it to true. | false | Boolean |
| **camel.component.aws2-kinesis.use-profile-credentials-provider** | Set whether the Kinesis client should expect to load credentials through a profile credentials provider. | false | Boolean |
| **camel.component.aws2-kinesis.use-session-credentials** | Set whether the Kinesis client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis. | false | Boolean |