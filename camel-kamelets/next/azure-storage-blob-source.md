# ![azure storage blob source](_images/kamelets/azure-storage-blob-source.svg) Azure Storage Blob Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files (blobs) in a container of Azure Blob Storage, one message per blob, and can delete each blob, or move it to another container, once it has been read.

Use it to process files that another system drops into a container, such as uploaded documents, exported reports or log files. To react to new blobs through Event Grid events instead of reading the container over and over, use `azure-storage-blob-event-based-source`.

Output: the body is the content of the blob, as a stream of bytes, and the `Content-Type` header is `application/octet-stream`. The headers give the name of the blob (`CamelAzureStorageBlobBlobName`, with its folder path), its type, content type, size, ETag and last-modified time.

Good to know: blobs are kept after they are read, so the same blobs are read again on every poll, every 500 milliseconds by default; set `deleteAfterRead` to true to delete each blob once it has been processed, or `moveAfterRead` to move it to another container. It reads all the blobs of the container, those in virtual folders too, unless `prefix` or `regex` narrows them down. With `deleteAfterRead`, the blob deleted is the one named in the `CamelAzureStorageBlobBlobName` header when processing ends, so do not change that header.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-blob-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The name of the storage account, as shown in the Azure portal under Storage accounts. It is the first part of the address of the account, `[https://<accountName>.blob.core.windows.net](https://\<accountName\>.blob.core.windows.net)`. | string |  | mystorageaccount |
| **containerName** | Container Name | **Required** The name of the container in the storage account to read the blobs from. | string |  | invoices |
| **accessKey** | Access Key | An access key of the storage account, from the Azure portal: the storage account, then Security + networking, then Access keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |
| **clientId** | Client ID | The application (client) ID of an app registration (service principal) in Microsoft Entra ID that has access to the storage account, from the Overview page of the app registration in the Azure portal. Used with `clientSecret` and `tenantId` when `credentialType` is `AZURE_IDENTITY`. | string |  |  |
| **clientSecret** | Client Secret | A client secret of the app registration, from the Azure portal: the app registration, then Certificates & secrets. Used with `clientId` and `tenantId` when `credentialType` is `AZURE_IDENTITY`. | string |  |  |
| **credentialType** | Credential Type | How to log in to the storage account. `SHARED_ACCOUNT_KEY`, the default, uses `accessKey`. `AZURE_SAS` uses `sasToken`. `AZURE_IDENTITY` uses `clientId`, `clientSecret` and `tenantId` when all three are set, and otherwise the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. Do not use `CLIENT_SECRET`: it does not use the three client options. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_SAS \* AZURE\_IDENTITY \* CLIENT\_SECRET | string | SHARED\_ACCOUNT\_KEY |  |
| **delay** | Delay | How long to wait between two polls of the container, in milliseconds. | integer | 500 |  |
| **deleteAfterRead** | Auto-delete Blob | If true, each blob is deleted from the container once it has been processed. When false, the blobs stay and are read again on every poll. | boolean | false |  |
| **destinationContainer** | Destination Container | The name of the container, in the same storage account, to move the blobs to when `moveAfterRead` is true, such as `processed`. It must exist. A container name has 3 to 63 lowercase letters, digits and hyphens. Required with `moveAfterRead`, without it the Kamelet does not start. | string |  | processed |
| **moveAfterRead** | Move Blob After Read | If true, each blob is moved to `destinationContainer` once it has been processed. It is copied there under the same name, with its virtual folder path, and then deleted from `containerName`. If the copy fails, for example because `destinationContainer` does not exist, the blob is kept and read again on the next poll, and a warning is logged. When both `moveAfterRead` and `deleteAfterRead` are true, the blob is moved. | boolean |  |  |
| **prefix** | Blob Name Prefix | Reads only the blobs whose name starts with this text, such as `in/` for the blobs in the virtual folder `in` and its subfolders, or `invoice-`. Ignored when `regex` is set. When neither is set, all the blobs of the container are read. | string |  | in/ |
| **regex** | Blob Name Pattern | Reads only the blobs whose whole name, with its virtual folder path, matches this Java regular expression, such as `.**\.csv**` **for the CSV files in any folder, or `in/[^/]`**`\.csv` for those directly in the folder `in`. It must match the whole name: `csv` alone matches no blob. When it is set, `prefix` is ignored, and the names of all the blobs of the container are listed on each poll and then filtered. | string |  | .\*\\.csv |
| **sasToken** | SAS Token | A shared access signature (SAS) token for the storage account or for the container, from the Azure portal: the storage account, then Security + networking, then Shared access signature, or the container, then Shared access tokens. Used when `credentialType` is `AZURE_SAS`. Give the token only, such as `sv=2022-11-02&ss=b&srt=sco&sp=rl&se=2026-12-31T00:00:00Z&spr=https&sig=…​`, with or without the leading `?`, not the whole SAS URL. It needs the List and Read permissions, and also Delete with `deleteAfterRead`, or Write and Delete with `moveAfterRead`. | string |  |  |
| **tenantId** | Tenant ID | The directory (tenant) ID of the app registration, from its Overview page in the Azure portal. Used with `clientId` and `clientSecret` when `credentialType` is `AZURE_IDENTITY`. | string |  |  |

