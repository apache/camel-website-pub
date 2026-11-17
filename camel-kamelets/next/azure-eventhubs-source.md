# ![azure eventhubs source](_images/kamelets/azure-eventhubs-source.svg) Azure Eventhubs Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the events of an event hub in Azure Event Hubs, one message per event, and saves how far it has read in an Azure Storage blob container.

Use it to process event streams, such as telemetry or changes, that other applications send to Event Hubs. To send events, use `azure-eventhubs-sink`.

Output: the body is the body of the event, as bytes. The headers give its partition (`CamelAzureEventHubsPartitionId`), offset, sequence number and the time it was enqueued, and `CamelAzureEventHubsMetadata` holds the custom properties of the event.

Good to know: when no position has been saved yet, it starts with the events that arrive after it starts, not the older ones. It reads as the `$Default` consumer group. It saves its position (a checkpoint) in `blobContainerName` every 500 events or every 5 seconds, so after a restart some events can be read again.

## Configuration Options

The following table summarizes the configuration options available for the `azure-eventhubs-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **blobAccessKey** | Checkpoint Access Key | **Required** An access key of the storage account `blobAccountName`, from the Azure portal: the storage account, then Security + networking, then Access keys. | string |  |  |
| **blobAccountName** | Checkpoint Storage Account | **Required** The name of the storage account where the source saves how far it has read each partition (its checkpoints). | string |  | mystorageaccount |
| **blobContainerName** | Checkpoint Container Name | **Required** The name of the blob container, in `blobAccountName`, for the checkpoints. | string |  | eventhub-checkpoints |
| **eventhubName** | Event Hub Name | **Required** The name of the event hub in the namespace to receive the events from. | string |  | orders |
| **namespaceName** | Event Hubs Namespace | **Required** The name of the Event Hubs namespace, the first part of its address `<namespaceName>.servicebus.windows.net`. | string |  | my-namespace |
| **credentialType** | Credential Type | How to log in to Event Hubs. `CONNECTION_STRING`, the default, uses `sharedAccessName` and `sharedAccessKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. Enum values: \* CONNECTION\_STRING \* AZURE\_IDENTITY | string | CONNECTION\_STRING |  |
| **sharedAccessKey** | Shared Access Key | The primary or secondary key of the shared access policy named in `sharedAccessName`. | string |  |  |
| **sharedAccessName** | Shared Access Name | The name of a shared access policy of the namespace or of the event hub, such as `RootManageSharedAccessKey`, from the Azure portal: the namespace or the event hub, then Settings, Shared access policies. Used when `credentialType` is `CONNECTION_STRING`, the default. | string |  | RootManageSharedAccessKey |

## Dependencies

At runtime, the `azure-eventhubs-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-eventhubs
    
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-eventhubs-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-eventhubs-source.kamelet.yaml)