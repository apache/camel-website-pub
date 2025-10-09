# camel-kafka-scram-sink-kafka-connector sink configuration

Connector Description: Send data to Kafka topics through SCRAM login module.

When using camel-kafka-scram-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-scram-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkascramsink.CamelKafkascramsinkSinkConnector
```

The camel-kafka-scram-sink sink connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-scram-sink.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-scram-sink.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-scram-sink.securityProtocol** | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | "SASL\_SSL" | MEDIUM |
| **camel.kamelet.kafka-scram-sink.saslMechanism** | The Simple Authentication and Security Layer (SASL) Mechanism used. | "SCRAM-SHA-512" | MEDIUM |
| **camel.kamelet.kafka-scram-sink.user** | **Required** Username to authenticate to Kafka . |  | HIGH |
| **camel.kamelet.kafka-scram-sink.password** | **Required** Password to authenticate to kafka. |  | HIGH |

The camel-kafka-scram-sink sink connector has no converters out of the box.

The camel-kafka-scram-sink sink connector has no transforms out of the box.

The camel-kafka-scram-sink sink connector has no aggregation strategies out of the box.