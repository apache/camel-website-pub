# ![jms ibm mq source](_images/kamelets/jms-ibm-mq-source.svg) JMS - IBM MQ Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message from a queue or a topic of an IBM MQ queue manager, through JMS.

Use it to process work or events that other applications put on IBM MQ, such as an existing enterprise or mainframe system. Use `jms-ibm-mq-sink` to send to IBM MQ.

Output: the body is text for a JMS text message, and bytes for a bytes message. The JMS properties of the message become headers, along with the JMS headers such as `JMSMessageID` and `JMSTimestamp`, and IBM MQ details such as `JMSXUserID`, `JMS_IBM_PutDate` and `JMS_IBM_Format`.

Good to know: the IBM MQ client library is not included, as its licence is not the Apache one: add `mvn:com.ibm.mq:com.ibm.mq.jakarta.client` with a version to the dependencies of the integration (Camel JBang adds it by itself). From a queue, each message is removed when it is received, even when the rest of the flow then fails, unless `transacted` is true or `acknowledgementModeName` is `CLIENT_ACKNOWLEDGE`: then a message whose flow failed is delivered again. Several copies of this source share the messages of a queue, and `concurrentConsumers` processes several messages at the same time. From a topic (`destinationType` set to `topic`), it receives only the messages sent while it is connected, unless `subscriptionDurable` is true: then the queue manager keeps the messages sent while it is stopped, under `subscriptionName`. A durable subscription needs `clientId` unless it is shared (`subscriptionShared`, JMS 2.0), and only one connection may use a client ID at a time. With `selector`, it receives only the messages whose properties and headers match the selector. It connects with no TLS unless `sslCipherSuite` is set; the trust store and the key store for TLS are those of the Java runtime (`javax.net.ssl.trustStore`, `javax.net.ssl.keyStore`). For a multi-instance queue manager, list its instances in `connectionNameList`. When the queue manager cannot be reached, it starts anyway and tries again every 5 seconds.

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
| **acknowledgementModeName** | Acknowledgement Mode | When the source acknowledges each message to the queue manager, which then removes it from the queue. `AUTO_ACKNOWLEDGE`: as soon as the message is received. `CLIENT_ACKNOWLEDGE`: once the rest of the flow has processed it; when the flow fails, the queue manager delivers it again, and the backout threshold and backout queue of the queue apply, as with `transacted`. `DUPS_OK_ACKNOWLEDGE`: in batches, which is faster, but the messages processed since the last batch are delivered again when the source stops without closing its connection, such as in a crash. Not used when `transacted` is true. When it is not set, `AUTO_ACKNOWLEDGE`. Enum values: \* AUTO\_ACKNOWLEDGE \* CLIENT\_ACKNOWLEDGE \* DUPS\_OK\_ACKNOWLEDGE | string |  |  |
| **clientId** | Client ID | The JMS client ID of the connection, which names this application to the queue manager. A durable subscription that is not shared needs one: the queue manager keeps the subscription under the client ID and `subscriptionName`, so use the same client ID each time the source starts. Only one connection may use a client ID at a time: two running copies of this source need different client IDs. When it is not set, the connection has no client ID. | string |  | orders-service |
| **concurrentConsumers** | Concurrent Consumers | How many messages the source processes at the same time, each in a thread of its own. From a queue, more than one makes the source faster when each message takes a while, but the messages are then no longer processed in the order of the queue. On a topic, each consumer is a subscription of its own and receives every message, so each message is processed that many times, unless `subscriptionShared` is true; a durable subscription that is not shared takes only one consumer. When it is not set, one message at a time. | integer |  | 5 |
| **connectionNameList** | Connection Name List | The addresses of the instances of a multi-instance queue manager, as `host(port)` separated by commas, such as `mq1.example.com(1414),mq2.example.com(1414)`. The client tries them in order and connects to the first that answers. `serverName` and `serverPort` take the place of the first address of the list, so set them to the first instance too. When it is not set, the client connects only to `serverName` and `serverPort`. | string |  | mq1.example.com(1414),mq2.example.com(1414) |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **selector** | Message Selector | A JMS message selector: the source receives only the messages that match it. It is a condition, in a syntax like the WHERE clause of SQL, on the JMS properties and headers of the message, not on its body, such as `priority > 5` or `region = 'EU' AND JMSPriority >= 7`. From a queue, the messages that do not match stay on the queue. When it is not set, the source receives every message. | string |  | priority > 5 |
| **sslCipherSuite** | TLS Cipher Suite | The TLS cipher suite to connect with, which must match the cipher spec of the channel on the queue manager, such as `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256` for `ANY_TLS12_OR_HIGHER`. When it is set, the connection uses TLS; when it is not set, it does not. The certificate of the queue manager is checked against the trust store of the Java runtime, and a channel that asks for a client certificate gets one from its key store: set them with the Java system properties `javax.net.ssl.trustStore` and `javax.net.ssl.keyStore`, with their passwords. Camel’s own TLS settings (`camel.ssl`) do not apply to IBM MQ. | string |  | TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256 |
| **subscriptionDurable** | Durable Subscription | Whether the subscription to a topic is durable. When it is true, the queue manager keeps the messages sent to the topic while this source is stopped or disconnected, and delivers them when it connects again; the queue manager keeps the subscription, and collects messages for it, until it is removed in the queue manager. Set `subscriptionName` with it, and `clientId` unless `subscriptionShared` is true. When it is false, the messages sent while the source is not connected are lost. Only for a topic: true makes `destinationName` a topic, even with `destinationType` set to `queue`. | boolean | false |  |
| **subscriptionName** | Subscription Name | The name of the durable or shared subscription to a topic, under which the queue manager keeps the subscription. Use the same name each time the source starts, to receive the messages kept while it was stopped. Set it whenever `subscriptionDurable` or `subscriptionShared` is true: without it, every source takes the same default name, so two sources with the same client ID, or two shared sources, take over one another’s subscription. Not used otherwise. | string |  | orders-audit |
| **subscriptionShared** | Shared Subscription | Whether the subscription to a topic is shared: the copies of this source that use the same `subscriptionName` share the messages of the topic, each message going to one of them, instead of each copy receiving every message. A shared subscription needs no `clientId`. Combine it with `subscriptionDurable` for a durable subscription that several copies share. Needs IBM MQ 8 or later (JMS 2.0). Only for a topic: true makes `destinationName` a topic, even with `destinationType` set to `queue`. | boolean | false |  |
| **transacted** | Transacted | Whether each message is received in a JMS transaction, which is committed once the rest of the flow has processed the message. When the flow fails, the transaction is rolled back and the queue manager delivers the message again, with the header `JMSRedelivered` true. Once the message has been delivered as many times as the backout threshold of the queue (`BOTHRESH`), the client moves it to the backout queue of the queue (`BOQNAME`); the user needs the authority to put messages on that queue with their context (`put` and `passall`), or the source stops receiving from the queue. A queue without a backout threshold (`BOTHRESH(0)`, the default) delivers a message that always fails again and again. When it is not set, the message is removed from the queue when it is received, even when the flow then fails. | boolean |  |  |

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
    
