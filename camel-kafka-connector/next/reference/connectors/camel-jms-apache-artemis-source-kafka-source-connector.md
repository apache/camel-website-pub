# camel-jms-apache-artemis-source-kafka-connector source configuration

Connector Description: Receive data from an Apache Artemis message broker by using JMS.

When using camel-jms-apache-artemis-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-jms-apache-artemis-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.jmsapacheartemissource.CamelJmsapacheartemissourceSourceConnector
```

The camel-jms-apache-artemis-source source connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.jms-apache-artemis-source.destinationType** | The JMS destination type (queue or topic). | "queue" | MEDIUM |
| **camel.kamelet.jms-apache-artemis-source.destinationName** | **Required** The JMS destination name. |  | HIGH |
| **camel.kamelet.jms-apache-artemis-source.brokerURL** | **Required** The JMS URL. Example: tcp://my-host:61616. |  | HIGH |

The camel-jms-apache-artemis-source source connector has no converters out of the box.

The camel-jms-apache-artemis-source source connector has no transforms out of the box.

The camel-jms-apache-artemis-source source connector has no aggregation strategies out of the box.