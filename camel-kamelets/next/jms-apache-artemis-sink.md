# ![jms apache artemis sink](_images/kamelets/jms-apache-artemis-sink.svg) JMS - Apache Artemis Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a queue or a topic in an Apache ActiveMQ Artemis broker, through JMS.

Use it to hand work to another application through a queue, such as orders to process, or to publish events on a topic for every application that listens. For a steady flow of messages, use `jms-pooled-apache-artemis-sink`, which reuses its connections to the broker and has `username` and `password` options. For another broker that speaks AMQP 1.0, use `jms-amqp-10-sink`.

Input: text is sent as a JMS text message, bytes as a JMS bytes message, and a Map as a JMS map message. The headers of the message, except the Camel ones, are sent along as JMS properties of the message.

Output: the message is unchanged.

Good to know: Messages go to a queue unless `destinationType` is `topic`, and a message sent to a topic reaches only the receivers subscribed at that moment. It connects with no TLS and no login, unless `brokerURL` asks for them. It does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does.

## Configuration Options

The following table summarizes the configuration options available for the `jms-apache-artemis-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The address of the Artemis broker, as `tcp://host:port`; the usual port is 61616. Add `?sslEnabled=true` for TLS. A broker that needs a login takes it in the URL too, as `tcp://host:61616?user=app&password=secret`. | string |  | tcp://localhost:61616 |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to send the messages to. | string |  | orders |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |

## Dependencies

At runtime, the `jms-apache-artemis-sink` Kamelet relies upon the presence of the following dependencies:

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-sink.kamelet.yaml)