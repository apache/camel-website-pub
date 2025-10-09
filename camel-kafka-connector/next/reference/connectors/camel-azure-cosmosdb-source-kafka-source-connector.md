# camel-azure-cosmosdb-source-kafka-connector source configuration

Connector Description: Consume Changes from a CosmosDB instance.

When using camel-azure-cosmosdb-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-cosmosdb-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurecosmosdbsource.CamelAzurecosmosdbsourceSourceConnector
```

The camel-azure-cosmosdb-source source connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-cosmosdb-source.databaseName** | **Required** The Azure Cosmos database name. |  | HIGH |
| **camel.kamelet.azure-cosmosdb-source.containerName** | **Required** The Azure Cosmos container name. |  | HIGH |
| **camel.kamelet.azure-cosmosdb-source.accountKey** | The Azure Cosmos account Key. |  | MEDIUM |
| **camel.kamelet.azure-cosmosdb-source.leaseDatabaseName** | Sets the lease container which acts as a state storage and coordinates processing the change feed across multiple workers. |  | MEDIUM |
| **camel.kamelet.azure-cosmosdb-source.leaseContainerName** | Sets the lease database where the `leaseContainerName` is stored. |  | MEDIUM |
| **camel.kamelet.azure-cosmosdb-source.createLeaseDatabaseIfNotExists** | Sets if the component should create Cosmos lease database for the consumer automatically in case it doesn’t exist in Cosmos account. | false | MEDIUM |
| **camel.kamelet.azure-cosmosdb-source.createLeaseContainerIfNotExists** | Sets if the component should create Cosmos lease container for the consumer automatically in case it doesn’t exist in Cosmos database. | false | MEDIUM |
| **camel.kamelet.azure-cosmosdb-source.databaseEndpoint** | **Required** Sets the Azure Cosmos database endpoint the component will connect to. |  | HIGH |
| **camel.kamelet.azure-cosmosdb-source.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |

The camel-azure-cosmosdb-source source connector has no converters out of the box.

The camel-azure-cosmosdb-source source connector has no transforms out of the box.

The camel-azure-cosmosdb-source source connector has no aggregation strategies out of the box.