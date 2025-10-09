# camel-mail-sink-kafka-connector sink configuration

Connector Description: Send mails to given SMTP server.

When using camel-mail-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-mail-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.mailsink.CamelMailsinkSinkConnector
```

The camel-mail-sink sink connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.mail-sink.connectionHost** | **Required** The mail server host Example: smtp.gmail.com. |  | HIGH |
| **camel.kamelet.mail-sink.connectionPort** | The mail server port. | "25" | MEDIUM |
| **camel.kamelet.mail-sink.username** | **Required** The username to access the mail box. |  | HIGH |
| **camel.kamelet.mail-sink.password** | **Required** The password to access the mail box. |  | HIGH |
| **camel.kamelet.mail-sink.from** | The `from` field of the outgoing mail. |  | MEDIUM |
| **camel.kamelet.mail-sink.to** | The `to` field of the outgoing mail. |  | MEDIUM |
| **camel.kamelet.mail-sink.subject** | The mail subject of the outgoing mail. |  | MEDIUM |

The camel-mail-sink sink connector has no converters out of the box.

The camel-mail-sink sink connector has no transforms out of the box.

The camel-mail-sink sink connector has no aggregation strategies out of the box.