# ![azure storage blob source](_images/kamelets/azure-storage-blob-source.svg) Azure Storage Blob Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume files from Azure Storage Blob.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-blob-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The Azure Storage Blob account name. | string |  |  |
| **containerName** | Container Name | **Required** The Azure Storage Blob container name. | string |  |  |
| **accessKey** | Access Key | The Azure Storage Blob access key. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY | string | SHARED\_ACCOUNT\_KEY |  |
| **delay** | Delay | The number of milliseconds before the next poll of the selected blob. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Blob | Specifies to delete blobs after consuming them. | boolean | false |  |

## Dependencies

At runtime, the `azure-storage-blob-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-storage-blob
    
-   camel:kamelet
    
-   camel:core
    
-   camel:jsonpath
    
-   camel:timer
    

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
      uri: "kamelet:azure-storage-blob-source"
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

## Azure Storage Blob Source Kamelet Description

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-source.kamelet.yaml)