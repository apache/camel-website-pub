# ![azure storage datalake source](_images/kamelets/azure-storage-datalake-source.svg) Azure Storage Blob Data Lake Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume files from Azure Storage Blob Data Lake.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-datalake-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The Azure Storage Blob Data lake account name. | string |  |  |
| **clientId** | Client Id | **Required** The Azure Storage Blob Data lake client Id. | string |  |  |
| **clientSecret** | Client Secret | **Required** The Azure Storage Blob Data lake client secret. | string |  |  |
| **fileSystemName** | File System Name | **Required** The Azure Storage Blob Data lake File system name. | string |  |  |
| **tenantId** | Tenant Id | **Required** The Azure Storage Blob Data lake tenant id. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* CLIENT\_SECRET \* SHARED\_KEY\_CREDENTIAL \* AZURE\_IDENTITY \* AZURE\_SAS \* SERVICE\_CLIENT\_INSTANCE | string | CLIENT\_SECRET |  |
| **delay** | Delay | The number of milliseconds before the next poll of the selected blob. | integer | 500 |  |

## Dependencies

At runtime, the `azure-storage-datalake-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-storage-datalake
    
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-datalake-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-datalake-source.kamelet.yaml)