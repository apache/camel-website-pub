# ![azure servicebus sink](_images/kamelets/azure-servicebus-sink.svg) Azure Servicebus Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a queue or a topic in Azure Service Bus, the Azure message broker.

Use it to hand work or events to other applications through Service Bus, such as orders to process, or notifications for all the subscribers of a topic. For simple storage queues, use `azure-storage-queue-sink`.

Input: the body is sent as text: text, bytes or a stream are read as text. A Map is sent as its text form, so turn it into JSON text first, for example with `json-serialize-action`. A List is sent as one message per element. The optional `CamelAzureServiceBusApplicationProperties` header, a Map, sets the custom properties of the message.

Output: the message is unchanged.

Good to know: the shared access policy of the connection string needs the Send right.

## Configuration Options

The following table summarizes the configuration options available for the `azure-servicebus-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionString** | Connection String | **Required** The connection string of the Service Bus namespace, from the Azure portal: the namespace, then Settings, Shared access policies, a policy, Primary Connection String. It starts with `Endpoint=sb://`. | string |  |  |
| **topicOrQueueName** | Topic or Queue Name | **Required** The name of the queue, or of the topic, to send the messages to. For a topic, set `serviceBusType` to `topic`. | string |  | orders |
| **credentialType** | Credential Type | How to log in to Service Bus. Keep `CONNECTION_STRING`, the default, which uses `connectionString`. `AZURE_IDENTITY` and `TOKEN_CREDENTIAL` also need the `fullyQualifiedNamespace` of the Camel component, which this Kamelet does not set. Enum values: \* AZURE\_IDENTITY \* CONNECTION\_STRING \* TOKEN\_CREDENTIAL | string | CONNECTION\_STRING |  |
| **serviceBusType** | Service Bus Type | Whether `topicOrQueueName` is a `queue` or a `topic`. Enum values: \* queue \* topic | string | queue |  |

## Dependencies

At runtime, the `azure-servicebus-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-servicebus
    
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

`AZURE_IDENTITY` and `TOKEN_CREDENTIAL` also need the fully qualified namespace of Service Bus, which this Kamelet does not set: configure the `fullyQualifiedNamespace` option of the Camel `azure-servicebus` component, or use `CONNECTION_STRING`.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-sink.kamelet.yaml)