-   `connectionNameList`: the instances of a multi-instance queue manager (see below)
    
-   `transacted`, `acknowledgementModeName` and `concurrentConsumers`: delivering a message again when its flow fails, and processing several messages at the same time (see below)
    

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

### TLS

Set `sslCipherSuite` to a cipher suite that matches the cipher spec of the channel, such as `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256` for `ANY_TLS12_OR_HIGHER`. The IBM MQ client checks the certificate of the queue manager against the trust store of the Java runtime, and sends the client certificate from its key store when the channel asks for one (`SSLCAUTH(REQUIRED)`). The Kamelet has no options for them: set the Java system properties, for example in `JAVA_TOOL_OPTIONS`:

```bash
export JAVA_TOOL_OPTIONS="-Djavax.net.ssl.trustStore=/etc/mq/truststore.p12 -Djavax.net.ssl.trustStorePassword=changeit -Djavax.net.ssl.keyStore=/etc/mq/client.p12 -Djavax.net.ssl.keyStorePassword=changeit"
```

Camel’s own TLS settings (`camel.ssl.*`) do not apply to the IBM MQ client.

### Multi-instance queue manager

For a multi-instance queue manager, list its instances in `connectionNameList`, as `host(port)` separated by commas. The client tries them in order and connects to the first that answers. `serverName` and `serverPort` take the place of the first address of the list, so set them to the first instance too.

```yaml
- route:
    from:
      uri: "kamelet:jms-ibm-mq-source"
      parameters:
        serverName: "mq1.example.com"
        serverPort: 1414
        connectionNameList: "mq1.example.com(1414),mq2.example.com(1414)"
        queueManager: "QM1"
        channel: "DEV.APP.SVRCONN"
        username: "app"
        password: "passw0rd"
        destinationName: "DEV.QUEUE.1"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Redelivery when the flow fails

By default, the source removes each message from the queue when it receives it, so a message whose flow fails is lost. With `transacted` set to `true`, each message is received in a transaction that is committed only once the flow has processed it. When the flow fails, the transaction is rolled back and the queue manager delivers the message again, with the header `JMSRedelivered` set to `true`.

Give the queue a backout threshold and a backout queue, such as `ALTER QLOCAL(DEV.QUEUE.1) BOTHRESH(3) BOQNAME(DEV.DEAD.LETTER.QUEUE)`: once the message has been delivered that many times, the client moves it to the backout queue. The user of the Kamelet needs the authority to put messages on the backout queue with their context (`put` and `passall`), or the source stops receiving from the queue. Without a backout threshold (`BOTHRESH(0)`, the default), a message that always fails is delivered again and again.

`concurrentConsumers` processes several messages of the queue at the same time, each in a thread of its own; the messages are then no longer processed in the order of the queue.

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
        transacted: true
        concurrentConsumers: 5
      steps:
        - to:
            uri: "kamelet:log-sink"
```

`acknowledgementModeName` set to `CLIENT_ACKNOWLEDGE` also delivers a message again when its flow fails, without a transaction. `DUPS_OK_ACKNOWLEDGE` acknowledges the messages in batches: it is faster, but the messages processed since the last batch are delivered again after a crash.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-source.kamelet.yaml)