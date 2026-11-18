# ![jms ibm mq source](_images/kamelets/jms-ibm-mq-source.svg) JMS - IBM MQ Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message from a queue or a topic of an IBM MQ queue manager, through JMS.

Use it to process work or events that other applications put on IBM MQ, such as an existing enterprise or mainframe system. Use `jms-ibm-mq-sink` to send to IBM MQ.

Output: the body is text for a JMS text message, and bytes for a bytes message. The JMS properties of the message become headers, along with the JMS headers such as `JMSMessageID` and `JMSTimestamp`, and IBM MQ details such as `JMSXUserID`, `JMS_IBM_PutDate` and `JMS_IBM_Format`.

Good to know: the IBM MQ client library is not included, as its licence is not the Apache one: add `mvn:com.ibm.mq:com.ibm.mq.jakarta.client` with a version to the dependencies of the integration (Camel JBang adds it by itself). From a queue, each message is removed when it is received, even when the rest of the flow then fails, and several copies of this source share the messages. From a topic (`destinationType` set to `topic`), it receives only the messages sent while it is connected, unless `subscriptionDurable` is true: then the queue manager keeps the messages sent while it is stopped, under `subscriptionName`. A durable subscription needs `clientId` unless it is shared (`subscriptionShared`, JMS 2.0), and only one connection may use a client ID at a time. With `selector`, it receives only the messages whose properties and headers match the selector. It connects with no TLS unless `sslCipherSuite` is set. When the queue manager cannot be reached, it starts anyway and tries again every 5 seconds.

## Configuration Options

The following table summarizes the configuration options available for the `jms-ibm-mq-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **channel** | Channel | **Required** The name of the server-connection channel of the queue manager to connect through. | string |  | DEV.APP.SVRCONN |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to receive the messages from, as defined in the queue manager. | string |  | DEV.QUEUE.1 |
| **password** | Password | **Required** The password to log in to the queue manager with, for the user `username`. | string |  |  |
| **queueManager** | Queue Manager | **Required** The name of the queue manager to connect to. | string |  | QM1 |
| **serverName** | Server Host | **Required** The host name or IP address of the IBM MQ server that runs the queue manager. | string |  | mq.example.com |
| **serverPort** | Server Port | **Required** The port of the listener of the queue manager on the server. The IBM MQ default is 1414. | integer | 1414 |  |
| **username** | Username | **Required** The user name to log in to the queue manager with. | string |  |  |
| **clientId** | Client ID | The JMS client ID of the connection, which names this application to the queue manager. A durable subscription that is not shared needs one: the queue manager keeps the subscription under the client ID and `subscriptionName`, so use the same client ID each time the source starts. Only one connection may use a client ID at a time: two running copies of this source need different client IDs. When it is not set, the connection has no client ID. | string |  | orders-service |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **selector** | Message Selector | A JMS message selector: the source receives only the messages that match it. It is a condition, in a syntax like the WHERE clause of SQL, on the JMS properties and headers of the message, not on its body, such as `priority > 5` or `region = 'EU' AND JMSPriority >= 7`. From a queue, the messages that do not match stay on the queue. When it is not set, the source receives every message. | string |  | priority > 5 |
| **sslCipherSuite** | TLS Cipher Suite | The TLS cipher suite to connect with, which must match the cipher spec of the channel on the queue manager. When it is set, the connection uses TLS; when it is not set, it does not. | string |  | TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 |
| **subscriptionDurable** | Durable Subscription | Whether the subscription to a topic is durable. When it is true, the queue manager keeps the messages sent to the topic while this source is stopped or disconnected, and delivers them when it connects again; the queue manager keeps the subscription, and collects messages for it, until it is removed in the queue manager. Set `subscriptionName` with it, and `clientId` unless `subscriptionShared` is true. When it is false, the messages sent while the source is not connected are lost. Only for a topic: true makes `destinationName` a topic, even with `destinationType` set to `queue`. | boolean | false |  |
| **subscriptionName** | Subscription Name | The name of the durable or shared subscription to a topic, under which the queue manager keeps the subscription. Use the same name each time the source starts, to receive the messages kept while it was stopped. Set it whenever `subscriptionDurable` or `subscriptionShared` is true: without it, every source takes the same default name, so two sources with the same client ID, or two shared sources, take over one another’s subscription. Not used otherwise. | string |  | orders-audit |
| **subscriptionShared** | Shared Subscription | Whether the subscription to a topic is shared: the copies of this source that use the same `subscriptionName` share the messages of the topic, each message going to one of them, instead of each copy receiving every message. A shared subscription needs no `clientId`. Combine it with `subscriptionDurable` for a durable subscription that several copies share. Needs IBM MQ 8 or later (JMS 2.0). Only for a topic: true makes `destinationName` a topic, even with `destinationType` set to `queue`. | boolean | false |  |

## Dependencies

At runtime, the `jms-ibm-mq-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
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
      uri: "kamelet:jms-ibm-mq-source"
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

