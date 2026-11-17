# ![azure storage files source](_images/kamelets/azure-storage-files-source.svg) Azure Storage File Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files in a directory of a file share in Azure Files, one message per file, and can delete each file once it has been read.

Use it to process files that people or applications put on a share, such as scanned documents or exports. For blob containers, use `azure-storage-blob-source`.

Output: the body is the content of the file, which converts to text, bytes or a stream. The `CamelFileName` header is the path of the file from `directoryName`, `CamelFileNameOnly` its name, and `CamelFileLength` and `CamelFileLastModified` its size and last-modified time.

Good to know: files are kept after they are read, so the same files are read again on every poll, every 500 milliseconds by default; set `deleteAfterRead` to true to delete each file once it has been processed. Subdirectories are read only when `recursive` is true.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-files-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The name of the storage account, as shown in the Azure portal under Storage accounts. It is the first part of the address of the account, `[https://<accountName>.file.core.windows.net](https://\<accountName\>.file.core.windows.net)`. | string |  | mystorageaccount |
| **shareName** | Share Name | **Required** The name of the file share in the storage account to read the files from. | string |  | documents |
| **credentialType** | Credential Type | How to log in to the storage account. `SHARED_ACCOUNT_KEY`, the default, uses `sharedKey`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. The other values need settings that this Kamelet does not offer. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_SAS | string | SHARED\_ACCOUNT\_KEY |  |
| **delay** | Delay | How long to wait between two polls of the directory, in milliseconds. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete File | If true, each file is deleted from the share once it has been processed. When false, the files stay and are read again on every poll. | boolean | false |  |
| **directoryName** | Directory Name | The directory of the share to read the files from, such as `inbox/orders`. `.`, the default, is the top of the share. | string | . | inbox/orders |
| **recursive** | Recursive Mode | If true, also reads the files in the subdirectories of `directoryName`. | boolean | false |  |
| **sharedKey** | Shared Access Key | An access key of the storage account, from the Azure portal: the storage account, then Security + networking, then Access keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |

## Dependencies

At runtime, the `azure-storage-files-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-files
    
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