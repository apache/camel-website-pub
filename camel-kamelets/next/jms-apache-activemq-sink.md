# ![jms apache activemq sink](_images/kamelets/jms-apache-activemq-sink.svg) JMS - Apache ActiveMQ Classic Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a queue or a topic in an Apache ActiveMQ Classic broker, through JMS over OpenWire.

Use it to hand work to another application through a queue, such as orders to process, or to publish events on a topic for every application that listens. For an Apache ActiveMQ Artemis broker, use `jms-apache-artemis-sink`; for another broker that speaks AMQP 1.0, use `jms-amqp-10-sink`.

Input: text is sent as a JMS text message, bytes as a JMS bytes message, and a Map as a JMS map message; `jmsMessageType` sends text or bytes as the other kind. The headers of the message, except the Camel ones, are sent along as JMS properties of the message.

Output: the message is unchanged, with the name of the queue or topic it was sent to in the `CamelJMSDestinationProduced` header.

Good to know: Messages go to a queue unless `destinationType` is `topic`, and a message sent to a topic reaches only the receivers subscribed at that moment. Messages are persistent, with priority 4, and never expire, unless `deliveryPersistent`, `priority` and `timeToLive` say otherwise. It connects with no TLS unless `brokerURL` starts with `ssl://`, and logs in with `username` and `password` when they are set; a message fails when the broker refuses the login, or cannot be reached and `brokerURL` does not use `failover:`. It keeps its connections to the broker in a pool and reuses them for the next messages. It does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does. Headers that start with `CamelJms` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `jms-apache-activemq-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The address of the ActiveMQ Classic broker, as `tcp://host:port`; the usual port is 61616. Use `ssl://host:port` for TLS, to a TLS connector of the broker (often on port 61617). For several brokers, `failover:(tcp://broker1:61616,tcp://broker2:61616)` connects to one of them and moves to another when it fails; while none can be reached, a message waits instead of failing. | string |  | tcp://localhost:61616 |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to send the messages to. | string |  | orders |
| **connectionIdleTimeout** | Connection Idle Timeout | How long a connection of the pool can stay unused before it is closed, in milliseconds. For example, 30000 is 30 seconds. | integer | 30000 |  |
| **deliveryPersistent** | Persistent Delivery | Whether the broker stores each message on disk, so that it survives a restart of the broker. False sends non-persistent messages, which are faster but lost when the broker stops. When it is not set, the messages are persistent. | boolean |  |  |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. Enum values: \* queue \* topic | string | queue |  |
| **jmsMessageType** | JMS Message Type | The kind of JMS message to send, whatever the body: `Text` sends a text message, and `Bytes` a bytes message, for a receiver that expects one kind. When it is not set, the kind follows the body: text is sent as a text message, and bytes as a bytes message. Enum values: \* Text \* Bytes | string |  |  |
| **maxIdleSessionsPerConnection** | Max Idle Sessions Per Connection | How many unused sessions each connection of the pool keeps open for reuse. Unused sessions beyond this number are closed. | integer | 500 |  |
| **maxSessionsPerConnection** | Max Sessions Per Connection | The most sessions that can be open at the same time on each connection of the pool. Each message being sent or received uses one session. | integer | 500 |  |
| **password** | Broker Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **priority** | Priority | The JMS priority of each message, from 0 (lowest) to 9 (highest). Of the messages waiting on a queue, the broker delivers those with the highest priority first. When it is not set, 4. | integer |  | 7 |
| **timeToLive** | Time to Live | How long each message may wait to be received, in milliseconds, such as 60000 for one minute. A message still waiting after that time expires: the broker does not deliver it, and moves a persistent message to the dead letter queue `ActiveMQ.DLQ` (the default of the broker) and drops a non-persistent one. When it is not set, the messages never expire. | integer |  | 60000 |
| **username** | Broker Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. | string |  |  |

## Dependencies

At runtime, the `jms-apache-activemq-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:kamelet
    
-   mvn:org.apache.activemq:activemq-client:6.4.0
    
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
            uri: "kamelet:jms-apache-activemq-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-activemq-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-activemq-sink.kamelet.yaml)