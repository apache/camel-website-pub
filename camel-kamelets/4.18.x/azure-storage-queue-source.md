# ![azure storage queue source](_images/kamelets/azure-storage-queue-source.svg) Azure Storage Queue Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive events from Azure Storage queues.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-queue-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The Azure Storage Queue access key. | string |  |  |
| **accountName** | Account Name | **Required** The Azure Storage Queue account name. | string |  |  |
| **queueName** | Queue Name | **Required** The Azure Storage Queue container name. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* SHARED\_ACCOUNT\_KEY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_IDENTITY | string | SHARED\_ACCOUNT\_KEY |  |
| **maxMessages** | Maximum Messages | The maximum number of messages to get. You can specify a value between 1 and 32. The default is 1 (one message). If there are fewer than the maximum number of messages in the queue, then all the messages are returned. | integer | 1 |  |

## Dependencies

At runtime, the `azure-storage-queue-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-storage-queue
    
-   camel:kamelet
    
-   camel:core
    

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-queue-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-queue-source.kamelet.yaml)