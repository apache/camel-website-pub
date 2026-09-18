# camel-azure-eventhubs-sink-kafka-connector sink configuration

Connector Description: Send events to Azure Event Hubs.

When using camel-azure-eventhubs-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-eventhubs-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azureeventhubssink.CamelAzureeventhubssinkSinkConnector
```

The camel-azure-eventhubs-sink sink connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-eventhubs-sink.namespaceName** | **Required** The Event Hubs namespace. |  | HIGH |
| **camel.kamelet.azure-eventhubs-sink.eventhubName** | **Required** The Event Hub name. |  | HIGH |
| **camel.kamelet.azure-eventhubs-sink.sharedAccessName** | The Event Hubs SAS key name. |  | MEDIUM |
| **camel.kamelet.azure-eventhubs-sink.sharedAccessKey** | The key for the Event Hubs SAS key name. |  | MEDIUM |
| **camel.kamelet.azure-eventhubs-sink.credentialType** | Determines the credential strategy to adopt. | "CONNECTION\_STRING" | MEDIUM |

The camel-azure-eventhubs-sink sink connector has no converters out of the box.

The camel-azure-eventhubs-sink sink connector has no transforms out of the box.

The camel-azure-eventhubs-sink sink connector has no aggregation strategies out of the box.