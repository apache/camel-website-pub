# camel-aws-kinesis-firehose-sink-kafka-connector sink configuration

Connector Description: Send message to an AWS Kinesis Firehose Stream.

When using camel-aws-kinesis-firehose-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-kinesis-firehose-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awskinesisfirehosesink.CamelAwskinesisfirehosesinkSinkConnector
```

The camel-aws-kinesis-firehose-sink sink connector supports 11 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-kinesis-firehose-sink.streamName** | **Required** The name of the stream we want to send to data to. |  | HIGH |
| **camel.kamelet.aws-kinesis-firehose-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-firehose-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-firehose-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-kinesis-firehose-sink.useDefaultCredentialsProvider** | Set whether the Kinesis Firehose client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | MEDIUM |
| **camel.kamelet.aws-kinesis-firehose-sink.useProfileCredentialsProvider** | Set whether the Kinesis Firehose client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-kinesis-firehose-sink.useSessionCredentials** | Set whether the Kinesis Firehose client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis Firehose. | false | MEDIUM |
| **camel.kamelet.aws-kinesis-firehose-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-firehose-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-firehose-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-firehose-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-kinesis-firehose-sink sink connector has no converters out of the box.

The camel-aws-kinesis-firehose-sink sink connector has no transforms out of the box.

The camel-aws-kinesis-firehose-sink sink connector has no aggregation strategies out of the box.