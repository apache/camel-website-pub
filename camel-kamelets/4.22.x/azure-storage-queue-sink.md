# ![azure storage queue sink](_images/kamelets/azure-storage-queue-sink.svg) Azure Storage Queue Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send events to Azure Storage queues.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-queue-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessKey** | Access Key | **Required** The Azure Storage Queue access key. | string |  |  |
| **accountName** | Account Name | **Required** The Azure Storage Queue account name. | string |  |  |
| **queueName** | Queue Name | **Required** The Azure Storage Queue container name. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* SHARED\_ACCOUNT\_KEY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_IDENTITY | string | SHARED\_ACCOUNT\_KEY |  |

## Dependencies

At runtime, the `azure-storage-queue-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:azure-storage-queue
    
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
            uri: "kamelet:azure-storage-queue-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Storage Queue Sink Kamelet Description

### Authentication methods

In this Kamelet, you can use these Azure authentication methods:

-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Plain Shared Account Key: `SHARED_ACCOUNT_KEY`
    
-   Shared Key Credentials: `SHARED_KEY_CREDENTIAL`
    

The default is SHARED\_ACCOUNT\_KEY.

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

In the header, you can set the `partition` / `ce-partition` property to determine how long an event remains in the Azure Storage queue. Use `PnDTnHnMn.nS.` format. For example, `PT20.345S` parses as 20.345 seconds and `P2D` parses as 2 days. If you not set the property in the header, the Kamelet uses the default of `P27D` (7 days).

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-queue-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-queue-sink.kamelet.yaml)