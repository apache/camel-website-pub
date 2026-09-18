# camel-jms-apache-artemis-sink-kafka-connector sink configuration

Connector Description: Send data to an Apache Artemis message broker by using JMS.

When using camel-jms-apache-artemis-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-jms-apache-artemis-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.jmsapacheartemissink.CamelJmsapacheartemissinkSinkConnector
```

The camel-jms-apache-artemis-sink sink connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.jms-apache-artemis-sink.destinationType** | The JMS destination type (queue or topic). | "queue" | MEDIUM |
| **camel.kamelet.jms-apache-artemis-sink.destinationName** | **Required** The JMS destination name. Example: person. |  | HIGH |
| **camel.kamelet.jms-apache-artemis-sink.brokerURL** | **Required** The JMS URL. Example: tcp://my-host:61616. |  | HIGH |

The camel-jms-apache-artemis-sink sink connector has no converters out of the box.

The camel-jms-apache-artemis-sink sink connector has no transforms out of the box.

The camel-jms-apache-artemis-sink sink connector has no aggregation strategies out of the box.