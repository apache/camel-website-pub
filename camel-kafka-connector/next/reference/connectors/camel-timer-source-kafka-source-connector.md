# camel-timer-source-kafka-connector source configuration

Connector Description: Produces periodic messages with a custom payload.

When using camel-timer-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-timer-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.timersource.CamelTimersourceSourceConnector
```

The camel-timer-source source connector supports 4 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.timer-source.period** | The interval (in milliseconds) to wait between producing the next message. | 1000 | MEDIUM |
| **camel.kamelet.timer-source.message** | **Required** The message to generate. Example: hello world. |  | HIGH |
| **camel.kamelet.timer-source.contentType** | The content type of the generated message. | "text/plain" | MEDIUM |
| **camel.kamelet.timer-source.repeatCount** | Specifies a maximum limit of number of fires. |  | MEDIUM |

The camel-timer-source source connector has no converters out of the box.

The camel-timer-source source connector has no transforms out of the box.

The camel-timer-source source connector has no aggregation strategies out of the box.