# ![jms amqp 10 sink](_images/kamelets/jms-amqp-10-sink.svg) JMS - AMQP 1.0 Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a queue or a topic in a message broker that speaks AMQP 1.0, such as Apache ActiveMQ Artemis, through JMS and the Apache Qpid client.

Use it to hand work to another application through a queue, or to publish events on a topic, on any broker that supports the AMQP 1.0 protocol. For an Artemis broker, `jms-apache-artemis-sink` works too.

Input: text is sent as a JMS text message, bytes as a JMS bytes message, and a Map as a JMS map message; `jmsMessageType` sends text or bytes as the other kind. The headers of the message, except the Camel ones, are sent along as JMS properties of the message.

Output: the message is unchanged, with the name of the queue or topic it was sent to in the `CamelJMSDestinationProduced` header.

Good to know: Messages go to a queue unless `destinationType` is `topic`, and a message sent to a topic reaches only the receivers subscribed at that moment. Messages are persistent, with priority 4, and never expire, unless `deliveryPersistent`, `priority` and `timeToLive` say otherwise. It logs in with `username` and `password` when they are set; the TLS settings go in `remoteURI`. It opens a new connection to the broker for each message. It does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does. Headers that start with `CamelJms` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `jms-amqp-10-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to send the messages to. | string |  | orders |
| **remoteURI** | Broker URL | **Required** The address of the broker, as `amqp://host:port` (the AMQP port is usually 5672), or `amqps://host:port` for TLS. Settings of the Qpid JMS client go after `?`, such as `transport.trustStoreLocation`, `transport.trustStorePassword`, `transport.keyStoreLocation` and `transport.keyStorePassword` for TLS. The login goes in `username` and `password`; `jms.username` and `jms.password` in the address work too. | string |  | amqp://localhost:5672 |
| **deliveryPersistent** | Persistent Delivery | Whether the broker stores each message on disk, so that it survives a restart of the broker. False sends non-persistent messages, which are faster but lost when the broker stops. When it is not set, the messages are persistent. | boolean |  |  |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **jmsMessageType** | JMS Message Type | The kind of JMS message to send, whatever the body: `Text` sends a text message, and `Bytes` a bytes message, for a receiver that expects one kind. When it is not set, the kind follows the body: text is sent as a text message, and bytes as a bytes message. Enum values: \* Text \* Bytes | string |  |  |
| **password** | Password | The password to log in to the broker with, for the user `username`. When it is set, it is used instead of `jms.password` in `remoteURI`. | string |  |  |
| **priority** | Priority | The JMS priority of each message, from 0 (lowest) to 9 (highest). Of the messages waiting on a queue, the broker delivers those with the highest priority first. When it is not set, 4. | integer |  | 7 |
| **timeToLive** | Time to Live | How long each message may wait to be received, in milliseconds, such as 60000 for one minute. A message still waiting after that time expires: the broker does not deliver it (Apache ActiveMQ Artemis moves it to the queue `ExpiryQueue`). When it is not set, the messages never expire. | integer |  | 60000 |
| **username** | Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. When it is set, it is used instead of `jms.username` in `remoteURI`. | string |  |  |

## Dependencies

At runtime, the `jms-amqp-10-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:jms-amqp-10-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## JMS - AMQP 1.0 Sink Kamelet Description

### Connection Configuration

This Kamelet connects to any AMQP 1.0 compliant message broker using the Apache Qpid JMS client.

### Destination Configuration

The Kamelet supports both queue and topic destinations. The destination type can be configured using the `destinationType` property, which defaults to `queue`.

### AMQP 1.0 Protocol

This sink uses the AMQP 1.0 protocol for sending messages to the broker. AMQP 1.0 is an open standard messaging protocol that provides reliable, secure, and interoperable messaging.

### Login and TLS

A broker that needs a login takes it in the `username` and `password` options. `jms.username` and `jms.password` in `remoteURI` work too, but `username` and `password` are used instead of them when they are set. For TLS, use the `amqps://` scheme in `remoteURI`, with `transport.trustStoreLocation` and `transport.trustStorePassword` after `?` when the broker certificate is not trusted by the Java runtime.

### Persistence, priority and expiry

By default, each message is persistent, has priority 4, and never expires. Three options change that for every message the sink sends:

-   `deliveryPersistent`: `false` sends non-persistent messages, which are faster, but lost when the broker stops.
    
-   `priority`: from 0 (lowest) to 9 (highest). Of the messages waiting on a queue, the broker delivers those with the highest priority first.
    
-   `timeToLive`: how long a message may wait to be received, in milliseconds. An expired message is not delivered; Apache ActiveMQ Artemis moves it to the queue `ExpiryQueue`.
    

`jmsMessageType` sends every message as a text message (`Text`) or a bytes message (`Bytes`), whatever the body, for a receiver that expects one kind.

```yaml
- route:
    from:
      uri: "kamelet:webhook-source"
      steps:
        - to:
            uri: "kamelet:jms-amqp-10-sink"
            parameters:
              remoteURI: "amqp://broker.example.com:5672"
              username: "app"
              password: "secret"
              destinationName: "alerts.queue"
              priority: 7
              timeToLive: 60000
              jmsMessageType: "Text"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-sink.kamelet.yaml)