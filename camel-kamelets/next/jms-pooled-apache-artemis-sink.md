# ![jms pooled apache artemis sink](_images/kamelets/jms-pooled-apache-artemis-sink.svg) JMS Pooled - Apache Artemis Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a queue or a topic in an Apache ActiveMQ Artemis broker, through JMS, reusing a pool of connections to the broker.

Use it to hand work to another application through a queue, or to publish events on a topic, when messages flow steadily: it reuses its connections, where `jms-apache-artemis-sink` connects anew for each message. Use it also for a broker that needs a login, which goes in `username` and `password`.

Input: text is sent as a JMS text message, bytes as a JMS bytes message, and a Map as a JMS map message. The headers of the message, except the Camel ones, are sent along as JMS properties of the message.

Output: the message is unchanged.

Good to know: Messages go to a queue unless `destinationType` is `topic`, and a message sent to a topic reaches only the receivers subscribed at that moment. It connects with no TLS unless `brokerURL` asks for it. It does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does.

## Configuration Options

The following table summarizes the configuration options available for the `jms-pooled-apache-artemis-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The address of the Artemis broker, as `tcp://host:port`; the usual port is 61616. Add `?sslEnabled=true` for TLS. | string |  | tcp://localhost:61616 |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to send the messages to. | string |  | orders |
| **connectionIdleTimeout** | Connection Idle Timeout | How long a connection of the pool can stay unused before it is closed, in milliseconds. For example, 30000 is 30 seconds. | integer | 30000 |  |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **maxIdleSessionsPerConnection** | Max Idle Sessions Per Connection | How many unused sessions each connection of the pool keeps open for reuse. Unused sessions beyond this number are closed. | integer | 500 |  |
| **maxSessionsPerConnection** | Max Sessions Per Connection | The most sessions that can be open at the same time on each connection of the pool. Each message being sent or received uses one session. | integer | 500 |  |
| **password** | Broker Password | The password to log in to the broker with, for the user `username`. | string |  |  |
| **username** | Broker Username | The user name to log in to the broker with. Leave it empty for a broker that accepts clients without a login. | string |  |  |

## Dependencies

At runtime, the `jms-pooled-apache-artemis-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:jms-pooled-apache-artemis-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## JMS Pooled - Apache Artemis Sink Kamelet Description

### Connection Configuration

This Kamelet connects to an Apache Artemis message broker using JMS with connection pooling for improved performance and resource management.

### Connection Pooling

The Kamelet uses pooled connections to optimize resource usage and performance. Key pooling configuration options include:

-   Maximum sessions per connection (default: 500)
    
-   Maximum idle sessions per connection (default: 500)
    
-   Connection idle timeout in milliseconds (default: 30000)
    

### Authentication

Optional authentication can be configured using username and password properties for secure broker connections.

### Destination Configuration

The Kamelet supports both queue and topic destinations. The destination type can be configured using the `destinationType` property, which defaults to `queue`.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-pooled-apache-artemis-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-pooled-apache-artemis-sink.kamelet.yaml)