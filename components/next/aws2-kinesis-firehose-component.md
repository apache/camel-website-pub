# AWS Kinesis Firehose

**Since Camel 3.2**

**Only producer is supported**

The AWS2 Kinesis Firehose component supports sending messages to Amazon Kinesis Firehose service (Batch not supported).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Kinesis Firehose. More information is available at [AWS Kinesis Firehose](https://aws.amazon.com/kinesis/firehose/)

## URI Format

```java
aws2-kinesis-firehose://delivery-stream-name[?options]
```

The stream needs to be created prior to it being used.

You can append query options to the URI in the following format:

`?options=value&option2=value&…​`

## URI Options

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

The AWS Kinesis Firehose component supports 20 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cborEnabled** (common) | This option will set the CBOR\_ENABLED property during the execution. | true | boolean |
| **configuration** (producer) | Component configuration. |  | KinesisFirehose2Configuration |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
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
| **region** (producer) | 

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
| **useDefaultCredentialsProvider** (common) | Set whether the Kinesis Firehose client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **amazonKinesisFirehoseClient** (advanced) | **Autowired** Amazon Kinesis Firehose client to use for all requests for this endpoint. |  | FirehoseClient |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Kinesis Firehose client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Kinesis Firehose client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Kinesis Firehose client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Kinesis Firehose client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Kinesis Firehose client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis Firehose. | false | boolean |

## Endpoint Options

The AWS Kinesis Firehose endpoint is configured using URI syntax:

aws2-kinesis-firehose:streamName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **streamName** (producer) | **Required** Name of the stream. |  | String |

### Query Parameters (18 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cborEnabled** (common) | This option will set the CBOR\_ENABLED property during the execution. | true | boolean |
| **overrideEndpoint** (common) | Set the need for overriding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **uriEndpointOverride** (common) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **operation** (producer) | 
The operation to do in case the user don’t want to send only a record.

Enum values:

-   sendBatchRecord
    
-   createDeliveryStream
    
-   deleteDeliveryStream
    
-   describeDeliveryStream
    
-   updateDestination
    





 |  | KinesisFirehose2Operations |
| **region** (producer) | 

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
| **useDefaultCredentialsProvider** (common) | Set whether the Kinesis Firehose client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **amazonKinesisFirehoseClient** (advanced) | **Autowired** Amazon Kinesis Firehose client to use for all requests for this endpoint. |  | FirehoseClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the Kinesis Firehose client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the Kinesis Firehose client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the Kinesis Firehose client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the Kinesis Firehose client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the Kinesis Firehose client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis Firehose. | false | boolean |

## Message Headers

The AWS Kinesis Firehose component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsKinesisFirehoseRecordId** (producer) Constant: [`RECORD_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/firehose/KinesisFirehose2Constants.html#RECORD_ID) | The record ID, as defined in [http://docs.aws.amazon.com/firehose/latest/APIReference/API\_PutRecord.html#API\_PutRecord\_ResponseSyntaxResponse](http://docs.aws.amazon.com/firehose/latest/APIReference/API_PutRecord.html#API_PutRecord_ResponseSyntaxResponse) Syntax. |  | String |
| **CamelAwsKinesisFirehoseOperation** (producer) Constant: [`KINESIS_FIREHOSE_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/firehose/KinesisFirehose2Constants.html#KINESIS_FIREHOSE_OPERATION) | The operation we want to perform. |  | String |
| **CamelAwsKinesisFirehoseDeliveryStreamName** (producer) Constant: [`KINESIS_FIREHOSE_STREAM_NAME`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/firehose/KinesisFirehose2Constants.html#KINESIS_FIREHOSE_STREAM_NAME) | The name of the delivery stream. |  | String |
| **CamelAwsKinesisFirehoseDeliveryStreamArn** (createDeliveryStream) Constant: [`DELIVERY_STREAM_ARN`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/firehose/KinesisFirehose2Constants.html#DELIVERY_STREAM_ARN) | The ARN of the delivery stream. |  | String |
| **CamelAwsKinesisFirehoseFailedRecordCount** (sendBatchRecord) Constant: [`FAILED_RECORD_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/firehose/KinesisFirehose2Constants.html#FAILED_RECORD_COUNT) | The number of records that failed in a batch put operation. |  | Integer |
| **CamelAwsKinesisFirehoseEncrypted** (sendBatchRecord) Constant: [`ENCRYPTED`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/firehose/KinesisFirehose2Constants.html#ENCRYPTED) | Whether the batch operation was encrypted. |  | Boolean |
| **CamelAwsKinesisFirehoseDeliveryStreamStatus** (describeDeliveryStream) Constant: [`DELIVERY_STREAM_STATUS`](https://javadoc.io/doc/org.apache.camel/camel-aws2-kinesis/latest/org/apache/camel/component/aws2/firehose/KinesisFirehose2Constants.html#DELIVERY_STREAM_STATUS) | The status of the delivery stream. |  | String |

Required Kinesis Firehose component options

You have to provide the FirehoseClient in the Registry with proxies and relevant credentials configured.

## Usage

### Static credentials, Default Credential Provider and Profile Credentials Provider

You have the possibility of avoiding the usage of explicit static credentials by specifying the useDefaultCredentialsProvider option and set it to true.

The order of evaluation for Default Credentials Provider is the following:

-   Java system properties - `aws.accessKeyId` and `aws.secretKey`
    
-   Environment variables - `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
    
-   Web Identity Token from AWS STS.
    
-   The shared credentials and config files.
    
-   Amazon ECS container credentials - loaded from the Amazon ECS if the environment variable `AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is set.
    
-   Amazon EC2 Instance profile credentials.
    

You have also the possibility of using Profile Credentials Provider, by specifying the useProfileCredentialsProvider option to true and profileCredentialsName to the profile name.

Only one of static, default and profile credentials could be used at the same time.

For more information about this you can look at [AWS credentials documentation](https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.md)

### Amazon Kinesis Firehose configuration

You then have to reference the FirehoseClient in the `amazonKinesisFirehoseClient` URI option.

-   Java
    
-   XML
    
-   YAML
    

```java
from("aws2-kinesis-firehose://mykinesisdeliverystream?amazonKinesisFirehoseClient=#kinesisClient")
    .to("log:out?showAll=true");
```

```xml
<route>
  <from uri="aws2-kinesis-firehose://mykinesisdeliverystream?amazonKinesisFirehoseClient=#kinesisClient"/>
  <to uri="log:out?showAll=true"/>
</route>
```

```yaml
- route:
    from:
      uri: aws2-kinesis-firehose://mykinesisdeliverystream
      parameters:
        amazonKinesisFirehoseClient: "#kinesisClient"
      steps:
        - to:
            uri: log:out
            parameters:
              showAll: true
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

You can send an iterable of Kinesis Record (as the following example shows), or you can send directly a PutRecordBatchRequest POJO instance in the body.

_Java-only: uses ProducerTemplate, inline Processor, and AWS SDK builders_

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