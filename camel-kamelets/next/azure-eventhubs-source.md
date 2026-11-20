# ![azure eventhubs source](_images/kamelets/azure-eventhubs-source.svg) Azure Eventhubs Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the events of an event hub in Azure Event Hubs, one message per event, and saves how far it has read in an Azure Storage blob container.

Use it to process event streams, such as telemetry or changes, that other applications send to Event Hubs. To send events, use `azure-eventhubs-sink`.

Output: the body is the body of the event, as bytes, and the `Content-Type` header is `application/octet-stream`. The headers give its partition (`CamelAzureEventHubsPartitionId`), offset, sequence number and the time it was enqueued, and `CamelAzureEventHubsMetadata` holds the custom properties of the event.

Good to know: log in with `sharedAccessName` and `sharedAccessKey`, with `connectionString`, or with `credentialType` `AZURE_IDENTITY`. Set `namespaceName` and `eventhubName` unless `connectionString` is set. When no position has been saved yet, it starts with the events that arrive after it starts, not the older ones. It reads as the `$Default` consumer group, or as the one in `consumerGroupName`, and each consumer group has its own saved position. For each partition, it saves its position (a checkpoint) in `blobContainerName` after `checkpointBatchSize` events (500 when not set), or `checkpointBatchTimeout` milliseconds (5000 when not set) after the first event since the last checkpoint, whichever comes first. The events read after the last checkpoint are read again after a restart.

## Configuration Options

The following table summarizes the configuration options available for the `azure-eventhubs-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **blobAccessKey** | Checkpoint Access Key | **Required** An access key of the storage account `blobAccountName`, from the Azure portal: the storage account, then Security + networking, then Access keys. | string |  |  |
| **blobAccountName** | Checkpoint Storage Account | **Required** The name of the storage account where the source saves how far it has read each partition (its checkpoints). | string |  | mystorageaccount |
| **blobContainerName** | Checkpoint Container Name | **Required** The name of the blob container, in `blobAccountName`, for the checkpoints. | string |  | eventhub-checkpoints |
| **checkpointBatchSize** | Checkpoint Batch Size | After how many events of a partition the source saves its position (a checkpoint) for that partition. A smaller number reads fewer events again after a restart, but writes to the blob container more often. When not set, 500. | integer |  | 100 |
| **checkpointBatchTimeout** | Checkpoint Batch Timeout | How long after the first event since the last checkpoint of a partition the source saves its position for that partition, when `checkpointBatchSize` events have not arrived by then, in milliseconds. When not set, 5000 (5 seconds). | integer |  | 1000 |
| **connectionString** | Connection String | A connection string of a shared access policy, such as `Endpoint=sb://my-namespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=…​;EntityPath=orders`, from the Azure portal: the namespace or the event hub, then Settings, Shared access policies, the policy, Connection string. Use it instead of `namespaceName`, `eventhubName`, `sharedAccessName` and `sharedAccessKey`, which are then not used. It must end with `;EntityPath=` and the name of the event hub: the connection string of a policy of the event hub has it, and one of a policy of the namespace does not, so add it. Without it, the integration fails to start with the error `'eventHubName' cannot be an empty string`. Used when `credentialType` is `CONNECTION_STRING`, the default. | string |  |  |
| **consumerGroupName** | Consumer Group | The consumer group to read as. Each consumer group receives every event of the event hub and has its own saved position, so two integrations that read the same event hub with different consumer groups both receive every event. The consumer group must exist: create it in the Azure portal, under the event hub, then Entities, Consumer groups. With a consumer group that does not exist, the integration starts but receives nothing, and logs a warning that the messaging entity could not be found. When not set, it reads as `$Default`, the consumer group every event hub has. | string |  | billing |
| **credentialType** | Credential Type | How to log in to Event Hubs. `CONNECTION_STRING`, the default, uses `sharedAccessName` and `sharedAccessKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. Enum values: \* CONNECTION\_STRING \* AZURE\_IDENTITY | string | CONNECTION\_STRING |  |
| **eventhubName** | Event Hub Name | The name of the event hub in the namespace to receive the events from. Required unless `connectionString` is set. | string |  | orders |
| **namespaceName** | Event Hubs Namespace | The name of the Event Hubs namespace, the first part of its address `<namespaceName>.servicebus.windows.net`. Required unless `connectionString` is set: with neither, the integration fails to start with the error `ConnectionString, ProducerAsyncClient or Namespace and EventHub name must be set`. | string |  | my-namespace |
| **sharedAccessKey** | Shared Access Key | The primary or secondary key of the shared access policy named in `sharedAccessName`. | string |  |  |
| **sharedAccessName** | Shared Access Name | The name of a shared access policy of the namespace or of the event hub, such as `RootManageSharedAccessKey`, from the Azure portal: the namespace or the event hub, then Settings, Shared access policies. Used when `credentialType` is `CONNECTION_STRING`, the default. | string |  | RootManageSharedAccessKey |

## Dependencies

At runtime, the `azure-eventhubs-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-eventhubs
    
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
      uri: "kamelet:azure-eventhubs-source"
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

