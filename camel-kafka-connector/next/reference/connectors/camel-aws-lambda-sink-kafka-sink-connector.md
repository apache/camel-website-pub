# camel-aws-lambda-sink-kafka-connector sink configuration

Connector Description: Send a payload to an AWS Lambda function.

When using camel-aws-lambda-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-lambda-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awslambdasink.CamelAwslambdasinkSinkConnector
```

The camel-aws-lambda-sink sink connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-lambda-sink.function** | **Required** The Lambda Function name. |  | HIGH |
| **camel.kamelet.aws-lambda-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-lambda-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-lambda-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-lambda-sink.useDefaultCredentialsProvider** | If true, the Lambda client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-lambda-sink.useProfileCredentialsProvider** | Set whether the Lambda client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-lambda-sink.useSessionCredentials** | Set whether the Lambda client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Lambda. | false | MEDIUM |
| **camel.kamelet.aws-lambda-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-lambda-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |

The camel-aws-lambda-sink sink connector has no converters out of the box.

The camel-aws-lambda-sink sink connector has no transforms out of the box.

The camel-aws-lambda-sink sink connector has no aggregation strategies out of the box.