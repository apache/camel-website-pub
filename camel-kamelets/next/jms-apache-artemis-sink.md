# ![jms apache artemis sink](_images/kamelets/jms-apache-artemis-sink.svg) JMS - Apache Artemis Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a queue or a topic in an Apache ActiveMQ Artemis broker, through JMS.

Use it to hand work to another application through a queue, such as orders to process, or to publish events on a topic for every application that listens. For another broker that speaks AMQP 1.0, use `jms-amqp-10-sink`.

Input: text is sent as a JMS text message, bytes as a JMS bytes message, and a Map as a JMS map message; `jmsMessageType` sends text or bytes as the other kind. The headers of the message, except the Camel ones, are sent along as JMS properties of the message.

Output: the message is unchanged, with the name of the queue or topic it was sent to in the `CamelJMSDestinationProduced` header.

Good to know: Messages go to a queue unless `destinationType` is `topic`, and a message sent to a topic reaches only the receivers subscribed at that moment. Messages are persistent, with priority 4, and never expire, unless `deliveryPersistent`, `priority` and `timeToLive` say otherwise. It connects with no TLS unless `brokerURL` asks for it, and logs in with `username` and `password` when they are set. It keeps its connections to the broker in a pool and reuses them for the next messages. It does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does. Headers that start with `CamelJms` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `jms-apache-artemis-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The address of the Artemis broker, as `tcp://host:port`; the usual port is 61616. Add `?sslEnabled=true` for TLS. A broker that needs a login takes it in the URL too, as `tcp://host:61616?user=app&password=secret`. | string |  | tcp://localhost:61616 |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to send the messages to. | string |  | orders |
| **connectionIdleTimeout** | Connection Idle Timeout | How long a connection of the pool can stay unused before it is closed, in milliseconds. For example, 30000 is 30 seconds. | integer | 30000 |  |
| **deliveryPersistent** | Persistent Delivery | Whether the broker stores each message on disk, so that it survives a restart of the broker. False sends non-persistent messages, which are faster but lost when the broker stops. When it is not set, the messages are persistent. | boolean |  |  |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **jmsMessageType** | JMS Message Type | The kind of JMS message to send, whatever the body: `Text` sends a text message, and `Bytes` a bytes message, for a receiver that expects one kind. When it is not set, the kind follows the body: text is sent as a text message, and bytes as a bytes message. Enum values: \* Text \* Bytes | string |  |  |
| **maxIdleSessionsPerConnection** | Max Idle Sessions Per Connection | How many unused sessions each connection of the pool keeps open for reuse. Unused sessions beyond this number are closed. | integer | 500 |  |
| **maxSessionsPerConnection** | Max Sessions Per Connection | The most sessions that can be open at the same time on each connection of the pool. Each message being sent or received uses one session. | integer | 500 |  |
| **password** | Broker Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **priority** | Priority | The JMS priority of each message, from 0 (lowest) to 9 (highest). Of the messages waiting on a queue, the broker delivers those with the highest priority first. When it is not set, 4. | integer |  | 7 |
| **timeToLive** | Time to Live | How long each message may wait to be received, in milliseconds, such as 60000 for one minute. A message still waiting after that time expires: the broker does not deliver it, and moves it to the queue `ExpiryQueue` (the default of the broker). When it is not set, the messages never expire. | integer |  | 60000 |
| **username** | Broker Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. | string |  |  |

## Dependencies

At runtime, the `jms-apache-artemis-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:kamelet
    
-   mvn:org.apache.activemq:artemis-jakarta-client-all:2.57.0
    
-   mvn:org.messaginghub:pooled-jms:3.2.6
    

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
            uri: "kamelet:jms-apache-artemis-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## JMS - Apache Artemis Sink Kamelet Description

### Connection Configuration

This Kamelet connects to an Apache Artemis message broker using JMS. Apache Artemis is a high-performance, scalable messaging broker that supports multiple messaging protocols.

### Destination Configuration

The Kamelet supports both queue and topic destinations. The destination type can be configured using the `destinationType` property, which defaults to `queue`.

### Apache Artemis Client

This sink uses the Apache Artemis Jakarta JMS client library to establish connections and send messages to the broker.

### Authentication

A broker that needs a login takes it in the `username` and `password` options. Without them, the Kamelet connects with no login.

### Connection Pooling

The Kamelet keeps its connections to the broker in a pool and reuses them for the next messages, instead of opening a new connection for each message. The pool is set with these options:

-   `maxSessionsPerConnection`: the most sessions open at the same time on each connection (default: 500)
    
-   `maxIdleSessionsPerConnection`: how many unused sessions each connection keeps for reuse (default: 500)
    
-   `connectionIdleTimeout`: how long an unused connection stays open, in milliseconds (default: 30000)
    

### Persistence, priority and expiry

By default, each message is persistent, has priority 4, and never expires. Three options change that for every message the sink sends:

-   `deliveryPersistent`: `false` sends non-persistent messages, which are faster, but lost when the broker stops.
    
-   `priority`: from 0 (lowest) to 9 (highest). Of the messages waiting on a queue, the broker delivers those with the highest priority first.
    
-   `timeToLive`: how long a message may wait to be received, in milliseconds. An expired message is not delivered: Artemis moves it to the queue `ExpiryQueue`.
    

`jmsMessageType` sends every message as a text message (`Text`) or a bytes message (`Bytes`), whatever the body, for a receiver that expects one kind.

```yaml
- route:
    from:
      uri: "kamelet:webhook-source"
      steps:
        - to:
            uri: "kamelet:jms-apache-artemis-sink"
            parameters:
              brokerURL: "tcp://artemis.example.com:61616"
              destinationName: "alerts.queue"
              priority: 7
              timeToLive: 60000
              jmsMessageType: "Text"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-sink.kamelet.yaml)