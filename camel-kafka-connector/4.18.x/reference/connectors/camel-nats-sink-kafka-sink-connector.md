# camel-nats-sink-kafka-connector sink configuration

Connector Description: Send data to NATS topics.

When using camel-nats-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-nats-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.natssink.CamelNatssinkSinkConnector
```

The camel-nats-sink sink connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.nats-sink.topic** | **Required** NATS Topic name. |  | HIGH |
| **camel.kamelet.nats-sink.servers** | **Required** Comma separated list of NATS Servers. |  | HIGH |
| **camel.kamelet.nats-sink.jetstreamEnabled** | Sets whether to enable JetStream support for this endpoint. | false | MEDIUM |
| **camel.kamelet.nats-sink.jetstreamName** | Sets the name of the JetStream stream to use. |  | MEDIUM |
| **camel.kamelet.nats-sink.jetstreamAsync** | Sets whether to operate JetStream requests asynchronously. | true | MEDIUM |

The camel-nats-sink sink connector has no converters out of the box.

The camel-nats-sink sink connector has no transforms out of the box.

The camel-nats-sink sink connector has no aggregation strategies out of the box.