# ![jms ibm mq sink](_images/kamelets/jms-ibm-mq-sink.svg) JMS - IBM MQ Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a queue or a topic of an IBM MQ queue manager, through JMS.

Use it to hand work or events to applications that read from IBM MQ, such as an existing enterprise or mainframe system. Use `jms-ibm-mq-source` to read from IBM MQ.

Input: text is sent as a JMS text message, and bytes as a JMS bytes message; `jmsMessageType` sends text or bytes as the other kind. The headers of the message, except the Camel ones, are sent along as JMS properties of the message.

Output: the message is unchanged.

Good to know: the IBM MQ client library is not included, as its licence is not the Apache one: add `mvn:com.ibm.mq:com.ibm.mq.jakarta.client` with a version to the dependencies of the integration (Camel JBang adds it by itself). It connects as a client over the network, with no TLS unless `sslCipherSuite` is set; the trust store and the key store for TLS are those of the Java runtime (`javax.net.ssl.trustStore`, `javax.net.ssl.keyStore`). For a multi-instance queue manager, list its instances in `connectionNameList`. Messages go to a queue unless `destinationType` is `topic`, and a message sent to a topic reaches only the receivers subscribed at that moment. Messages are persistent, with priority 4, and never expire, unless `deliveryPersistent`, `priority` and `timeToLive` say otherwise. It does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does. Headers that start with `CamelJms` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `jms-ibm-mq-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **channel** | Channel | **Required** The name of the server-connection channel of the queue manager to connect through. | string |  | DEV.APP.SVRCONN |
| **destinationName** | Queue or Topic Name | **Required** The name of the queue or topic to send the messages to, as defined in the queue manager. | string |  | DEV.QUEUE.1 |
| **password** | Password | **Required** The password to log in to the queue manager with, for the user `username`. | string |  |  |
| **queueManager** | Queue Manager | **Required** The name of the queue manager to connect to. | string |  | QM1 |
| **serverName** | Server Host | **Required** The host name or IP address of the IBM MQ server that runs the queue manager. | string |  | mq.example.com |
| **serverPort** | Server Port | **Required** The port of the listener of the queue manager on the server. The IBM MQ default is 1414. | integer | 1414 |  |
| **username** | Username | **Required** The user name to log in to the queue manager with. | string |  |  |
| **clientId** | Client ID | An optional JMS client ID for the connection, which names this application to the queue manager. Leave it empty unless your IBM MQ administrator asks for one. | string |  |  |
| **connectionNameList** | Connection Name List | The addresses of the instances of a multi-instance queue manager, as `host(port)` separated by commas, such as `mq1.example.com(1414),mq2.example.com(1414)`. The client tries them in order and connects to the first that answers. `serverName` and `serverPort` take the place of the first address of the list, so set them to the first instance too. When it is not set, the client connects only to `serverName` and `serverPort`. | string |  | mq1.example.com(1414),mq2.example.com(1414) |
| **deliveryPersistent** | Persistent Delivery | Whether the queue manager stores each message on disk, so that it survives a restart of the queue manager. False sends non-persistent messages, which are faster but lost when the queue manager stops. When it is not set, the messages are persistent. | boolean |  |  |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **jmsMessageType** | JMS Message Type | The kind of JMS message to send, whatever the body: `Text` sends a text message, and `Bytes` a bytes message, for a receiver that expects one kind. When it is not set, the kind follows the body: text is sent as a text message, and bytes as a bytes message. Enum values: \* Text \* Bytes | string |  |  |
| **priority** | Priority | The JMS priority of each message, from 0 (lowest) to 9 (highest). Of the messages waiting on a queue, the queue manager delivers those with the highest priority first. When it is not set, 4. | integer |  | 7 |
| **sslCipherSuite** | TLS Cipher Suite | The TLS cipher suite to connect with, which must match the cipher spec of the channel on the queue manager, such as `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256` for `ANY_TLS12_OR_HIGHER`. When it is set, the connection uses TLS; when it is not set, it does not. The certificate of the queue manager is checked against the trust store of the Java runtime, and a channel that asks for a client certificate gets one from its key store: set them with the Java system properties `javax.net.ssl.trustStore` and `javax.net.ssl.keyStore`, with their passwords. Camel’s own TLS settings (`camel.ssl`) do not apply to IBM MQ. | string |  | TLS\_ECDHE\_RSA\_WITH\_AES\_128\_GCM\_SHA256 |
| **timeToLive** | Time to Live | How long each message may wait to be received, in milliseconds, such as 60000 for one minute. A message still waiting after that time expires: the queue manager does not deliver it, and removes it. When it is not set, the messages never expire. | integer |  | 60000 |

## Dependencies

At runtime, the `jms-ibm-mq-sink` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:jms-ibm-mq-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## JMS - IBM MQ Sink Kamelet Description

### Connection Configuration

This Kamelet connects to an IBM MQ message broker using JMS. IBM MQ is an enterprise-grade messaging middleware that provides reliable message delivery.

### Authentication

The Kamelet requires authentication credentials including username and password to connect to the IBM MQ server. These credentials should be configured securely.

### Destination Configuration

The Kamelet supports both queue and topic destinations. The destination type can be configured using the `destinationType` property, which defaults to `queue`.

### SSL/TLS Support

Optional SSL/TLS encryption can be enabled by configuring the `sslCipherSuite` property with an appropriate cipher suite. The IBM MQ client checks the certificate of the queue manager against the trust store of the Java runtime, and sends the client certificate from its key store: set them with the Java system properties `javax.net.ssl.trustStore` and `javax.net.ssl.keyStore`, with their passwords. Camel’s own TLS settings (`camel.ssl.*`) do not apply to the IBM MQ client.

### Multi-instance queue manager

For a multi-instance queue manager, list its instances in `connectionNameList`, such as `mq1.example.com(1414),mq2.example.com(1414)`. The client tries them in order and connects to the first that answers. `serverName` and `serverPort` take the place of the first address of the list, so set them to the first instance too.

### Persistence, priority and expiry

By default, each message is persistent, has priority 4, and never expires. Three options change that for every message the sink sends:

-   `deliveryPersistent`: `false` sends non-persistent messages, which are faster, but lost when the queue manager stops.
    
-   `priority`: from 0 (lowest) to 9 (highest). Of the messages waiting on a queue, the queue manager delivers those with the highest priority first.
    
-   `timeToLive`: how long a message may wait to be received, in milliseconds. An expired message is not delivered: the queue manager removes it.
    

`jmsMessageType` sends every message as a text message (`Text`) or a bytes message (`Bytes`), whatever the body, for a receiver that expects one kind.

```yaml
- route:
    from:
      uri: "kamelet:webhook-source"
      steps:
        - to:
            uri: "kamelet:jms-ibm-mq-sink"
            parameters:
              serverName: "mq.example.com"
              serverPort: 1414
              queueManager: "QM1"
              channel: "DEV.APP.SVRCONN"
              username: "app"
              password: "passw0rd"
              destinationName: "DEV.QUEUE.1"
              priority: 7
              timeToLive: 60000
              jmsMessageType: "Text"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-sink.kamelet.yaml)