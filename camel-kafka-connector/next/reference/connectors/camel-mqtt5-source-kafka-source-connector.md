# camel-mqtt5-source-kafka-connector source configuration

Connector Description: Allows receiving messages from any endpoint that supports the MQTT v5 protocol, such as a message broker.

When using camel-mqtt5-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-mqtt5-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.mqtt5source.CamelMqtt5sourceSourceConnector
```

The camel-mqtt5-source source connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.mqtt5-source.topic** | **Required** The topic to subscribe to Example: mytopic. |  | HIGH |
| **camel.kamelet.mqtt5-source.brokerUrl** | **Required** The URL of the broker where to establish the connection Example: tcp://mosquitto:1883. |  | HIGH |
| **camel.kamelet.mqtt5-source.clientId** | The client ID to use when connecting to the resource. | "mqtt-source" | MEDIUM |
| **camel.kamelet.mqtt5-source.username** | Username to use when connecting to the MQTT v5 compliant broker. |  | MEDIUM |
| **camel.kamelet.mqtt5-source.password** | Password to use when connecting to the MQTT v5 compliant broker. |  | MEDIUM |

The camel-mqtt5-source source connector has no converters out of the box.

The camel-mqtt5-source source connector has no transforms out of the box.

The camel-mqtt5-source source connector has no aggregation strategies out of the box.