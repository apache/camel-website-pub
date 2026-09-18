# ![azure eventhubs sink](_images/kamelets/azure-eventhubs-sink.svg) Azure Eventhubs Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send events to Azure Event Hubs.

## Configuration Options

The following table summarizes the configuration options available for the `azure-eventhubs-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **eventhubName** | Eventhubs Name | **Required** The Event Hub name. | string |  |  |
| **namespaceName** | Eventhubs Namespace | **Required** The Event Hubs namespace. | string |  |  |
| **credentialType** | Credential Type | Determines the credential strategy to adopt. Enum values: \* CONNECTION\_STRING \* AZURE\_IDENTITY | string | CONNECTION\_STRING |  |
| **sharedAccessKey** | Share Access Key | The key for the Event Hubs SAS key name. | string |  |  |
| **sharedAccessName** | Share Access Name | The Event Hubs SAS key name. | string |  |  |

## Dependencies

At runtime, the `azure-eventhubs-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:azure-eventhubs
    
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
            uri: "kamelet:azure-eventhubs-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Event Hubs Sink Kamelet Description

### Authentication methods

In this Kamelet, you can use these Azure authentication methods:

-   Azure Identity mechanism: `AZURE_IDENTITY`
    
-   Connection string: `CONNECTION_STRING`
    

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

In the headers, you can optionally set the `partition-id` / `ce-partition-id` property to specify the partition id for a specific item.

If you do not set the property in the header, Azure Event Hubs will do that for you.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-eventhubs-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-eventhubs-sink.kamelet.yaml)