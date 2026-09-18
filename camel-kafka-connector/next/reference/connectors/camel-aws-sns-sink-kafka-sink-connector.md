# camel-aws-sns-sink-kafka-connector sink configuration

Connector Description: Send message to an Amazon Simple Notification Service (SNS) topic.

When using camel-aws-sns-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-sns-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awssnssink.CamelAwssnssinkSinkConnector
```

The camel-aws-sns-sink sink connector supports 12 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-sns-sink.topicNameOrArn** | **Required** The SNS topic name name or Amazon Resource Name (ARN). |  | HIGH |
| **camel.kamelet.aws-sns-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-sns-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-sns-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-sns-sink.autoCreateTopic** | Setting the autocreation of the SNS topic. | false | MEDIUM |
| **camel.kamelet.aws-sns-sink.useDefaultCredentialsProvider** | If true, the SNS client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-sns-sink.useProfileCredentialsProvider** | Set whether the SNS client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-sns-sink.useSessionCredentials** | Set whether the SNS client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in SNS. | false | MEDIUM |
| **camel.kamelet.aws-sns-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-sns-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-sns-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-sns-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-sns-sink sink connector has no converters out of the box.

The camel-aws-sns-sink sink connector has no transforms out of the box.

The camel-aws-sns-sink sink connector has no aggregation strategies out of the box.