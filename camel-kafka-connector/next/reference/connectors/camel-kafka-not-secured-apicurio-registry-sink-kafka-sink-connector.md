# camel-kafka-not-secured-apicurio-registry-sink-kafka-connector sink configuration

Connector Description: Send data to Kafka topics on an insecure broker with Apicurio Registry secured with Keycloak.

When using camel-kafka-not-secured-apicurio-registry-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-kafka-not-secured-apicurio-registry-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.kafkanotsecuredapicurioregistrysink.CamelKafkanotsecuredapicurioregistrysinkSinkConnector
```

The camel-kafka-not-secured-apicurio-registry-sink sink connector supports 11 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.topic** | **Required** Comma separated list of Kafka topic names. |  | HIGH |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.bootstrapServers** | **Required** Comma separated list of Kafka Broker URLs. |  | HIGH |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.valueSerializer** | Serliazer class for value that implements the Serializer interface. | "io.apicurio.registry.serde.avro.AvroKafkaSerializer" | MEDIUM |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.apicurioRegistryUrl** | **Required** The Apicurio Schema Registry URL. |  | HIGH |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.avroDatumProvider** | How to write data with Avro. | "io.apicurio.registry.serde.avro.ReflectAvroDatumProvider" | MEDIUM |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.apicurioAuthServiceUrl** | **Required** The URL for Keycloak instance securing the Apicurio Registry Example: [http://my-keycloak.com:8080/](http://my-keycloak.com:8080/). |  | HIGH |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.apicurioAuthRealm** | **Required** The Realm in Keycloak instance securing the Apicurio Registry. |  | HIGH |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.apicurioAuthClientId** | **Required** The Client ID in Keycloak instance securing the Apicurio Registry. |  | HIGH |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.apicurioAuthClientSecret** | **Required** The Client Secret in Keycloak instance securing the Apicurio Registry. |  | HIGH |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.apicurioAuthUsername** | **Required** The Username in Keycloak instance securing the Apicurio Registry. |  | HIGH |
| **camel.kamelet.kafka-not-secured-apicurio-registry-sink.apicurioAuthPassword** | **Required** The Password in Keycloak instance securing the Apicurio Registry. |  | HIGH |

The camel-kafka-not-secured-apicurio-registry-sink sink connector has no converters out of the box.

The camel-kafka-not-secured-apicurio-registry-sink sink connector has no transforms out of the box.

The camel-kafka-not-secured-apicurio-registry-sink sink connector has no aggregation strategies out of the box.