# camel-mail-imap-source-kafka-connector source configuration

Connector Description: Receive unread emails from an IMAP mail server, marking them as read once they are received.

When using camel-mail-imap-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-mail-imap-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.mailimapsource.CamelMailimapsourceSourceConnector
```

The camel-mail-imap-source source connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.mail-imap-source.connectionHost** | **Required** The IMAP server host. Example: imap.gmail.com. |  | HIGH |
| **camel.kamelet.mail-imap-source.connectionPort** | **Required** The IMAP server port. | "993" | HIGH |
| **camel.kamelet.mail-imap-source.username** | **Required** The username to access the mail box. |  | HIGH |
| **camel.kamelet.mail-imap-source.password** | **Required** The password to access the mail box. |  | HIGH |
| **camel.kamelet.mail-imap-source.fetchSize** | The number of messages fetched for each poll (-1 for no limits). | 10 | MEDIUM |
| **camel.kamelet.mail-imap-source.delay** | The delay between fetches in milliseconds. | 60000 | MEDIUM |

The camel-mail-imap-source source connector has no converters out of the box.

The camel-mail-imap-source source connector has no transforms out of the box.

The camel-mail-imap-source source connector has no aggregation strategies out of the box.