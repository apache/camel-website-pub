# camel-google-vertexai-sink-kafka-connector sink configuration

Connector Description: Send data to Google Vertex AI for generating content with generative AI models.

When using camel-google-vertexai-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-vertexai-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlevertexaisink.CamelGooglevertexaisinkSinkConnector
```

The camel-google-vertexai-sink sink connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-vertexai-sink.projectId** | **Required** The Google Cloud Project ID. |  | HIGH |
| **camel.kamelet.google-vertexai-sink.location** | **Required** The Google Cloud region (e.g., us-central1). |  | HIGH |
| **camel.kamelet.google-vertexai-sink.modelId** | **Required** The Model ID to use for predictions (e.g., gemini-2.5-pro). |  | HIGH |
| **camel.kamelet.google-vertexai-sink.serviceAccountKey** | The service account key to use as credentials for the Vertex AI client. You must encode this value in base64. |  | MEDIUM |
| **camel.kamelet.google-vertexai-sink.operation** | The operation to perform. | "generateText" | MEDIUM |
| **camel.kamelet.google-vertexai-sink.temperature** | Controls randomness in generation. Lower values make output more deterministic. Range 0.0 to 1.0. |  | MEDIUM |
| **camel.kamelet.google-vertexai-sink.maxOutputTokens** | Maximum number of tokens to generate in the response. |  | MEDIUM |
| **camel.kamelet.google-vertexai-sink.topP** | Nucleus sampling parameter. Considers tokens with top\_p probability mass. Range 0.0 to 1.0. |  | MEDIUM |
| **camel.kamelet.google-vertexai-sink.topK** | Only sample from the top K options for each subsequent token. |  | MEDIUM |

The camel-google-vertexai-sink sink connector has no converters out of the box.

The camel-google-vertexai-sink sink connector has no transforms out of the box.

The camel-google-vertexai-sink sink connector has no aggregation strategies out of the box.