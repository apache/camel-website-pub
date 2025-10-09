# camel-azure-servicebus-source-kafka-connector source configuration

Connector Description: Consume Messages from Azure Servicebus.

When using camel-azure-servicebus-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-servicebus-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azureservicebussource.CamelAzureservicebussourceSourceConnector
```

The camel-azure-servicebus-source source connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-servicebus-source.topicOrQueueName** | **Required** Topic Or Queue Name for the Azure Servicebus instance. |  | HIGH |
| **camel.kamelet.azure-servicebus-source.connectionString** | **Required** Connection String for Azure Servicebus instance. |  | HIGH |
| **camel.kamelet.azure-servicebus-source.serviceBusReceiveMode** | Sets the receive mode for the receiver. | "PEEK\_LOCK" | MEDIUM |
| **camel.kamelet.azure-servicebus-source.subscriptionName** | Sets the name of the subscription in the topic to listen to. This parameter is mandatory in case of topic. |  | MEDIUM |
| **camel.kamelet.azure-servicebus-source.serviceBusType** | The service bus type of connection to execute. Queue is for typical queue option and topic for subscription based model. | "queue" | MEDIUM |
| **camel.kamelet.azure-servicebus-source.credentialType** | Determines the credential strategy to adopt. | "CONNECTION\_STRING" | MEDIUM |

The camel-azure-servicebus-source source connector has no converters out of the box.

The camel-azure-servicebus-source source connector has no transforms out of the box.

The camel-azure-servicebus-source source connector has no aggregation strategies out of the box.