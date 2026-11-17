# ![jms apache artemis source](_images/kamelets/jms-apache-artemis-source.svg) JMS - Apache Artemis Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message from a queue or a topic in an Apache ActiveMQ Artemis broker, through JMS.

Use it to process work that other applications put on a queue, such as orders or jobs, or to react to events published on a topic. `jms-pooled-apache-artemis-source` does the same with a pool of connections and has `username` and `password` options. For another broker that speaks AMQP 1.0, use `jms-amqp-10-source`.

Output: the body is text for a JMS text message, bytes for a bytes message, and a Map for a map message. The JMS properties of the message become headers, along with the JMS headers such as `JMSMessageID`, `JMSDestination`, `JMSTimestamp`, `JMSPriority` and `JMSRedelivered`.

Good to know: From a queue, each message is removed when it is received, even when the rest of the flow then fails, and several copies of this source share the messages. From a topic (`destinationType` set to `topic`), it receives only the messages sent while it is connected, as the subscription is not durable. It connects with no TLS and no login, unless `brokerURL` asks for them. When the broker cannot be reached, it starts anyway and tries again every 5 seconds.

## Configuration Options

The following table summarizes the configuration options available for the `jms-apache-artemis-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The address of the Artemis broker, as `tcp://host:port`; the usual port is 61616. Add `?sslEnabled=true` for TLS. A broker that needs a login takes it in the URL too, as `tcp://host:61616?user=app&password=secret`. | string |  | tcp://localhost:61616 |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to receive the messages from. | string |  | orders |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |

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

This Kamelet has no `username` and `password` options. A broker that needs a login takes it in `brokerURL`, as `tcp://artemis.example.com:61616?user=artemisuser&password=artemispass`. To keep the password in an option of its own, use `jms-pooled-apache-artemis-source`, which has `username` and `password`.

### Configuration

The JMS Apache Artemis Source Kamelet supports the following configurations:

-   **Broker URL**: Apache Artemis broker URL (required)
    
-   **Destination Name**: JMS destination (queue or topic) name (required)
    
-   **Destination Type**: Type of destination - queue or topic (default: queue)
    

The subscription to a topic is not durable, and the Kamelet has no option for a message selector.

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

The source receives only the messages published to the topic while it is connected.

```yaml
- route:
    from:
      uri: "kamelet:jms-apache-artemis-source"
      parameters:
        brokerURL: "tcp://artemis.example.com:61616?user=artemisuser&password=artemispass"
        destinationName: "events.topic"
        destinationType: "topic"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Connection Management

When the broker cannot be reached, the Kamelet starts anyway and tries to connect again every 5 seconds. It does not pool connections; `jms-pooled-apache-artemis-source` does.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-source.kamelet.yaml)