# ![jms ibm mq source](_images/kamelets/jms-ibm-mq-source.svg) JMS - IBM MQ Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

A Kamelet that can read events from an IBM MQ message queue using JMS.

## Configuration Options

The following table summarizes the configuration options available for the `jms-ibm-mq-source` Kamelet:

     
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

This Kamelet supports IBM MQ authentication including:

-   Channel and queue manager configuration
    
-   Username and password authentication
    
-   IBM MQ specific connection settings
    

### Output format

The Kamelet consumes messages from IBM MQ queues and produces the message data in the configured format.

### Configuration

The Kamelet requires IBM MQ specific connection parameters:

-   `destinationName`: The destination queue name
    
-   `queueManager`: IBM MQ queue manager name
    
-   `channel`: IBM MQ channel name
    
-   `connName`: IBM MQ connection name (host:port)
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: jms-ibm-mq-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: jms-ibm-mq-source
    properties:
      destinationName: "MY.QUEUE"
      queueManager: "QM1"
      channel: "DEV.APP.SVRCONN"
      connName: "localhost(1414)"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-ibm-mq-source.kamelet.yaml)