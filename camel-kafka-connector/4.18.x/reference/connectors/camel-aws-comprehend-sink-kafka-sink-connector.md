# camel-aws-comprehend-sink-kafka-connector sink configuration

Connector Description: Send data to AWS Comprehend for natural language processing.

When using camel-aws-comprehend-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-comprehend-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awscomprehendsink.CamelAwscomprehendsinkSinkConnector
```

The camel-aws-comprehend-sink sink connector supports 13 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-comprehend-sink.operation** | The operation to perform on the input text. | "detectDominantLanguage" | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.languageCode** | The language code of the input text. Required for all operations except detectDominantLanguage. Use a 2-letter ISO 639-1 code (e.g., 'en' for English, 'es' for Spanish). |  | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.endpointArn** | The Amazon Resource Name (ARN) of the endpoint to use for document classification. Required for classifyDocument operation. |  | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-comprehend-sink.useDefaultCredentialsProvider** | If true, the Comprehend client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.useProfileCredentialsProvider** | Set whether the Comprehend client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.useSessionCredentials** | Set whether the Comprehend client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Comprehend. | false | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-comprehend-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-comprehend-sink sink connector has no converters out of the box.

The camel-aws-comprehend-sink sink connector has no transforms out of the box.

The camel-aws-comprehend-sink sink connector has no aggregation strategies out of the box.