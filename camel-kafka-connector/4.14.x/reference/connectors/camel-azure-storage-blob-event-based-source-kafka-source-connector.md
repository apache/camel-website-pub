# camel-azure-storage-blob-event-based-source-kafka-connector source configuration

Connector Description: Receive data from Azure Service Bus subscribed to Azure Eventgrid reporting events related to a Azure Storage Blob account.

When using camel-azure-storage-blob-event-based-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-blob-event-based-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestorageblobeventbasedsource.CamelAzurestorageblobeventbasedsourceSourceConnector
```

The camel-azure-storage-blob-event-based-source source connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-blob-event-based-source.topicOrQueueName** | **Required** Topic Or Queue Name for the Azure Servicebus instance. |  | HIGH |
| **camel.kamelet.azure-storage-blob-event-based-source.connectionString** | **Required** Connection String for Azure Servicebus instance. |  | HIGH |
| **camel.kamelet.azure-storage-blob-event-based-source.serviceBusReceiveMode** | Sets the receive mode for the receiver. | "RECEIVE\_AND\_DELETE" | MEDIUM |
| **camel.kamelet.azure-storage-blob-event-based-source.subscriptionName** | Sets the name of the subscription in the topic to listen to. This parameter is mandatory in case of topic. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-event-based-source.accountName** | **Required** The Azure Storage Blob account name. |  | HIGH |
| **camel.kamelet.azure-storage-blob-event-based-source.containerName** | **Required** The Azure Storage Blob container name. |  | HIGH |
| **camel.kamelet.azure-storage-blob-event-based-source.accessKey** | **Required** The Azure Storage Blob access key. |  | HIGH |
| **camel.kamelet.azure-storage-blob-event-based-source.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |
| **camel.kamelet.azure-storage-blob-event-based-source.getBlob** | If `getBlob` is enabled, then the file created in the container is retrieved and returned as body. If not only the event is returned as body. | false | MEDIUM |

The camel-azure-storage-blob-event-based-source source connector has no converters out of the box.

The camel-azure-storage-blob-event-based-source source connector has no transforms out of the box.

The camel-azure-storage-blob-event-based-source source connector has no aggregation strategies out of the box.