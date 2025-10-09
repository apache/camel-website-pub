# AWS Kinesis

**Since Camel 3.2**

**Both producer and consumer are supported**

The AWS2 Kinesis component supports receiving messages from and sending messages to Amazon Kinesis (no Batch supported) service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Kinesis. More information are available at [AWS Kinesis](https://aws.amazon.com/kinesis/)

## URI Format

aws2-kinesis://stream-name\[?options\]

The stream needs to be created prior to it being used.  
You can append query options to the URI in the following format, ?options=value&option2=value&…​

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The AWS Kinesis component supports 21 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonKinesisClient** (common) | **Autowired** Amazon Kinesis client to use for all requests for this endpoint. |  | KinesisClient |
| **cborEnabled** (common) | This option will set the CBOR\_ENABLED property during the execution. | true | boolean |
| **configuration** (common) | Component configuration. |  | Kinesis2Configuration |
| **overrideEndpoint** (common) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **proxyHost** (common) | To define a proxy host when instantiating the Kinesis client. |  | String |
| **proxyPort** (common) | To define a proxy port when instantiating the Kinesis client. |  | Integer |
| **proxyProtocol** (common) | 
To define a proxy protocol when instantiating the Kinesis client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (common) | The region in which Kinesis Firehose client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (common) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (common) | Set whether the Kinesis client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
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
| **sequenceNumber** (consumer) | The sequence number to start polling from. Required if iteratorType is set to AFTER\_SEQUENCE\_NUMBER or AT\_SEQUENCE\_NUMBER. |  | String |
| **shardClosed** (consumer) | 

Define what will be the behavior in case of shard closed. Possible value are ignore, silent and fail. In case of ignore a message will be logged and the consumer will restart from the beginning,in case of silent there will be no logging and the consumer will start from the beginning,in case of fail a ReachedClosedStateException will be raised.

Enum values:

-   ignore
    
-   fail
    
-   silent
    





 | ignore | Kinesis2ShardClosedStrategyEnum |
| **shardId** (consumer) | Defines which shardId in the Kinesis stream to get records from. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS Kinesis endpoint is configured using URI syntax:

aws2-kinesis:streamName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **streamName** (common) | **Required** Name of the stream. |  | String |

### Query Parameters (37 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonKinesisClient** (common) | **Autowired** Amazon Kinesis client to use for all requests for this endpoint. |  | KinesisClient |
| **cborEnabled** (common) | This option will set the CBOR\_ENABLED property during the execution. | true | boolean |
| **overrideEndpoint** (common) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **proxyHost** (common) | To define a proxy host when instantiating the Kinesis client. |  | String |
| **proxyPort** (common) | To define a proxy port when instantiating the Kinesis client. |  | Integer |
| **proxyProtocol** (common) | 
To define a proxy protocol when instantiating the Kinesis client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (common) | The region in which Kinesis Firehose client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (common) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (common) | Set whether the Kinesis client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
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
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **sequenceNumber** (consumer) | The sequence number to start polling from. Required if iteratorType is set to AFTER\_SEQUENCE\_NUMBER or AT\_SEQUENCE\_NUMBER. |  | String |
| **shardClosed** (consumer) | 

Define what will be the behavior in case of shard closed. Possible value are ignore, silent and fail. In case of ignore a message will be logged and the consumer will restart from the beginning,in case of silent there will be no logging and the consumer will start from the beginning,in case of fail a ReachedClosedStateException will be raised.

Enum values:

-   ignore
    
-   fail
    
-   silent
    





 | ignore | Kinesis2ShardClosedStrategyEnum |
| **shardId** (consumer) | Defines which shardId in the Kinesis stream to get records from. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
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
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. |  | Map |
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

Required Kinesis component options

You have to provide the KinesisClient in the Registry with proxies and relevant credentials configured.

## Batch Consumer

This component implements the Batch Consumer.

This allows you for instance to know how many messages exists in this batch and for instance let the Aggregator aggregate this number of messages.

## Usage

### Static credentials vs Default Credential Provider

You have the possibility of avoiding the usage of explicit static credentials, by specifying the useDefaultCredentialsProvider option and set it to true.

-   Java system properties - aws.accessKeyId and aws.secretKey
    
-   Environment variables - AWS\_ACCESS\_KEY\_ID and AWS\_SECRET\_ACCESS\_KEY.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable AWS\_CONTAINER\_CREDENTIALS\_RELATIVE\_URI is set.
    
-   Amazon EC2 Instance profile credentials.
    

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

## Message Headers

The AWS Kinesis component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsKinesisSequenceNumber** (common) Constant: [`SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#SEQUENCE_NUMBER) | The sequence number of the record, as defined in [http://docs.aws.amazon.com/kinesis/latest/APIReference/API\_PutRecord.html#API\_PutRecord\_ResponseSyntaxResponse](http://docs.aws.amazon.com/kinesis/latest/APIReference/API_PutRecord.html#API_PutRecord_ResponseSyntaxResponse) Syntax. |  | String |
| **CamelAwsKinesisApproximateArrivalTimestamp** (common) Constant: [`APPROX_ARRIVAL_TIME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#APPROX_ARRIVAL_TIME) | The time AWS assigned as the arrival time of the record. |  | String |
| **CamelAwsKinesisPartitionKey** (common) Constant: [`PARTITION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#PARTITION_KEY) | Identifies which shard in the stream the data record is assigned to. |  | String |
| **CamelMessageTimestamp** (common) Constant: [`MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#MESSAGE_TIMESTAMP) | The timestamp of the message. |  | long |
| **CamelAwsKinesisShardId** (common) Constant: [`SHARD_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/kinesis/Kinesis2Constants.html#SHARD_ID) | The shard ID of the shard where the data record was placed. |  | String |

### AmazonKinesis configuration

You then have to reference the KinesisClient in the `amazonKinesisClient` URI option.

```java
from("aws2-kinesis://mykinesisstream?amazonKinesisClient=#kinesisClient")
  .to("log:out?showAll=true");
```

### Providing AWS Credentials

It is recommended that the credentials are obtained by using the [DefaultAWSCredentialsProviderChain](http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/auth/DefaultAWSCredentialsProviderChain.md) that is the default when creating a new ClientConfiguration instance, however, a different [AWSCredentialsProvider](http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/auth/AWSCredentialsProvider.md) can be specified when calling createClient(…​).

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

The component supports 39 options, which are listed below.

   
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
| **camel.component.aws2-kinesis-firehose.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-kinesis-firehose.proxy-host** | To define a proxy host when instantiating the Kinesis Firehose client. |  | String |
| **camel.component.aws2-kinesis-firehose.proxy-port** | To define a proxy port when instantiating the Kinesis Firehose client. |  | Integer |
| **camel.component.aws2-kinesis-firehose.proxy-protocol** | To define a proxy protocol when instantiating the Kinesis Firehose client. |  | Protocol |
| **camel.component.aws2-kinesis-firehose.region** | The region in which Kinesis Firehose client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-kinesis-firehose.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-kinesis-firehose.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-kinesis-firehose.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-kinesis-firehose.use-default-credentials-provider** | Set whether the Kinesis Firehose client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-kinesis.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-kinesis.amazon-kinesis-client** | Amazon Kinesis client to use for all requests for this endpoint. The option is a software.amazon.awssdk.services.kinesis.KinesisClient type. |  | KinesisClient |
| **camel.component.aws2-kinesis.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-kinesis.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.aws2-kinesis.cbor-enabled** | This option will set the CBOR\_ENABLED property during the execution. | true | Boolean |
| **camel.component.aws2-kinesis.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.kinesis.Kinesis2Configuration type. |  | Kinesis2Configuration |
| **camel.component.aws2-kinesis.enabled** | Whether to enable auto configuration of the aws2-kinesis component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-kinesis.iterator-type** | Defines where in the Kinesis stream to start getting records. |  | ShardIteratorType |
| **camel.component.aws2-kinesis.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-kinesis.max-results-per-request** | Maximum number of records that will be fetched in each poll. | 1 | Integer |
| **camel.component.aws2-kinesis.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-kinesis.proxy-host** | To define a proxy host when instantiating the Kinesis client. |  | String |
| **camel.component.aws2-kinesis.proxy-port** | To define a proxy port when instantiating the Kinesis client. |  | Integer |
| **camel.component.aws2-kinesis.proxy-protocol** | To define a proxy protocol when instantiating the Kinesis client. |  | Protocol |
| **camel.component.aws2-kinesis.region** | The region in which Kinesis Firehose client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-kinesis.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-kinesis.sequence-number** | The sequence number to start polling from. Required if iteratorType is set to AFTER\_SEQUENCE\_NUMBER or AT\_SEQUENCE\_NUMBER. |  | String |
| **camel.component.aws2-kinesis.shard-closed** | Define what will be the behavior in case of shard closed. Possible value are ignore, silent and fail. In case of ignore a message will be logged and the consumer will restart from the beginning,in case of silent there will be no logging and the consumer will start from the beginning,in case of fail a ReachedClosedStateException will be raised. |  | Kinesis2ShardClosedStrategyEnum |
| **camel.component.aws2-kinesis.shard-id** | Defines which shardId in the Kinesis stream to get records from. |  | String |
| **camel.component.aws2-kinesis.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-kinesis.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-kinesis.use-default-credentials-provider** | Set whether the Kinesis client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |