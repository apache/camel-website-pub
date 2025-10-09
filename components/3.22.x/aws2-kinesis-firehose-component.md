# AWS Kinesis Firehose

**Since Camel 3.2**

**Only producer is supported**

The AWS2 Kinesis Firehose component supports sending messages to Amazon Kinesis Firehose service (Batch not supported).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Kinesis Firehose. More information are available at [AWS Kinesis Firehose](https://aws.amazon.com/kinesis/firehose/)

> **Note**
> The AWS2 Kinesis Firehose component is not supported in OSGI

## URI Format

```java
aws2-kinesis-firehose://delivery-stream-name[?options]
```

The stream needs to be created prior to it being used.  
You can append query options to the URI in the following format, ?options=value&option2=value&…​

## URI Options

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

The AWS Kinesis Firehose component supports 16 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonKinesisFirehoseClient** (producer) | **Autowired** Amazon Kinesis Firehose client to use for all requests for this endpoint. |  | FirehoseClient |
| **cborEnabled** (common) | This option will set the CBOR\_ENABLED property during the execution. | true | boolean |
| **configuration** (producer) | Component configuration. |  | KinesisFirehose2Configuration |
| **overrideEndpoint** (common) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to do in case the user don’t want to send only a record.

Enum values:

-   sendBatchRecord
    
-   createDeliveryStream
    
-   deleteDeliveryStream
    
-   describeDeliveryStream
    
-   updateDestination
    





 |  | KinesisFirehose2Operations |
| **proxyHost** (producer) | To define a proxy host when instantiating the Kinesis Firehose client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the Kinesis Firehose client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the Kinesis Firehose client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which Kinesis Firehose client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (common) | Set whether the Kinesis Firehose client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS Kinesis Firehose endpoint is configured using URI syntax:

aws2-kinesis-firehose:streamName

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **streamName** (producer) | **Required** Name of the stream. |  | String |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonKinesisFirehoseClient** (producer) | **Autowired** Amazon Kinesis Firehose client to use for all requests for this endpoint. |  | FirehoseClient |
| **cborEnabled** (common) | This option will set the CBOR\_ENABLED property during the execution. | true | boolean |
| **overrideEndpoint** (common) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **operation** (producer) | 
The operation to do in case the user don’t want to send only a record.

Enum values:

-   sendBatchRecord
    
-   createDeliveryStream
    
-   deleteDeliveryStream
    
-   describeDeliveryStream
    
-   updateDestination
    





 |  | KinesisFirehose2Operations |
| **proxyHost** (producer) | To define a proxy host when instantiating the Kinesis Firehose client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the Kinesis Firehose client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the Kinesis Firehose client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **region** (producer) | The region in which Kinesis Firehose client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (common) | Set whether the Kinesis Firehose client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

Required Kinesis Firehose component options

You have to provide the FirehoseClient in the Registry with proxies and relevant credentials configured.

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

The AWS Kinesis Firehose component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsKinesisFirehoseRecordId** (producer) Constant: [`RECORD_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/firehose/KinesisFirehose2Constants.html#RECORD_ID) | The record ID, as defined in [http://docs.aws.amazon.com/firehose/latest/APIReference/API\_PutRecord.html#API\_PutRecord\_ResponseSyntaxResponse](http://docs.aws.amazon.com/firehose/latest/APIReference/API_PutRecord.html#API_PutRecord_ResponseSyntaxResponse) Syntax. |  | String |
| **CamelAwsKinesisFirehoseOperation** (producer) Constant: [`KINESIS_FIREHOSE_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/firehose/KinesisFirehose2Constants.html#KINESIS_FIREHOSE_OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsKinesisFirehoseDeliveryStreamName** (producer) Constant: [`KINESIS_FIREHOSE_STREAM_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/firehose/KinesisFirehose2Constants.html#KINESIS_FIREHOSE_STREAM_NAME) | The name of the delivery stream. |  | String |

### Amazon Kinesis Firehose configuration

You then have to reference the FirehoseClient in the `amazonKinesisFirehoseClient` URI option.

```java
from("aws2-kinesis-firehose://mykinesisdeliverystream?amazonKinesisFirehoseClient=#kinesisClient")
  .to("log:out?showAll=true");
```

### Providing AWS Credentials

It is recommended that the credentials are obtained by using the [DefaultAWSCredentialsProviderChain](http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/auth/DefaultAWSCredentialsProviderChain.md) that is the default when creating a new ClientConfiguration instance, however, a different [AWSCredentialsProvider](http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/auth/AWSCredentialsProvider.md) can be specified when calling createClient(…​).

### Kinesis Firehose Producer operations

Camel-AWS s3 component provides the following operation on the producer side:

-   SendBatchRecord
    
-   CreateDeliveryStream
    
-   DeleteDeliveryStream
    
-   DescribeDeliveryStream
    
-   UpdateDestination
    

### Send Batch Records Example

You can send an iterable of Kinesis Record (as the following example shows) or you can send directly a PutRecordBatchRequest POJO instance in the body.

```java
    @Test
    public void testFirehoseBatchRouting() throws Exception {
        Exchange exchange = template.send("direct:start", ExchangePattern.InOnly, new Processor() {
            public void process(Exchange exchange) throws Exception {
                List<Record> recs = new ArrayList<Record>();
                Record rec = Record.builder().data(SdkBytes.fromString("Test1", Charset.defaultCharset())).build();
                Record rec1 = Record.builder().data(SdkBytes.fromString("Test2", Charset.defaultCharset())).build();
                recs.add(rec);
                recs.add(rec1);
                exchange.getIn().setBody(recs);
            }
        });
        assertNotNull(exchange.getIn().getBody());
    }

from("direct:start").to("aws2-kinesis-firehose://cc?amazonKinesisFirehoseClient=#FirehoseClient&operation=sendBatchRecord");
```

In the deliveryStream you’ll find "Test1Test2".

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

When using aws2-kinesis-firehose with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

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