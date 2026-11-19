# ![jms amqp 10 source](_images/kamelets/jms-amqp-10-source.svg) JMS - AMQP 1.0 Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message from a queue or a topic in a message broker that speaks AMQP 1.0, such as Apache ActiveMQ Artemis, through JMS and the Apache Qpid client.

Use it to process work that other applications put on a queue, or to react to events published on a topic, on any broker that supports the AMQP 1.0 protocol. For an Artemis broker, `jms-apache-artemis-source` works too.

Output: the body is text for a JMS text message, bytes for a bytes message, and a Map for a map message. The JMS properties of the message become headers, along with the JMS headers such as `JMSMessageID`, `JMSDestination`, `JMSTimestamp`, `JMSPriority` and `JMSRedelivered`.

Good to know: From a queue, each message is removed when it is received, even when the rest of the flow then fails, unless `transacted` is true or `acknowledgementModeName` is `CLIENT_ACKNOWLEDGE`: then a message whose flow failed is delivered again. Several copies of this source share the messages of a queue, and `concurrentConsumers` processes several messages at the same time. From a topic (`destinationType` set to `topic`), it receives only the messages sent while it is connected, unless `subscriptionDurable` is true: then the broker keeps the messages sent while it is stopped, under `subscriptionName`. A durable subscription needs `clientId` unless it is shared (`subscriptionShared`, JMS 2.0), and only one connection may use a client ID at a time. With `selector`, it receives only the messages whose properties and headers match the selector. It logs in with `username` and `password` when they are set; the TLS settings go in `remoteURI`. When the broker cannot be reached, it starts anyway and tries again every 5 seconds.

## Configuration Options

The following table summarizes the configuration options available for the `jms-amqp-10-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to receive the messages from. | string |  | orders |
| **remoteURI** | Broker URL | **Required** The address of the broker, as `amqp://host:port` (the AMQP port is usually 5672), or `amqps://host:port` for TLS. Settings of the Qpid JMS client go after `?`, such as `transport.trustStoreLocation`, `transport.trustStorePassword`, `transport.keyStoreLocation` and `transport.keyStorePassword` for TLS. The login goes in `username` and `password`; `jms.username` and `jms.password` in the address work too. | string |  | amqp://localhost:5672 |
| **acknowledgementModeName** | Acknowledgement Mode | When the source acknowledges each message to the broker, which then removes it from the queue. `AUTO_ACKNOWLEDGE`: as soon as the message is received. `CLIENT_ACKNOWLEDGE`: once the rest of the flow has processed it; when the flow fails, the Qpid client delivers the message to the flow again by itself, with no limit, unless `remoteURI` sets `jms.redeliveryPolicy.maxRedeliveries`. Use `transacted` instead to leave the attempts and the dead letter queue to the broker. `DUPS_OK_ACKNOWLEDGE`: the Qpid client acknowledges each message when it is received, as with `AUTO_ACKNOWLEDGE`. Not used when `transacted` is true. When it is not set, `AUTO_ACKNOWLEDGE`. Enum values: \* AUTO\_ACKNOWLEDGE \* CLIENT\_ACKNOWLEDGE \* DUPS\_OK\_ACKNOWLEDGE | string |  |  |
| **clientId** | Client ID | The JMS client ID of the connection, which names this application to the broker. A durable subscription that is not shared needs one: the broker keeps the subscription under the client ID and `subscriptionName`, so use the same client ID each time the source starts. Only one connection may use a client ID at a time: two running copies of this source need different client IDs. When it is not set, the connection has no client ID. | string |  | orders-service |
| **concurrentConsumers** | Concurrent Consumers | How many messages the source processes at the same time, each in a thread of its own. From a queue, more than one makes the source faster when each message takes a while, but the messages are then no longer processed in the order of the queue. On a topic, each consumer is a subscription of its own and receives every message, so each message is processed that many times, unless `subscriptionShared` is true; a durable subscription that is not shared takes only one consumer. When it is not set, one message at a time. | integer |  | 5 |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **password** | Password | The password to log in to the broker with, for the user `username`. When it is set, it is used instead of `jms.password` in `remoteURI`. | string |  |  |
| **selector** | Message Selector | A JMS message selector: the source receives only the messages that match it. It is a condition, in a syntax like the WHERE clause of SQL, on the JMS properties and headers of the message, not on its body, such as `priority > 5` or `region = 'EU' AND JMSPriority >= 7`. From a queue, the messages that do not match stay on the queue. When it is not set, the source receives every message. | string |  | priority > 5 |
| **subscriptionDurable** | Durable Subscription | Whether the subscription to a topic is durable. When it is true, the broker keeps the messages sent to the topic while this source is stopped or disconnected, and delivers them when it connects again; the broker keeps the subscription, and collects messages for it, until it is removed in the broker. Set `subscriptionName` with it, and `clientId` unless `subscriptionShared` is true. When it is false, the messages sent while the source is not connected are lost. Only for a topic: true makes `destinationName` a topic, even with `destinationType` set to `queue`. | boolean | false |  |
| **subscriptionName** | Subscription Name | The name of the durable or shared subscription to a topic, under which the broker keeps the subscription. Use the same name each time the source starts, to receive the messages kept while it was stopped. Set it whenever `subscriptionDurable` or `subscriptionShared` is true: without it, every source takes the same default name, so two sources with the same client ID, or two shared sources, take over one another’s subscription. Not used otherwise. | string |  | orders-audit |
| **subscriptionShared** | Shared Subscription | Whether the subscription to a topic is shared: the copies of this source that use the same `subscriptionName` share the messages of the topic, each message going to one of them, instead of each copy receiving every message. A shared subscription needs no `clientId`. Combine it with `subscriptionDurable` for a durable subscription that several copies share. Needs a broker that supports JMS 2.0. Only for a topic: true makes `destinationName` a topic, even with `destinationType` set to `queue`. | boolean | false |  |
| **transacted** | Transacted | Whether each message is received in a JMS transaction, which is committed once the rest of the flow has processed the message. When the flow fails, the transaction is rolled back and the broker delivers the message again, with the header `JMSRedelivered` true; after the number of attempts set in the broker (Apache ActiveMQ Artemis: 10 by default), the broker moves it to a dead letter queue (Artemis: `DLQ`). When it is not set, the message is removed from the queue when it is received, even when the flow then fails. | boolean |  |  |
| **username** | Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. When it is set, it is used instead of `jms.username` in `remoteURI`. | string |  |  |

