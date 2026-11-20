# ![azure cosmosdb source](_images/kamelets/azure-cosmosdb-source.svg) Azure CosmosDB Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the items created or changed in a container of Azure Cosmos DB, through its change feed, as a JSON array per batch.

Use it to react to new or updated documents, for example to copy them to a search index, a cache or Kafka. To create items, use `azure-cosmosdb-sink`.

Output: the body is a JSON array of the items of one batch, as JSON text in bytes, each item with the fields that Cosmos DB adds, such as `_etag`. The `Content-Type` header is `application/json`.

Good to know: it reads only the changes made after it first starts, unless `startFromBeginning` is true, and it does not see deleted items. It keeps its position in a lease container, `camel-lease` in the database `databaseName` unless set otherwise, which must exist unless `createLeaseContainerIfNotExists` is true. Two integrations that read the same container with the same lease container share one position, and each change goes to only one of them, unless each has its own `leasePrefix`. It checks for new changes every 5 seconds unless `feedPollDelay` is set. Set `hostName` so that after a crash, the integration continues at once instead of after up to a minute.

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
| **feedPollDelay** | Feed Poll Delay | How long to wait before checking again for new changes, when there were none, in milliseconds. A smaller value receives changes sooner, but makes more requests to Cosmos DB, which use request units. When not set, 5000 (5 seconds). | integer |  | 1000 |
| **hostName** | Host Name | A name for this running copy of the integration, which the source writes into the lease container to mark the leases it holds. When it is not set, the source takes a new random name at each start, so after a crash it cannot take back the leases of its previous run until they expire, and receives no changes for up to a minute. With a name that stays the same across restarts, it continues at once. Give each copy that runs at the same time its own name. | string |  | orders-sync-1 |
| **leaseContainerName** | Lease Container Name | The name of the container where the source keeps its leases, which record how far it has read the change feed. When it is not set, `camel-lease`. | string |  | camel-lease |
| **leaseDatabaseName** | Lease Database Name | The name of the database of the lease container. When it is not set, the lease container is in `databaseName`. | string |  | shop |
| **leasePrefix** | Lease Prefix | A prefix for the names of the leases of this source in the lease container, such as `search-`. Give each integration that reads the same container its own prefix, so that they can share a lease container and each receives every change. Changing the prefix of a source starts it again without a saved position. | string |  | search- |
| **maxItemCount** | Max Items Per Batch | The largest number of items in one message, the JSON array of a batch. When not set, 100. | integer |  | 10 |
| **startFromBeginning** | Start From Beginning | If true, the first start reads all the items of the container, from the oldest change, instead of only the changes made after it starts. Used only when the lease container holds no position yet for this source; afterwards the source continues from its saved position. | boolean |  |  |

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

### Reading the change feed

The Kamelet keeps its position in the lease container. These options change how it reads:

-   `startFromBeginning`: if true, the first start reads all the items of the container. Once a position is saved, the source continues from it.
    
-   `maxItemCount`: the largest number of items in one message, 100 by default.
    
-   `feedPollDelay`: how long to wait before checking again for new changes, in milliseconds, 5000 by default. A smaller value receives changes sooner, with more requests to Cosmos DB.
    
-   `leasePrefix`: two integrations that read the same container with the same lease container share one position, and each change goes to only one of them. Give each integration its own `leasePrefix` to have each receive every change.
    
-   `hostName`: the name the source marks its leases with. Without it, the source takes a new random name at each start, and after a crash waits up to a minute for the leases of its previous run to expire. With a name that stays the same, it continues at once. Give each copy that runs at the same time its own name.
    

```yaml
- route:
    from:
      uri: "kamelet:azure-cosmosdb-source"
      parameters:
        databaseEndpoint: "https://my-account.documents.azure.com:443/"
        accountKey: "{{cosmos.key}}"
        databaseName: "shop"
        containerName: "orders"
        createLeaseContainerIfNotExists: true
        startFromBeginning: true
        maxItemCount: 10
        feedPollDelay: 1000
        leasePrefix: "search-"
        hostName: "orders-search-1"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-cosmosdb-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-cosmosdb-source.kamelet.yaml)