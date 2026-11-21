# ![azure storage blob event based source](_images/kamelets/azure-storage-blob-event-based-source.svg) Azure Storage Blob Event-based Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives the Event Grid events of an Azure Storage account from a Service Bus queue or topic, and can read the content of each new blob in a container.

Use it to react quickly to new blobs, such as uploaded files, without reading the container over and over. It needs an Event Grid subscription on the storage account that sends the events, in the Event Grid schema, to a Service Bus queue, or to a topic so that other applications can receive the same events from subscriptions of their own. To read the container on a timer instead, use `azure-storage-blob-source`.

Output: when `getBlob` is false, the default, the body is the Event Grid event as JSON (an Azure `BinaryData`, which converts to text or bytes). When `getBlob` is true, the body of a `Microsoft.Storage.BlobCreated` event for a blob of `containerName` is the content of that blob, as a stream of bytes, with the `CamelAzureStorageBlob…​` headers of the blob, such as `CamelAzureStorageBlobContentType`, but no header with its name; the other events are passed on as parsed JSON (a Jackson JSON node). In both cases, the `azure-storage-blob-event-id` header identifies the event.

Good to know: with the default `serviceBusReceiveMode` of `RECEIVE_AND_DELETE`, an event is removed from the queue, or from the subscription of the topic, as soon as it is received, so an event whose processing fails is lost. With `getBlob`, only blobs at the top of the container can be read: an event for a blob in a virtual folder, such as `in/a.txt`, fails. Events are processed one at a time, in order, unless `maxConcurrentCalls` is set. Azure delivers storage events at least once, so the same event can come twice; `azure-storage-blob-event-id` is the same in both. To process each event once, put the steps after the Kamelet in an `idempotentConsumer` step on `${header[azure-storage-blob-event-id]}`. A `MemoryIdempotentRepository` remembers the events of one process, until it restarts; with more than one replica, use a shared repository, such as the ones of `camel-infinispan` or `camel-sql`.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-blob-event-based-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The name of the storage account, as shown in the Azure portal under Storage accounts. It is the first part of the address of the account, `[https://<accountName>.blob.core.windows.net](https://\<accountName\>.blob.core.windows.net)`. | string |  | mystorageaccount |
| **connectionString** | Connection String | **Required** The connection string of the Service Bus namespace, from the Azure portal: the namespace, then Settings, Shared access policies, a policy, Primary Connection String. It starts with `Endpoint=sb://`. | string |  |  |
| **containerName** | Container Name | **Required** The name of the container whose new blobs are read when `getBlob` is true. Events for other containers are passed on as they are. | string |  | uploads |
| **topicOrQueueName** | Queue or Topic Name | **Required** The name of the Service Bus queue, or of the topic when `serviceBusType` is `topic`, that the Event Grid subscription of the storage account sends its events to. | string |  | blob-events |
| **accessKey** | Access Key | An access key of the storage account, from the Azure portal: the storage account, then Security + networking, then Access keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |
| **clientId** | Client ID | The application (client) ID of an app registration (service principal) in Microsoft Entra ID that has access to the storage account, from the Overview page of the app registration in the Azure portal. Used with `clientSecret` and `tenantId` when `credentialType` is `AZURE_IDENTITY`. | string |  |  |
| **clientSecret** | Client Secret | A client secret of the app registration, from the Azure portal: the app registration, then Certificates & secrets. Used with `clientId` and `tenantId` when `credentialType` is `AZURE_IDENTITY`. | string |  |  |
| **credentialType** | Credential Type | How to log in to the storage account to read the new blobs. `SHARED_ACCOUNT_KEY`, the default, and `SHARED_KEY_CREDENTIAL` use `accessKey`. `AZURE_IDENTITY` uses `clientId`, `clientSecret` and `tenantId` when all three are set, and otherwise the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. Do not use `CLIENT_SECRET`: it does not use the three client options. Enum values: \* SHARED\_ACCOUNT\_KEY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_IDENTITY \* CLIENT\_SECRET | string | SHARED\_ACCOUNT\_KEY |  |
| **getBlob** | Get Blob | If true, the body of each event about a new blob in `containerName` is replaced by the content of that blob. If false, the body is the event. | boolean | false |  |
| **maxConcurrentCalls** | Max Concurrent Events | How many events are processed at the same time. When it is not set, one at a time, in order. With a higher number, events are processed in parallel and can finish out of order. | integer |  | 4 |
| **serviceBusReceiveMode** | Service Bus Receive Mode | `RECEIVE_AND_DELETE`, the default, removes each event from the queue as soon as it is received, so an event whose processing fails is lost. `PEEK_LOCK` removes it only once it has been processed, and gives it back to the queue when processing fails. Enum values: \* RECEIVE\_AND\_DELETE \* PEEK\_LOCK | string | RECEIVE\_AND\_DELETE |  |
| **serviceBusType** | Service Bus Type | `queue` reads the events from the queue `topicOrQueueName`. `topic` reads them from the subscription `subscriptionName` of the topic `topicOrQueueName`. When it is not set, it reads from a queue. Enum values: \* queue \* topic | string |  |  |
| **subscriptionName** | Subscription Name | The name of the subscription of the topic to read the events from. Required when `serviceBusType` is `topic`, without it the Kamelet does not start. Not used with a queue. | string |  |  |
| **tenantId** | Tenant ID | The directory (tenant) ID of the app registration, from its Overview page in the Azure portal. Used with `clientId` and `clientSecret` when `credentialType` is `AZURE_IDENTITY`. | string |  |  |

## Dependencies

At runtime, the `azure-storage-blob-event-based-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-servicebus
    
-   camel:azure-storage-blob
    
-   camel:kamelet
    
-   camel:jsonpath
    
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
      uri: "kamelet:azure-storage-blob-event-based-source"
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

## Azure Storage Blob Event Based Source Kamelet Description

### Authentication methods

For this Kamelet the Connection string is the basic method for authenticating to the Azure Servicebus Queue.

To use this Kamelet you’ll need to set up Events on your Azure Storage Blob account and select as an endpoint an Azure Servicebus Queue or Topic, with the Event Grid event schema.

For the Azure Storage Blob access, you can use these Azure authentication methods:

-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Plain Shared Account Key: `SHARED_ACCOUNT_KEY`
    
-   Shared Key Credential: `SHARED_KEY_CREDENTIAL`
    

To log in as an app registration (a service principal), set `credentialType` to `AZURE_IDENTITY` and provide `clientId`, `clientSecret`, and `tenantId`: when all three are set, they are used instead of the identity of the environment. `CLIENT_SECRET` does not use these three properties.

For more information, see the [Azure Identity documentation](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)

### Example: Read the Events from a Topic

When the events go to a Service Bus topic, so that other applications can receive them from subscriptions of their own, set **serviceBusType** to `topic`, **topicOrQueueName** to the name of the topic, and **subscriptionName** to the subscription this Kamelet reads from:

```yaml
- route:
    from:
      uri: "kamelet:azure-storage-blob-event-based-source"
      parameters:
        connectionString: "Endpoint=sb://my-namespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=..."
        serviceBusType: "topic"
        topicOrQueueName: "blob-events"
        subscriptionName: "invoice-processor"
        maxConcurrentCalls: 4
        accountName: "mystorageaccount"
        containerName: "invoices"
        accessKey: "..."
        getBlob: true
      steps:
        - to: "log:blob"
```

Without **subscriptionName** the Kamelet does not start. **maxConcurrentCalls** processes up to four events at the same time; when it is not set, events are processed one at a time, in order.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-event-based-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-event-based-source.kamelet.yaml)