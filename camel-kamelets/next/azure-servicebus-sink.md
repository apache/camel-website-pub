# ![azure servicebus sink](_images/kamelets/azure-servicebus-sink.svg) Azure Servicebus Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a queue or a topic in Azure Service Bus, the Azure message broker.

Use it to hand work or events to other applications through Service Bus, such as orders to process, or notifications for all the subscribers of a topic, now or after a delay. For simple storage queues, use `azure-storage-queue-sink`.

Input: the body is sent as text: text, bytes or a stream are read as text, so bytes that are not UTF-8 text, such as an image, are damaged. With `binary` set to `true`, the body is sent as bytes, exactly as they are, and text as its UTF-8 bytes. A Map is sent as its text form, so turn it into JSON text first, for example with `json-serialize-action`; with `binary`, a Map cannot be sent at all. A List is sent as one message per element. The optional `CamelAzureServiceBusApplicationProperties` header, a Map, sets the custom properties of the message.

Output: the message is unchanged.

Good to know: the shared access policy of the connection string needs the Send right. Headers that start with `CamelAzureServiceBus`, except `CamelAzureServiceBusApplicationProperties`, are removed from the message first, so they cannot change what the Kamelet does.

A queue created with sessions enabled accepts only messages with a session ID: without one, the send fails. A topic accepts them, but each of its subscriptions with sessions enabled moves them to its dead-letter queue. Set `sessionId` to send every message with that session ID; a reader of the queue or subscription then receives the messages of the session in the order they were sent. The session ID is fixed for the Kamelet: the `CamelAzureServiceBusSessionId` header is not read, so messages that must go to different sessions need one sink for each session ID.

Set `scheduledEnqueueDelay` to have Service Bus hold each message for that many seconds before readers can receive it, for example to send a reminder. The delay is the same for every message, and counts from the clock of the integration.

To log in with an Azure identity instead of a connection string, set `credentialType` to `AZURE_IDENTITY` and `fullyQualifiedNamespace`, and leave `connectionString` unset.

## Configuration Options

The following table summarizes the configuration options available for the `azure-servicebus-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **topicOrQueueName** | Topic or Queue Name | **Required** The name of the queue, or of the topic, to send the messages to. For a topic, set `serviceBusType` to `topic`. | string |  | orders |
| **binary** | Binary | Set to `true` to send the body as bytes, exactly as they are, such as an image or a compressed file. When unset, the body is sent as text, and bytes that are not UTF-8 text are damaged. Text is sent as its UTF-8 bytes either way. With `binary`, a Map body fails to send, so turn it into JSON text first. | boolean |  |  |
| **connectionString** | Connection String | The connection string of the Service Bus namespace, from the Azure portal: the namespace, then Settings, Shared access policies, a policy, Primary Connection String. It starts with `Endpoint=sb://`. Required with the default `credentialType`, `CONNECTION_STRING`. | string |  |  |
| **credentialType** | Credential Type | How to log in to Service Bus. `CONNECTION_STRING`, the default, uses `connectionString`. `AZURE_IDENTITY` uses the Azure identity of the environment, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables, a managed identity or the Azure CLI login, and needs `fullyQualifiedNamespace`. `TOKEN_CREDENTIAL` also needs `fullyQualifiedNamespace`, and a `com.azure.core.credential.TokenCredential` bean in the Camel registry. Enum values: \* AZURE\_IDENTITY \* CONNECTION\_STRING \* TOKEN\_CREDENTIAL | string | CONNECTION\_STRING |  |
| **fullyQualifiedNamespace** | Fully Qualified Namespace | The host name of the Service Bus namespace, such as `my-namespace.servicebus.windows.net`, without `sb://` or `https://`. Required with `credentialType` `AZURE_IDENTITY` or `TOKEN_CREDENTIAL`; not used with `CONNECTION_STRING`, where the connection string names the namespace. | string |  | my-namespace.servicebus.windows.net |
| **scheduledEnqueueDelay** | Scheduled Enqueue Delay | How many seconds Service Bus holds each message before readers can receive it. The message is accepted at once, and appears in the queue or topic once the delay is over, with that time as its enqueued time. When unset, the message can be received straight away. | integer |  | 600 |
| **serviceBusType** | Service Bus Type | Whether `topicOrQueueName` is a `queue` or a `topic`. Enum values: \* queue \* topic | string | queue |  |
| **sessionId** | Session ID | The session ID to send every message with, up to 128 characters, kept as written. Required to send to a queue, or to a topic subscription, with sessions enabled; a reader receives the messages of one session in the order they were sent. A queue without sessions accepts the session ID too, and ignores it. | string |  | customer-42 |

## Dependencies

At runtime, the `azure-servicebus-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:azure-servicebus
    
-   camel:bean
    
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

`AZURE_IDENTITY` and `TOKEN_CREDENTIAL` also need **fullyQualifiedNamespace**, the host name of the Service Bus namespace, such as `my-namespace.servicebus.windows.net`. Leave **connectionString** unset with them.

### Example with a Session ID

A queue created with sessions enabled accepts only messages with a session ID; without one, the send fails with `The SessionId was not set on a message`. A topic accepts them, but each of its subscriptions with sessions enabled moves them to its dead-letter queue. Set **sessionId** to send every message with that session ID:

```yaml
- route:
    from:
      uri: "timer:tick"
      parameters:
        period: 60000
      steps:
        - setBody:
            constant: "order-1"
        - to:
            uri: "kamelet:azure-servicebus-sink"
            parameters:
              topicOrQueueName: "orders"
              connectionString: "{{servicebus.connection-string}}"
              sessionId: "customer-42"
```

A reader of the queue receives the messages of a session in the order they were sent. The session ID is fixed for the Kamelet; the `CamelAzureServiceBusSessionId` header is not read. To spread messages over several sessions, use one sink for each session ID, for example behind a content-based router.

### Example Sending Binary Data

The body is sent as text, so bytes that are not UTF-8 text, such as an image or a compressed file, are damaged. Set **binary** to `true` to send the bytes exactly as they are:

```yaml
- route:
    from:
      uri: "file:/data/images"
      steps:
        - to:
            uri: "kamelet:azure-servicebus-sink"
            parameters:
              topicOrQueueName: "images"
              connectionString: "{{servicebus.connection-string}}"
              binary: true
```

Text is sent as its UTF-8 bytes either way. With **binary**, a Map body fails to send: turn it into JSON text first, for example with `json-serialize-action`.

### Example with a Delay

Set **scheduledEnqueueDelay** to have Service Bus hold each message for that many seconds before readers can receive it:

```yaml
- route:
    from:
      uri: "timer:tick"
      parameters:
        period: 60000
      steps:
        - setBody:
            constant: "Your order is ready for pickup"
        - to:
            uri: "kamelet:azure-servicebus-sink"
            parameters:
              topicOrQueueName: "reminders"
              connectionString: "{{servicebus.connection-string}}"
              scheduledEnqueueDelay: 600
```

The send returns at once, and the message appears in the queue ten minutes later, with that time as its enqueued time (`CamelAzureServiceBusEnqueuedTime` for a reader). The delay is the same for every message, and counts from the clock of the integration.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/azure-servicebus-sink.kamelet.yaml)