## Dependencies

At runtime, the `jms-amqp-10-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:amqp
    
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
      uri: "kamelet:jms-amqp-10-source"
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

## JMS AMQP 1.0 Source Kamelet Description

### Login and TLS

-   A login: `username` and `password`. `jms.username` and `jms.password` in `remoteURI`, as `amqp://broker.example.com:5672?jms.username=app&jms.password=secret`, work too, but `username` and `password` are used instead of them when they are set.
    
-   TLS: the `amqps://` scheme in `remoteURI`, with `transport.trustStoreLocation` and `transport.trustStorePassword` after `?` when the broker certificate is not trusted by the Java runtime.
    

### Output format

The body is text for a JMS text message, bytes for a bytes message, and a Map for a map message. The JMS properties of the message become headers.

### Configuration

The Kamelet requires connection parameters for the AMQP 1.0 broker:

-   `remoteURI`: the address of the broker
    
-   `username` and `password`: the login, when the broker needs one
    
-   `destinationName`: the name of the queue or topic
    
-   `destinationType`: `queue` (the default) or `topic`
    
-   `subscriptionDurable`, `subscriptionShared`, `subscriptionName` and `clientId`: a durable or shared subscription to a topic (see below)
    
-   `selector`: receive only the messages that match a condition on their properties and headers
    
-   `transacted`, `acknowledgementModeName` and `concurrentConsumers`: delivering a message again when its flow fails, and processing several messages at the same time (see below)
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:jms-amqp-10-source"
      parameters:
        remoteURI: "amqp://broker.example.com:5672"
        username: "app"
        password: "secret"
        destinationName: "my-queue"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Durable topic subscription

From a topic, the source receives by default only the messages published while it is connected. With `subscriptionDurable` set to `true`, the broker keeps the messages published while the source is stopped, and delivers them when it starts again. The broker keeps the subscription under the client ID and the subscription name, so use the same `clientId` and `subscriptionName` each time the source starts.

```yaml
- route:
    from:
      uri: "kamelet:jms-amqp-10-source"
      parameters:
        remoteURI: "amqp://broker.example.com:5672?jms.username=app&jms.password=secret"
        destinationName: "events"
        destinationType: "topic"
        subscriptionDurable: true
        subscriptionName: "audit"
        clientId: "audit-service"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The JMS rules to know:

-   A durable subscription that is not shared needs a `clientId`. Without one, the source starts but receives nothing, and logs that a client ID must be set.
    
-   Only one connection may use a client ID at a time: two running copies of the source need different client IDs.
    
-   To run several copies of the source on one durable subscription, set `subscriptionShared` to `true` as well, and leave `clientId` empty: the copies share the messages of the topic by `subscriptionName`, each message going to one of them. Shared subscriptions are part of JMS 2.0.
    
-   The durable subscription stays on the broker, and keeps collecting messages, until it is removed in the broker.
    

### Message selector

With `selector`, the source receives only the messages that match it, a condition on the JMS properties and headers of the message, such as `priority > 5`. From a queue, the other messages stay on the queue.

### Redelivery when the flow fails

By default, the source removes each message from the queue when it receives it, so a message whose flow fails is lost. With `transacted` set to `true`, each message is received in a transaction that is committed only once the flow has processed it. When the flow fails, the transaction is rolled back and the broker delivers the message again, with the header `JMSRedelivered` set to `true`.

The broker decides how many times: Apache ActiveMQ Artemis moves the message to the dead letter queue, `DLQ`, after 10 attempts by default.

`concurrentConsumers` processes several messages of the queue at the same time, each in a thread of its own; the messages are then no longer processed in the order of the queue.

```yaml
- route:
    from:
      uri: "kamelet:jms-amqp-10-source"
      parameters:
        remoteURI: "amqp://broker.example.com:5672"
        username: "app"
        password: "secret"
        destinationName: "orders.queue"
        transacted: true
        concurrentConsumers: 5
      steps:
        - to:
            uri: "kamelet:log-sink"
```

`acknowledgementModeName` set to `CLIENT_ACKNOWLEDGE` also delivers a message again when its flow fails, without a transaction, but the Qpid client does it by itself, with no limit, unless `remoteURI` sets `jms.redeliveryPolicy.maxRedeliveries`. Prefer `transacted`, which leaves the attempts and the dead letter queue to the broker. With the Qpid client, `DUPS_OK_ACKNOWLEDGE` acknowledges each message when it is received, as `AUTO_ACKNOWLEDGE` does.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-source.kamelet.yaml)