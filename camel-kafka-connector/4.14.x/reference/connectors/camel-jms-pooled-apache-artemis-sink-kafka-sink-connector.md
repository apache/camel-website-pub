# camel-jms-pooled-apache-artemis-sink-kafka-connector sink configuration

Connector Description: Send data to an Apache Artemis message broker by using JMS Pooled.

When using camel-jms-pooled-apache-artemis-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-jms-pooled-apache-artemis-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.jmspooledapacheartemissink.CamelJmspooledapacheartemissinkSinkConnector
```

The camel-jms-pooled-apache-artemis-sink sink connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.jms-pooled-apache-artemis-sink.destinationType** | The JMS destination type (queue or topic). | "queue" | MEDIUM |
| **camel.kamelet.jms-pooled-apache-artemis-sink.destinationName** | **Required** The JMS destination name. Example: person. |  | HIGH |
| **camel.kamelet.jms-pooled-apache-artemis-sink.brokerURL** | **Required** The JMS URL. Example: tcp://my-host:61616. |  | HIGH |
| **camel.kamelet.jms-pooled-apache-artemis-sink.username** | The JMS Broker Username. |  | MEDIUM |
| **camel.kamelet.jms-pooled-apache-artemis-sink.password** | The JMS Broker Password. |  | MEDIUM |
| **camel.kamelet.jms-pooled-apache-artemis-sink.maxSessionsPerConnection** | The maximum number of pooled sessions per connection in the pool. | 500 | MEDIUM |
| **camel.kamelet.jms-pooled-apache-artemis-sink.maxIdleSessionsPerConnection** | The number of idle sessions allowed per connection before they are closed. | 500 | MEDIUM |
| **camel.kamelet.jms-pooled-apache-artemis-sink.connectionIdleTimeout** | The maximum time a pooled Connection can sit unused before it is eligible for removal (in milliseconds). | 30000 | MEDIUM |

The camel-jms-pooled-apache-artemis-sink sink connector has no converters out of the box.

The camel-jms-pooled-apache-artemis-sink sink connector has no transforms out of the box.

The camel-jms-pooled-apache-artemis-sink sink connector has no aggregation strategies out of the box.