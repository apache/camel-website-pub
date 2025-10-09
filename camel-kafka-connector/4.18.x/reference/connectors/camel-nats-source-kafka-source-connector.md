# camel-nats-source-kafka-connector source configuration

Connector Description: Receive data from NATS topics.

When using camel-nats-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-nats-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.natssource.CamelNatssourceSourceConnector
```

The camel-nats-source source connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.nats-source.topic** | **Required** NATS Topic name. |  | HIGH |
| **camel.kamelet.nats-source.servers** | **Required** Comma separated list of NATS Servers. |  | HIGH |
| **camel.kamelet.nats-source.jetstreamEnabled** | Sets whether to enable JetStream support for this endpoint. | false | MEDIUM |
| **camel.kamelet.nats-source.jetstreamName** | Sets the name of the JetStream stream to use. |  | MEDIUM |
| **camel.kamelet.nats-source.jetstreamAsync** | Sets whether to operate JetStream requests asynchronously. | true | MEDIUM |

The camel-nats-source source connector has no converters out of the box.

The camel-nats-source source connector has no transforms out of the box.

The camel-nats-source source connector has no aggregation strategies out of the box.