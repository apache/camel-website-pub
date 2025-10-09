# camel-mqtt-source-kafka-connector source configuration

Connector Description: Allows receiving messages from any endpoint that supports the MQTT protocol, such as a message broker.

When using camel-mqtt-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-mqtt-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.mqttsource.CamelMqttsourceSourceConnector
```

The camel-mqtt-source source connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.mqtt-source.topic** | **Required** The topic to subscribe to Example: mytopic. |  | HIGH |
| **camel.kamelet.mqtt-source.brokerUrl** | **Required** The URL of the broker where to establish the connection Example: tcp://mosquitto:1883. |  | HIGH |
| **camel.kamelet.mqtt-source.clientId** | The client ID to use when connecting to the resource. | "mqtt-source" | MEDIUM |
| **camel.kamelet.mqtt-source.username** | Username to use when connecting to the MQTT broker. |  | MEDIUM |
| **camel.kamelet.mqtt-source.password** | Password to use when connecting to the MQTT broker. |  | MEDIUM |

The camel-mqtt-source source connector has no converters out of the box.

The camel-mqtt-source source connector has no transforms out of the box.

The camel-mqtt-source source connector has no aggregation strategies out of the box.