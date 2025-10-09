# ![azure storage files source](_images/kamelets/azure-storage-files-source.svg) Azure Storage File Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume files from Azure Storage File Shares.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-files-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The Azure Storage File Share account name. | string |  |  |
| **shareName** | Share Name | **Required** The Azure Storage File Share share name. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_SAS | string | SHARED\_ACCOUNT\_KEY |  |
| **delay** | Delay | The number of milliseconds before the next poll of the selected blob. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Blob | Specifies to delete blobs after consuming them. | boolean | false |  |
| **directoryName** | Directory Name | The directory from where the consumer will start reading files. | string | . |  |
| **recursive** | Recursive Mode | If a directory, the consumer will look for files in all the sub-directories as well. | boolean | false |  |
| **sharedKey** | Shared Access Key | The Azure Storage Blob access key. | string |  |  |

## Dependencies

At runtime, the `azure-storage-files-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-files
    
-   camel:kamelet
    
-   camel:core
    
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
      uri: "kamelet:azure-storage-files-source"
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

## Azure Storage Files Source Kamelet Description

### Authentication methods

In this Kamelet, you can use these Azure authentication methods:

-   Plain Shared Account Key: `SHARED_ACCOUNT_KEY` (default)
    
-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Shared key credentials: `SHARED_KEY_CREDENTIAL`
    
-   Azure SAS: `AZURE_SAS`
    

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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-files-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-files-source.kamelet.yaml)