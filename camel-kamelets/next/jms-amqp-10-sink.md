# ![jms amqp 10 sink](_images/kamelets/jms-amqp-10-sink.svg) JMS - AMQP 1.0 Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a queue or a topic in a message broker that speaks AMQP 1.0, such as Apache ActiveMQ Artemis, through JMS and the Apache Qpid client.

Use it to hand work to another application through a queue, or to publish events on a topic, on any broker that supports the AMQP 1.0 protocol. For an Artemis broker, `jms-apache-artemis-sink` and `jms-pooled-apache-artemis-sink` work too.

Input: text is sent as a JMS text message, bytes as a JMS bytes message, and a Map as a JMS map message. The headers of the message, except the Camel ones, are sent along as JMS properties of the message.

Output: the message is unchanged.

Good to know: Messages go to a queue unless `destinationType` is `topic`, and a message sent to a topic reaches only the receivers subscribed at that moment. The login and the TLS settings go in `remoteURI`: there are no separate options for them. It opens a new connection to the broker for each message. It does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does.

## Configuration Options

The following table summarizes the configuration options available for the `jms-amqp-10-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to send the messages to. | string |  | orders |
| **remoteURI** | Broker URL | **Required** The address of the broker, as `amqp://host:port` (the AMQP port is usually 5672), or `amqps://host:port` for TLS. Settings of the Qpid JMS client go after `?`: `jms.username` and `jms.password` for a login, as `amqp://host:5672?jms.username=app&jms.password=secret`, and `transport.trustStoreLocation`, `transport.trustStorePassword`, `transport.keyStoreLocation` and `transport.keyStorePassword` for TLS. | string |  | amqp://localhost:5672 |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-sink.kamelet.yaml)