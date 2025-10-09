# ![azure storage blob changefeed source](_images/kamelets/azure-storage-blob-changefeed-source.svg) Azure Storage Blob Changefeed Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume events from an Azure Storage Blob change feed.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-blob-changefeed-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The Azure Storage Blob account name. | string |  |  |
| **period** | Period between Polls | **Required** The interval (in milliseconds) between fetches to the Azure Storage change feed. | integer | 10000 |  |
| **accessKey** | Access Key | The Azure Storage Blob access Key. | string |  |  |
| **clientId** | Client Id | The Azure Storage Blob client Id. | string |  |  |
| **clientSecret** | Client Secret | The Azure Storage Blob client secret. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* SHARED\_ACCOUNT\_KEY \* AZURE\_IDENTITY \* CLIENT\_SECRET | string | SHARED\_ACCOUNT\_KEY |  |
| **tenantId** | Tenant Id | The Azure Storage Blob tenant id. | string |  |  |

## Dependencies

At runtime, the `azure-storage-blob-changefeed-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-storage-blob
    
-   camel:kamelet
    
-   camel:core
    
-   camel:jackson
    
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
      uri: "kamelet:azure-storage-blob-changefeed-source"
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

## Azure Storage Blob Changefeed Source Kamelet Description

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-changefeed-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-changefeed-source.kamelet.yaml)