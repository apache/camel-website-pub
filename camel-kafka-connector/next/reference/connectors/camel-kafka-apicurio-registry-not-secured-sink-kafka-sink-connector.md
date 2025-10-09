# camel-kafka-apicurio-registry-not-secured-sink-kafka-connector sink configuration

Connector Description: Send data to Kafka topics on an insecure broker with Apicurio Registry.

When using camel-kafka-apicurio-registry-not-secured-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-apicurio-registry-not-secured-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkaapicurioregistrynotsecuredsink.CamelKafkaapicurioregistrynotsecuredsinkSinkConnector
```

The camel-kafka-apicurio-registry-not-secured-sink sink connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-apicurio-registry-not-secured-sink.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-apicurio-registry-not-secured-sink.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-apicurio-registry-not-secured-sink.valueSerializer** | Serliazer class for value that implements the Serializer interface. | "io.apicurio.registry.serde.avro.AvroKafkaSerializer" | MEDIUM |
| **camel.kamelet.kafka-apicurio-registry-not-secured-sink.apicurioRegistryUrl** | **Required** The Apicurio Schema Registry URL. |  | HIGH |
| **camel.kamelet.kafka-apicurio-registry-not-secured-sink.avroDatumProvider** | How to write data with Avro. | "io.apicurio.registry.serde.avro.ReflectAvroDatumProvider" | MEDIUM |

The camel-kafka-apicurio-registry-not-secured-sink sink connector has no converters out of the box.

The camel-kafka-apicurio-registry-not-secured-sink sink connector has no transforms out of the box.

The camel-kafka-apicurio-registry-not-secured-sink sink connector has no aggregation strategies out of the box.