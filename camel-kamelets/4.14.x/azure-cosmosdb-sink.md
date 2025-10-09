# ![azure cosmosdb sink](_images/kamelets/azure-cosmosdb-sink.svg) Azure CosmosDB Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send Data to an Azure CosmosDB instance

## Configuration Options

The following table summarizes the configuration options available for the `azure-cosmosdb-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **containerName** | Container Name | **Required** The Azure Cosmos container name. | string |  |  |
| **databaseEndpoint** | Database Endpoint | **Required** Sets the Azure Cosmos database endpoint the component will connect to. | string |  |  |
| **databaseName** | Database Name | **Required** The Azure Cosmos database name. | string |  |  |
| **accountKey** | Account Key | The Azure Cosmos account Key. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY | string | SHARED\_ACCOUNT\_KEY |  |
| **itemPartitionKey** | Item Partition Key | Represents a partition key value in the Azure Cosmos DB database service. A partition key identifies the partition where the item is stored in. | string |  |  |

## Dependencies

At runtime, the `azure-cosmosdb-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-cosmosdb
    
-   camel:kamelet
    
-   camel:jackson
    
-   camel:core
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:azure-cosmosdb-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure CosmosDB Sink Kamelet Description

### Authentication methods

In this Kamelet, you can use these Azure authentication methods:

-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Plain Shared Account Key: `SHARED_ACCOUNT_KEY`
    

The order of evaluation for `AZURE_IDENTITY` is the following:

-   Enviroment
    
-   Workload Identity
    
-   Managed Identity
    
-   Azure Developer CLI
    
-   IntelliJ
    
-   Azure CLI
    
-   Azure Powershell
    

For more information, see the [Azure Identity documentation](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)

### Optional Headers

In the headers, you can optionally set the `itemPartitionKey` / `ce-itemPartitionKey` property to specify the partition key for a specific item.

If you do not set the property in the header, you’ll need to use the static property itemPartitonKey.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-cosmosdb-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-cosmosdb-sink.kamelet.yaml)