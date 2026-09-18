# camel-jms-ibm-mq-sink-kafka-connector sink configuration

Connector Description: A Kamelet that can produce events to an IBM MQ message queue using JMS.

When using camel-jms-ibm-mq-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-jms-ibm-mq-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.jmsibmmqsink.CamelJmsibmmqsinkSinkConnector
```

The camel-jms-ibm-mq-sink sink connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.jms-ibm-mq-sink.serverName** | **Required** IBM MQ Server name or address. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-sink.serverPort** | **Required** IBM MQ Server port. | 1414 | HIGH |
| **camel.kamelet.jms-ibm-mq-sink.destinationType** | The JMS destination type (queue or topic). | "queue" | MEDIUM |
| **camel.kamelet.jms-ibm-mq-sink.destinationName** | **Required** The destination name. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-sink.queueManager** | **Required** Name of the IBM MQ Queue Manager. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-sink.channel** | **Required** Name of the IBM MQ Channel. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-sink.clientId** | Name of the IBM MQ Client ID. |  | MEDIUM |
| **camel.kamelet.jms-ibm-mq-sink.username** | **Required** Username to authenticate to IBM MQ server. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-sink.password** | **Required** Password to authenticate to IBM MQ server. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-sink.sslCipherSuite** | CipherSuite to use for enabling TLS. |  | MEDIUM |

The camel-jms-ibm-mq-sink sink connector has no converters out of the box.

The camel-jms-ibm-mq-sink sink connector has no transforms out of the box.

The camel-jms-ibm-mq-sink sink connector has no aggregation strategies out of the box.