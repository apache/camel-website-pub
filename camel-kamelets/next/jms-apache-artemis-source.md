# ![jms apache artemis source](_images/kamelets/jms-apache-artemis-source.svg) JMS - Apache Artemis Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message from a queue or a topic in an Apache ActiveMQ Artemis broker, through JMS.

Use it to process work that other applications put on a queue, such as orders or jobs, or to react to events published on a topic. For another broker that speaks AMQP 1.0, use `jms-amqp-10-source`.

Output: the body is text for a JMS text message, bytes for a bytes message, and a Map for a map message. The JMS properties of the message become headers, along with the JMS headers such as `JMSMessageID`, `JMSDestination`, `JMSTimestamp`, `JMSPriority` and `JMSRedelivered`.

Good to know: From a queue, each message is removed when it is received, even when the rest of the flow then fails, unless `transacted` is true or `acknowledgementModeName` is `CLIENT_ACKNOWLEDGE`: then a message whose flow failed is delivered again. Several copies of this source share the messages of a queue, and `concurrentConsumers` processes several messages at the same time. From a topic (`destinationType` set to `topic`), it receives only the messages sent while it is connected, unless `subscriptionDurable` is true: then the broker keeps the messages sent while it is stopped, under `subscriptionName`. A durable subscription needs `clientId` unless it is shared (`subscriptionShared`, JMS 2.0), and only one connection may use a client ID at a time. With `selector`, it receives only the messages whose properties and headers match the selector. It connects with no TLS unless `brokerURL` asks for it, and logs in with `username` and `password` when they are set. When the broker cannot be reached, it starts anyway and tries again every 5 seconds.

## Configuration Options

The following table summarizes the configuration options available for the `jms-apache-artemis-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The address of the Artemis broker, as `tcp://host:port`; the usual port is 61616. Add `?sslEnabled=true` for TLS. A broker that needs a login takes it in the URL too, as `tcp://host:61616?user=app&password=secret`. | string |  | tcp://localhost:61616 |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to receive the messages from. | string |  | orders |
| **acknowledgementModeName** | Acknowledgement Mode | When the source acknowledges each message to the broker, which then removes it from the queue. `AUTO_ACKNOWLEDGE`: as soon as the message is received. `CLIENT_ACKNOWLEDGE`: once the rest of the flow has processed it; when the flow fails, the broker delivers it again, as with `transacted`, and moves it to the dead letter queue after the number of attempts set in the broker. `DUPS_OK_ACKNOWLEDGE`: in batches, which is faster, but the messages processed since the last batch are delivered again when the source stops without closing its connection, such as in a crash. Not used when `transacted` is true. When it is not set, `AUTO_ACKNOWLEDGE`. Enum values: \* AUTO\_ACKNOWLEDGE \* CLIENT\_ACKNOWLEDGE \* DUPS\_OK\_ACKNOWLEDGE | string |  |  |
| **clientId** | Client ID | The JMS client ID of the connection, which names this application to the broker. A durable subscription that is not shared needs one: the broker keeps the subscription under the client ID and `subscriptionName`, so use the same client ID each time the source starts. Only one connection may use a client ID at a time: two running copies of this source need different client IDs. When it is not set, the connection has no client ID. | string |  | orders-service |
| **concurrentConsumers** | Concurrent Consumers | How many messages the source processes at the same time, each in a thread of its own. From a queue, more than one makes the source faster when each message takes a while, but the messages are then no longer processed in the order of the queue. On a topic, each consumer is a subscription of its own and receives every message, so each message is processed that many times, unless `subscriptionShared` is true; a durable subscription that is not shared takes only one consumer. When it is not set, one message at a time. | integer |  | 5 |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **password** | Broker Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **selector** | Message Selector | A JMS message selector: the source receives only the messages that match it. It is a condition, in a syntax like the WHERE clause of SQL, on the JMS properties and headers of the message, not on its body, such as `priority > 5` or `region = 'EU' AND JMSPriority >= 7`. From a queue, the messages that do not match stay on the queue. When it is not set, the source receives every message. | string |  | priority > 5 |
| **subscriptionDurable** | Durable Subscription | Whether the subscription to a topic is durable. When it is true, the broker keeps the messages sent to the topic while this source is stopped or disconnected, and delivers them when it connects again; the broker keeps the subscription, and collects messages for it, until it is removed in the broker. Set `subscriptionName` with it, and `clientId` unless `subscriptionShared` is true. When it is false, the messages sent while the source is not connected are lost. Only for a topic: true makes `destinationName` a topic, even with `destinationType` set to `queue`. | boolean | false |  |
| **subscriptionName** | Subscription Name | The name of the durable or shared subscription to a topic, under which the broker keeps the subscription. Use the same name each time the source starts, to receive the messages kept while it was stopped. Set it whenever `subscriptionDurable` or `subscriptionShared` is true: without it, every source takes the same default name, so two sources with the same client ID, or two shared sources, take over one another’s subscription. Not used otherwise. | string |  | orders-audit |
| **subscriptionShared** | Shared Subscription | Whether the subscription to a topic is shared: the copies of this source that use the same `subscriptionName` share the messages of the topic, each message going to one of them, instead of each copy receiving every message. A shared subscription needs no `clientId`. Combine it with `subscriptionDurable` for a durable subscription that several copies share. Needs a broker that supports JMS 2.0. Only for a topic: true makes `destinationName` a topic, even with `destinationType` set to `queue`. | boolean | false |  |
| **transacted** | Transacted | Whether each message is received in a JMS transaction, which is committed once the rest of the flow has processed the message. When the flow fails, the transaction is rolled back and the broker delivers the message again, with the header `JMSRedelivered` true; after the number of attempts set in the broker (10 by default), the broker moves it to the dead letter queue (`DLQ` by default). When it is not set, the message is removed from the queue when it is received, even when the flow then fails. | boolean |  |  |
| **username** | Broker Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. | string |  |  |

