# camel-kafka-azure-schema-registry-sink-kafka-connector sink configuration

Connector Description: Send data to Kafka topics on Azure Eventhubs combined with Azure Schema Registry.

When using camel-kafka-azure-schema-registry-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-azure-schema-registry-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkaazureschemaregistrysink.CamelKafkaazureschemaregistrysinkSinkConnector
```

The camel-kafka-azure-schema-registry-sink sink connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-azure-schema-registry-sink.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-azure-schema-registry-sink.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-azure-schema-registry-sink.securityProtocol** | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | "SASL\_SSL" | MEDIUM |
| **camel.kamelet.kafka-azure-schema-registry-sink.saslMechanism** | The Simple Authentication and Security Layer (SASL) Mechanism used. | "PLAIN" | MEDIUM |
| **camel.kamelet.kafka-azure-schema-registry-sink.password** | **Required** Password to authenticate to kafka. |  | HIGH |
| **camel.kamelet.kafka-azure-schema-registry-sink.valueSerializer** | Deserializer class for value that implements the Deserializer interface. | "com.microsoft.azure.schemaregistry.kafka.avro.KafkaAvroSerializer" | MEDIUM |
| **camel.kamelet.kafka-azure-schema-registry-sink.azureRegistryUrl** | **Required** The Apicurio Schema Registry URL. |  | HIGH |
| **camel.kamelet.kafka-azure-schema-registry-sink.specificAvroValueType** | The Specific Type Avro will have to deal with Example: com.example.Order. |  | MEDIUM |

The camel-kafka-azure-schema-registry-sink sink connector has no converters out of the box.

The camel-kafka-azure-schema-registry-sink sink connector has no transforms out of the box.

The camel-kafka-azure-schema-registry-sink sink connector has no aggregation strategies out of the box.