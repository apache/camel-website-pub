# camel-azure-servicebus-sink-kafka-connector sink configuration

Connector Description: Send Messages to Azure Servicebus.

When using camel-azure-servicebus-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-servicebus-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azureservicebussink.CamelAzureservicebussinkSinkConnector
```

The camel-azure-servicebus-sink sink connector supports 4 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-servicebus-sink.topicOrQueueName** | **Required** Topic Or Queue Name for the Azure Servicebus instance. |  | HIGH |
| **camel.kamelet.azure-servicebus-sink.connectionString** | **Required** Connection String for Azure Servicebus instance. |  | HIGH |
| **camel.kamelet.azure-servicebus-sink.serviceBusType** | The service bus type of connection to execute. Queue is for typical queue option and topic for subscription based model. | "queue" | MEDIUM |
| **camel.kamelet.azure-servicebus-sink.credentialType** | Determines the credential strategy to adopt. | "CONNECTION\_STRING" | MEDIUM |

The camel-azure-servicebus-sink sink connector has no converters out of the box.

The camel-azure-servicebus-sink sink connector has no transforms out of the box.

The camel-azure-servicebus-sink sink connector has no aggregation strategies out of the box.