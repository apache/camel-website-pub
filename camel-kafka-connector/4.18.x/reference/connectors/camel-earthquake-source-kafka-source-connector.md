# camel-earthquake-source-kafka-connector source configuration

Connector Description: Get data about current earthquake events happening in the world using the USGS API

When using camel-earthquake-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-earthquake-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.earthquakesource.CamelEarthquakesourceSourceConnector
```

The camel-earthquake-source source connector supports 2 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.earthquake-source.period** | The interval between fetches to the earthquake API in milliseconds. | 60000 | MEDIUM |
| **camel.kamelet.earthquake-source.lookAhead** | The amount of minutes to look ahead when starting the integration afresh. | 120 | MEDIUM |

The camel-earthquake-source source connector has no converters out of the box.

The camel-earthquake-source source connector has no transforms out of the box.

The camel-earthquake-source source connector has no aggregation strategies out of the box.