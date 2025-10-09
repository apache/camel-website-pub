# camel-aws-kinesis-sink-kafka-connector sink configuration

Connector Description: Send data to AWS Kinesis.

When using camel-aws-kinesis-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-kinesis-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awskinesissink.CamelAwskinesissinkSinkConnector
```

The camel-aws-kinesis-sink sink connector supports 11 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-kinesis-sink.stream** | **Required** The Kinesis stream that you want to access. The Kinesis stream that you specify must already exist. |  | HIGH |
| **camel.kamelet.aws-kinesis-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-kinesis-sink.useDefaultCredentialsProvider** | If true, the Kinesis client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-kinesis-sink.useProfileCredentialsProvider** | Set whether the Kinesis client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-kinesis-sink.useSessionCredentials** | Set whether the Kinesis client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis. | false | MEDIUM |
| **camel.kamelet.aws-kinesis-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-kinesis-sink sink connector has no converters out of the box.

The camel-aws-kinesis-sink sink connector has no transforms out of the box.

The camel-aws-kinesis-sink sink connector has no aggregation strategies out of the box.