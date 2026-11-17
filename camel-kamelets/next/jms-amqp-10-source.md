# ![jms amqp 10 source](_images/kamelets/jms-amqp-10-source.svg) JMS - AMQP 1.0 Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message from a queue or a topic in a message broker that speaks AMQP 1.0, such as Apache ActiveMQ Artemis, through JMS and the Apache Qpid client.

Use it to process work that other applications put on a queue, or to react to events published on a topic, on any broker that supports the AMQP 1.0 protocol. For an Artemis broker, `jms-apache-artemis-source` and `jms-pooled-apache-artemis-source` work too.

Output: the body is text for a JMS text message, bytes for a bytes message, and a Map for a map message. The JMS properties of the message become headers, along with the JMS headers such as `JMSMessageID`, `JMSDestination`, `JMSTimestamp`, `JMSPriority` and `JMSRedelivered`.

Good to know: From a queue, each message is removed when it is received, even when the rest of the flow then fails, and several copies of this source share the messages. From a topic (`destinationType` set to `topic`), it receives only the messages sent while it is connected, as the subscription is not durable. The login and the TLS settings go in `remoteURI`: there are no separate options for them. When the broker cannot be reached, it starts anyway and tries again every 5 seconds.

## Configuration Options

The following table summarizes the configuration options available for the `jms-amqp-10-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to receive the messages from. | string |  | orders |
| **remoteURI** | Broker URL | **Required** The address of the broker, as `amqp://host:port` (the AMQP port is usually 5672), or `amqps://host:port` for TLS. Settings of the Qpid JMS client go after `?`: `jms.username` and `jms.password` for a login, as `amqp://host:5672?jms.username=app&jms.password=secret`, and `transport.trustStoreLocation`, `transport.trustStorePassword`, `transport.keyStoreLocation` and `transport.keyStorePassword` for TLS. | string |  | amqp://localhost:5672 |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |

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

The Kamelet has no separate options for the login or TLS: they go in `remoteURI`, as settings of the Apache Qpid JMS client after `?`.

-   A login: `amqp://broker.example.com:5672?jms.username=app&jms.password=secret`
    
-   TLS: the `amqps://` scheme, with `transport.trustStoreLocation` and `transport.trustStorePassword` when the broker certificate is not trusted by the Java runtime.
    

### Output format

The body is text for a JMS text message, bytes for a bytes message, and a Map for a map message. The JMS properties of the message become headers.

### Configuration

The Kamelet requires connection parameters for the AMQP 1.0 broker:

-   `remoteURI`: the address of the broker, with the login when the broker needs one
    
-   `destinationName`: the name of the queue or topic
    
-   `destinationType`: `queue` (the default) or `topic`
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:jms-amqp-10-source"
      parameters:
        remoteURI: "amqp://broker.example.com:5672?jms.username=app&jms.password=secret"
        destinationName: "my-queue"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-source.kamelet.yaml)