## Azure Event Hubs Source Kamelet Description

### Authentication methods

In this Kamelet, you can use these Azure authentication methods:

-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Connection string: `CONNECTION_STRING`
    

The order of evaluation for `AZURE_IDENTITY` is the following:

-   Enviroment
    
-   Workload Identity
    
-   Managed Identity
    
-   Azure Developer CLI
    
-   IntelliJ
    
-   Azure CLI
    
-   Azure Powershell
    

For more information, see the [Azure Identity documentation](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)

### Reading with your own consumer group

By default the Kamelet reads as the `$Default` consumer group. To read the same event hub from several integrations, each receiving every event, create a consumer group for each of them in the Azure portal (the event hub, then Entities, Consumer groups) and set it in `consumerGroupName`:

```yaml
- route:
    from:
      uri: "kamelet:azure-eventhubs-source"
      parameters:
        namespaceName: "my-namespace"
        eventhubName: "orders"
        sharedAccessName: "RootManageSharedAccessKey"
        sharedAccessKey: "{{eventhubs.key}}"
        blobAccountName: "mystorageaccount"
        blobAccessKey: "{{storage.key}}"
        blobContainerName: "eventhub-checkpoints"
        consumerGroupName: "billing"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Each consumer group has its own saved position in `blobContainerName`, so the integrations can share the container. A consumer group without a saved position starts with the events that arrive after the integration starts. With a consumer group that does not exist, the integration starts but receives nothing, and logs a warning that the messaging entity could not be found.

### Connecting with a connection string

Instead of `namespaceName`, `eventhubName`, `sharedAccessName` and `sharedAccessKey`, you can set `connectionString`, as the Azure portal shows it under the namespace or the event hub, then Settings, Shared access policies, the policy. The connection string must end with `;EntityPath=` and the name of the event hub. The connection string of a policy of the event hub has it; for one of a policy of the namespace, add it. Without it, the integration fails to start with the error `'eventHubName' cannot be an empty string`.

```yaml
- route:
    from:
      uri: "kamelet:azure-eventhubs-source"
      parameters:
        connectionString: "Endpoint=sb://my-namespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=...;EntityPath=orders"
        blobAccountName: "mystorageaccount"
        blobAccessKey: "{{storage.key}}"
        blobContainerName: "eventhub-checkpoints"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The connection string holds the key, so keep it in a secret, like `sharedAccessKey`.

### How often the position is saved

For each partition, the Kamelet saves how far it has read (a checkpoint) in `blobContainerName` after `checkpointBatchSize` events, 500 by default, or `checkpointBatchTimeout` milliseconds, 5000 by default, after the first event since the last checkpoint, whichever comes first. After a restart, it reads again the events that came after the last checkpoint. To read fewer events again, save the position more often, at the cost of more writes to the storage account:

```yaml
        checkpointBatchSize: 100
        checkpointBatchTimeout: 1000
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-eventhubs-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-eventhubs-source.kamelet.yaml)