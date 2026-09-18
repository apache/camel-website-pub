# camel-kafka-batch-apicurio-registry-source-kafka-connector source configuration

Connector Description: Receive data from Kafka topics in batch on an insecure broker combined with Apicurio Registry secured with Keycloak and commit them manually through KafkaManualCommit or auto commit.

When using camel-kafka-batch-apicurio-registry-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-batch-apicurio-registry-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkabatchapicurioregistrysource.CamelKafkabatchapicurioregistrysourceSourceConnector
```

The camel-kafka-batch-apicurio-registry-source source connector supports 22 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-batch-apicurio-registry-source.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-batch-apicurio-registry-source.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-batch-apicurio-registry-source.autoCommitEnable** | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | true | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.allowManualCommit** | Whether to allow doing manual commits. | false | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.pollOnError** | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | "ERROR\_HANDLER" | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.autoOffsetReset** | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | "latest" | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.consumerGroup** | A string that uniquely identifies the group of consumers to which this source belongs Example: my-group-id. |  | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.deserializeHeaders** | When enabled the Kamelet source will deserialize all message headers to String representation. | true | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.valueDeserializer** | Deserializer class for value that implements the Deserializer interface. | "io.apicurio.registry.serde.avro.AvroKafkaDeserializer" | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.apicurioRegistryUrl** | **Required** The Apicurio Schema Registry URL. |  | HIGH |
| **camel.kamelet.kafka-batch-apicurio-registry-source.avroDatumProvider** | How to read data with Avro. | "io.apicurio.registry.serde.avro.ReflectAvroDatumProvider" | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.batchSize** | The maximum number of records returned in a single call to poll(). | 500 | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.pollTimeout** | The timeout used when polling the KafkaConsumer. | 5000 | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.maxPollIntervalMs** | The maximum delay between invocations of poll() when using consumer group management. |  | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.batchingIntervalMs** | In consumer batching mode, then this option is specifying a time in millis, to trigger batch completion eager when the current batch size has not reached the maximum size defined by maxPollRecords. Notice the trigger is not exact at the given interval, as this can only happen between kafka polls (see pollTimeoutMs option). |  | MEDIUM |
| **camel.kamelet.kafka-batch-apicurio-registry-source.apicurioAuthServiceUrl** | **Required** The URL for Keycloak instance securing the Apicurio Registry Example: [http://my-keycloak.com:8080/](http://my-keycloak.com:8080/). |  | HIGH |
| **camel.kamelet.kafka-batch-apicurio-registry-source.apicurioAuthRealm** | **Required** The Realm in Keycloak instance securing the Apicurio Registry. |  | HIGH |
| **camel.kamelet.kafka-batch-apicurio-registry-source.apicurioAuthClientId** | **Required** The Client ID in Keycloak instance securing the Apicurio Registry. |  | HIGH |
| **camel.kamelet.kafka-batch-apicurio-registry-source.apicurioAuthClientSecret** | **Required** The Client Secret in Keycloak instance securing the Apicurio Registry. |  | HIGH |
| **camel.kamelet.kafka-batch-apicurio-registry-source.apicurioAuthUsername** | **Required** The Username in Keycloak instance securing the Apicurio Registry. |  | HIGH |
| **camel.kamelet.kafka-batch-apicurio-registry-source.apicurioAuthPassword** | **Required** The Password in Keycloak instance securing the Apicurio Registry. |  | HIGH |
| **camel.kamelet.kafka-batch-apicurio-registry-source.topicIsPattern** | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | false | MEDIUM |

The camel-kafka-batch-apicurio-registry-source source connector has no converters out of the box.

The camel-kafka-batch-apicurio-registry-source source connector has no transforms out of the box.

The camel-kafka-batch-apicurio-registry-source source connector has no aggregation strategies out of the box.