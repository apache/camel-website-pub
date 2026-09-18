# camel-azure-eventhubs-source-kafka-connector source configuration

Connector Description: Receive events from Azure Event Hubs.

When using camel-azure-eventhubs-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-eventhubs-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azureeventhubssource.CamelAzureeventhubssourceSourceConnector
```

The camel-azure-eventhubs-source source connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-eventhubs-source.namespaceName** | **Required** The Event Hubs namespace. |  | HIGH |
| **camel.kamelet.azure-eventhubs-source.eventhubName** | **Required** The Event Hub name. |  | HIGH |
| **camel.kamelet.azure-eventhubs-source.sharedAccessName** | The Event Hubs SAS key name. |  | MEDIUM |
| **camel.kamelet.azure-eventhubs-source.sharedAccessKey** | The key for the Event Hubs SAS key name. |  | MEDIUM |
| **camel.kamelet.azure-eventhubs-source.blobAccountName** | **Required** The name of the Storage Blob account. |  | HIGH |
| **camel.kamelet.azure-eventhubs-source.blobContainerName** | **Required** The name of the Storage Blob container. |  | HIGH |
| **camel.kamelet.azure-eventhubs-source.blobAccessKey** | **Required** The key for the Azure Storage Blob service that is associated with the Storage Blob account name. |  | HIGH |
| **camel.kamelet.azure-eventhubs-source.credentialType** | Determines the credential strategy to adopt. | "CONNECTION\_STRING" | MEDIUM |

The camel-azure-eventhubs-source source connector has no converters out of the box.

The camel-azure-eventhubs-source source connector has no transforms out of the box.

The camel-azure-eventhubs-source source connector has no aggregation strategies out of the box.