# camel-webhook-source-kafka-connector source configuration

Connector Description: Creates an HTTP endpoint that can be used as a bridge to forward data to the Kamelet sink.

When using camel-webhook-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-webhook-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.webhooksource.CamelWebhooksourceSourceConnector
```

The camel-webhook-source source connector supports 1 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.webhook-source.subpath** | The subpath where the webhook is registered . | "webhook" | MEDIUM |

The camel-webhook-source source connector has no converters out of the box.

The camel-webhook-source source connector has no transforms out of the box.

The camel-webhook-source source connector has no aggregation strategies out of the box.