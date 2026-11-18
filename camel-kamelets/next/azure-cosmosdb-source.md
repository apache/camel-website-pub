# ![azure cosmosdb source](_images/kamelets/azure-cosmosdb-source.svg) Azure CosmosDB Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the items created or changed in a container of Azure Cosmos DB, through its change feed, as a JSON array per batch.

Use it to react to new or updated documents, for example to copy them to a search index, a cache or Kafka. To create items, use `azure-cosmosdb-sink`.

Output: the body is a JSON array of the items of one batch, as bytes, each item with the fields that Cosmos DB adds, such as `_etag`.

Good to know: it reads only the changes made after it first starts, and it does not see deleted items. It keeps its position in a lease container, `camel-lease` in the database `databaseName` unless set otherwise, which must exist unless `createLeaseContainerIfNotExists` is true.

## Configuration Options

The following table summarizes the configuration options available for the `azure-cosmosdb-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **containerName** | Container Name | **Required** The name of the container in the database to receive the changes of. | string |  | orders |
| **databaseEndpoint** | Database Endpoint | **Required** The address of the Azure Cosmos DB account, shown as URI on the Overview page of the account in the Azure portal. | string |  | https://my-account.documents.azure.com:443/ |
| **databaseName** | Database Name | **Required** The name of the database in the Azure Cosmos DB account. | string |  | shop |
| **accountKey** | Account Key | The primary or secondary key of the Azure Cosmos DB account, from the Azure portal: the account, then Settings, Keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |
| **createLeaseContainerIfNotExists** | Autocreate Lease Container | If true, the lease container is created when it does not exist. If false, a missing lease container stops the source from starting. | boolean | false |  |
| **createLeaseDatabaseIfNotExists** | Autocreate Lease Database | If true, the lease database is created when it does not exist. If false, a missing lease database stops the source from starting. | boolean | false |  |
| **credentialType** | Credential Type | How to log in to Azure Cosmos DB. `SHARED_ACCOUNT_KEY`, the default, uses `accountKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY | string | SHARED\_ACCOUNT\_KEY |  |
| **leaseContainerName** | Lease Container Name | The name of the container where the source keeps its leases, which record how far it has read the change feed. When it is not set, `camel-lease`. | string |  | camel-lease |
| **leaseDatabaseName** | Lease Database Name | The name of the database of the lease container. When it is not set, the lease container is in `databaseName`. | string |  | shop |

## Dependencies

At runtime, the `azure-cosmosdb-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-cosmosdb
    
-   camel:kamelet
    
-   camel:jackson3
    

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