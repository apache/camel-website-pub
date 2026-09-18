# camel-splunk-sink-kafka-connector sink configuration

Connector Description: Send data to Splunk either by using "submit" or "stream" mode.

When using camel-splunk-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-splunk-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.splunksink.CamelSplunksinkSinkConnector
```

The camel-splunk-sink sink connector supports 11 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.splunk-sink.serverHostname** | **Required** The address of your Splunk server. Example: my\_server\_splunk.com. |  | HIGH |
| **camel.kamelet.splunk-sink.serverPort** | The address of your Splunk server. | 8089 | MEDIUM |
| **camel.kamelet.splunk-sink.username** | **Required** The username to authenticate to Splunk Server. |  | HIGH |
| **camel.kamelet.splunk-sink.password** | **Required** The password to authenticate to Splunk Server. |  | HIGH |
| **camel.kamelet.splunk-sink.index** | Splunk index to write to. |  | MEDIUM |
| **camel.kamelet.splunk-sink.protocol** | Connection Protocol to Splunk server. | "https" | MEDIUM |
| **camel.kamelet.splunk-sink.source** | The source named field of the data. |  | MEDIUM |
| **camel.kamelet.splunk-sink.sourceType** | The source named field of the data. |  | MEDIUM |
| **camel.kamelet.splunk-sink.app** | The app name in Splunk. |  | MEDIUM |
| **camel.kamelet.splunk-sink.connectionTimeout** | Timeout in milliseconds when connecting to Splunk server. | 5000 | MEDIUM |
| **camel.kamelet.splunk-sink.mode** | The mode to publish events to Splunk. | "stream" | MEDIUM |

The camel-splunk-sink sink connector has no converters out of the box.

The camel-splunk-sink sink connector has no transforms out of the box.

The camel-splunk-sink sink connector has no aggregation strategies out of the box.