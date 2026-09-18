# camel-counter-source-kafka-connector source configuration

Connector Description: Generates sequential number events starting from a configurable value, incrementing by a specified step. Useful for testing, scheduled tasks, or creating ordered event sequences.

When using camel-counter-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-counter-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.countersource.CamelCountersourceSourceConnector
```

The camel-counter-source source connector supports 3 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.counter-source.period** | The time interval between two numbers. | 1000 | MEDIUM |
| **camel.kamelet.counter-source.start** | The starting number. | 1 | MEDIUM |
| **camel.kamelet.counter-source.numbers** | How many numbers to generate. |  | MEDIUM |

The camel-counter-source source connector has no converters out of the box.

The camel-counter-source source connector has no transforms out of the box.

The camel-counter-source source connector has no aggregation strategies out of the box.