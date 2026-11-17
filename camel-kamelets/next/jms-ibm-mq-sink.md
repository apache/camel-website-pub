# ![jms ibm mq sink](_images/kamelets/jms-ibm-mq-sink.svg) JMS - IBM MQ Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a queue or a topic of an IBM MQ queue manager, through JMS.

Use it to hand work or events to applications that read from IBM MQ, such as an existing enterprise or mainframe system. Use `jms-ibm-mq-source` to read from IBM MQ.

Input: text is sent as a JMS text message, and bytes as a JMS bytes message. The headers of the message, except the Camel ones, are sent along as JMS properties of the message.

Output: the message is unchanged.

Good to know: the IBM MQ client library is not included, as its licence is not the Apache one: add `mvn:com.ibm.mq:com.ibm.mq.jakarta.client` with a version to the dependencies of the integration (Camel JBang adds it by itself). It connects as a client over the network, with no TLS unless `sslCipherSuite` is set. Messages go to a queue unless `destinationType` is `topic`, and a message sent to a topic reaches only the receivers subscribed at that moment. It does not wait for a reply, even when the incoming message expects one, as one from `webhook-source` does.

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
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **sslCipherSuite** | TLS Cipher Suite | The TLS cipher suite to connect with, which must match the cipher spec of the channel on the queue manager. When it is set, the connection uses TLS; when it is not set, it does not. | string |  | TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 |

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

Optional SSL/TLS encryption can be enabled by configuring the `sslCipherSuite` property with an appropriate cipher suite.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-sink.kamelet.yaml)