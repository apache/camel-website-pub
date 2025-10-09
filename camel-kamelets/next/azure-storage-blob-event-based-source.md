# ![azure storage blob event based source](_images/kamelets/azure-storage-blob-event-based-source.svg) Azure Storage Blob Event-based Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from Azure Service Bus subscribed to Azure Eventgrid reporting events related to a Azure Storage Blob account.

## Configuration Options

The following table summarizes the configuration options available for the `azure-storage-blob-event-based-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accountName** | Account Name | **Required** The Azure Storage Blob account name. | string |  |  |
| **connectionString** | Connection String | **Required** Connection String for Azure Servicebus instance. | string |  |  |
| **containerName** | Container Name | **Required** The Azure Storage Blob container name. | string |  |  |
| **topicOrQueueName** | Topic Or Queue Name | **Required** Topic Or Queue Name for the Azure Servicebus instance. | string |  |  |
| **accessKey** | Access Key | The Azure Storage Blob access key. | string |  |  |
| **clientId** | Client Id | The Azure Storage Blob client Id. | string |  |  |
| **clientSecret** | Client Secret | The Azure Storage Blob client secret. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* SHARED\_ACCOUNT\_KEY \* SHARED\_KEY\_CREDENTIAL \* AZURE\_IDENTITY \* CLIENT\_SECRET | string | SHARED\_ACCOUNT\_KEY |  |
| **getBlob** | Get Object in Container | If `getBlob` is enabled, then the file created in the container is retrieved and returned as body. If not only the event is returned as body. | boolean | false |  |
| **serviceBusReceiveMode** | Servicebus Receive Mode | Sets the receive mode for the receiver. Enum values: \* RECEIVE\_AND\_DELETE \* PEEK\_LOCK | string | RECEIVE\_AND\_DELETE |  |
| **subscriptionName** | Subscription Name | Sets the name of the subscription in the topic to listen to. This parameter is mandatory in case of topic. | string |  |  |
| **tenantId** | Tenant Id | The Azure Storage Blob tenant id. | string |  |  |

## Dependencies

At runtime, the `azure-storage-blob-event-based-source` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-servicebus
    
-   camel:azure-storage-blob
    
-   camel:kamelet
    
-   camel:core
    
-   camel:jsonpath
    
-   camel:jackson
    

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
      uri: "kamelet:azure-storage-blob-event-based-source"
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

## Azure Storage Blob Event Based Source Kamelet Description

### Authentication methods

For this Kamelet the Connection string is the basic method for authenticating to the Azure Servicebus Queue.

To use this Kamelet you’ll need to set up Events on your Azure Storage Blob account and select as an endpoint an Azure Servicebus Queue.

For the Azure Storage Blob access, you can use these Azure authentication methods:

-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Plain Shared Account Key: `SHARED_ACCOUNT_KEY`
    
-   Shared Key Credential: `SHARED_KEY_CREDENTIAL`
    
-   Client Secret Credentials: `CLIENT_SECRET`
    

For `CLIENT_SECRET` you’ll need to provide `clientId`, `clientSecret`, and `tenantId` properties.

For more information, see the [Azure Identity documentation](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-event-based-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-storage-blob-event-based-source.kamelet.yaml)