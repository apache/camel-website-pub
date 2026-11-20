# ![azure storage queue source](_images/kamelets/azure-storage-queue-source.svg) Azure Storage Queue Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the messages of a queue in Azure Queue Storage, one message each, and deletes each message from the queue once it has been processed.

Use it to process work that other applications put in a storage queue, such as orders or jobs. For Service Bus queues and topics, use `azure-servicebus-source`.

Output: the body is the text of the queue message, as text, and the `Content-Type` header is `text/plain`. The headers give its ID (`CamelAzureStorageQueueMessageId`), the times it was inserted and expires, its pop receipt, and how many times it has been received (`CamelAzureStorageQueueDequeueCount`).

Good to know: a received message is hidden from other readers while it is processed. When the processing fails, it stays in the queue and is received again once that time is over, 30 seconds by default (`visibilityTimeout`), with a higher dequeue count. The queue is checked for new messages every 500 milliseconds, unless `delay` says otherwise.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-queue-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** An access key of the storage account, from the Azure portal: the storage account, then Security + networking, then Access keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |
| **accountName** | Account Name | **Required** The name of the storage account, as shown in the Azure portal under Storage accounts. It is the first part of the address of the account, `[https://<accountName>.queue.core.windows.net](https://\<accountName\>.queue.core.windows.net)`. | string |  | mystorageaccount |
| **queueName** | Queue Name | **Required** The name of the queue in the storage account to receive the messages from. | string |  | orders |
| **credentialType** | Credential Type | How to log in to the storage account. `SHARED_ACCOUNT_KEY`, the default, and `SHARED_KEY_CREDENTIAL` use `accessKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login; `accessKey` must still be given, but is not used. Enum values: \* SHARED\_ACCOUNT\_KEY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_IDENTITY | string | SHARED\_ACCOUNT\_KEY |  |
| **delay** | Delay | How long to wait between two checks of the queue for new messages, in milliseconds. When it is not set, 500. | integer |  | 5000 |
| **maxMessages** | Maximum Messages | The most messages to receive at each poll, from 1 to 32. When the queue holds fewer, all of them are received. | integer | 1 |  |
| **visibilityTimeout** | Visibility Timeout | How long a received message stays hidden from other readers of the queue, as an ISO-8601 duration such as `PT5M` (five minutes), from 1 second to 7 days. Once processed, the message is deleted. When the processing fails, the message is received again after this time. Set it longer than the processing of a message takes, as a message still being processed after this time can be received again, by another copy of the integration or, when a step waits without holding up the source, by this one, and is then processed twice. A plain number is read as milliseconds, not seconds. When it is not set, 30 seconds. | string |  | PT5M |

## Dependencies

At runtime, the `azure-storage-queue-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-storage-queue
    
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
      uri: "kamelet:azure-storage-queue-source"
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

## Azure Storage Queue Source Kamelet Description

### Authentication methods

In this Kamelet, you can use these Azure authentication methods:

-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Plain Shared Account Key: `SHARED_ACCOUNT_KEY`
    
-   Shared Key Credentials: `SHARED_KEY_CREDENTIAL`
    

The default is SHARED\_ACCOUNT\_KEY.

The order of evaluation for `AZURE_IDENTITY` is the following:

-   Enviroment
    
-   Workload Identity
    
-   Managed Identity
    
-   Azure Developer CLI
    
-   IntelliJ
    
-   Azure CLI
    
-   Azure Powershell
    

For more information, see the [Azure Identity documentation](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)

### Example with Slow Processing

```yaml
- route:
    from:
      uri: "kamelet:azure-storage-queue-source"
      parameters:
        accountName: "mystorageaccount"
        accessKey: "the-access-key"
        queueName: "orders"
        visibilityTimeout: "PT5M"
        delay: 5000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Each received message stays hidden from other readers for 5 minutes, instead of 30 seconds, so a message whose processing takes a few minutes is not received a second time while it is processed. A message whose processing fails is received again after these 5 minutes. The queue is checked for new messages every 5 seconds instead of every 500 milliseconds.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-queue-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-queue-source.kamelet.yaml)