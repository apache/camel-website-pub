# ![azure eventhubs sink](_images/kamelets/azure-eventhubs-sink.svg) Azure Eventhubs Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as an event to an event hub in Azure Event Hubs, the Azure service for event streams.

Use it to publish events, such as clicks, sensor readings or changes, for stream processing or for other applications to read. To receive them, use `azure-eventhubs-source`.

Input: the body becomes the body of the event: text, bytes or a stream. A Map fails: turn it into JSON text first, for example with `json-serialize-action`. A List is sent as one event per element. The optional `partition-id` header (or `ce-partition-id`) is the partition to send to, such as `0`; without it, Event Hubs chooses one.

Output: the message is unchanged.

Good to know: the shared access policy needs the Send right.

## Configuration Options

The following table summarizes the configuration options available for the `azure-eventhubs-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **eventhubName** | Event Hub Name | **Required** The name of the event hub in the namespace to send the events to. | string |  | orders |
| **namespaceName** | Event Hubs Namespace | **Required** The name of the Event Hubs namespace, the first part of its address `<namespaceName>.servicebus.windows.net`. | string |  | my-namespace |
| **credentialType** | Credential Type | How to log in to Event Hubs. `CONNECTION_STRING`, the default, uses `sharedAccessName` and `sharedAccessKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. Enum values: \* CONNECTION\_STRING \* AZURE\_IDENTITY | string | CONNECTION\_STRING |  |
| **sharedAccessKey** | Shared Access Key | The primary or secondary key of the shared access policy named in `sharedAccessName`. | string |  |  |
| **sharedAccessName** | Shared Access Name | The name of a shared access policy of the namespace or of the event hub, such as `RootManageSharedAccessKey`, from the Azure portal: the namespace or the event hub, then Settings, Shared access policies. Used when `credentialType` is `CONNECTION_STRING`, the default. | string |  | RootManageSharedAccessKey |

## Dependencies

At runtime, the `azure-eventhubs-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-eventhubs
    
-   camel:kamelet
    

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
            uri: "kamelet:azure-eventhubs-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Event Hubs Sink Kamelet Description

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

### Optional Headers

In the headers, you can optionally set the `partition-id` / `ce-partition-id` property to specify the partition id for a specific item.

If you do not set the property in the header, Azure Event Hubs will do that for you.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-eventhubs-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-eventhubs-sink.kamelet.yaml)