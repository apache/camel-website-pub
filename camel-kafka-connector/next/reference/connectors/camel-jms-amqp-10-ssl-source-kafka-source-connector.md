# camel-jms-amqp-10-ssl-source-kafka-connector source configuration

Connector Description: Consume data from any AMQP 1.0 compliant message broker over an SSL/TLS connection by using the Apache Qpid JMS client. SSL transport options can be configured as query parameters on the remoteURI (e.g. transport.trustStoreLocation, transport.trustStorePassword, transport.keyStoreLocation, transport.keyStorePassword, transport.verifyHost, transport.trustAll).

When using camel-jms-amqp-10-ssl-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-jms-amqp-10-ssl-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.jmsamqp10sslsource.CamelJmsamqp10sslsourceSourceConnector
```

The camel-jms-amqp-10-ssl-source source connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.jms-amqp-10-ssl-source.destinationType** | The JMS destination type (queue or topic). | "queue" | MEDIUM |
| **camel.kamelet.jms-amqp-10-ssl-source.destinationName** | **Required** The JMS destination name. |  | HIGH |
| **camel.kamelet.jms-amqp-10-ssl-source.remoteURI** | **Required** The JMS URL with amqps scheme and SSL transport options as query parameters. Example: amqps://my-host:5671?transport.trustStoreLocation=/path/to/truststore.jks&transport.trustStorePassword=changeit. |  | HIGH |

The camel-jms-amqp-10-ssl-source source connector has no converters out of the box.

The camel-jms-amqp-10-ssl-source source connector has no transforms out of the box.

The camel-jms-amqp-10-ssl-source source connector has no aggregation strategies out of the box.