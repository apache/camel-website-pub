# ![jms apache artemis source](_images/kamelets/jms-apache-artemis-source.svg) JMS - Apache Artemis Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from an Apache Artemis message broker by using JMS.

## Configuration Options

The following table summarizes the configuration options available for the `jms-apache-artemis-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **brokerURL** | Broker URL | **Required** The JMS URL. | string |  | tcp://my-host:61616 |
| **destinationName** | Destination Name | **Required** The JMS destination name. | string |  |  |
| **destinationType** | Destination Type | The JMS destination type (queue or topic). | string | queue |  |

## Dependencies

At runtime, the `jms-apache-artemis-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:kamelet
    
-   mvn:org.apache.activemq:artemis-jakarta-client-all:2.44.0
    

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

This Kamelet supports username and password authentication to connect to Apache Artemis JMS broker. Connection can be configured with or without authentication based on broker setup.

### Configuration

The JMS Apache Artemis Source Kamelet supports the following configurations:

-   **Broker URL**: Apache Artemis broker URL (required)
    
-   **Destination Name**: JMS destination (queue or topic) name (required)
    
-   **Destination Type**: Type of destination - queue or topic (default: queue)
    
-   **Username**: Username for broker authentication (optional)
    
-   **Password**: Password for broker authentication (optional)
    
-   **Client ID**: JMS client ID for durable subscriptions
    
-   **Durable Subscription Name**: Name for durable topic subscription
    
-   **Message Selector**: JMS message selector for filtering
    

### Output Format

The Kamelet outputs JMS messages including message body, headers, and JMS properties. Message format depends on the original message type (text, bytes, object, etc.).

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:jms-apache-artemis-source"
      parameters:
        brokerURL: "tcp://artemis.example.com:61616"
        destinationName: "orders.queue"
        destinationType: "queue"
        username: "artemisuser"
        password: "artemispass"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Topic Subscription

```yaml
- route:
    from:
      uri: "kamelet:jms-apache-artemis-source"
      parameters:
        brokerURL: "tcp://artemis.example.com:61616"
        destinationName: "events.topic"
        destinationType: "topic"
        username: "artemisuser"
        password: "artemispass"
        clientId: "my-consumer"
        durableSubscriptionName: "my-subscription"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Message Selector

```yaml
- route:
    from:
      uri: "kamelet:jms-apache-artemis-source"
      parameters:
        brokerURL: "tcp://artemis.example.com:61616"
        destinationName: "notifications.queue"
        destinationType: "queue"
        username: "artemisuser"
        password: "artemispass"
        messageSelector: "priority > 5"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Connection Management

The kamelet manages connections to Apache Artemis automatically, including connection pooling and reconnection on failures. It supports both embedded and standalone Artemis deployments.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-apache-artemis-source.kamelet.yaml)