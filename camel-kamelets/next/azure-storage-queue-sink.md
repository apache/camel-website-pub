# ![azure storage queue sink](_images/kamelets/azure-storage-queue-sink.svg) Azure Storage Queue Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Adds each message to a queue in Azure Queue Storage, as the text of a queue message.

Use it to hand work to another application or worker that reads the queue, such as orders to process or jobs to run. For a message broker with topics and dead-letter queues, use `azure-servicebus-sink`.

Input: the body is the text of the queue message: text or bytes. A Map is sent as its text form, so turn it into JSON text first, for example with `json-serialize-action`. The optional `expiration` header (or `ce-expiration`) sets how long the message stays in the queue, as an ISO-8601 duration such as `PT1H` (one hour) or `P2D` (two days); without it, the message expires after 7 days.

Output: the body afterwards is `true`, and headers such as `CamelAzureStorageQueueMessageId` and `CamelAzureStorageQueueExpirationTime` describe the message sent.

Good to know: the queue must exist: a missing queue fails the message. An `expiration` that is a plain number, such as `600`, fails the message.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-queue-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** An access key of the storage account, from the Azure portal: the storage account, then Security + networking, then Access keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |
| **accountName** | Account Name | **Required** The name of the storage account, as shown in the Azure portal under Storage accounts. It is the first part of the address of the account, `[https://<accountName>.queue.core.windows.net](https://\<accountName\>.queue.core.windows.net)`. | string |  | mystorageaccount |
| **queueName** | Queue Name | **Required** The name of the queue in the storage account to send the messages to. | string |  | orders |
| **credentialType** | Credential Type | How to log in to the storage account. `SHARED_ACCOUNT_KEY`, the default, and `SHARED_KEY_CREDENTIAL` use `accessKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login; `accessKey` must still be given, but is not used. Enum values: \* SHARED\_ACCOUNT\_KEY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_IDENTITY | string | SHARED\_ACCOUNT\_KEY |  |

## Dependencies

At runtime, the `azure-storage-queue-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:azure-storage-queue-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Storage Queue Sink Kamelet Description

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

### Optional Headers

In the header, you can set the `expiration` / `ce-expiration` property to determine how long an event remains in the Azure Storage queue. Use `PnDTnHnMn.nS.` format. For example, `PT20.345S` parses as 20.345 seconds and `P2D` parses as 2 days. A plain number, such as `600`, fails the message. If you do not set the property in the header, the message expires after 7 days.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-queue-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-queue-sink.kamelet.yaml)