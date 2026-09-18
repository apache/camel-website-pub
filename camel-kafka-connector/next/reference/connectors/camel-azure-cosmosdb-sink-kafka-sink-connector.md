# camel-azure-cosmosdb-sink-kafka-connector sink configuration

Connector Description: Send Data to an Azure CosmosDB instance

When using camel-azure-cosmosdb-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-cosmosdb-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurecosmosdbsink.CamelAzurecosmosdbsinkSinkConnector
```

The camel-azure-cosmosdb-sink sink connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-cosmosdb-sink.databaseName** | **Required** The Azure Cosmos database name. |  | HIGH |
| **camel.kamelet.azure-cosmosdb-sink.containerName** | **Required** The Azure Cosmos container name. |  | HIGH |
| **camel.kamelet.azure-cosmosdb-sink.accountKey** | The Azure Cosmos account Key. |  | MEDIUM |
| **camel.kamelet.azure-cosmosdb-sink.databaseEndpoint** | **Required** Sets the Azure Cosmos database endpoint the component will connect to. |  | HIGH |
| **camel.kamelet.azure-cosmosdb-sink.itemPartitionKey** | Represents a partition key value in the Azure Cosmos DB database service. A partition key identifies the partition where the item is stored in. |  | MEDIUM |
| **camel.kamelet.azure-cosmosdb-sink.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |

The camel-azure-cosmosdb-sink sink connector has no converters out of the box.

The camel-azure-cosmosdb-sink sink connector has no transforms out of the box.

The camel-azure-cosmosdb-sink sink connector has no aggregation strategies out of the box.