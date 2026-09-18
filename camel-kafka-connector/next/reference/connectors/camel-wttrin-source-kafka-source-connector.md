# camel-wttrin-source-kafka-connector source configuration

Connector Description: Get weather forecasts from the wttr.in weather forecast service

When using camel-wttrin-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-wttrin-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.wttrinsource.CamelWttrinsourceSourceConnector
```

The camel-wttrin-source source connector supports 4 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.wttrin-source.period** | The interval between fetches to the wttr.in service in milliseconds. | 60000 | MEDIUM |
| **camel.kamelet.wttrin-source.wttrLocation** | The location to get weather forecasts Example: "paris", "~Eiffel+tower", "Москва", "muc", "@stackoverflow.com", "94107", "-78.46,106.79". |  | MEDIUM |
| **camel.kamelet.wttrin-source.wttrLanguage** | The language to use for displaying weather forecasts Example: am ar af be bn ca da de el et fr fa hi hu ia id it lt mg nb nl oc pl pt-br ro ru ta tr th uk vi zh-cn zh-tw. |  | MEDIUM |
| **camel.kamelet.wttrin-source.output** | The type of output Example: current, weather, full. | "current" | MEDIUM |

The camel-wttrin-source source connector has no converters out of the box.

The camel-wttrin-source source connector has no transforms out of the box.

The camel-wttrin-source source connector has no aggregation strategies out of the box.