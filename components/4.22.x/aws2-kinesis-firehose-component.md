# AWS Kinesis Firehose

**Since Camel 3.2**

**Only producer is supported**

The AWS2 Kinesis Firehose component supports sending messages to Amazon Kinesis Firehose service (Batch not supported).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon Kinesis Firehose. More information is available at [AWS Kinesis Firehose](https://aws.amazon.com/kinesis/firehose/)

## URI Format

```text
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

The AWS Kinesis Firehose component supports the following options which are listed below.

   
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

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **streamName** (producer) | **Required** Name of the stream. |  | String |

### Query Parameters

   
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

The AWS Kinesis Firehose component supports the following message header(s), which is/are listed below:

   
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

_Java-only: uses AWS SDK `Record` builders_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setBody(List.of(
            Record.builder().data(SdkBytes.fromString("Test1", Charset.defaultCharset())).build(),
            Record.builder().data(SdkBytes.fromString("Test2", Charset.defaultCharset())).build()));
    })
    .to("aws2-kinesis-firehose://cc?amazonKinesisFirehoseClient=#FirehoseClient&operation=sendBatchRecord");
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