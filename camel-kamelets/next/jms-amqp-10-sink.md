# ![jms amqp 10 sink](_images/kamelets/jms-amqp-10-sink.svg) JMS - AMQP 1.0 Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to any AMQP 1.0 compliant message broker by using the Apache Qpid JMS client. For SSL/TLS connections, use the amqps:// scheme in the remoteURI and configure SSL transport options as query parameters (e.g. transport.trustStoreLocation, transport.trustStorePassword, transport.keyStoreLocation, transport.keyStorePassword, transport.verifyHost, transport.trustAll).

## Configuration Options

The following table summarizes the configuration options available for the `jms-amqp-10-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **destinationName** | Destination Name | **Required** The JMS destination name. | string |  |  |
| **remoteURI** | Broker URL | **Required** The JMS URL. Use the amqps:// scheme for SSL/TLS connections. | string |  | amqp://my-host:31616 |
| **destinationType** | Destination Type | The JMS destination type (queue or topic). | string | queue |  |

## Dependencies

At runtime, the `jms-amqp-10-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jms
    
-   camel:amqp
    
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
            uri: "kamelet:jms-amqp-10-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## JMS - AMQP 1.0 Sink Kamelet Description

### Connection Configuration

This Kamelet connects to any AMQP 1.0 compliant message broker using the Apache Qpid JMS client.

### Destination Configuration

The Kamelet supports both queue and topic destinations. The destination type can be configured using the `destinationType` property, which defaults to `queue`.

### AMQP 1.0 Protocol

This sink uses the AMQP 1.0 protocol for sending messages to the broker. AMQP 1.0 is an open standard messaging protocol that provides reliable, secure, and interoperable messaging.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-sink.kamelet.yaml)