# camel-kafka-scram-source-kafka-connector source configuration

Connector Description: Receive data from Kafka topics through SCRAM login module.

When using camel-kafka-scram-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-scram-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkascramsource.CamelKafkascramsourceSourceConnector
```

The camel-kafka-scram-source source connector supports 13 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-scram-source.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-scram-source.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-scram-source.securityProtocol** | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | "SASL\_SSL" | MEDIUM |
| **camel.kamelet.kafka-scram-source.saslMechanism** | The Simple Authentication and Security Layer (SASL) Mechanism used. | "SCRAM-SHA-512" | MEDIUM |
| **camel.kamelet.kafka-scram-source.user** | **Required** Username to authenticate to Kafka. |  | HIGH |
| **camel.kamelet.kafka-scram-source.password** | **Required** Password to authenticate to kafka. |  | HIGH |
| **camel.kamelet.kafka-scram-source.autoCommitEnable** | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | true | MEDIUM |
| **camel.kamelet.kafka-scram-source.allowManualCommit** | Whether to allow doing manual commits. | false | MEDIUM |
| **camel.kamelet.kafka-scram-source.pollOnError** | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | "ERROR\_HANDLER" | MEDIUM |
| **camel.kamelet.kafka-scram-source.autoOffsetReset** | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | "latest" | MEDIUM |
| **camel.kamelet.kafka-scram-source.consumerGroup** | A string that uniquely identifies the group of consumers to which this source belongs Example: my-group-id. |  | MEDIUM |
| **camel.kamelet.kafka-scram-source.deserializeHeaders** | When enabled the Kamelet source will deserialize all message headers to String representation. | true | MEDIUM |
| **camel.kamelet.kafka-scram-source.topicIsPattern** | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | false | MEDIUM |

The camel-kafka-scram-source source connector has no converters out of the box.

The camel-kafka-scram-source source connector has no transforms out of the box.

The camel-kafka-scram-source source connector has no aggregation strategies out of the box.