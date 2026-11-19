# ![azure servicebus source](_images/kamelets/azure-servicebus-source.svg) Azure Servicebus Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the messages of a queue, or of a topic subscription, in Azure Service Bus, one message each.

Use it to process work or events that other applications send through Service Bus, one at a time or several at once, including a queue with sessions, or to read the messages that Service Bus has dead-lettered. To read new blobs from Event Grid events that arrive in a Service Bus queue, use `azure-storage-blob-event-based-source`.

Output: the body is the body of the Service Bus message, as bytes. The headers give its ID (`CamelAzureServiceBusMessageId`), its custom properties (`CamelAzureServiceBusApplicationProperties`, a Map), its content type, correlation ID, subject, enqueued time and delivery count, its session ID (`CamelAzureServiceBusSessionId`) when it was sent with one, and, for a dead-lettered message, why it was dead-lettered (`CamelAzureServiceBusDeadLetterReason` and `CamelAzureServiceBusDeadLetterErrorDescription`).

Good to know: with the default `serviceBusReceiveMode` of `PEEK_LOCK`, a message is removed only once it has been processed; a message whose processing fails is given back and received again, until Service Bus moves it to the dead-letter queue after the maximum delivery count (10 by default). With `enableDeadLettering` set to `true`, it is moved to the dead-letter queue straight away instead, with the exception as the reason, such as `java.lang.IllegalStateException: Invalid order`. With `RECEIVE_AND_DELETE`, a message is removed as soon as it is received, so a failure loses it. For a topic, set `serviceBusType` to `topic` and `subscriptionName`.

The messages are processed one at a time, in the order they arrive, unless a step of the integration works asynchronously, such as a delay. With `maxConcurrentCalls` set above 1, that many are processed at the same time, in no particular order.

A queue or subscription created with sessions enabled can be read only with `sessionEnabled` set to `true`: without it, the integration starts but receives nothing, and logs a warning from Service Bus every few seconds (`It is not possible for an entity that requires sessions to create a non-sessionful message receiver`). With sessions, the messages of one session are received in the order they were sent, and the next one only once the previous one has been processed, unless a step of the integration works asynchronously, such as a delay. A message whose processing fails is received again before the next one of its session, unless `enableDeadLettering` moves it to the dead-letter queue. `maxConcurrentSessions` sessions, 1 by default, are read at the same time; the messages of different sessions have no order between them. `maxConcurrentCalls` counts for each session: above 1, the messages of one session are processed at the same time too, and lose their order.

To read the dead-letter queue, set `subQueue` to `DEAD_LETTER_QUEUE`, and leave `sessionEnabled` unset even when the queue has sessions, because the dead-letter queue has none. A dead-lettered message whose processing fails is not moved anywhere else: it is given back and received again straight away, over and over, and holds up the dead letters behind it.

To log in with an Azure identity instead of a connection string, set `credentialType` to `AZURE_IDENTITY` and `fullyQualifiedNamespace`, and leave `connectionString` unset.

## Configuration Options

The following table summarizes the configuration options available for the `azure-servicebus-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **topicOrQueueName** | Topic or Queue Name | **Required** The name of the queue, or of the topic, to receive the messages from. For a topic, also set `serviceBusType` to `topic` and `subscriptionName`. | string |  | orders |
| **connectionString** | Connection String | The connection string of the Service Bus namespace, from the Azure portal: the namespace, then Settings, Shared access policies, a policy, Primary Connection String. It starts with `Endpoint=sb://`. Required with the default `credentialType`, `CONNECTION_STRING`. | string |  |  |
| **credentialType** | Credential Type | How to log in to Service Bus. `CONNECTION_STRING`, the default, uses `connectionString`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login, and needs `fullyQualifiedNamespace`. `TOKEN_CREDENTIAL` also needs `fullyQualifiedNamespace`, and a `com.azure.core.credential.TokenCredential` bean in the Camel registry. Enum values: \* AZURE\_IDENTITY \* CONNECTION\_STRING \* TOKEN\_CREDENTIAL | string | CONNECTION\_STRING |  |
| **enableDeadLettering** | Enable Dead Lettering | Set to `true` to move a message whose processing fails to the dead-letter queue straight away, instead of giving it back to be received again until the maximum delivery count of the queue is reached. The dead-lettered message has the exception as its reason (`CamelAzureServiceBusDeadLetterReason` when read back), such as `java.lang.IllegalStateException: Invalid order`, and its stack trace as the error description. Works only with the default `serviceBusReceiveMode`, `PEEK_LOCK`. While reading a dead-letter queue with `subQueue`, it does nothing: a failing dead letter is still received again. | boolean |  |  |
| **fullyQualifiedNamespace** | Fully Qualified Namespace | The host name of the Service Bus namespace, such as `my-namespace.servicebus.windows.net`, without `sb://` or `https://`. Required with `credentialType` `AZURE_IDENTITY` or `TOKEN_CREDENTIAL`; not used with `CONNECTION_STRING`, where the connection string names the namespace. | string |  | my-namespace.servicebus.windows.net |
| **maxConcurrentCalls** | Max Concurrent Calls | How many messages are processed at the same time, 1 when unset. Above 1, the messages are no longer processed in the order they arrive. With `sessionEnabled`, it counts for each session, so the messages of one session are processed at the same time too, and lose the order that sessions otherwise keep. | integer |  | 8 |
| **maxConcurrentSessions** | Max Concurrent Sessions | With `sessionEnabled`, how many sessions are read at the same time, 1 when unset. The Kamelet keeps reading a session until it has had no message for a minute, so with 1, the messages of another session wait meanwhile. Messages of the same session are always received one at a time. | integer |  | 8 |
| **serviceBusReceiveMode** | Service Bus Receive Mode | `PEEK_LOCK`, the default, removes a message only once it has been processed, and gives it back when processing fails. `RECEIVE_AND_DELETE` removes each message as soon as it is received, so a message whose processing fails is lost. Enum values: \* PEEK\_LOCK \* RECEIVE\_AND\_DELETE | string | PEEK\_LOCK |  |
| **serviceBusType** | Service Bus Type | Whether `topicOrQueueName` is a `queue` or a `topic`. Enum values: \* queue \* topic | string | queue |  |
| **sessionEnabled** | Sessions Enabled | Set to `true` to read a queue or subscription created with sessions enabled, which can be read no other way. The messages of one session are then received in the order they were sent, one after the other. Leave it unset for a queue or subscription without sessions, and for a dead-letter queue, which cannot be read with it. | boolean |  |  |
| **subQueue** | Sub-Queue | Set to `DEAD_LETTER_QUEUE` to read the dead-letter queue of the queue or subscription, where Service Bus moves the messages that could not be delivered or processed, or to `TRANSFER_DEAD_LETTER_QUEUE` for the messages that could not be forwarded or transferred. Leave it unset to read the queue or subscription itself. Enum values: \* DEAD\_LETTER\_QUEUE \* TRANSFER\_DEAD\_LETTER\_QUEUE | string |  |  |
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