## Dependencies

At runtime, the `jms-apache-artemis-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:kamelet
    
-   mvn:org.apache.activemq:artemis-jakarta-client-all:2.57.0
    

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
      uri: "kamelet:jms-apache-artemis-source"
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

## JMS Apache Artemis Source Kamelet Description

### Authentication

A broker that needs a login takes it in the `username` and `password` options. Without them, the Kamelet connects with no login.

### Configuration

The JMS Apache Artemis Source Kamelet supports the following configurations:

-   **Broker URL**: Apache Artemis broker URL (required)
    
-   **Destination Name**: JMS destination (queue or topic) name (required)
    
-   **Destination Type**: Type of destination - queue or topic (default: queue)
    
-   **Username** and **Password**: the login to the broker, when it needs one
    
-   **Durable Subscription**, **Shared Subscription**, **Subscription Name** and **Client ID**: a durable or shared subscription to a topic (see below)
    
-   **Message Selector**: receive only the messages that match a condition on their properties and headers
    
-   **Transacted**, **Acknowledgement Mode** and **Concurrent Consumers**: delivering a message again when its flow fails, and processing several messages at the same time (see below)
    

### Output Format

The Kamelet outputs JMS messages including message body, headers, and JMS properties. The body is text for a text message, bytes for a bytes message, and a Map for a map message.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:jms-apache-artemis-source"
      parameters:
        brokerURL: "tcp://artemis.example.com:61616"
        destinationName: "orders.queue"
        destinationType: "queue"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Topic Subscription

By default, the source receives only the messages published to the topic while it is connected.

```yaml
- route:
    from:
      uri: "kamelet:jms-apache-artemis-source"
      parameters:
        brokerURL: "tcp://artemis.example.com:61616"
        username: "artemisuser"
        password: "artemispass"
        destinationName: "events.topic"
        destinationType: "topic"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with a Durable Topic Subscription

With `subscriptionDurable` set to `true`, the broker keeps the messages published to the topic while the source is stopped, and delivers them when it starts again. The broker keeps the subscription under the client ID and the subscription name, so use the same `clientId` and `subscriptionName` each time the source starts.

```yaml
- route:
    from:
      uri: "kamelet:jms-apache-artemis-source"
      parameters:
        brokerURL: "tcp://artemis.example.com:61616"
        username: "artemisuser"
        password: "artemispass"
        destinationName: "events.topic"
        destinationType: "topic"
        subscriptionDurable: true
        subscriptionName: "audit"
        clientId: "audit-service"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The JMS rules to know:

-   A durable subscription that is not shared needs a `clientId`. Without one, the source starts but receives nothing, and logs that the client ID is not set.
    
-   Only one connection may use a client ID at a time. A second copy of the source with the same `clientId` receives nothing, and logs that the client ID is already in use.
    
-   To run several copies of the source on one durable subscription, set `subscriptionShared` to `true` as well, and leave `clientId` empty: the copies share the messages of the topic by `subscriptionName`, each message going to one of them. Shared subscriptions are part of JMS 2.0.
    
-   The durable subscription stays on the broker, and keeps collecting messages, until it is removed in the broker.
    

### Example with a Message Selector

The source receives only the messages that match `selector`, a condition on the JMS properties and headers of the message. From a queue, the other messages stay on the queue.

```yaml
- route:
    from:
      uri: "kamelet:jms-apache-artemis-source"
      parameters:
        brokerURL: "tcp://artemis.example.com:61616"
        destinationName: "orders.queue"
        selector: "priority > 5"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Redelivery when the flow fails

By default, the source removes each message from the queue when it receives it, so a message whose flow fails is lost. With `transacted` set to `true`, each message is received in a transaction that is committed only once the flow has processed it. When the flow fails, the transaction is rolled back and the broker delivers the message again, with the header `JMSRedelivered` set to `true`.

After 10 attempts, the default of the broker (`max-delivery-attempts`), Artemis moves the message to the dead letter queue, `DLQ` by default.

`concurrentConsumers` processes several messages of the queue at the same time, each in a thread of its own; the messages are then no longer processed in the order of the queue.

```yaml
- route:
    from:
      uri: "kamelet:jms-apache-artemis-source"
      parameters:
        brokerURL: "tcp://artemis.example.com:61616"
        destinationName: "orders.queue"
        transacted: true
        concurrentConsumers: 5
      steps:
        - to:
            uri: "kamelet:log-sink"
```

`acknowledgementModeName` set to `CLIENT_ACKNOWLEDGE` also delivers a message again when its flow fails, without a transaction. `DUPS_OK_ACKNOWLEDGE` acknowledges the messages in batches: it is faster, but the messages processed since the last batch are delivered again after a crash.

### Connection Management

When the broker cannot be reached, the Kamelet starts anyway and tries to connect again every 5 seconds. It does not pool connections, and does not need to: it keeps its connection open while it receives.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-source.kamelet.yaml)