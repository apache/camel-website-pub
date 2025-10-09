# camel-aws-kinesis-source-kafka-connector source configuration

Connector Description: Receive data from AWS Kinesis.

When using camel-aws-kinesis-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-kinesis-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awskinesissource.CamelAwskinesissourceSourceConnector
```

The camel-aws-kinesis-source source connector supports 15 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-kinesis-source.stream** | **Required** The Kinesis stream that you want to access. The Kinesis stream that you specify must already exist. |  | HIGH |
| **camel.kamelet.aws-kinesis-source.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-source.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-source.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-kinesis-source.useDefaultCredentialsProvider** | If true, the Kinesis client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-kinesis-source.useProfileCredentialsProvider** | Set whether the Kinesis client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-kinesis-source.useSessionCredentials** | Set whether the Kinesis client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Kinesis. | false | MEDIUM |
| **camel.kamelet.aws-kinesis-source.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-source.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-source.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-kinesis-source.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |
| **camel.kamelet.aws-kinesis-source.delay** | The number of milliseconds before the next poll of the selected stream. | 500 | MEDIUM |
| **camel.kamelet.aws-kinesis-source.asyncClient** | If we want a KinesisAsyncClient instance set it to true. | false | MEDIUM |
| **camel.kamelet.aws-kinesis-source.useKclConsumers** | If we want to a KCL Consumer set it to true. | false | MEDIUM |
| **camel.kamelet.aws-kinesis-source.kclDisableCloudwatchMetricsExport** | Define if we want to use a KCL Consumer and disable the CloudWatch Metrics Export. | false | MEDIUM |

The camel-aws-kinesis-source source connector has no converters out of the box.

The camel-aws-kinesis-source source connector has no transforms out of the box.

The camel-aws-kinesis-source source connector has no aggregation strategies out of the box.