# camel-slack-source-kafka-connector source configuration

Connector Description: Receive messages from a Slack channel.

When using camel-slack-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-slack-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.slacksource.CamelSlacksourceSourceConnector
```

The camel-slack-source source connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.slack-source.serverUrl** | The Slack API server endpoint URL. Example: [https://slack.com](https://slack.com). | "https://slack.com" | MEDIUM |
| **camel.kamelet.slack-source.channel** | **Required** The Slack channel to receive messages from. Example: #myroom. |  | HIGH |
| **camel.kamelet.slack-source.token** | **Required** The Bot User OAuth Access Token to access Slack. A Slack app that has the following permissions is required: `channels:history`, `groups:history`, `im:history`, `mpim:history`, `channels:read`, `groups:read`, `im:read`, and `mpim:read`. |  | HIGH |
| **camel.kamelet.slack-source.delay** | The delay between polls. If no unit provided, milliseconds is the default. Example: 60s or 6000 or 1m. | "60000" | MEDIUM |
| **camel.kamelet.slack-source.naturalOrder** | Create exchanges in natural order (oldest to newest) or not. | false | MEDIUM |

The camel-slack-source source connector has no converters out of the box.

The camel-slack-source source connector has no transforms out of the box.

The camel-slack-source source connector has no aggregation strategies out of the box.