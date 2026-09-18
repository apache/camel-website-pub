# camel-chuck-norris-source-kafka-connector source configuration

Connector Description: Gets periodically Chuck Norris jokes

When using camel-chuck-norris-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-chuck-norris-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.chucknorrissource.CamelChucknorrissourceSourceConnector
```

The camel-chuck-norris-source source connector supports 1 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.chuck-norris-source.period** | The interval (msec) to wait before getting the next joke. | 10000 | MEDIUM |

The camel-chuck-norris-source source connector has no converters out of the box.

The camel-chuck-norris-source source connector has no transforms out of the box.

The camel-chuck-norris-source source connector has no aggregation strategies out of the box.