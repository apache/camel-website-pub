# AWS DynamoDB Streams

**Since Camel 3.1**

**Only consumer is supported**

The AWS2 DynamoDB Stream component supports receiving messages from Amazon DynamoDB Stream service.

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon DynamoDB Streams. More information are available at [AWS DynamoDB](https://aws.amazon.com/dynamodb/)

## URI Format

aws2-ddbstream://table-name\[?options\]

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

The AWS DynamoDB Streams component supports 16 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonDynamoDbStreamsClient** (consumer) | **Autowired** Amazon DynamoDB client to use for all requests for this endpoint. |  | DynamoDbStreamsClient |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **configuration** (consumer) | The component configuration. |  | Ddb2StreamConfiguration |
| **maxResultsPerRequest** (consumer) | Maximum number of records that will be fetched in each poll. |  | int |
| **overrideEndpoint** (consumer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **proxyHost** (consumer) | To define a proxy host when instantiating the DDBStreams client. |  | String |
| **proxyPort** (consumer) | To define a proxy port when instantiating the DDBStreams client. |  | Integer |
| **proxyProtocol** (consumer) | 
To define a proxy protocol when instantiating the DDBStreams client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (consumer) | The region in which DDBStreams client needs to work. |  | String |
| **streamIteratorType** (consumer) | 

Defines where in the DynamoDB stream to start getting records. Note that using FROM\_START can cause a significant delay before the stream has caught up to real-time.

Enum values:

-   FROM\_LATEST
    
-   FROM\_START
    





 | FROM\_LATEST | StreamIteratorType |
| **trustAllCertificates** (consumer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (consumer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (consumer) | Set whether the DynamoDB Streams client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS DynamoDB Streams endpoint is configured using URI syntax:

aws2-ddbstream:tableName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **tableName** (consumer) | **Required** Name of the dynamodb table. |  | String |

### Query Parameters (32 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonDynamoDbStreamsClient** (consumer) | **Autowired** Amazon DynamoDB client to use for all requests for this endpoint. |  | DynamoDbStreamsClient |
| **maxResultsPerRequest** (consumer) | Maximum number of records that will be fetched in each poll. |  | int |
| **overrideEndpoint** (consumer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **proxyHost** (consumer) | To define a proxy host when instantiating the DDBStreams client. |  | String |
| **proxyPort** (consumer) | To define a proxy port when instantiating the DDBStreams client. |  | Integer |
| **proxyProtocol** (consumer) | 
To define a proxy protocol when instantiating the DDBStreams client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (consumer) | The region in which DDBStreams client needs to work. |  | String |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **streamIteratorType** (consumer) | 

Defines where in the DynamoDB stream to start getting records. Note that using FROM\_START can cause a significant delay before the stream has caught up to real-time.

Enum values:

-   FROM\_LATEST
    
-   FROM\_START
    





 | FROM\_LATEST | StreamIteratorType |
| **trustAllCertificates** (consumer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (consumer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (consumer) | Set whether the DynamoDB Streams client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
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

Required DynamoDBStream component options

You have to provide the DynamoDbStreamsClient in the Registry with proxies and relevant credentials configured.

## Sequence Numbers

You can provide a literal string as the sequence number or provide a bean in the registry. An example of using the bean would be to save your current position in the change feed and restore it on Camel startup.

It is an error to provide a sequence number that is greater than the largest sequence number in the describe-streams result, as this will lead to the AWS call returning an HTTP 400.

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

## Coping with Downtime

### AWS DynamoDB Streams outage of less than 24 hours

The consumer will resume from the last seen sequence number (as implemented for [CAMEL-9515](https://issues.apache.org/jira/browse/CAMEL-9515)), so you should receive a flood of events in quick succession, as long as the outage did not also include DynamoDB itself.

### AWS DynamoDB Streams outage of more than 24 hours

Given that AWS only retain 24 hours worth of changes, you will have missed change events no matter what mitigations are in place.

### Message Body

The Message body is instance of "software.amazon.awssdk.services.dynamodb.model.Record", for more information about it, have a look at the [related javadoc](https://sdk.amazonaws.com/java/api/latest/software/amazon/awssdk/services/dynamodb/model/Record.md)

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-ddb</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-ddbstream with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-ddb-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 40 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-ddb.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-ddb.amazon-d-d-b-client** | To use the AmazonDynamoDB as the client. The option is a software.amazon.awssdk.services.dynamodb.DynamoDbClient type. |  | DynamoDbClient |
| **camel.component.aws2-ddb.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-ddb.configuration** | The component configuration. The option is a org.apache.camel.component.aws2.ddb.Ddb2Configuration type. |  | Ddb2Configuration |
| **camel.component.aws2-ddb.consistent-read** | Determines whether or not strong consistency should be enforced when data is read. | false | Boolean |
| **camel.component.aws2-ddb.enabled** | Whether to enable auto configuration of the aws2-ddb component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-ddb.enabled-initial-describe-table** | Set whether the initial Describe table operation in the DDB Endpoint must be done, or not. | true | Boolean |
| **camel.component.aws2-ddb.key-attribute-name** | Attribute name when creating table. |  | String |
| **camel.component.aws2-ddb.key-attribute-type** | Attribute type when creating table. |  | String |
| **camel.component.aws2-ddb.key-scalar-type** | The key scalar type, it can be S (String), N (Number) and B (Bytes). |  | String |
| **camel.component.aws2-ddb.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-ddb.operation** | What operation to perform. |  | Ddb2Operations |
| **camel.component.aws2-ddb.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-ddb.proxy-host** | To define a proxy host when instantiating the DDB client. |  | String |
| **camel.component.aws2-ddb.proxy-port** | The region in which DynamoDB client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | Integer |
| **camel.component.aws2-ddb.proxy-protocol** | To define a proxy protocol when instantiating the DDB client. |  | Protocol |
| **camel.component.aws2-ddb.read-capacity** | The provisioned throughput to reserve for reading resources from your table. |  | Long |
| **camel.component.aws2-ddb.region** | The region in which DDB client needs to work. |  | String |
| **camel.component.aws2-ddb.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-ddb.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-ddb.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-ddb.use-default-credentials-provider** | Set whether the S3 client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |
| **camel.component.aws2-ddb.write-capacity** | The provisioned throughput to reserved for writing resources to your table. |  | Long |
| **camel.component.aws2-ddbstream.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-ddbstream.amazon-dynamo-db-streams-client** | Amazon DynamoDB client to use for all requests for this endpoint. The option is a software.amazon.awssdk.services.dynamodb.streams.DynamoDbStreamsClient type. |  | DynamoDbStreamsClient |
| **camel.component.aws2-ddbstream.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-ddbstream.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.aws2-ddbstream.configuration** | The component configuration. The option is a org.apache.camel.component.aws2.ddbstream.Ddb2StreamConfiguration type. |  | Ddb2StreamConfiguration |
| **camel.component.aws2-ddbstream.enabled** | Whether to enable auto configuration of the aws2-ddbstream component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-ddbstream.max-results-per-request** | Maximum number of records that will be fetched in each poll. |  | Integer |
| **camel.component.aws2-ddbstream.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-ddbstream.proxy-host** | To define a proxy host when instantiating the DDBStreams client. |  | String |
| **camel.component.aws2-ddbstream.proxy-port** | To define a proxy port when instantiating the DDBStreams client. |  | Integer |
| **camel.component.aws2-ddbstream.proxy-protocol** | To define a proxy protocol when instantiating the DDBStreams client. |  | Protocol |
| **camel.component.aws2-ddbstream.region** | The region in which DDBStreams client needs to work. |  | String |
| **camel.component.aws2-ddbstream.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-ddbstream.stream-iterator-type** | Defines where in the DynamoDB stream to start getting records. Note that using FROM\_START can cause a significant delay before the stream has caught up to real-time. |  | Ddb2StreamConfiguration$StreamIteratorType |
| **camel.component.aws2-ddbstream.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-ddbstream.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-ddbstream.use-default-credentials-provider** | Set whether the DynamoDB Streams client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | Boolean |