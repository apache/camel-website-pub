# ![azure cosmosdb sink](_images/kamelets/azure-cosmosdb-sink.svg) Azure CosmosDB Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Creates an item (a JSON document) in a container of Azure Cosmos DB for each message, from the JSON object in the body.

Use it to store orders, events or profiles as JSON documents in Cosmos DB. To receive the changes made to a container, use `azure-cosmosdb-source`.

Input: the body is one item as JSON text: a JSON object with an `id` field, such as `{"id": "1001", "region": "EU"}`. A Map fails: turn it into JSON text first, for example with `json-serialize-action`. The partition key value of the item comes from the `itemPartitionKey` option or, when the option is not set, from the `itemPartitionKey` header (or `ce-itemPartitionKey`) of each message.

Output: the body afterwards is the item as it was created, as a Map, with the fields that Cosmos DB adds.

Good to know: a message without a partition key value fails, and so does an item whose `id` already exists in the same partition: the sink creates items and never replaces them.

## Configuration Options

The following table summarizes the configuration options available for the `azure-cosmosdb-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **containerName** | Container Name | **Required** The name of the container in the database to create the items in. | string |  | orders |
| **databaseEndpoint** | Database Endpoint | **Required** The address of the Azure Cosmos DB account, shown as URI on the Overview page of the account in the Azure portal. | string |  | https://my-account.documents.azure.com:443/ |
| **databaseName** | Database Name | **Required** The name of the database in the Azure Cosmos DB account. | string |  | shop |
| **accountKey** | Account Key | The primary or secondary key of the Azure Cosmos DB account, from the Azure portal: the account, then Settings, Keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |
| **credentialType** | Credential Type | How to log in to Azure Cosmos DB. `SHARED_ACCOUNT_KEY`, the default, uses `accountKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY | string | SHARED\_ACCOUNT\_KEY |  |
| **itemPartitionKey** | Item Partition Key | The value of the partition key of the items, the same for every item, such as `EU` when the partition key of the container is `/region`. When it is not set, the value comes from the `itemPartitionKey` header of each message. | string |  | EU |

## Dependencies

At runtime, the `azure-cosmosdb-sink` Kamelet relies upon the presence of the following dependencies:

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-cosmosdb-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-cosmosdb-sink.kamelet.yaml)