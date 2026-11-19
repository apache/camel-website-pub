# ![azure storage blob append sink](_images/kamelets/azure-storage-blob-append-sink.svg) Azure Storage Blob Append Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Adds each message at the end of an append blob in Azure Blob Storage, named after the `file` header, and creates the blob when it does not exist yet.

Use it to collect log lines, audit records or CSV rows from many messages into one growing blob. To write each message as a blob of its own, use `azure-storage-blob-sink`.

Input: the body is the data to add: text, bytes or a stream. It is added as it is, so end each line with a line break yourself. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The `file` header (or `ce-file`) is the name of the blob, such as `logs/app.log`. Without it, each message goes to a new blob with a generated unique name.

Output: the body afterwards is `true`, and headers such as `CamelAzureStorageBlobAppendOffset` and `CamelAzureStorageBlobCommittedBlockCount` describe the append.

Good to know: the container must exist: a missing container fails the message. A name that is already used by a block blob, such as one written by `azure-storage-blob-sink`, fails the message too. Headers that start with `CamelAzureStorageBlob` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-blob-append-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The name of the storage account, as shown in the Azure portal under Storage accounts. It is the first part of the address of the account, `[https://<accountName>.blob.core.windows.net](https://\<accountName\>.blob.core.windows.net)`. | string |  | mystorageaccount |
| **containerName** | Container Name | **Required** The name of the container in the storage account that holds the append blobs. | string |  | logs |
| **accessKey** | Access Key | An access key of the storage account, from the Azure portal: the storage account, then Security + networking, then Access keys. Used when `credentialType` is `SHARED_ACCOUNT_KEY`, the default. | string |  |  |
| **clientId** | Client ID | The application (client) ID of an app registration (service principal) in Microsoft Entra ID that has access to the storage account, from the Overview page of the app registration in the Azure portal. Used with `clientSecret` and `tenantId` when `credentialType` is `AZURE_IDENTITY`. | string |  |  |
| **clientSecret** | Client Secret | A client secret of the app registration, from the Azure portal: the app registration, then Certificates & secrets. Used with `clientId` and `tenantId` when `credentialType` is `AZURE_IDENTITY`. | string |  |  |
| **credentialType** | Credential Type | How to log in to the storage account. `SHARED_ACCOUNT_KEY`, the default, uses `accessKey`. `AZURE_SAS` uses `sasToken`. `AZURE_IDENTITY` uses `clientId`, `clientSecret` and `tenantId` when all three are set, and otherwise the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login. Do not use `CLIENT_SECRET`: it does not use the three client options. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_SAS \* AZURE\_IDENTITY \* CLIENT\_SECRET | string | SHARED\_ACCOUNT\_KEY |  |
| **sasToken** | SAS Token | A shared access signature (SAS) token for the storage account or for the container, from the Azure portal: the storage account, then Security + networking, then Shared access signature, or the container, then Shared access tokens. Used when `credentialType` is `AZURE_SAS`. Give the token only, such as `sv=2022-11-02&ss=b&srt=sco&sp=rw&se=2026-12-31T00:00:00Z&spr=https&sig=…​`, with or without the leading `?`, not the whole SAS URL. It needs the Read and Write permissions. | string |  |  |
| **tenantId** | Tenant ID | The directory (tenant) ID of the app registration, from its Overview page in the Azure portal. Used with `clientId` and `clientSecret` when `credentialType` is `AZURE_IDENTITY`. | string |  |  |

## Dependencies

At runtime, the `azure-storage-blob-append-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:azure-storage-blob-append-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Storage Blob Append Sink Kamelet Description

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

A shared access signature (SAS) token gives access to the storage account, or to one container, with the permissions and the expiry chosen when it was made, without handing out an access key. Create one in the Azure portal: the storage account, then **Security + networking**, then **Shared access signature**, or the container, then **Shared access tokens**. Set **credentialType** to `AZURE_SAS` and **sasToken** to the token, without the URL in front of it; a leading `?` is allowed. The append sink needs the Read and Write permissions. A token that lacks a permission, or has expired, fails with status 403.

### Optional Headers

In the headers, you can set the `file` / `ce-file` property to specify the filename to upload. If you do not set it, the blob gets a generated unique name.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-append-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-append-sink.kamelet.yaml)