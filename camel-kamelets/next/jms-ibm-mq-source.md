# ![jms ibm mq source](_images/kamelets/jms-ibm-mq-source.svg) JMS - IBM MQ Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each message from a queue or a topic of an IBM MQ queue manager, through JMS.

Use it to process work or events that other applications put on IBM MQ, such as an existing enterprise or mainframe system. Use `jms-ibm-mq-sink` to send to IBM MQ.

Output: the body is text for a JMS text message, and bytes for a bytes message. The JMS properties of the message become headers, along with the JMS headers such as `JMSMessageID` and `JMSTimestamp`, and IBM MQ details such as `JMSXUserID`, `JMS_IBM_PutDate` and `JMS_IBM_Format`.

Good to know: the IBM MQ client library is not included, as its licence is not the Apache one: add `mvn:com.ibm.mq:com.ibm.mq.jakarta.client` with a version to the dependencies of the integration (Camel JBang adds it by itself). From a queue, each message is removed when it is received, even when the rest of the flow then fails, and several copies of this source share the messages. From a topic (`destinationType` set to `topic`), it receives only the messages sent while it is connected, as the subscription is not durable. It connects with no TLS unless `sslCipherSuite` is set. When the queue manager cannot be reached, it starts anyway and tries again every 5 seconds.

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
| **clientId** | Client ID | An optional JMS client ID for the connection, which names this application to the queue manager. Leave it empty unless your IBM MQ administrator asks for one. | string |  |  |
| **destinationType** | Queue or Topic | Whether `destinationName` is a queue (`queue`) or a topic (`topic`). A queue keeps each message until one receiver takes it; a topic hands each message to every receiver subscribed at that moment. | string | queue |  |
| **sslCipherSuite** | TLS Cipher Suite | The TLS cipher suite to connect with, which must match the cipher spec of the channel on the queue manager. When it is set, the connection uses TLS; when it is not set, it does not. | string |  | TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 |

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-source.kamelet.yaml)