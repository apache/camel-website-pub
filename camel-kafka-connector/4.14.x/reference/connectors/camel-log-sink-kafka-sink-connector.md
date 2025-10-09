# camel-log-sink-kafka-connector sink configuration

Connector Description: A sink that logs all data that it receives, useful for debugging purposes.

When using camel-log-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-log-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.logsink.CamelLogsinkSinkConnector
```

The camel-log-sink sink connector supports 13 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.log-sink.loggerName** | Name of the logging category to use. | "log-sink" | MEDIUM |
| **camel.kamelet.log-sink.level** | Logging level to use. | "INFO" | MEDIUM |
| **camel.kamelet.log-sink.logMask** | Mask sensitive information like password or passphrase in the log. | false | MEDIUM |
| **camel.kamelet.log-sink.marker** | An optional Marker name to use. |  | MEDIUM |
| **camel.kamelet.log-sink.multiline** | If enabled then each information is outputted on a newline. | false | MEDIUM |
| **camel.kamelet.log-sink.showAllProperties** | Show all of the exchange properties (both internal and custom). | false | MEDIUM |
| **camel.kamelet.log-sink.showBody** | Show the message body. | true | MEDIUM |
| **camel.kamelet.log-sink.showBodyType** | Show the body Java type. | true | MEDIUM |
| **camel.kamelet.log-sink.showExchangePattern** | Shows the Message Exchange Pattern (or MEP for short). | true | MEDIUM |
| **camel.kamelet.log-sink.showHeaders** | Show the headers received. | false | MEDIUM |
| **camel.kamelet.log-sink.showProperties** | Show the exchange properties (only custom). Use showAllProperties to show both internal and custom properties. | false | MEDIUM |
| **camel.kamelet.log-sink.showStreams** | Show the stream bodies (they may not be available in following steps). | false | MEDIUM |
| **camel.kamelet.log-sink.showCachedStreams** | Whether Camel should show cached stream bodies or not. | true | MEDIUM |

The camel-log-sink sink connector has no converters out of the box.

The camel-log-sink sink connector has no transforms out of the box.

The camel-log-sink sink connector has no aggregation strategies out of the box.