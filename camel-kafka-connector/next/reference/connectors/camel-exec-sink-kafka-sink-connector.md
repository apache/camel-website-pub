# camel-exec-sink-kafka-connector sink configuration

Connector Description: Execute system commands

When using camel-exec-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-exec-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.execsink.CamelExecsinkSinkConnector
```

The camel-exec-sink sink connector supports 1 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.exec-sink.executable** | **Required** The command to execute. |  | HIGH |

The camel-exec-sink sink connector has no converters out of the box.

The camel-exec-sink sink connector has no transforms out of the box.

The camel-exec-sink sink connector has no aggregation strategies out of the box.