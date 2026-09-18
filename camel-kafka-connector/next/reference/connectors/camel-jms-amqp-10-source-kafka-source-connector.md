# camel-jms-amqp-10-source-kafka-connector source configuration

Connector Description: Consume data from any AMQP 1.0 compliant message broker by using the Apache Qpid JMS client. For SSL/TLS connections, use the amqps:// scheme in the remoteURI and configure SSL transport options as query parameters (e.g. transport.trustStoreLocation, transport.trustStorePassword, transport.keyStoreLocation, transport.keyStorePassword, transport.verifyHost, transport.trustAll).

When using camel-jms-amqp-10-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-jms-amqp-10-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.jmsamqp10source.CamelJmsamqp10sourceSourceConnector
```

The camel-jms-amqp-10-source source connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.jms-amqp-10-source.destinationType** | The JMS destination type (queue or topic). | "queue" | MEDIUM |
| **camel.kamelet.jms-amqp-10-source.destinationName** | **Required** The JMS destination name. |  | HIGH |
| **camel.kamelet.jms-amqp-10-source.remoteURI** | **Required** The JMS URL. Use the amqps:// scheme for SSL/TLS connections. Example: amqp://my-host:31616. |  | HIGH |

The camel-jms-amqp-10-source source connector has no converters out of the box.

The camel-jms-amqp-10-source source connector has no transforms out of the box.

The camel-jms-amqp-10-source source connector has no aggregation strategies out of the box.