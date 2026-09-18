# ![azure cosmosdb source](_images/kamelets/azure-cosmosdb-source.svg) Azure CosmosDB Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume Changes from a CosmosDB instance.

## Configuration Options

The following table summarizes the configuration options available for the `azure-cosmosdb-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **containerName** | Container Name | **Required** The Azure Cosmos container name. | string |  |  |
| **databaseEndpoint** | Database Endpoint | **Required** Sets the Azure Cosmos database endpoint the component will connect to. | string |  |  |
| **databaseName** | Database Name | **Required** The Azure Cosmos database name. | string |  |  |
| **accountKey** | Account Key | The Azure Cosmos account Key. | string |  |  |
| **createLeaseContainerIfNotExists** | Autocreate Lease Container | Sets if the component should create Cosmos lease container for the consumer automatically in case it doesn’t exist in Cosmos database. | boolean | false |  |
| **createLeaseDatabaseIfNotExists** | Autocreate Lease Database | Sets if the component should create Cosmos lease database for the consumer automatically in case it doesn’t exist in Cosmos account. | boolean | false |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY | string | SHARED\_ACCOUNT\_KEY |  |
| **leaseContainerName** | Lease Container Name | Sets the lease database where the `leaseContainerName` is stored. | string |  |  |
| **leaseDatabaseName** | Lease Database Name | Sets the lease container which acts as a state storage and coordinates processing the change feed across multiple workers. | string |  |  |

## Dependencies

At runtime, the `azure-cosmosdb-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-cosmosdb
    
-   camel:kamelet
    
-   camel:jackson
    

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
      uri: "kamelet:azure-cosmosdb-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure CosmosDB Source Kamelet Description

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-cosmosdb-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-cosmosdb-source.kamelet.yaml)