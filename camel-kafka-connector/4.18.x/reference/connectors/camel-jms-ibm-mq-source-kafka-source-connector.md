# camel-jms-ibm-mq-source-kafka-connector source configuration

Connector Description: A Kamelet that can read events from an IBM MQ message queue using JMS.

When using camel-jms-ibm-mq-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-jms-ibm-mq-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.jmsibmmqsource.CamelJmsibmmqsourceSourceConnector
```

The camel-jms-ibm-mq-source source connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.jms-ibm-mq-source.serverName** | **Required** IBM MQ Server name or address. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-source.serverPort** | **Required** IBM MQ Server port. | 1414 | HIGH |
| **camel.kamelet.jms-ibm-mq-source.destinationType** | The JMS destination type (queue or topic). | "queue" | MEDIUM |
| **camel.kamelet.jms-ibm-mq-source.destinationName** | **Required** The destination name. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-source.queueManager** | **Required** Name of the IBM MQ Queue Manager. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-source.channel** | **Required** Name of the IBM MQ Channel. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-source.clientId** | Name of the IBM MQ Client ID. |  | MEDIUM |
| **camel.kamelet.jms-ibm-mq-source.username** | **Required** Username to authenticate to IBM MQ server. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-source.password** | **Required** Password to authenticate to IBM MQ server. |  | HIGH |
| **camel.kamelet.jms-ibm-mq-source.sslCipherSuite** | CipherSuite to use for enabling TLS. |  | MEDIUM |

The camel-jms-ibm-mq-source source connector has no converters out of the box.

The camel-jms-ibm-mq-source source connector has no transforms out of the box.

The camel-jms-ibm-mq-source source connector has no aggregation strategies out of the box.