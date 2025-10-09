# AWS Simple Notification System (SNS)

**Since Camel 3.1**

**Only producer is supported**

The AWS2 SNS component allows messages to be sent to an [Amazon Simple Notification](https://aws.amazon.com/sns) Topic. The implementation of the Amazon API is provided by the [AWS SDK](https://aws.amazon.com/sdkforjava/).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon SNS. More information is available at [Amazon SNS](https://aws.amazon.com/sns).

## URI Format

aws2-sns://topicNameOrArn\[?options\]

The topic will be created if they don’t already exists.  
You can append query options to the URI in the following format, `?options=value&option2=value&…​`

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

The AWS Simple Notification System (SNS) component supports 24 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonSNSClient** (producer) | **Autowired** To use the AmazonSNS as the client. |  | SnsClient |
| **autoCreateTopic** (producer) | Setting the autocreation of the topic. | false | boolean |
| **configuration** (producer) | Component configuration. |  | Sns2Configuration |
| **kmsMasterKeyId** (producer) | The ID of an AWS-managed customer master key (CMK) for Amazon SNS or a custom CMK. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **messageDeduplicationIdStrategy** (producer) | 
Only for FIFO Topic. Strategy for setting the messageDeduplicationId on the message. Can be one of the following options: useExchangeId, useContentBasedDeduplication. For the useContentBasedDeduplication option, no messageDeduplicationId will be set on the message.

Enum values:

-   useExchangeId
    
-   useContentBasedDeduplication
    





 | useExchangeId | String |
| **messageGroupIdStrategy** (producer) | 

Only for FIFO Topic. Strategy for setting the messageGroupId on the message. Can be one of the following options: useConstant, useExchangeId, usePropertyValue. For the usePropertyValue option, the value of property CamelAwsMessageGroupId will be used.

Enum values:

-   useConstant
    
-   useExchangeId
    
-   usePropertyValue
    





 |  | String |
| **messageStructure** (producer) | The message structure to use such as json. |  | String |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **policy** (producer) | The policy for this topic. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **proxyHost** (producer) | To define a proxy host when instantiating the SNS client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the SNS client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the SNS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **queueUrl** (producer) | The queueUrl to subscribe to. |  | String |
| **region** (producer) | The region in which SNS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **serverSideEncryptionEnabled** (producer) | Define if Server Side Encryption is enabled or not on the topic. | false | boolean |
| **subject** (producer) | The subject which is used if the message header 'CamelAwsSnsSubject' is not present. |  | String |
| **subscribeSNStoSQS** (producer) | Define if the subscription between SNS Topic and SQS must be done or not. | false | boolean |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the SNS client should expect to load credentials on an AWS infra instance or to expect static credentials to be passed in. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

## Endpoint Options

The AWS Simple Notification System (SNS) endpoint is configured using URI syntax:

aws2-sns:topicNameOrArn

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topicNameOrArn** (producer) | **Required** Topic name or ARN. |  | String |

### Query Parameters (23 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amazonSNSClient** (producer) | **Autowired** To use the AmazonSNS as the client. |  | SnsClient |
| **autoCreateTopic** (producer) | Setting the autocreation of the topic. | false | boolean |
| **headerFilterStrategy** (producer) | To use a custom HeaderFilterStrategy to map headers to/from Camel. |  | HeaderFilterStrategy |
| **kmsMasterKeyId** (producer) | The ID of an AWS-managed customer master key (CMK) for Amazon SNS or a custom CMK. |  | String |
| **messageDeduplicationIdStrategy** (producer) | 
Only for FIFO Topic. Strategy for setting the messageDeduplicationId on the message. Can be one of the following options: useExchangeId, useContentBasedDeduplication. For the useContentBasedDeduplication option, no messageDeduplicationId will be set on the message.

Enum values:

-   useExchangeId
    
-   useContentBasedDeduplication
    





 | useExchangeId | String |
| **messageGroupIdStrategy** (producer) | 

Only for FIFO Topic. Strategy for setting the messageGroupId on the message. Can be one of the following options: useConstant, useExchangeId, usePropertyValue. For the usePropertyValue option, the value of property CamelAwsMessageGroupId will be used.

Enum values:

-   useConstant
    
-   useExchangeId
    
-   usePropertyValue
    





 |  | String |
| **messageStructure** (producer) | The message structure to use such as json. |  | String |
| **overrideEndpoint** (producer) | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | boolean |
| **policy** (producer) | The policy for this topic. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **proxyHost** (producer) | To define a proxy host when instantiating the SNS client. |  | String |
| **proxyPort** (producer) | To define a proxy port when instantiating the SNS client. |  | Integer |
| **proxyProtocol** (producer) | 

To define a proxy protocol when instantiating the SNS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **queueUrl** (producer) | The queueUrl to subscribe to. |  | String |
| **region** (producer) | The region in which SNS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **serverSideEncryptionEnabled** (producer) | Define if Server Side Encryption is enabled or not on the topic. | false | boolean |
| **subject** (producer) | The subject which is used if the message header 'CamelAwsSnsSubject' is not present. |  | String |
| **subscribeSNStoSQS** (producer) | Define if the subscription between SNS Topic and SQS must be done or not. | false | boolean |
| **trustAllCertificates** (producer) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **useDefaultCredentialsProvider** (producer) | Set whether the SNS client should expect to load credentials on an AWS infra instance or to expect static credentials to be passed in. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |

Required SNS component options

You have to provide the amazonSNSClient in the Registry or your accessKey and secretKey to access the [Amazon’s SNS](https://aws.amazon.com/sns).

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

The AWS Simple Notification System (SNS) component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsSnsMessageId** (producer) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sns/latest/org/apache/camel/component/aws2/sns/Sns2Constants.html#MESSAGE_ID) | The Amazon SNS message ID. |  | String |
| **CamelAwsSnsSubject** (producer) Constant: [`SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sns/latest/org/apache/camel/component/aws2/sns/Sns2Constants.html#SUBJECT) | The Amazon SNS message subject. If not set, the subject from the SnsConfiguration is used. |  | String |
| **CamelAwsSnsMessageStructure** (producer) Constant: [`MESSAGE_STRUCTURE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sns/latest/org/apache/camel/component/aws2/sns/Sns2Constants.html#MESSAGE_STRUCTURE) | The message structure to use such as json. |  | String |

### Advanced AmazonSNS configuration

If you need more control over the `SnsClient` instance configuration you can create your own instance and refer to it from the URI:

```java
from("direct:start")
.to("aws2-sns://MyTopic?amazonSNSClient=#client");
```

The `#client` refers to a `AmazonSNS` in the Registry.

### Create a subscription between an AWS SNS Topic and an AWS SQS Queue

You can create a subscription of an SQS Queue to an SNS Topic in this way:

```java
from("direct:start")
.to("aws2-sns://test-camel-sns1?amazonSNSClient=#amazonSNSClient&subscribeSNStoSQS=true&queueUrl=https://sqs.eu-central-1.amazonaws.com/780410022472/test-camel");
```

The `#amazonSNSClient` refers to a `SnsClient` in the Registry. By specifying `subscribeSNStoSQS` to true and a `queueUrl` of an existing SQS Queue, you’ll be able to subscribe your SQS Queue to your SNS Topic.

At this point you can consume messages coming from SNS Topic through your SQS Queue

```java
from("aws2-sqs://test-camel?amazonSQSClient=#amazonSQSClient&delay=50&maxMessagesPerPoll=5")
    .to(...);
```

## Topic Autocreation

With the option `autoCreateTopic` users are able to avoid the autocreation of an SNS Topic in case it doesn’t exist. The default for this option is `false`. If set to false any operation on a not-existent topic in AWS won’t be successful and an error will be returned.

## SNS FIFO

SNS FIFO are supported. While creating the SQS queue you will subscribe to the SNS topic there is an important point to remember, you’ll need to make possible for the SNS Topic to send message to the SQS Queue.

This is clear with an example.

Suppose you created an SNS FIFO Topic called Order.fifo and an SQS Queue called QueueSub.fifo.

In the access Policy of the QueueSub.fifo you should submit something like this

```json
{
  "Version": "2008-10-17",
  "Id": "__default_policy_ID",
  "Statement": [
    {
      "Sid": "__owner_statement",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::780560123482:root"
      },
      "Action": "SQS:*",
      "Resource": "arn:aws:sqs:eu-west-1:780560123482:QueueSub.fifo"
    },
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "sns.amazonaws.com"
      },
      "Action": "SQS:SendMessage",
      "Resource": "arn:aws:sqs:eu-west-1:780560123482:QueueSub.fifo",
      "Condition": {
        "ArnLike": {
          "aws:SourceArn": "arn:aws:sns:eu-west-1:780410022472:Order.fifo"
        }
      }
    }
  ]
}
```

This is a critical step to make the subscription work correctly.

### SNS Fifo Topic Message group Id Strategy and message Deduplication Id Strategy

When sending something to the FIFO topic you’ll need to always set up a message group Id strategy.

If the content-based message deduplication has been enabled on the SNS Fifo topic, where won’t be the need of setting a message deduplication id strategy, otherwise you’ll have to set it.

## Examples

### Producer Examples

Sending to a topic

```java
from("direct:start")
  .to("aws2-sns://camel-topic?subject=The+subject+message&autoCreateTopic=true");
```

## Dependencies

Maven users will need to add the following dependency to their pom.xml.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-aws2-sns</artifactId>
    <version>${camel-version}</version>
</dependency>
```

where `${camel-version}` must be replaced by the actual version of Camel.

## Spring Boot Auto-Configuration

When using aws2-sns with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-aws2-sns-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 25 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.aws2-sns.access-key** | Amazon AWS Access Key. |  | String |
| **camel.component.aws2-sns.amazon-s-n-s-client** | To use the AmazonSNS as the client. The option is a software.amazon.awssdk.services.sns.SnsClient type. |  | SnsClient |
| **camel.component.aws2-sns.auto-create-topic** | Setting the autocreation of the topic. | false | Boolean |
| **camel.component.aws2-sns.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.aws2-sns.configuration** | Component configuration. The option is a org.apache.camel.component.aws2.sns.Sns2Configuration type. |  | Sns2Configuration |
| **camel.component.aws2-sns.enabled** | Whether to enable auto configuration of the aws2-sns component. This is enabled by default. |  | Boolean |
| **camel.component.aws2-sns.kms-master-key-id** | The ID of an AWS-managed customer master key (CMK) for Amazon SNS or a custom CMK. |  | String |
| **camel.component.aws2-sns.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.aws2-sns.message-deduplication-id-strategy** | Only for FIFO Topic. Strategy for setting the messageDeduplicationId on the message. Can be one of the following options: useExchangeId, useContentBasedDeduplication. For the useContentBasedDeduplication option, no messageDeduplicationId will be set on the message. | useExchangeId | String |
| **camel.component.aws2-sns.message-group-id-strategy** | Only for FIFO Topic. Strategy for setting the messageGroupId on the message. Can be one of the following options: useConstant, useExchangeId, usePropertyValue. For the usePropertyValue option, the value of property CamelAwsMessageGroupId will be used. |  | String |
| **camel.component.aws2-sns.message-structure** | The message structure to use such as json. |  | String |
| **camel.component.aws2-sns.override-endpoint** | Set the need for overidding the endpoint. This option needs to be used in combination with uriEndpointOverride option. | false | Boolean |
| **camel.component.aws2-sns.policy** | The policy for this topic. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **camel.component.aws2-sns.proxy-host** | To define a proxy host when instantiating the SNS client. |  | String |
| **camel.component.aws2-sns.proxy-port** | To define a proxy port when instantiating the SNS client. |  | Integer |
| **camel.component.aws2-sns.proxy-protocol** | To define a proxy protocol when instantiating the SNS client. |  | Protocol |
| **camel.component.aws2-sns.queue-url** | The queueUrl to subscribe to. |  | String |
| **camel.component.aws2-sns.region** | The region in which SNS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id(). |  | String |
| **camel.component.aws2-sns.secret-key** | Amazon AWS Secret Key. |  | String |
| **camel.component.aws2-sns.server-side-encryption-enabled** | Define if Server Side Encryption is enabled or not on the topic. | false | Boolean |
| **camel.component.aws2-sns.subject** | The subject which is used if the message header 'CamelAwsSnsSubject' is not present. |  | String |
| **camel.component.aws2-sns.subscribe-s-n-sto-s-q-s** | Define if the subscription between SNS Topic and SQS must be done or not. | false | Boolean |
| **camel.component.aws2-sns.trust-all-certificates** | If we want to trust all certificates in case of overriding the endpoint. | false | Boolean |
| **camel.component.aws2-sns.uri-endpoint-override** | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **camel.component.aws2-sns.use-default-credentials-provider** | Set whether the SNS client should expect to load credentials on an AWS infra instance or to expect static credentials to be passed in. | false | Boolean |