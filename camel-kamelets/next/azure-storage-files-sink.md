# ![azure storage files sink](_images/kamelets/azure-storage-files-sink.svg) Azure Storage Files Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Upload data to Azure Storage Files Share.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-files-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The Azure Storage Blob account name. | string |  |  |
| **shareName** | Share Name | **Required** The Azure Storage File Share share name. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_SAS | string | SHARED\_ACCOUNT\_KEY |  |
| **directoryName** | Directory Name | The directory from where the producer will upload the file. | string | . |  |
| **sharedKey** | Shared Access Key | The Azure Storage Blob access key. | string |  |  |

## Dependencies

At runtime, the `azure-storage-files-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:azure-storage-blob
    
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
            uri: "kamelet:azure-storage-files-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Storage Files Sink Kamelet Description

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

### Optional Headers

In the headers, you can set the `file` / `ce-file` property to specify the filename to upload. If you do set property in the header, the Kamelet uses the exchange ID as filename.

The value is reduced to a single file name before use: any directory component is dropped, so `reports/2026/data.csv` is stored as `data.csv`. The file is always written inside the configured directory.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-files-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-files-sink.kamelet.yaml)