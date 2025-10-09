# camel-aws-bedrock-agent-runtime-sink-kafka-connector sink configuration

Connector Description: Send data for invoking a knowledge base from AWS Bedrock.

When using camel-aws-bedrock-agent-runtime-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-aws-bedrock-agent-runtime-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.awsbedrockagentruntimesink.CamelAwsbedrockagentruntimesinkSinkConnector
```

The camel-aws-bedrock-agent-runtime-sink sink connector supports 12 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.modelId** | **Required** The model Id to be used to generate responses. |  | HIGH |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.knowledgeBaseId** | **Required** The Knowledge Base Id to be used to retrieve and generate responses. |  | HIGH |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.accessKey** | The access key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.secretKey** | The secret key obtained from AWS. |  | MEDIUM |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.region** | **Required** The AWS region to access. |  | HIGH |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.useDefaultCredentialsProvider** | If true, the Bedrock client loads credentials through a default credentials provider. If false, it uses the basic authentication method (access key and secret key). | false | MEDIUM |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.useProfileCredentialsProvider** | Set whether the Bedrock client should expect to load credentials through a profile credentials provider. | false | MEDIUM |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.useSessionCredentials** | Set whether the Bedrock client should expect to use Session Credentials. This is useful in situation in which the user needs to assume a IAM role for doing operations in Bedrock. | false | MEDIUM |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.profileCredentialsName** | If using a profile credentials provider this parameter sets the profile name. |  | MEDIUM |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.sessionToken** | Amazon AWS Session Token used when the user needs to assume a IAM role. |  | MEDIUM |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.uriEndpointOverride** | The overriding endpoint URI. To use this option, you must also select the `overrideEndpoint` option. |  | MEDIUM |
| **camel.kamelet.aws-bedrock-agent-runtime-sink.overrideEndpoint** | Select this option to override the endpoint URI. To use this option, you must also provide a URI for the `uriEndpointOverride` option. | false | MEDIUM |

The camel-aws-bedrock-agent-runtime-sink sink connector has no converters out of the box.

The camel-aws-bedrock-agent-runtime-sink sink connector has no transforms out of the box.

The camel-aws-bedrock-agent-runtime-sink sink connector has no aggregation strategies out of the box.