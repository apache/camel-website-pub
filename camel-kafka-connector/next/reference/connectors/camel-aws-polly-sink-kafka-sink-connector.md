# camel-aws-polly-sink-kafka-connector sink configuration

Connector Description: Synthesize speech from text using AWS Polly.

When using camel-aws-polly-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-polly-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awspollysink.CamelAwspollysinkSinkConnector
```

The camel-aws-polly-sink sink connector supports 16 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-polly-sink.voiceId** | The voice ID to use for speech synthesis (e.g., Joanna, Matthew, Amy, Brian). |  | MEDIUM |
| **camel.kamelet.aws-polly-sink.outputFormat** | The audio format in which the resulting stream will be encoded. | "MP3" | MEDIUM |
| **camel.kamelet.aws-polly-sink.textType** | Specifies whether the input text is plain text or SSML. | "TEXT" | MEDIUM |
| **camel.kamelet.aws-polly-sink.engine** | Specifies the engine (standard, neural, long-form, generative) for Amazon Polly to use when processing input text for speech synthesis. |  | MEDIUM |
| **camel.kamelet.aws-polly-sink.sampleRate** | The audio frequency in Hz. |  | MEDIUM |
| **camel.kamelet.aws-polly-sink.languageCode** | Optional language code for voice synthesis. This is only necessary if using a bilingual voice. |  | MEDIUM |
| **camel.kamelet.aws-polly-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-polly-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-polly-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-polly-sink.useDefaultCredentialsProvider** | If true, the Polly client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-polly-sink.useProfileCredentialsProvider** | Set whether the Polly client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-polly-sink.useSessionCredentials** | Set whether the Polly client should expect to use Session Credentials. This is useful in a situation in which the user needs to assume an IAM role for doing operations in Polly. | false | MEDIUM |
| **camel.kamelet.aws-polly-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-polly-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume an IAM role. |  | MEDIUM |
| **camel.kamelet.aws-polly-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-polly-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-polly-sink sink connector has no converters out of the box.

The camel-aws-polly-sink sink connector has no transforms out of the box.

The camel-aws-polly-sink sink connector has no aggregation strategies out of the box.