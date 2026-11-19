# ![azure storage datalake source](_images/kamelets/azure-storage-datalake-source.svg) Azure Storage Blob Data Lake Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the files in a file system of Azure Data Lake Storage Gen2, one message per file, on every poll.

Use it to process files that land in a data lake, such as exports or reports. For plain blob containers, use `azure-storage-blob-source`, which can also delete what it reads.

Output: the body is the content of the file, as a stream of bytes. The `CamelAzureStorageDataLakeFileName` header is the name of the file, and other headers give its size, content type, ETag and last-modified time.

Good to know: it neither deletes nor moves the files, so it reads all of them again on every poll, every 500 milliseconds by default. It reads the files at the top of the file system, or of `directoryName`; the files in directories below are read only when `recursive` is true. `regex` keeps only the files whose path matches, and `fileName` reads one file. Log in as an app registration with `clientId`, `clientSecret` and `tenantId` (the default), or with an account key (`accountKey`) or a SAS token (`sasSignature`).

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-datalake-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The name of the storage account, an Azure Data Lake Storage Gen2 account (a storage account with hierarchical namespace), as shown in the Azure portal under Storage accounts. | string |  | mydatalake |
| **fileSystemName** | File System Name | **Required** The name of the file system (the container) in the account to read the files from. | string |  | raw-data |
| **accountKey** | Account Key | An access key of the storage account, from the Azure portal: the storage account, then Security + networking, then Access keys. Used when `credentialType` is `SHARED_KEY_CREDENTIAL`. | string |  |  |
| **clientId** | Client ID | The application (client) ID of an app registration (service principal) in Microsoft Entra ID that has access to the account, from the Overview page of the app registration in the Azure portal. Required when `credentialType` is `CLIENT_SECRET`, the default. | string |  |  |
| **clientSecret** | Client Secret | A client secret of the app registration, from the Azure portal: the app registration, then Certificates & secrets. Required when `credentialType` is `CLIENT_SECRET`, the default. | string |  |  |
| **credentialType** | Credential Type | How to log in to the account. `CLIENT_SECRET`, the default, uses `clientId`, `clientSecret` and `tenantId`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. The other values need a credential object, such as a `DataLakeServiceClient` for `SERVICE_CLIENT_INSTANCE`, in the application. Enum values: \* CLIENT\_SECRET \* SHARED\_KEY\_CREDENTIAL \* AZURE\_IDENTITY \* AZURE\_SAS \* SERVICE\_CLIENT\_INSTANCE | string | CLIENT\_SECRET |  |
| **delay** | Delay | How long to wait between two polls of the file system, in milliseconds. | integer | 500 |  |
| **directoryName** | Directory Name | The directory of the file system to read the files from, such as `exports/2026`. When it is not set, the top of the file system. The `CamelAzureStorageDataLakeFileName` header is still the path of the file from the top of the file system, such as `exports/2026/sales.csv`. | string |  | exports/2026 |
| **fileName** | File Name | The path of one file to read, from the top of the file system, such as `exports/sales.csv`. Only this file is read, on every poll, and `directoryName`, `recursive` and `regex` are not used. When the file does not exist, each poll fails with a warning in the log. | string |  | exports/sales.csv |
| **recursive** | Recursive | If true, also reads the files in the directories below the top of the file system, or below `directoryName`. When it is not set, only the files directly in it are read. | boolean |  |  |
| **regex** | File Name Pattern | A regular expression that the path of a file, from the top of the file system, must match as a whole to be read, such as `.**\.csv**` **for all CSV files, or `exports/.`**`\.csv`. It is case-sensitive. When it is not set, all files are read. | string |  | .\*\\.csv |
| **sasSignature** | SAS Token | A shared access signature (SAS) token that gives access to the account or the file system, such as `sv=2022-11-02&ss=b&srt=co&sp=rl&se=2026-12-31T00:00:00Z&sig=…​`, without a leading `?`. Create it in the Azure portal under Shared access signature of the storage account, or under Shared access tokens of the container. It must allow listing and reading. Used when `credentialType` is `AZURE_SAS`. | string |  |  |
| **tenantId** | Tenant ID | The directory (tenant) ID of the app registration, from its Overview page in the Azure portal. Required when `credentialType` is `CLIENT_SECRET`, the default. | string |  |  |

## Dependencies

At runtime, the `azure-storage-datalake-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-storage-datalake
    
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
      uri: "kamelet:azure-storage-datalake-source"
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

## Azure Storage Blob Data Lake Source Kamelet Description

### Authentication methods

In this Kamelet, you can use these Azure authentication methods:

-   Client secret: `CLIENT_SECRET` (default), with **clientId**, **clientSecret** and **tenantId**
    
-   Shared key credentials: `SHARED_KEY_CREDENTIAL`, with **accountKey**
    
-   Azure SAS: `AZURE_SAS`, with **sasSignature**
    
-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Service client instance: `SERVICE_CLIENT_INSTANCE`
    

For more information, see the [Azure Identity documentation](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)

### Example with a Directory and a File Name Pattern

```yaml
- route:
    from:
      uri: "kamelet:azure-storage-datalake-source"
      parameters:
        accountName: "mydatalake"
        fileSystemName: "raw-data"
        credentialType: "SHARED_KEY_CREDENTIAL"
        accountKey: "the-account-key"
        directoryName: "exports"
        recursive: true
        regex: ".*\\.csv"
        delay: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Every minute, all the CSV files in the `exports` directory and the directories below it are read, such as `exports/a.csv` and `exports/2026/c.csv`. **regex** must match the whole path of the file from the top of the file system. The files are not deleted or moved, so they are read again at every poll. To read one file only, give its path in **fileName**.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-datalake-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-datalake-source.kamelet.yaml)