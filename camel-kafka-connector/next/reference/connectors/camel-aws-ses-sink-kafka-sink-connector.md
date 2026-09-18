# camel-aws-ses-sink-kafka-connector sink configuration

Connector Description: Send email through the Amazon Simple Email Service (SES).

When using camel-aws-ses-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-ses-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awssessink.CamelAwssessinkSinkConnector
```

The camel-aws-ses-sink sink connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-ses-sink.from** | **Required** From address Example: [user@example.com](mailto:user@example.com). |  | HIGH |
| **camel.kamelet.aws-ses-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-ses-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-ses-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-ses-sink.useDefaultCredentialsProvider** | If true, the SES client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-ses-sink.useProfileCredentialsProvider** | Set whether the SES client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-ses-sink.useSessionCredentials** | Set whether the SES client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in SES. | false | MEDIUM |
| **camel.kamelet.aws-ses-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-ses-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |

The camel-aws-ses-sink sink connector has no converters out of the box.

The camel-aws-ses-sink sink connector has no transforms out of the box.

The camel-aws-ses-sink sink connector has no aggregation strategies out of the box.