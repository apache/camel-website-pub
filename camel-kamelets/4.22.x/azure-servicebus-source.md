# ![azure servicebus source](_images/kamelets/azure-servicebus-source.svg) Azure Servicebus Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume Messages from Azure Servicebus.

## Configuration Options

The following table summarizes the configuration options available for the `azure-servicebus-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionString** | Connection String | **Required** Connection String for Azure Servicebus instance. | string |  |  |
| **topicOrQueueName** | Topic Or Queue Name | **Required** Topic Or Queue Name for the Azure Servicebus instance. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* AZURE\_IDENTITY \* CONNECTION\_STRING \* TOKEN\_CREDENTIAL | string | CONNECTION\_STRING |  |
| **serviceBusReceiveMode** | Servicebus Receive Mode | Sets the receive mode for the receiver. Enum values: \* PEEK\_LOCK \* RECEIVE\_AND\_DELETE | string | PEEK\_LOCK |  |
| **serviceBusType** | Servicebus Type | The service bus type of connection to execute. Queue is for typical queue option and topic for subscription based model. Enum values: \* queue \* topic | string | queue |  |
| **subscriptionName** | Subscription Name | Sets the name of the subscription in the topic to listen to. This parameter is mandatory in case of topic. | string |  |  |

## Dependencies

At runtime, the `azure-servicebus-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:azure-servicebus-source"
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

## Azure Servicebus Source Kamelet Description

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

### Topic vs Queue

The subscribtion name parameter needs to be populated in case of consuming from a Topic, while it’s not required in case of Queue.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-source.kamelet.yaml)