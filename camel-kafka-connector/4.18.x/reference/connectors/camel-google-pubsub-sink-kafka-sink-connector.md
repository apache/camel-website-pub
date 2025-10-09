# camel-google-pubsub-sink-kafka-connector sink configuration

Connector Description: Send messages to Google Cloud Pub/Sub.

When using camel-google-pubsub-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-pubsub-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlepubsubsink.CamelGooglepubsubsinkSinkConnector
```

The camel-google-pubsub-sink sink connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-pubsub-sink.projectId** | **Required** The Google Cloud Pub/Sub Project ID. |  | HIGH |
| **camel.kamelet.google-pubsub-sink.destinationName** | **Required** The destination name. |  | HIGH |
| **camel.kamelet.google-pubsub-sink.serviceAccountKey** | The service account key to use as credentials for the Pub/Sub publisher/subscriber. You must encode this value in base64. |  | MEDIUM |

The camel-google-pubsub-sink sink connector has no converters out of the box.

The camel-google-pubsub-sink sink connector has no transforms out of the box.

The camel-google-pubsub-sink sink connector has no aggregation strategies out of the box.