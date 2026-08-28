# ![azure servicebus sink](_images/kamelets/azure-servicebus-sink.svg) Azure Servicebus Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send Messages to Azure Servicebus.

## Configuration Options

The following table summarizes the configuration options available for the `azure-servicebus-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionString** | Connection String | **Required** Connection String for Azure Servicebus instance. | string |  |  |
| **topicOrQueueName** | Topic Or Queue Name | **Required** Topic Or Queue Name for the Azure Servicebus instance. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* AZURE\_IDENTITY \* CONNECTION\_STRING \* TOKEN\_CREDENTIAL | string | CONNECTION\_STRING |  |
| **serviceBusType** | Servicebus Type | The service bus type of connection to execute. Queue is for typical queue option and topic for subscription based model. Enum values: \* queue \* topic | string | queue |  |

## Dependencies

At runtime, the `azure-servicebus-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-servicebus
    
-   camel:kamelet
    
-   camel:core
    

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
            uri: "kamelet:azure-servicebus-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Servicebus Sink Kamelet Description

### Authentication methods

In this Kamelet, you can use these Azure authentication methods:

-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Connection string: `CONNECTION_STRING`
    
-   Token credentials: `TOKEN_CREDENTIAL`
    

The order of evaluation for `AZURE_IDENTITY` is the following:

-   Enviroment
    
-   Workload Identity
    
-   Managed Identity
    
-   Azure Developer CLI
    
-   IntelliJ
    
-   Azure CLI
    
-   Azure Powershell
    

For more information, see the [Azure Identity documentation](https://learn.microsoft.com/en-us/java/api/overview/azure/identity-readme)

For `TOKEN_CREDENTIAL` type, you’ll need to add `com.azure.core.credential.TokenCredential` instance in the Camel registry.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-sink.kamelet.yaml)