# AWS Simple Notification System (SNS)

**Since Camel 3.1**

**Only producer is supported**

The AWS2 SNS component allows messages to be sent to an [Amazon Simple Notification](https://aws.amazon.com/sns) Topic. The implementation of the Amazon API is provided by the [AWS SDK](https://aws.amazon.com/sdkforjava/).

Prerequisites

You must have a valid Amazon Web Services developer account, and be signed up to use Amazon SNS. More information is available at [Amazon SNS](https://aws.amazon.com/sns).

## URI Format

aws2-sns://topicNameOrArn\[?options\]

The topic will be created if they don’t already exist.

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

The AWS Simple Notification System (SNS) component supports 31 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateTopic** (producer) | Setting the auto-creation of the topic. | false | boolean |
| **batchEnabled** (producer) | Define if we are publishing a single message or a batch. | false | boolean |
| **configuration** (producer) | Component configuration. |  | Sns2Configuration |
| **kmsMasterKeyId** (producer) | The ID of an AWS-managed customer master key (CMK) for Amazon SNS or a custom CMK. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **messageDeduplicationIdStrategy** (producer) | 
Only for FIFO Topic. Strategy for setting the messageDeduplicationId on the message. It can be one of the following options: useExchangeId, useContentBasedDeduplication. For the useContentBasedDeduplication option, no messageDeduplicationId will be set on the message.

Enum values:

-   useExchangeId
    
-   useContentBasedDeduplication
    





 | useExchangeId | String |
| **messageGroupIdStrategy** (producer) | 

Only for FIFO Topic. Strategy for setting the messageGroupId on the message. It can be one of the following options: useConstant, useExchangeId, usePropertyValue. For the usePropertyValue option, the value of property CamelAwsSnsMessageGroupId will be used.

Enum values:

-   useConstant
    
-   useExchangeId
    
-   usePropertyValue
    





 |  | String |
| **messageStructure** (producer) | The message structure to use such as json. |  | String |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **policy** (producer) | The policy for this topic. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **queueArn** (producer) | The ARN endpoint to subscribe to. |  | String |
| **region** (producer) | 

The region in which the SNS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **serverSideEncryptionEnabled** (producer) | Define if Server Side Encryption is enabled or not on the topic. | false | boolean |
| **subject** (producer) | The subject which is used if the message header 'CamelAwsSnsSubject' is not present. |  | String |
| **subscribeSNStoSQS** (producer) | Define if the subscription between SNS Topic and SQS must be done or not. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **amazonSNSClient** (advanced) | **Autowired** To use the AmazonSNS as the client. |  | SnsClient |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **proxyHost** (proxy) | To define a proxy host when instantiating the SNS client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the SNS client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the SNS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the SNS client should expect to load credentials on an AWS infra instance or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the SNS client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the SNS client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in SNS. | false | boolean |

## Endpoint Options

The AWS Simple Notification System (SNS) endpoint is configured using URI syntax:

aws2-sns:topicNameOrArn

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topicNameOrArn** (producer) | **Required** Topic name or ARN. |  | String |

### Query Parameters (28 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **autoCreateTopic** (producer) | Setting the auto-creation of the topic. | false | boolean |
| **batchEnabled** (producer) | Define if we are publishing a single message or a batch. | false | boolean |
| **headerFilterStrategy** (producer) | To use a custom HeaderFilterStrategy to map headers to/from Camel. |  | HeaderFilterStrategy |
| **kmsMasterKeyId** (producer) | The ID of an AWS-managed customer master key (CMK) for Amazon SNS or a custom CMK. |  | String |
| **messageDeduplicationIdStrategy** (producer) | 
Only for FIFO Topic. Strategy for setting the messageDeduplicationId on the message. It can be one of the following options: useExchangeId, useContentBasedDeduplication. For the useContentBasedDeduplication option, no messageDeduplicationId will be set on the message.

Enum values:

-   useExchangeId
    
-   useContentBasedDeduplication
    





 | useExchangeId | String |
| **messageGroupIdStrategy** (producer) | 

Only for FIFO Topic. Strategy for setting the messageGroupId on the message. It can be one of the following options: useConstant, useExchangeId, usePropertyValue. For the usePropertyValue option, the value of property CamelAwsSnsMessageGroupId will be used.

Enum values:

-   useConstant
    
-   useExchangeId
    
-   usePropertyValue
    





 |  | String |
| **messageStructure** (producer) | The message structure to use such as json. |  | String |
| **overrideEndpoint** (producer) | Set the need for overriding the endpoint. This option needs to be used in combination with the uriEndpointOverride option. | false | boolean |
| **policy** (producer) | The policy for this topic. Is loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **queueArn** (producer) | The ARN endpoint to subscribe to. |  | String |
| **region** (producer) | 

The region in which the SNS client needs to work. When using this parameter, the configuration will expect the lowercase name of the region (for example, ap-east-1) You’ll need to use the name Region.EU\_WEST\_1.id().

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
| **serverSideEncryptionEnabled** (producer) | Define if Server Side Encryption is enabled or not on the topic. | false | boolean |
| **subject** (producer) | The subject which is used if the message header 'CamelAwsSnsSubject' is not present. |  | String |
| **subscribeSNStoSQS** (producer) | Define if the subscription between SNS Topic and SQS must be done or not. | false | boolean |
| **uriEndpointOverride** (producer) | Set the overriding uri endpoint. This option needs to be used in combination with overrideEndpoint option. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **amazonSNSClient** (advanced) | **Autowired** To use the AmazonSNS as the client. |  | SnsClient |
| **proxyHost** (proxy) | To define a proxy host when instantiating the SNS client. |  | String |
| **proxyPort** (proxy) | To define a proxy port when instantiating the SNS client. |  | Integer |
| **proxyProtocol** (proxy) | 

To define a proxy protocol when instantiating the SNS client.

Enum values:

-   HTTP
    
-   HTTPS
    





 | HTTPS | Protocol |
| **accessKey** (security) | Amazon AWS Access Key. |  | String |
| **profileCredentialsName** (security) | If using a profile credentials provider, this parameter will set the profile name. |  | String |
| **secretKey** (security) | Amazon AWS Secret Key. |  | String |
| **sessionToken** (security) | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | String |
| **trustAllCertificates** (security) | If we want to trust all certificates in case of overriding the endpoint. | false | boolean |
| **useDefaultCredentialsProvider** (security) | Set whether the SNS client should expect to load credentials on an AWS infra instance or to expect static credentials to be passed in. | false | boolean |
| **useProfileCredentialsProvider** (security) | Set whether the SNS client should expect to load credentials through a profile credentials provider. | false | boolean |
| **useSessionCredentials** (security) | Set whether the SNS client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in SNS. | false | boolean |

## Message Headers

The AWS Simple Notification System (SNS) component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAwsSnsMessageId** (producer) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sns/latest/org/apache/camel/component/aws2/sns/Sns2Constants.html#MESSAGE_ID) | The Amazon SNS message ID. |  | String |
| **CamelAwsSnsSubject** (producer) Constant: [`SUBJECT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sns/latest/org/apache/camel/component/aws2/sns/Sns2Constants.html#SUBJECT) | The Amazon SNS message subject. If not set, the subject from the SnsConfiguration is used. |  | String |
| **CamelAwsSnsMessageStructure** (producer) Constant: [`MESSAGE_STRUCTURE`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sns/latest/org/apache/camel/component/aws2/sns/Sns2Constants.html#MESSAGE_STRUCTURE) | The message structure to use such as json. |  | String |
| **CamelAwsSnsSequenceNumber** (producer) Constant: [`SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sns/latest/org/apache/camel/component/aws2/sns/Sns2Constants.html#SEQUENCE_NUMBER) | The sequence number for FIFO topics. |  | String |
| **CamelAwsSnsFailedMessageCount** (producer) Constant: [`FAILED_MESSAGE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sns/latest/org/apache/camel/component/aws2/sns/Sns2Constants.html#FAILED_MESSAGE_COUNT) | The number of failed messages in a batch publish operation. |  | Integer |
| **CamelAwsSnsSuccessfulMessageCount** (producer) Constant: [`SUCCESSFUL_MESSAGE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-aws2-sns/latest/org/apache/camel/component/aws2/sns/Sns2Constants.html#SUCCESSFUL_MESSAGE_COUNT) | The number of successful messages in a batch publish operation. |  | Integer |

Required SNS component options

You have to provide the amazonSNSClient in the Registry or your accessKey and secretKey to access the [Amazon’s SNS](https://aws.amazon.com/sns).

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

## Usage

### Advanced AmazonSNS configuration

If you need more control over the `SnsClient` instance configuration you can create your own instance and refer to it from the URI:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("aws2-sns://MyTopic?amazonSNSClient=#client");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="aws2-sns://MyTopic?amazonSNSClient=#client"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: aws2-sns://MyTopic
            parameters:
              amazonSNSClient: "#client"
```

The `#client` refers to a `AmazonSNS` in the Registry.

### Create a subscription between an AWS SNS Topic and an AWS SQS Queue

You can create a subscription of an SQS Queue to an SNS Topic in this way:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("aws2-sns://test-camel-sns1?amazonSNSClient=#amazonSNSClient&subscribeSNStoSQS=true&queueArn=arn:aws:sqs:eu-central-1:123456789012:test_camel");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="aws2-sns://test-camel-sns1?amazonSNSClient=#amazonSNSClient&amp;subscribeSNStoSQS=true&amp;queueArn=arn:aws:sqs:eu-central-1:123456789012:test_camel"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
    steps:
      - to:
          uri: aws2-sns://test-camel-sns1
          parameters:
            amazonSNSClient: "#amazonSNSClient"
            subscribeSNStoSQS: true
            queueArn: "arn:aws:sqs:eu-central-1:123456789012:test_camel"
```

The `#amazonSNSClient` refers to a `SnsClient` in the Registry. By specifying `subscribeSNStoSQS` to true and a `queueArn` of an existing SQS Queue, you’ll be able to subscribe your SQS Queue to your SNS Topic.

At this point, you can consume messages coming from SNS Topic through your SQS Queue

-   Java
    
-   XML
    
-   YAML
    

```java
from("aws2-sqs://test-camel?amazonSQSClient=#amazonSQSClient&delay=50&maxMessagesPerPoll=5")
    .to("...");
```

```xml
<route>
  <from uri="aws2-sqs://test-camel?amazonSQSClient=#amazonSQSClient&amp;delay=50&amp;maxMessagesPerPoll=5"/>
  <to uri="..."/>
</route>
```

```yaml
- route:
    from:
      uri: aws2-sqs://test-camel
      parameters:
        amazonSQSClient: "#amazonSQSClient"
        delay: 50
        maxMessagesPerPoll: 5
      steps:
        - to:
            uri: "..."
```

### Topic Auto-creation

With the option `autoCreateTopic` users are able to avoid the auto-creation of an SNS Topic in case it doesn’t exist. The default for this option is `false`. If set to false, any operation on a non-existent topic in AWS won’t be successful and an error will be returned.

### SNS FIFO

SNS FIFO are supported. While creating the SQS queue, you will subscribe to the SNS topic there is an important point to remember, you’ll need to make possible for the SNS Topic to send the message to the SQS Queue.

This is clear with an example.

Suppose you created an SNS FIFO Topic called `Order.fifo` and an SQS Queue called `QueueSub.fifo`.

In the access Policy of the `QueueSub.fifo` you should submit something like this

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

### SNS Fifo Topic Message group ID Strategy and message Deduplication ID Strategy

When sending something to the FIFO topic, you’ll need to always set up a message group ID strategy.

If the content-based message deduplication has been enabled on the SNS Fifo topic, where won’t be the need of setting a message deduplication id strategy, otherwise you’ll have to set it.

### Message Subject Length Limitation

AWS SNS has a maximum subject length of 100 characters. If you send a message with a subject longer than 100 characters (for example, when using CloudEvents with long subjects), the subject will be automatically truncated to 100 characters.

This behavior ensures compatibility with AWS SNS constraints while allowing seamless integration with systems like CloudEvents that do not impose such restrictions.

## Examples

### Producer Examples

Sending to a topic

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("aws2-sns://camel-topic?subject=The+subject+message&autoCreateTopic=true");
```

```xml
<route>
    <from uri="direct:start"/>
    <to uri="aws2-sns://camel-topic?subject=The+subject+message&amp;autoCreateTopic=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
    steps:
      - to:
          uri: aws2-sns://camel-topic
          parameters:
            subject: "The+subject+message"
            autoCreateTopic: true
```

Sending batch to a topic

_Java-only: requires constructing `PublishBatchRequestEntry` objects programmatically_

```java
from("direct:start")
     .process(exchange -> {
          List<PublishBatchRequestEntry> pubList = List.of(
               PublishBatchRequestEntry.builder().id("message1").message("This is message 1").build(),
               PublishBatchRequestEntry.builder().id("message2").message("This is message 2").build(),
               PublishBatchRequestEntry.builder().id("message3").message("This is message 3").build()
          );
          exchange.getIn().setBody(pubList);
  })
  .to("aws2-sns://camel-topic?subject=The+subject+message&autoCreateTopic=true&batchEnabled=true");
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