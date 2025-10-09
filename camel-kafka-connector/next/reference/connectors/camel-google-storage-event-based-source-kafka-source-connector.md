# camel-google-storage-event-based-source-kafka-connector source configuration

Connector Description: Receive data from Google Pubsub reporting events related to a Google Storage bucket.

When using camel-google-storage-event-based-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-storage-event-based-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlestorageeventbasedsource.CamelGooglestorageeventbasedsourceSourceConnector
```

The camel-google-storage-event-based-source source connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-storage-event-based-source.projectId** | **Required** The Google Cloud Pub/Sub Project ID. |  | HIGH |
| **camel.kamelet.google-storage-event-based-source.subscriptionName** | **Required** The subscription name. |  | HIGH |
| **camel.kamelet.google-storage-event-based-source.serviceAccountKey** | **Required** The service account key to use as credentials for the Pub/Sub publisher/subscriber. You must encode this value in base64. |  | HIGH |
| **camel.kamelet.google-storage-event-based-source.synchronousPull** | Specifies to synchronously pull batches of messages. | false | MEDIUM |
| **camel.kamelet.google-storage-event-based-source.maxMessagesPerPoll** | The maximum number of messages to receive from the server in a single API call. | 1 | MEDIUM |
| **camel.kamelet.google-storage-event-based-source.concurrentConsumers** | The number of parallel streams to consume from the subscription. | 1 | MEDIUM |
| **camel.kamelet.google-storage-event-based-source.bucketNameOrArn** | **Required** The Google Cloud Storage bucket name or Bucket Amazon Resource Name (ARN). |  | HIGH |
| **camel.kamelet.google-storage-event-based-source.getObject** | If `getObject` is enabled, then the file created in the Bucket is retreived and returned as body, if not only the event is returned as body. | false | MEDIUM |

The camel-google-storage-event-based-source source connector has no converters out of the box.

The camel-google-storage-event-based-source source connector has no transforms out of the box.

The camel-google-storage-event-based-source source connector has no aggregation strategies out of the box.