# camel-splunk-hec-sink-kafka-connector sink configuration

Connector Description: The Splunk HEC sink allows to send data to Splunk using the [HTTP Event Collector](https://docs.splunk.com/Documentation/Splunk/latest/Data/UsetheHTTPEventCollector).

When using camel-splunk-hec-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-splunk-hec-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.splunkhecsink.CamelSplunkhecsinkSinkConnector
```

The camel-splunk-hec-sink sink connector supports 11 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.splunk-hec-sink.splunkUrl** | **Required** The URL of your Splunk server. No need to set the protocol prefix. Example: my\_server.splunkcloud.com:8088. |  | HIGH |
| **camel.kamelet.splunk-hec-sink.token** | **Required** The Token of the HEC. Note it is not the user’s authentication token. |  | HIGH |
| **camel.kamelet.splunk-hec-sink.hostPayload** | The host field set in the data sent to Splunk, it is not related to the Splunk URL or the connection to Splunk server. |  | MEDIUM |
| **camel.kamelet.splunk-hec-sink.bodyOnly** | Send to Splunk only data contained in the body. | false | MEDIUM |
| **camel.kamelet.splunk-hec-sink.headersOnly** | Send to Splunk only data contained in the headers. | false | MEDIUM |
| **camel.kamelet.splunk-hec-sink.index** | Splunk index to write to. |  | MEDIUM |
| **camel.kamelet.splunk-hec-sink.source** | The source named field of the data. |  | MEDIUM |
| **camel.kamelet.splunk-hec-sink.sourceType** | The source named field of the data. |  | MEDIUM |
| **camel.kamelet.splunk-hec-sink.skipTlsVerify** | Skip TLS verification. | false | MEDIUM |
| **camel.kamelet.splunk-hec-sink.https** | Use a secure HTTPS connection. | true | MEDIUM |
| **camel.kamelet.splunk-hec-sink.time** | Time this event occurred. By default, the time is when this event hits the Splunk server. |  | MEDIUM |

The camel-splunk-hec-sink sink connector has no converters out of the box.

The camel-splunk-hec-sink sink connector has no transforms out of the box.

The camel-splunk-hec-sink sink connector has no aggregation strategies out of the box.