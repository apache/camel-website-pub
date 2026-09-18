# camel-slack-sink-kafka-connector sink configuration

Connector Description: Send messages to a Slack channel.

When using camel-slack-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-slack-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.slacksink.CamelSlacksinkSinkConnector
```

The camel-slack-sink sink connector supports 2 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.slack-sink.channel** | **Required** The Slack channel to send messages to. Example: #myroom. |  | HIGH |
| **camel.kamelet.slack-sink.webhookUrl** | **Required** The webhook URL used by the Slack channel to handle incoming messages. |  | HIGH |

The camel-slack-sink sink connector has no converters out of the box.

The camel-slack-sink sink connector has no transforms out of the box.

The camel-slack-sink sink connector has no aggregation strategies out of the box.