`AZURE_IDENTITY` and `TOKEN_CREDENTIAL` also need **fullyQualifiedNamespace**, the host name of the Service Bus namespace, such as `my-namespace.servicebus.windows.net`. Leave **connectionString** unset with them.

### Topic vs Queue

The subscribtion name parameter needs to be populated in case of consuming from a Topic, while it’s not required in case of Queue.

### Example with Sessions

A queue or subscription created with sessions enabled can be read only with **sessionEnabled** set to `true`. Without it, the integration receives nothing and logs a warning every few seconds: `It is not possible for an entity that requires sessions to create a non-sessionful message receiver`. A queue without sessions cannot be read with it.

```yaml
- route:
    from:
      uri: "kamelet:azure-servicebus-source"
      parameters:
        topicOrQueueName: "orders"
        connectionString: "{{servicebus.connection-string}}"
        sessionEnabled: true
        maxConcurrentSessions: 8
      steps:
        - log: "Order ${body} of session $\{header.CamelAzureServiceBusSessionId}"
```

The messages of one session are received in the order they were sent, and the next one only once the previous one has been processed (unless a step of the integration works asynchronously, such as a delay). A message whose processing fails is received again before the next one of its session. Different sessions are read at the same time, up to **maxConcurrentSessions**, 1 by default, and have no order between them. A session is kept until it has had no message for a minute: with the default of 1, the messages of another session wait meanwhile.

### Example Reading the Dead-Letter Queue

Service Bus moves a message to the dead-letter queue of its queue or subscription, for example once its processing has failed the maximum delivery count of times. Set **subQueue** to `DEAD_LETTER_QUEUE` to read them:

```yaml
- route:
    from:
      uri: "kamelet:azure-servicebus-source"
      parameters:
        topicOrQueueName: "orders"
        connectionString: "{{servicebus.connection-string}}"
        subQueue: "DEAD_LETTER_QUEUE"
      steps:
        - log: "Dead letter ${body}: $\{header.CamelAzureServiceBusDeadLetterReason} - $\{header.CamelAzureServiceBusDeadLetterErrorDescription}"
```

The dead-letter queue has no sessions, so leave **sessionEnabled** unset, even for a queue with sessions. A dead-lettered message whose processing fails stays where it is: it is received again straight away, over and over, and holds up the dead letters behind it. `TRANSFER_DEAD_LETTER_QUEUE` reads the messages that could not be forwarded or transferred instead.

### Example Processing Messages in Parallel

The messages are processed one at a time, in the order they arrive, unless a step of the integration works asynchronously, such as a delay. Set **maxConcurrentCalls** to process that many at the same time, for example when each message calls a slow service:

```yaml
- route:
    from:
      uri: "kamelet:azure-servicebus-source"
      parameters:
        topicOrQueueName: "orders"
        connectionString: "{{servicebus.connection-string}}"
        maxConcurrentCalls: 5
      steps:
        - to: "http://order-service/orders"
```

With 5, ten messages that take a second each are processed in about two seconds instead of ten, and in no particular order. With **sessionEnabled**, **maxConcurrentCalls** counts for each session: above 1, the messages of one session are processed at the same time too, and lose their order.

### Example Dead-Lettering Failed Messages

By default, a message whose processing fails is given back and received again, until Service Bus moves it to the dead-letter queue after the maximum delivery count of the queue (10 by default). Set **enableDeadLettering** to `true` to move it there straight away:

```yaml
- route:
    from:
      uri: "kamelet:azure-servicebus-source"
      parameters:
        topicOrQueueName: "orders"
        connectionString: "{{servicebus.connection-string}}"
        enableDeadLettering: true
      steps:
        - to: "http://order-service/orders"
```

The dead-lettered message has the exception as its reason, such as `java.lang.IllegalStateException: Invalid order`, and its stack trace as the error description; read them back with **subQueue** set to `DEAD_LETTER_QUEUE`, in the `CamelAzureServiceBusDeadLetterReason` and `CamelAzureServiceBusDeadLetterErrorDescription` headers. It works only with the default **serviceBusReceiveMode**, `PEEK_LOCK`, and does nothing while reading the dead-letter queue itself.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-source.kamelet.yaml)