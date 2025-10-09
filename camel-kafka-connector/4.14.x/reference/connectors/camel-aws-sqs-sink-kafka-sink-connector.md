# camel-aws-sqs-sink-kafka-connector sink configuration

Connector Description: Send messages to an Amazon Simple Queue Service (SQS) queue.

When using camel-aws-sqs-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-sqs-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awssqssink.CamelAwssqssinkSinkConnector
```

The camel-aws-sqs-sink sink connector supports 14 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-sqs-sink.queueNameOrArn** | **Required** The SQS Queue name or or Amazon Resource Name (ARN). |  | HIGH |
| **camel.kamelet.aws-sqs-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-sqs-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-sqs-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-sqs-sink.autoCreateQueue** | Automatically create the SQS queue. | false | MEDIUM |
| **camel.kamelet.aws-sqs-sink.amazonAWSHost** | The hostname of the Amazon AWS cloud. | "amazonaws.com" | MEDIUM |
| **camel.kamelet.aws-sqs-sink.protocol** | The underlying protocol used to communicate with SQS. Example: http or https. | "https" | MEDIUM |
| **camel.kamelet.aws-sqs-sink.useDefaultCredentialsProvider** | If true, the SQS client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-sqs-sink.useProfileCredentialsProvider** | Set whether the SQS client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-sqs-sink.useSessionCredentials** | Set whether the SQS client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in SQS. | false | MEDIUM |
| **camel.kamelet.aws-sqs-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-sqs-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-sqs-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-sqs-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-sqs-sink sink connector has no converters out of the box.

The camel-aws-sqs-sink sink connector has no transforms out of the box.

The camel-aws-sqs-sink sink connector has no aggregation strategies out of the box.