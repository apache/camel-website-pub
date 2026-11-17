# ![jms pooled apache artemis source](_images/kamelets/jms-pooled-apache-artemis-source.svg) JMS Pooled - Apache Artemis Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Deprecated"**

Deprecated, use `jms-apache-artemis-source` instead, which now has the same login options: receives each message from a queue or a topic in an Apache ActiveMQ Artemis broker.

Use it to process work that other applications put on a queue, or to react to events published on a topic, on a broker that needs a login. This Kamelet will be removed in a later release: `jms-apache-artemis-source` now takes `username` and `password`, so change the name of the Kamelet and drop the pool options, which a source does not need because it keeps its connection open.

Output: the body is text for a JMS text message, bytes for a bytes message, and a Map for a map message. The JMS properties of the message become headers, along with the JMS headers such as `JMSMessageID`, `JMSDestination`, `JMSTimestamp`, `JMSPriority` and `JMSRedelivered`.

Good to know: From a queue, each message is removed when it is received, even when the rest of the flow then fails, and several copies of this source share the messages. From a topic (`destinationType` set to `topic`), it receives only the messages sent while it is connected, as the subscription is not durable. It connects with no TLS unless `brokerURL` asks for it. When the broker cannot be reached, it starts anyway and tries again every 5 seconds.

## Configuration Options

The following table summarizes the configuration options available for the `jms-pooled-apache-artemis-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The address of the Artemis broker, as `tcp://host:port`; the usual port is 61616. Add `?sslEnabled=true` for TLS. | string |  | tcp://localhost:61616 |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to receive the messages from. | string |  | orders |
| **connectionIdleTimeout** | Connection Idle Timeout | How long a connection of the pool can stay unused before it is closed, in milliseconds. For example, 30000 is 30 seconds. | integer | 30000 |  |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **maxIdleSessionsPerConnection** | Max Idle Sessions Per Connection | How many unused sessions each connection of the pool keeps open for reuse. Unused sessions beyond this number are closed. | integer | 500 |  |
| **maxSessionsPerConnection** | Max Sessions Per Connection | The most sessions that can be open at the same time on each connection of the pool. Each message being sent or received uses one session. | integer | 500 |  |
| **password** | Broker Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **username** | Broker Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. | string |  |  |

## Dependencies

At runtime, the `jms-pooled-apache-artemis-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:jms-pooled-apache-artemis-source"
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

## JMS Pooled Apache Artemis Source Kamelet Description

> **Note**
> This Kamelet is deprecated and will be removed in a later release. Use [![jms apache artemis source](_images/kamelets/jms-apache-artemis-source.svg) JMS - Apache Artemis Source](jms-apache-artemis-source.html), which has the same `username` and `password` options. It needs no pool options: a source keeps its connection open.

### Authentication methods

This Kamelet connects to Apache Artemis JMS broker using:

-   Broker URL and connection credentials
    
-   Pooled connection factory for better performance
    
-   Username and password authentication
    

### Output format

The Kamelet consumes messages from Apache Artemis queues or topics. The body is text for a JMS text message, bytes for a bytes message, and a Map for a map message; the JMS properties of the message become headers.

### Configuration

The Kamelet requires Apache Artemis connection parameters:

-   `brokerURL`: The Apache Artemis broker URL
    
-   `destinationName`: The destination queue or topic name
    
-   `username`: Username for authentication, when the broker needs a login
    
-   `password`: Password for authentication, when the broker needs a login
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:jms-pooled-apache-artemis-source"
      parameters:
        brokerURL: "tcp://artemis-broker:61616"
        destinationName: "my-queue"
        username: "artemisuser"
        password: "artemispass"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-pooled-apache-artemis-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-pooled-apache-artemis-source.kamelet.yaml)