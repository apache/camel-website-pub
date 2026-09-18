# camel-aws-timestream-query-sink-kafka-connector sink configuration

Connector Description: Query an AWS Timestream Database

When using camel-aws-timestream-query-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-timestream-query-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awstimestreamquerysink.CamelAwstimestreamquerysinkSinkConnector
```

The camel-aws-timestream-query-sink sink connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-timestream-query-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-timestream-query-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-timestream-query-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-timestream-query-sink.useDefaultCredentialsProvider** | If true, the CloudWatch client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-timestream-query-sink.useProfileCredentialsProvider** | Set whether the Timestream client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-timestream-query-sink.useSessionCredentials** | Set whether the Timestream client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Timestream. | false | MEDIUM |
| **camel.kamelet.aws-timestream-query-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-timestream-query-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-timestream-query-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-timestream-query-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-timestream-query-sink sink connector has no converters out of the box.

The camel-aws-timestream-query-sink sink connector has no transforms out of the box.

The camel-aws-timestream-query-sink sink connector has no aggregation strategies out of the box.