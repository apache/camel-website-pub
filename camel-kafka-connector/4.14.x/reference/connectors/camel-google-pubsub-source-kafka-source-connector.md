# camel-google-pubsub-source-kafka-connector source configuration

Connector Description: Consume messages from Google Cloud Pub/Sub.

When using camel-google-pubsub-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-pubsub-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlepubsubsource.CamelGooglepubsubsourceSourceConnector
```

The camel-google-pubsub-source source connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-pubsub-source.projectId** | **Required** The Google Cloud Pub/Sub Project ID. |  | HIGH |
| **camel.kamelet.google-pubsub-source.subscriptionName** | **Required** The subscription name. |  | HIGH |
| **camel.kamelet.google-pubsub-source.serviceAccountKey** | The service account key to use as credentials for the Pub/Sub publisher/subscriber. You must encode this value in base64. |  | MEDIUM |
| **camel.kamelet.google-pubsub-source.synchronousPull** | Specifies to synchronously pull batches of messages. | false | MEDIUM |
| **camel.kamelet.google-pubsub-source.maxMessagesPerPoll** | The maximum number of messages to receive from the server in a single API call. | 1 | MEDIUM |
| **camel.kamelet.google-pubsub-source.concurrentConsumers** | The number of parallel streams to consume from the subscription. | 1 | MEDIUM |

The camel-google-pubsub-source source connector has no converters out of the box.

The camel-google-pubsub-source source connector has no transforms out of the box.

The camel-google-pubsub-source source connector has no aggregation strategies out of the box.