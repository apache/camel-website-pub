# ![azure eventhubs sink](_images/kamelets/azure-eventhubs-sink.svg) Azure Eventhubs Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as an event to an event hub in Azure Event Hubs, the Azure service for event streams.

Use it to publish events, such as clicks, sensor readings or changes, for stream processing or for other applications to read. To receive them, use `azure-eventhubs-source`.

Input: the body becomes the body of the event: text, bytes or a stream. A Map fails: turn it into JSON text first, for example with `json-serialize-action`. A List is sent as one event per element. The optional `partition-id` header (or `ce-partition-id`) is the partition to send to, such as `0`; without it, and without `partitionKey`, Event Hubs chooses one.

Output: the message is unchanged.

Good to know: log in with `sharedAccessName` and `sharedAccessKey`, with `connectionString`, or with `credentialType` `AZURE_IDENTITY`. Set `namespaceName` and `eventhubName` unless `connectionString` is set. The shared access policy needs the Send right. Headers that start with `CamelAzureEventHubs` are removed from the message first, so they cannot change what the Kamelet does. With `partitionKey` set, a message with a `partition-id` or `ce-partition-id` header fails.

## Configuration Options

The following table summarizes the configuration options available for the `azure-eventhubs-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionString** | Connection String | A connection string of a shared access policy, such as `Endpoint=sb://my-namespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=…​;EntityPath=orders`, from the Azure portal: the namespace or the event hub, then Settings, Shared access policies, the policy, Connection string. Use it instead of `namespaceName`, `eventhubName`, `sharedAccessName` and `sharedAccessKey`, which are then not used. It must end with `;EntityPath=` and the name of the event hub: the connection string of a policy of the event hub has it, and one of a policy of the namespace does not, so add it. Without it, the integration fails to start with the error `'eventHubName' cannot be an empty string`. Used when `credentialType` is `CONNECTION_STRING`, the default. | string |  |  |
| **credentialType** | Credential Type | How to log in to Event Hubs. `CONNECTION_STRING`, the default, uses `sharedAccessName` and `sharedAccessKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. Enum values: \* CONNECTION\_STRING \* AZURE\_IDENTITY | string | CONNECTION\_STRING |  |
| **eventhubName** | Event Hub Name | The name of the event hub in the namespace to send the events to. Required unless `connectionString` is set. | string |  | orders |
| **namespaceName** | Event Hubs Namespace | The name of the Event Hubs namespace, the first part of its address `<namespaceName>.servicebus.windows.net`. Required unless `connectionString` is set: with neither, the integration fails to start with the error `ConnectionString, ProducerAsyncClient or Namespace and EventHub name must be set`. | string |  | my-namespace |
| **partitionKey** | Partition Key | A partition key for all the events, such as `orders`. Event Hubs sends all the events with the same partition key to the same partition, which it chooses from the key, so they are read in the order they were sent. Use it instead of the `partition-id` header, as a message with both fails. When not set, each event goes to the partition in its `partition-id` header, or Event Hubs chooses one. | string |  | orders |
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

If you set neither the header nor `partitionKey`, Azure Event Hubs chooses the partition.

### Sending all events to the same partition

Event Hubs keeps the order of the events only within a partition. To read the events in the order they were sent, set `partitionKey`: Event Hubs sends all the events with the same partition key to the same partition, which it chooses from the key. Do not set the `partition-id` header as well: a message with both fails with the error `Both partitionKey and partitionId are set`.

### Connecting with a connection string

Instead of `namespaceName`, `eventhubName`, `sharedAccessName` and `sharedAccessKey`, you can set `connectionString`. It must end with `;EntityPath=` and the name of the event hub, which the connection string of a policy of the namespace does not have: add it.

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
            uri: "kamelet:azure-eventhubs-sink"
            parameters:
              connectionString: "Endpoint=sb://my-namespace.servicebus.windows.net/;SharedAccessKeyName=send-policy;SharedAccessKey=...;EntityPath=orders"
              partitionKey: "orders"
```

The connection string holds the key, so keep it in a secret, like `sharedAccessKey`.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-eventhubs-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-eventhubs-sink.kamelet.yaml)