## Dependencies

At runtime, the `azure-storage-blob-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-storage-blob
    
-   camel:kamelet
    
-   camel:jsonpath
    

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
    
-   Shared access signature (SAS) token: `AZURE_SAS`, with the token in `sasToken`
    

The order of evaluation for `AZURE_IDENTITY` is the following:

-   Enviroment
    
-   Workload Identity
    
-   Managed Identity
    
-   Azure Developer CLI
    
-   IntelliJ
    
-   Azure CLI
    
-   Azure Powershell
    

To log in as an app registration (a service principal), set `credentialType` to `AZURE_IDENTITY` and provide `clientId`, `clientSecret`, and `tenantId`: when all three are set, they are used instead of the order above. `CLIENT_SECRET` does not use these three properties.

For more information, see the [Azure Identity documentation](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)

### Log in with a SAS Token

A shared access signature (SAS) token gives access to the storage account, or to one container, with the permissions and the expiry chosen when it was made, without handing out an access key. Create one in the Azure portal: the storage account, then **Security + networking**, then **Shared access signature**, or the container, then **Shared access tokens**. Set **credentialType** to `AZURE_SAS` and **sasToken** to the token, without the URL in front of it; a leading `?` is allowed. The source needs the List and Read permissions, and also Delete with **deleteAfterRead**, or Write and Delete with **moveAfterRead**. A token that lacks a permission, or has expired, fails with status 403.

### Example: Read Some of the Blobs and Move Them Once Read

By default the source reads every blob of the container on every poll. Use **prefix** or **regex** to read only some of them, and **moveAfterRead** to move each blob to another container once it has been processed:

```yaml
- route:
    from:
      uri: "kamelet:azure-storage-blob-source"
      parameters:
        accountName: "mystorageaccount"
        containerName: "uploads"
        credentialType: "AZURE_SAS"
        sasToken: "sv=2022-11-02&ss=b&srt=sco&sp=rwdl&se=2026-12-31T00:00:00Z&spr=https&sig=..."
        prefix: "in/"
        moveAfterRead: true
        destinationContainer: "processed"
      steps:
        - to: "log:blob?showHeaders=true"
```

The source reads only the blobs whose name starts with `in/`, such as `in/orders.csv` and `in/2026/report.csv`. Once a blob has been processed, it is copied to the container `processed` under the same name, `in/orders.csv`, and deleted from `uploads`. The container `processed` must exist: when the copy fails, the blob stays in `uploads` and is read again on the next poll.

To select blobs by a pattern instead, set **regex** to a Java regular expression that matches the whole name, such as `.*\.csv` for the CSV files in any folder. When **regex** is set, **prefix** is ignored.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-source.kamelet.yaml)