# ![jms apache activemq source](_images/kamelets/jms-apache-activemq-source.svg) JMS - Apache ActiveMQ Classic Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message from a queue or a topic in an Apache ActiveMQ Classic broker, through JMS over OpenWire.

Use it to process work that other applications put on a queue, such as orders or jobs, or to react to events published on a topic. For an Apache ActiveMQ Artemis broker, use `jms-apache-artemis-source`; for another broker that speaks AMQP 1.0, use `jms-amqp-10-source`.

Output: the body is text for a JMS text message, bytes for a bytes message, and a Map for a map message. The JMS properties of the message become headers, along with the JMS headers such as `JMSMessageID`, `JMSDestination`, `JMSTimestamp`, `JMSPriority` and `JMSRedelivered`.

Good to know: From a queue, each message is removed when it is received, even when the rest of the flow then fails, unless `transacted` is true or `acknowledgementModeName` is `CLIENT_ACKNOWLEDGE`: then a message whose flow failed is delivered again, up to 6 more times, and then moved to the dead letter queue `ActiveMQ.DLQ`. Several copies of this source share the messages of a queue, and `concurrentConsumers` processes several messages at the same time. From a topic (`destinationType` set to `topic`), it receives only the messages sent while it is connected, unless `subscriptionDurable` is true: then the broker keeps the messages sent while it is stopped, under `clientId` and `subscriptionName`. ActiveMQ Classic has no shared subscriptions (JMS 2.0), so each copy of the source on a topic receives every message. With `selector`, it receives only the messages whose properties and headers match the selector. It connects with no TLS unless `brokerURL` starts with `ssl://`, and logs in with `username` and `password` when they are set. When the broker cannot be reached, or refuses the login, it starts anyway and tries again every 5 seconds. An answer is sent only when the incoming message has a `JMSReplyTo`, the queue on which its sender waits for one: the message at the end of the flow then goes back to that queue, as the reply. Headers set during the flow, such as `JMSReplyTo` or `CamelJmsDestinationName`, cannot send the answer to another queue, nor make one for a message without `JMSReplyTo`.

## Configuration Options

The following table summarizes the configuration options available for the `jms-apache-activemq-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The address of the ActiveMQ Classic broker, as `tcp://host:port`; the usual port is 61616. Use `ssl://host:port` for TLS, to a TLS connector of the broker (often on port 61617). For several brokers, `failover:(tcp://broker1:61616,tcp://broker2:61616)` connects to one of them, moves to another when it fails, and keeps trying while none can be reached. | string |  | tcp://localhost:61616 |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to receive the messages from. | string |  | orders |
| **acknowledgementModeName** | Acknowledgement Mode | When the source acknowledges each message to the broker, which then removes it from the queue. `AUTO_ACKNOWLEDGE`: as soon as the message is received. `CLIENT_ACKNOWLEDGE`: once the rest of the flow has processed it; when the flow fails, the message is delivered again, as with `transacted`, and moved to the dead letter queue `ActiveMQ.DLQ` after 6 more attempts. `DUPS_OK_ACKNOWLEDGE`: in batches, which is faster, but the messages processed since the last batch are delivered again when the source stops without closing its connection, such as in a crash. Not used when `transacted` is true. When it is not set, `AUTO_ACKNOWLEDGE`. Enum values: \* AUTO\_ACKNOWLEDGE \* CLIENT\_ACKNOWLEDGE \* DUPS\_OK\_ACKNOWLEDGE | string |  |  |
| **clientId** | Client ID | The JMS client ID of the connection, which names this application to the broker. A durable subscription needs one: the broker keeps the subscription under the client ID and `subscriptionName`, so use the same client ID each time the source starts; without one, a durable subscription is refused, and the source logs the error and tries again every 5 seconds. Only one connection may use a client ID at a time: two running copies of this source need different client IDs. When it is not set, the connection has no client ID. | string |  | orders-service |
| **concurrentConsumers** | Concurrent Consumers | How many messages the source processes at the same time, each in a thread of its own. From a queue, more than one makes the source faster when each message takes a while, but the messages are then no longer processed in the order of the queue. On a topic, each consumer is a subscription of its own and receives every message, so each message is processed that many times; a durable subscription takes only one consumer. When it is not set, one message at a time. | integer |  | 5 |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. Enum values: \* queue \* topic | string | queue |  |
| **password** | Broker Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **selector** | Message Selector | A JMS message selector: the source receives only the messages that match it. It is a condition, in a syntax like the WHERE clause of SQL, on the JMS properties and headers of the message, not on its body, such as `priority > 5` or `region = 'EU' AND JMSPriority >= 7`. From a queue, the messages that do not match stay on the queue. When it is not set, the source receives every message. | string |  | priority > 5 |
| **subscriptionDurable** | Durable Subscription | Whether the subscription to a topic is durable. When it is true, the broker keeps the messages sent to the topic while this source is stopped or disconnected, and delivers them when it connects again; the broker keeps the subscription, and collects messages for it, until it is removed in the broker. Set `subscriptionName` and `clientId` with it. When it is false, the messages sent while the source is not connected are lost. Only for a topic: true makes `destinationName` a topic, even with `destinationType` set to `queue`. | boolean | false |  |
| **subscriptionName** | Subscription Name | The name of the durable subscription to a topic, under which the broker keeps the subscription, together with `clientId`. Use the same name each time the source starts, to receive the messages kept while it was stopped. Set it whenever `subscriptionDurable` is true. Not used otherwise. | string |  | orders-audit |
| **transacted** | Transacted | Whether each message is received in a JMS transaction, which is committed once the rest of the flow has processed the message. When the flow fails, the transaction is rolled back and the message is delivered again, with the header `JMSRedelivered` true; after 6 more attempts (the default of the ActiveMQ client), the broker moves it to the dead letter queue `ActiveMQ.DLQ`. When it is not set, the message is removed from the queue when it is received, even when the flow then fails. | boolean |  |  |
| **username** | Broker Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. | string |  |  |

## Dependencies

At runtime, the `jms-apache-activemq-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:kamelet
    
-   mvn:org.apache.activemq:activemq-client:6.3.2
    

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
      uri: "kamelet:jms-apache-activemq-source"
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-activemq-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-activemq-source.kamelet.yaml)