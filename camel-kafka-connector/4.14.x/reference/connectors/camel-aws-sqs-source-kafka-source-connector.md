# camel-aws-sqs-source-kafka-connector source configuration

Connector Description: Receive data from AWS SQS.

When using camel-aws-sqs-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-sqs-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awssqssource.CamelAwssqssourceSourceConnector
```

The camel-aws-sqs-source source connector supports 21 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-sqs-source.queueNameOrArn** | **Required** The SQS Queue Name or ARN. |  | HIGH |
| **camel.kamelet.aws-sqs-source.deleteAfterRead** | Delete messages after consuming them. | true | MEDIUM |
| **camel.kamelet.aws-sqs-source.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-sqs-source.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-sqs-source.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-sqs-source.autoCreateQueue** | Setting the autocreation of the SQS queue. | false | MEDIUM |
| **camel.kamelet.aws-sqs-source.amazonAWSHost** | The hostname of the Amazon AWS cloud. | "amazonaws.com" | MEDIUM |
| **camel.kamelet.aws-sqs-source.protocol** | The underlying protocol used to communicate with SQS. Example: http or https. | "https" | MEDIUM |
| **camel.kamelet.aws-sqs-source.queueURL** | The full SQS Queue URL (required if using KEDA). |  | MEDIUM |
| **camel.kamelet.aws-sqs-source.useDefaultCredentialsProvider** | If true, the SQS client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-sqs-source.useProfileCredentialsProvider** | Set whether the SQS client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-sqs-source.useSessionCredentials** | Set whether the SQS client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in SQS. | false | MEDIUM |
| **camel.kamelet.aws-sqs-source.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-sqs-source.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-sqs-source.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-sqs-source.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |
| **camel.kamelet.aws-sqs-source.delay** | The number of milliseconds before the next poll of the selected stream. | 500 | MEDIUM |
| **camel.kamelet.aws-sqs-source.greedy** | If greedy is enabled, then the polling will happen immediately again, if the previous run polled 1 or more messages. | false | MEDIUM |
| **camel.kamelet.aws-sqs-source.maxMessagesPerPoll** | The maximum number of messages to return. Amazon SQS never returns more messages than this value (however, fewer messages might be returned). Valid values 1 to 10. Default 1. | 1 | MEDIUM |
| **camel.kamelet.aws-sqs-source.waitTimeSeconds** | The duration (in seconds) for which the call waits for a message to arrive in the queue before returning. If a message is available, the call returns sooner than WaitTimeSeconds. If no messages are available and the wait time expires, the call does not return a message list. |  | MEDIUM |
| **camel.kamelet.aws-sqs-source.visibilityTimeout** | The duration (in seconds) that the received messages are hidden from subsequent retrieve requests after being retrieved by a ReceiveMessage request. |  | MEDIUM |

The camel-aws-sqs-source source connector has no converters out of the box.

The camel-aws-sqs-source source connector has no transforms out of the box.

The camel-aws-sqs-source source connector has no aggregation strategies out of the box.