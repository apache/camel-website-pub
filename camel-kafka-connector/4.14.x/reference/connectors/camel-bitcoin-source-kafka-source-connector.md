# camel-bitcoin-source-kafka-connector source configuration

Connector Description: Provides a feed of the value of the Bitcoin compared to USDT using the Binance service.

When using camel-bitcoin-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-bitcoin-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.bitcoinsource.CamelBitcoinsourceSourceConnector
```

The camel-bitcoin-source source connector supports 1 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.bitcoin-source.period** | The interval between updates in milliseconds. | 10000 | MEDIUM |

The camel-bitcoin-source source connector has no converters out of the box.

The camel-bitcoin-source source connector has no transforms out of the box.

The camel-bitcoin-source source connector has no aggregation strategies out of the box.