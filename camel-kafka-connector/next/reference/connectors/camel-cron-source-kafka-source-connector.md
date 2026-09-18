# camel-cron-source-kafka-connector source configuration

Connector Description: Send events at specific time.

When using camel-cron-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-cron-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.cronsource.CamelCronsourceSourceConnector
```

The camel-cron-source source connector supports 2 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.cron-source.schedule** | **Required** A cron expression that is used to trigger events generation. Example: 0/3 10 \* \* \* ?. |  | HIGH |
| **camel.kamelet.cron-source.message** | **Required** The message to generate Example: hello world. |  | HIGH |

The camel-cron-source source connector has no converters out of the box.

The camel-cron-source source connector has no transforms out of the box.

The camel-cron-source source connector has no aggregation strategies out of the box.