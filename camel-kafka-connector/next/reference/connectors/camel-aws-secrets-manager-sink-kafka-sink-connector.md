# camel-aws-secrets-manager-sink-kafka-connector sink configuration

Connector Description: Create a secret in AWS Secrets Manager.

When using camel-aws-secrets-manager-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-secrets-manager-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awssecretsmanagersink.CamelAwssecretsmanagersinkSinkConnector
```

The camel-aws-secrets-manager-sink sink connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-secrets-manager-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-secrets-manager-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-secrets-manager-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-secrets-manager-sink.useDefaultCredentialsProvider** | Set whether the Secrets Manager client should expect to load credentials through a default credentials provider or to expect static credentials to be passed in. | false | MEDIUM |
| **camel.kamelet.aws-secrets-manager-sink.useProfileCredentialsProvider** | Set whether the Secrets Manager client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-secrets-manager-sink.useSessionCredentials** | Set whether the Secrets Manager client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Secrets Manager. | false | MEDIUM |
| **camel.kamelet.aws-secrets-manager-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-secrets-manager-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |

The camel-aws-secrets-manager-sink sink connector has no converters out of the box.

The camel-aws-secrets-manager-sink sink connector has no transforms out of the box.

The camel-aws-secrets-manager-sink sink connector has no aggregation strategies out of the box.