## JMS IBM MQ Source Kamelet Description

### Authentication methods

This Kamelet connects to IBM MQ as a client, with:

-   Channel and queue manager configuration
    
-   Username and password authentication
    
-   TLS, when `sslCipherSuite` is set to a cipher suite that matches the channel
    

### IBM MQ client library

The IBM MQ client library is not included in the Kamelet. Add it to the dependencies of the integration, for example `mvn:com.ibm.mq:com.ibm.mq.jakarta.client:<version>`. Camel JBang adds it by itself.

### Output format

The body is text for a JMS text message and bytes for a bytes message. The JMS properties of the message become headers, along with IBM MQ details such as `JMS_IBM_PutDate`.

### Configuration

The Kamelet requires IBM MQ specific connection parameters:

-   `serverName` and `serverPort`: the host and the port of the queue manager listener (1414 by default)
    
-   `queueManager`: IBM MQ queue manager name
    
-   `channel`: IBM MQ channel name
    
-   `username` and `password`: the login
    
-   `destinationName`: The destination queue name
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:jms-ibm-mq-source"
      parameters:
        serverName: "mq.example.com"
        serverPort: 1414
        queueManager: "QM1"
        channel: "DEV.APP.SVRCONN"
        username: "app"
        password: "passw0rd"
        destinationName: "DEV.QUEUE.1"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Durable topic subscription

From a topic, the source receives by default only the messages published while it is connected. With `subscriptionDurable` set to `true`, the queue manager keeps the messages published while the source is stopped, and delivers them when it starts again. The queue manager keeps the subscription under the client ID and the subscription name, so use the same `clientId` and `subscriptionName` each time the source starts. The user `username` needs the authority to subscribe to the topic.

```yaml
- route:
    from:
      uri: "kamelet:jms-ibm-mq-source"
      parameters:
        serverName: "mq.example.com"
        serverPort: 1414
        queueManager: "QM1"
        channel: "DEV.APP.SVRCONN"
        username: "app"
        password: "passw0rd"
        destinationType: "topic"
        destinationName: "orders/events"
        subscriptionDurable: true
        subscriptionName: "audit"
        clientId: "audit-service"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The JMS rules to know:

-   A durable subscription that is not shared needs a `clientId`.
    
-   Only one connection may use a client ID at a time: two running copies of the source need different client IDs.
    
-   To run several copies of the source on one durable subscription, set `subscriptionShared` to `true` as well, and leave `clientId` empty: the copies share the messages of the topic by `subscriptionName`, each message going to one of them. Shared subscriptions are part of JMS 2.0.
    
-   The durable subscription stays on the queue manager, and keeps collecting messages, until it is removed in the queue manager.
    

### Message selector

With `selector`, the source receives only the messages that match it, a condition on the JMS properties and headers of the message, such as `priority > 5`. From a queue, the other messages stay on the queue.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-source.kamelet.yaml)