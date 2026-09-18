# ![azure storage blob append sink](_images/kamelets/azure-storage-blob-append-sink.svg) Azure Storage Blob Append Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Upload data in append mode to Azure Storage Blob.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-blob-append-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The Azure Storage Blob account name. | string |  |  |
| **containerName** | Container Name | **Required** The Azure Storage Blob container name. | string |  |  |
| **accessKey** | Access Key | The Azure Storage Blob access key. | string |  |  |
| **clientId** | Client Id | The Azure Storage Blob client Id. | string |  |  |
| **clientSecret** | Client Secret | The Azure Storage Blob client secret. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY \* CLIENT\_SECRET | string | SHARED\_ACCOUNT\_KEY |  |
| **tenantId** | Tenant Id | The Azure Storage Blob tenant id. | string |  |  |

## Dependencies

At runtime, the `azure-storage-blob-append-sink` Kamelet relies upon the presence of the following dependencies:

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
    
-   Client Secret Credentials: `CLIENT_SECRET`
    

The order of evaluation for `AZURE_IDENTITY` is the following:

-   Enviroment
    
-   Workload Identity
    
-   Managed Identity
    
-   Azure Developer CLI
    
-   IntelliJ
    
-   Azure CLI
    
-   Azure Powershell
    

For `CLIENT_SECRET` you’ll need to provide `clientId`, `clientSecret`, and `tenantId` properties.

For more information, see the [Azure Identity documentation](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)

### Optional Headers

In the headers, you can set the `file` / `ce-file` property to specify the filename to upload. If you do set property in the header, the Kamelet uses the exchange ID as filename.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-append-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-append-sink.kamelet.yaml)