# ![azure storage datalake sink](_images/kamelets/azure-storage-datalake-sink.svg) Azure Storage Blob Data Lake Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Uploads each message as a file to a file system in Azure Data Lake Storage Gen2, named after the `file` header.

Use it to land data for analytics, such as exports, events or reports, in a data lake. For plain blob containers, use `azure-storage-blob-sink`.

Input: the body is the content of the file: text, bytes or a stream. A Map fails: turn it into JSON text first, for example with `json-serialize-action`. The optional `file` header (or `ce-file`) is the name of the file, such as `sales-2026-05.csv`. Without it, the file gets a generated unique name.

Output: the body afterwards is `true`.

Good to know: the file is written at the top of the file system, or in `directoryName`. By default it logs in as an app registration, with `clientId`, `clientSecret` and `tenantId`, so that app needs a role on the account that allows writing, such as Storage Blob Data Contributor. Headers that start with `CamelAzureStorageDataLake` are removed from the message first, so they cannot change what the Kamelet does. It can log in with an account key (`accountKey`) or a SAS token (`sasSignature`) instead.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-datalake-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The name of the storage account, an Azure Data Lake Storage Gen2 account (a storage account with hierarchical namespace), as shown in the Azure portal under Storage accounts. | string |  | mydatalake |
| **fileSystemName** | File System Name | **Required** The name of the file system (the container) in the account to write the files to. | string |  | raw-data |
| **accountKey** | Account Key | An access key of the storage account, from the Azure portal: the storage account, then Security + networking, then Access keys. Used when `credentialType` is `SHARED_KEY_CREDENTIAL`. | string |  |  |
| **clientId** | Client ID | The application (client) ID of an app registration (service principal) in Microsoft Entra ID that has access to the account, from the Overview page of the app registration in the Azure portal. Required when `credentialType` is `CLIENT_SECRET`, the default. | string |  |  |
| **clientSecret** | Client Secret | A client secret of the app registration, from the Azure portal: the app registration, then Certificates & secrets. Required when `credentialType` is `CLIENT_SECRET`, the default. | string |  |  |
| **credentialType** | Credential Type | How to log in to the account. `CLIENT_SECRET`, the default, uses `clientId`, `clientSecret` and `tenantId`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. The other values need a credential object, such as a `DataLakeServiceClient` for `SERVICE_CLIENT_INSTANCE`, in the application. Enum values: \* CLIENT\_SECRET \* SHARED\_KEY\_CREDENTIAL \* AZURE\_IDENTITY \* AZURE\_SAS \* SERVICE\_CLIENT\_INSTANCE | string | CLIENT\_SECRET |  |
| **directoryName** | Directory Name | The directory of the file system to write the files to, such as `exports/2026`, without a `/` at the start or the end. The name of each file is put after it, so the `file` header `sales.csv` is written as `exports/2026/sales.csv`, and `2026/q1.csv` as `exports/2026/2026/q1.csv`. When it is not set, the files are written at the top of the file system. | string |  | exports/2026 |
| **sasSignature** | SAS Token | A shared access signature (SAS) token that gives access to the account or the file system, such as `sv=2022-11-02&ss=b&srt=co&sp=rwc&se=2026-12-31T00:00:00Z&sig=…​`, without a leading `?`. Create it in the Azure portal under Shared access signature of the storage account, or under Shared access tokens of the container. It must allow creating and writing. Used when `credentialType` is `AZURE_SAS`. | string |  |  |
| **tenantId** | Tenant ID | The directory (tenant) ID of the app registration, from its Overview page in the Azure portal. Required when `credentialType` is `CLIENT_SECRET`, the default. | string |  |  |

## Dependencies

At runtime, the `azure-storage-datalake-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:azure-storage-datalake-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Storage Datalake Sink Kamelet Description

### Authentication methods

In this Kamelet, you can use these Azure authentication methods:

-   Client secret: `CLIENT_SECRET` (default)
    
-   Azure SAS: `AZURE_SAS`
    
-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Service client instance: `SERVICE_CLIENT_INSTANCE`
    
-   Shared key credentials: `SHARED_KEY_CREDENTIAL`
    

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

In the headers, you can set the `file` / `ce-file` property to specify the filename to upload. If you do not set it, the file gets a generated unique name.

### Example with a Directory and an Account Key

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "id,amount"
        period: 60000
      steps:
        - setHeader:
            name: file
            simple: "sales-$\{date:now:yyyyMMddHHmmss}.csv"
        - to:
            uri: "kamelet:azure-storage-datalake-sink"
            parameters:
              accountName: "mydatalake"
              fileSystemName: "raw-data"
              credentialType: "SHARED_KEY_CREDENTIAL"
              accountKey: "the-account-key"
              directoryName: "exports/2026"
```

Each file is written to the `exports/2026` directory of the `raw-data` file system, such as `exports/2026/sales-20261118093000.csv`. With **credentialType** `AZURE_SAS`, give a SAS token in **sasSignature** instead of **accountKey**. **clientId**, **clientSecret** and **tenantId** are needed only with `CLIENT_SECRET`, the default.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-datalake-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-datalake-sink.kamelet.yaml)