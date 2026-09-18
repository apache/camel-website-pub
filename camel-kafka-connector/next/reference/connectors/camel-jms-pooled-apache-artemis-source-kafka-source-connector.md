# camel-jms-pooled-apache-artemis-source-kafka-connector source configuration

Connector Description: Receive data from an Apache Artemis message broker by using JMS Pooled Connection.

When using camel-jms-pooled-apache-artemis-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-jms-pooled-apache-artemis-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.jmspooledapacheartemissource.CamelJmspooledapacheartemissourceSourceConnector
```

The camel-jms-pooled-apache-artemis-source source connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.jms-pooled-apache-artemis-source.destinationType** | The JMS destination type (queue or topic). | "queue" | MEDIUM |
| **camel.kamelet.jms-pooled-apache-artemis-source.destinationName** | **Required** The JMS destination name. |  | HIGH |
| **camel.kamelet.jms-pooled-apache-artemis-source.brokerURL** | **Required** The JMS URL. Example: tcp://my-host:61616. |  | HIGH |
| **camel.kamelet.jms-pooled-apache-artemis-source.username** | The JMS Broker Username. |  | MEDIUM |
| **camel.kamelet.jms-pooled-apache-artemis-source.password** | The JMS Broker Password. |  | MEDIUM |
| **camel.kamelet.jms-pooled-apache-artemis-source.maxSessionsPerConnection** | The maximum number of pooled sessions per connection in the pool. | 500 | MEDIUM |
| **camel.kamelet.jms-pooled-apache-artemis-source.maxIdleSessionsPerConnection** | The number of idle sessions allowed per connection before they are closed. | 500 | MEDIUM |
| **camel.kamelet.jms-pooled-apache-artemis-source.connectionIdleTimeout** | The maximum time a pooled Connection can sit unused before it is eligible for removal (in milliseconds). | 30000 | MEDIUM |

The camel-jms-pooled-apache-artemis-source source connector has no converters out of the box.

The camel-jms-pooled-apache-artemis-source source connector has no transforms out of the box.

The camel-jms-pooled-apache-artemis-source source connector has no aggregation strategies out of the box.