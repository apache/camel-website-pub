# ![azure eventhubs source](_images/kamelets/azure-eventhubs-source.svg) Azure Eventhubs Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive events from Azure Event Hubs.

## Configuration Options

The following table summarizes the configuration options available for the `azure-eventhubs-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **blobAccessKey** | Azure Storage Blob Access Key | **Required** The key for the Azure Storage Blob service that is associated with the Storage Blob account name. | string |  |  |
| **blobAccountName** | Azure Storage Blob Account Name | **Required** The name of the Storage Blob account. | string |  |  |
| **blobContainerName** | Azure Storage Blob Container Name | **Required** The name of the Storage Blob container. | string |  |  |
| **eventhubName** | Eventhubs Name | **Required** The Event Hub name. | string |  |  |
| **namespaceName** | Eventhubs Namespace | **Required** The Event Hubs namespace. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* CONNECTION\_STRING \* AZURE\_IDENTITY | string | CONNECTION\_STRING |  |
| **sharedAccessKey** | Share Access Key | The key for the Event Hubs SAS key name. | string |  |  |
| **sharedAccessName** | Share Access Name | The Event Hubs SAS key name. | string |  |  |

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