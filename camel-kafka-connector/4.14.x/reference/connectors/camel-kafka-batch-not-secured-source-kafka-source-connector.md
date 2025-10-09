# camel-kafka-batch-not-secured-source-kafka-connector source configuration

Connector Description: Receive data from Kafka topics in batch on an insecure broker and commit them manually through KafkaManualCommit.

When using camel-kafka-batch-not-secured-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-batch-not-secured-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkabatchnotsecuredsource.CamelKafkabatchnotsecuredsourceSourceConnector
```

The camel-kafka-batch-not-secured-source source connector supports 13 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-batch-not-secured-source.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-batch-not-secured-source.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-batch-not-secured-source.autoCommitEnable** | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | true | MEDIUM |
| **camel.kamelet.kafka-batch-not-secured-source.allowManualCommit** | Whether to allow doing manual commits. | false | MEDIUM |
| **camel.kamelet.kafka-batch-not-secured-source.pollOnError** | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | "ERROR\_HANDLER" | MEDIUM |
| **camel.kamelet.kafka-batch-not-secured-source.autoOffsetReset** | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | "latest" | MEDIUM |
| **camel.kamelet.kafka-batch-not-secured-source.consumerGroup** | A string that uniquely identifies the group of consumers to which this source belongs Example: my-group-id. |  | MEDIUM |
| **camel.kamelet.kafka-batch-not-secured-source.deserializeHeaders** | When enabled the Kamelet source will deserialize all message headers to String representation. | true | MEDIUM |
| **camel.kamelet.kafka-batch-not-secured-source.batchSize** | The maximum number of records returned in a single call to poll(). | 500 | MEDIUM |
| **camel.kamelet.kafka-batch-not-secured-source.pollTimeout** | The timeout used when polling the KafkaConsumer. | 5000 | MEDIUM |
| **camel.kamelet.kafka-batch-not-secured-source.maxPollIntervalMs** | The maximum delay between invocations of poll() when using consumer group management. |  | MEDIUM |
| **camel.kamelet.kafka-batch-not-secured-source.batchingIntervalMs** | In consumer batching mode, then this option is specifying a time in millis, to trigger batch completion eager when the current batch size has not reached the maximum size defined by maxPollRecords. Notice the trigger is not exact at the given interval, as this can only happen between kafka polls (see pollTimeoutMs option). |  | MEDIUM |
| **camel.kamelet.kafka-batch-not-secured-source.topicIsPattern** | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | false | MEDIUM |

The camel-kafka-batch-not-secured-source source connector has no converters out of the box.

The camel-kafka-batch-not-secured-source source connector has no transforms out of the box.

The camel-kafka-batch-not-secured-source source connector has no aggregation strategies out of the box.