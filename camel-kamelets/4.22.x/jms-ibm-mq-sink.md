# ![jms ibm mq sink](_images/kamelets/jms-ibm-mq-sink.svg) JMS - IBM MQ Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

A Kamelet that can produce events to an IBM MQ message queue using JMS.

## Configuration Options

The following table summarizes the configuration options available for the `jms-ibm-mq-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **channel** | IBM MQ Channel | **Required** Name of the IBM MQ Channel. | string |  |  |
| **destinationName** | Destination Name | **Required** The destination name. | string |  |  |
| **password** | Password | **Required** Password to authenticate to IBM MQ server. | string |  |  |
| **queueManager** | IBM MQ Queue Manager | **Required** Name of the IBM MQ Queue Manager. | string |  |  |
| **serverName** | IBM MQ Server name | **Required** IBM MQ Server name or address. | string |  |  |
| **serverPort** | IBM MQ Server Port | **Required** IBM MQ Server port. | integer | 1414 |  |
| **username** | Username | **Required** Username to authenticate to IBM MQ server. | string |  |  |
| **clientId** | IBM MQ Client ID | Name of the IBM MQ Client ID. | string |  |  |
| **destinationType** | Destination Type | The JMS destination type (queue or topic). | string | queue |  |
| **sslCipherSuite** | CipherSuite | CipherSuite to use for enabling TLS. | string |  |  |

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