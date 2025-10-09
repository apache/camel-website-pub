# camel-kafka-not-secured-sink-kafka-connector sink configuration

Connector Description: Send data to Kafka topics on an insecure broker.

When using camel-kafka-not-secured-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-not-secured-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkanotsecuredsink.CamelKafkanotsecuredsinkSinkConnector
```

The camel-kafka-not-secured-sink sink connector supports 2 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-not-secured-sink.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-not-secured-sink.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |

The camel-kafka-not-secured-sink sink connector has no converters out of the box.

The camel-kafka-not-secured-sink sink connector has no transforms out of the box.

The camel-kafka-not-secured-sink sink connector has no aggregation strategies out of the box.