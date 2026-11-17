# ![azure servicebus source](_images/kamelets/azure-servicebus-source.svg) Azure Servicebus Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the messages of a queue, or of a topic subscription, in Azure Service Bus, one message each.

Use it to process work or events that other applications send through Service Bus. To read new blobs from Event Grid events that arrive in a Service Bus queue, use `azure-storage-blob-event-based-source`.

Output: the body is the body of the Service Bus message, as bytes. The headers give its ID (`CamelAzureServiceBusMessageId`), its custom properties (`CamelAzureServiceBusApplicationProperties`, a Map), its content type, correlation ID, subject, enqueued time and delivery count.

Good to know: with the default `serviceBusReceiveMode` of `PEEK_LOCK`, a message is removed only once it has been processed; a message whose processing fails is given back and received again, until Service Bus moves it to the dead-letter queue after the maximum delivery count (10 by default). With `RECEIVE_AND_DELETE`, a message is removed as soon as it is received, so a failure loses it. For a topic, set `serviceBusType` to `topic` and `subscriptionName`.

## Configuration Options

The following table summarizes the configuration options available for the `azure-servicebus-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **connectionString** | Connection String | **Required** The connection string of the Service Bus namespace, from the Azure portal: the namespace, then Settings, Shared access policies, a policy, Primary Connection String. It starts with `Endpoint=sb://`. | string |  |  |
| **topicOrQueueName** | Topic or Queue Name | **Required** The name of the queue, or of the topic, to receive the messages from. For a topic, also set `serviceBusType` to `topic` and `subscriptionName`. | string |  | orders |
| **credentialType** | Credential Type | How to log in to Service Bus. Keep `CONNECTION_STRING`, the default, which uses `connectionString`. `AZURE_IDENTITY` and `TOKEN_CREDENTIAL` also need the `fullyQualifiedNamespace` of the Camel component, which this Kamelet does not set. Enum values: \* AZURE\_IDENTITY \* CONNECTION\_STRING \* TOKEN\_CREDENTIAL | string | CONNECTION\_STRING |  |
| **serviceBusReceiveMode** | Service Bus Receive Mode | `PEEK_LOCK`, the default, removes a message only once it has been processed, and gives it back when processing fails. `RECEIVE_AND_DELETE` removes each message as soon as it is received, so a message whose processing fails is lost. Enum values: \* PEEK\_LOCK \* RECEIVE\_AND\_DELETE | string | PEEK\_LOCK |  |
| **serviceBusType** | Service Bus Type | Whether `topicOrQueueName` is a `queue` or a `topic`. Enum values: \* queue \* topic | string | queue |  |
| **subscriptionName** | Subscription Name | The name of the subscription of the topic to receive from. Required when `serviceBusType` is `topic`; not used for a queue. | string |  | all-orders |

## Dependencies

At runtime, the `azure-servicebus-source` Kamelet relies upon the presence of the following dependencies:

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

`AZURE_IDENTITY` and `TOKEN_CREDENTIAL` also need the fully qualified namespace of Service Bus, which this Kamelet does not set: configure the `fullyQualifiedNamespace` option of the Camel `azure-servicebus` component, or use `CONNECTION_STRING`.

### Topic vs Queue

The subscribtion name parameter needs to be populated in case of consuming from a Topic, while it’s not required in case of Queue.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-source.kamelet.yaml)