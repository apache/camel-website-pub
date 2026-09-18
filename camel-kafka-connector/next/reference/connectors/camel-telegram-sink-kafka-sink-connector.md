# camel-telegram-sink-kafka-connector sink configuration

Connector Description: Send a message to a Telegram chat by using your Telegram bot as sender.

When using camel-telegram-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-telegram-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.telegramsink.CamelTelegramsinkSinkConnector
```

The camel-telegram-sink sink connector supports 2 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.telegram-sink.authorizationToken** | **Required** The token to access your bot on Telegram. You you can obtain it from the Telegram @botfather. |  | HIGH |
| **camel.kamelet.telegram-sink.chatId** | The Chat ID to where you want to send messages by default. |  | MEDIUM |

The camel-telegram-sink sink connector has no converters out of the box.

The camel-telegram-sink sink connector has no transforms out of the box.

The camel-telegram-sink sink connector has no aggregation strategies out of the box.