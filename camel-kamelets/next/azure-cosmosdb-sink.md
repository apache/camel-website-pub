# ![azure cosmosdb sink](_images/kamelets/azure-cosmosdb-sink.svg) Azure CosmosDB Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Creates or replaces an item (a JSON document) in a container of Azure Cosmos DB for each message, from the JSON object in the body.

Use it to store orders, events or profiles as JSON documents in Cosmos DB. To receive the changes made to a container, use `azure-cosmosdb-source`.

Input: the body is one item as JSON text: a JSON object with an `id` field, such as `{"id": "1001", "region": "EU"}`. A Map fails: turn it into JSON text first, for example with `json-serialize-action`. The partition key value of the item comes from the `itemPartitionKey` option or, when the option is not set, from the `itemPartitionKey` header (or `ce-itemPartitionKey`) of each message.

Output: the body afterwards is the item as it was created, as a Map, with the fields that Cosmos DB adds.

Good to know: a message without a partition key value fails. With `operation` `createItem`, the default, an item whose `id` already exists in the same partition fails; with `upsertItem`, it replaces the existing item. The database and the container must exist, unless `createDatabaseIfNotExists` and `createContainerIfNotExists` are true; a new container needs `containerPartitionKeyPath`. Headers that start with `CamelAzureCosmosDb` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `azure-cosmosdb-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **containerName** | Container Name | **Required** The name of the container in the database to create the items in. | string |  | orders |
| **databaseEndpoint** | Database Endpoint | **Required** The address of the Azure Cosmos DB account, shown as URI on the Overview page of the account in the Azure portal. | string |  | https://my-account.documents.azure.com:443/ |
| **databaseName** | Database Name | **Required** The name of the database in the Azure Cosmos DB account. | string |  | shop |
| **accountKey** | Account Key | The primary or secondary key of the Azure Cosmos DB account, from the Azure portal: the account, then Settings, Keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |
| **containerPartitionKeyPath** | Container Partition Key Path | The partition key of the container to create when `createContainerIfNotExists` is true, as the path of a field of the items, such as `/region`. Not used for a container that exists. | string |  | /region |
| **createContainerIfNotExists** | Autocreate Container | If true, the container `containerName` is created when it does not exist, with `containerPartitionKeyPath` as its partition key; then `containerPartitionKeyPath` is required. When not set, or false, a missing container fails each message. | boolean |  |  |
| **createDatabaseIfNotExists** | Autocreate Database | If true, the database `databaseName` is created when it does not exist. When not set, or false, a missing database fails each message. | boolean |  |  |
| **credentialType** | Credential Type | How to log in to Azure Cosmos DB. `SHARED_ACCOUNT_KEY`, the default, uses `accountKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY | string | SHARED\_ACCOUNT\_KEY |  |
| **itemPartitionKey** | Item Partition Key | The value of the partition key of the items, the same for every item, such as `EU` when the partition key of the container is `/region`. When it is not set, the value comes from the `itemPartitionKey` header of each message. | string |  | EU |
| **operation** | Operation | What to do with each item. `createItem` creates the item, and fails when an item with the same `id` already exists in the same partition. `upsertItem` creates the item, or replaces the existing item with the same `id` in the same partition with it, as a whole. Enum values: \* createItem \* upsertItem | string | createItem |  |

## Dependencies

At runtime, the `azure-cosmosdb-sink` Kamelet relies upon the presence of the following dependencies:

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

If you do not set the property in the header, you’ll need to use the static property `itemPartitionKey`. A message without a partition key fails.

### Creating or replacing items

With `operation` `createItem`, the default, an item whose `id` already exists in the same partition fails with the error `The document already exists`. With `upsertItem`, the item is created, or replaces the existing item with the same `id` and partition key value, as a whole.

### Creating the database and the container

The database and the container must exist, unless `createDatabaseIfNotExists` and `createContainerIfNotExists` are true. A new container takes `containerPartitionKeyPath` as its partition key, such as `/region`; without it, each message fails with the error `containerPartitionKeyPath cannot be empty!`. For a container that exists, `containerPartitionKeyPath` is not used.

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "orders"
        bootstrapServers: "kafka.example.com:9092"
        saslAuthType: "NONE"
      steps:
        - to:
            uri: "kamelet:azure-cosmosdb-sink"
            parameters:
              databaseEndpoint: "https://my-account.documents.azure.com:443/"
              accountKey: "{{cosmos.key}}"
              databaseName: "shop"
              containerName: "orders"
              itemPartitionKey: "EU"
              operation: "upsertItem"
              createDatabaseIfNotExists: true
              createContainerIfNotExists: true
              containerPartitionKeyPath: "/region"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-cosmosdb-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-cosmosdb-sink.kamelet.yaml)