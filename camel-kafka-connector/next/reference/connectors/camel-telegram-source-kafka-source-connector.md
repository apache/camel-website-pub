# camel-telegram-source-kafka-connector source configuration

Connector Description: Receive all messages that people send to your Telegram bot.

When using camel-telegram-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-telegram-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.telegramsource.CamelTelegramsourceSourceConnector
```

The camel-telegram-source source connector supports 1 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.telegram-source.authorizationToken** | **Required** The token to access your bot on Telegram. You can obtain it from the Telegram @botfather. |  | HIGH |

The camel-telegram-source source connector has no converters out of the box.

The camel-telegram-source source connector has no transforms out of the box.

The camel-telegram-source source connector has no aggregation strategies out of the box.