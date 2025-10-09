# camel-aws-sqs-batch-sink-kafka-connector sink configuration

Connector Description: Send Batch message to an AWS SQS Queue.

When using camel-aws-sqs-batch-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-sqs-batch-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awssqsbatchsink.CamelAwssqsbatchsinkSinkConnector
```

The camel-aws-sqs-batch-sink sink connector supports 15 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-sqs-batch-sink.queueNameOrArn** | **Required** The SQS Queue name or ARN. |  | HIGH |
| **camel.kamelet.aws-sqs-batch-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-sqs-batch-sink.autoCreateQueue** | Setting the autocreation of the SQS queue. | false | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.batchSeparator** | **Required** The batch separator string Example: ,. |  | HIGH |
| **camel.kamelet.aws-sqs-batch-sink.amazonAWSHost** | The hostname of the Amazon AWS cloud. | "amazonaws.com" | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.protocol** | The underlying protocol used to communicate with SQS Example: http or https. | "https" | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.useDefaultCredentialsProvider** | Set whether the SQS client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.useProfileCredentialsProvider** | Set whether the SQS client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.useSessionCredentials** | Set whether the SQS client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in SQS. | false | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-sqs-batch-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-sqs-batch-sink sink connector has no converters out of the box.

The camel-aws-sqs-batch-sink sink connector has no transforms out of the box.

The camel-aws-sqs-batch-sink sink connector has no aggregation strategies out of the box.