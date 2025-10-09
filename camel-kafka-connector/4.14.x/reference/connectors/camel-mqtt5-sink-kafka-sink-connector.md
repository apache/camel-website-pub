# camel-mqtt5-sink-kafka-connector sink configuration

Connector Description: Allows sending messages to any endpoint that supports the MQTT v5 protocol, such as a message broker.

When using camel-mqtt5-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-mqtt5-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.mqtt5sink.CamelMqtt5sinkSinkConnector
```

The camel-mqtt5-sink sink connector supports 4 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.mqtt5-sink.topic** | **Required** The topic to send messages to. Example: mytopic. |  | HIGH |
| **camel.kamelet.mqtt5-sink.brokerUrl** | **Required** The URL of the broker where to establish the connection. Example: tcp://mosquitto:1883. |  | HIGH |
| **camel.kamelet.mqtt5-sink.username** | Username to use when connecting to the MQTT v5 compliant broker. |  | MEDIUM |
| **camel.kamelet.mqtt5-sink.password** | Password to use when connecting to the MQTT v5 compliant broker. |  | MEDIUM |

The camel-mqtt5-sink sink connector has no converters out of the box.

The camel-mqtt5-sink sink connector has no transforms out of the box.

The camel-mqtt5-sink sink connector has no aggregation strategies out of the box.