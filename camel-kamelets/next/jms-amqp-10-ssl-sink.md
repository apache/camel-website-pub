# ![jms amqp 10 ssl sink](_images/kamelets/jms-amqp-10-ssl-sink.svg) JMS - AMQP 1.0 SSL Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to any AMQP 1.0 compliant message broker over an SSL/TLS connection by using the Apache Qpid JMS client. SSL transport options can be configured as query parameters on the remoteURI (e.g. transport.trustStoreLocation, transport.trustStorePassword, transport.keyStoreLocation, transport.keyStorePassword, transport.verifyHost, transport.trustAll).

## Configuration Options

The following table summarizes the configuration options available for the `jms-amqp-10-ssl-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **destinationName** | Destination Name | **Required** The JMS destination name. | string |  |  |
| **remoteURI** | Broker URL | **Required** The JMS URL with amqps scheme and SSL transport options as query parameters. | string |  | amqps://my-host:5671?transport.trustStoreLocation=/path/to/truststore.jks&transport.trustStorePassword=changeit |
| **destinationType** | Destination Type | The JMS destination type (queue or topic). | string | queue |  |

## Dependencies

At runtime, the `jms-amqp-10-ssl-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:jms-amqp-10-ssl-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## JMS - AMQP 1.0 SSL Sink Kamelet Description

### Connection Configuration

This Kamelet connects to any AMQP 1.0 compliant message broker over an SSL/TLS connection using the Apache Qpid JMS client.

### SSL/TLS Configuration

SSL transport options are configured as query parameters on the `remoteURI`. Common options include:

-   `transport.trustStoreLocation`: Path to the truststore file
    
-   `transport.trustStorePassword`: Password for the truststore
    
-   `transport.keyStoreLocation`: Path to the keystore file
    
-   `transport.keyStorePassword`: Password for the keystore
    
-   `transport.verifyHost`: Verify hostname matches certificate (default: true)
    
-   `transport.trustAll`: Trust server certificate implicitly (default: false)
    

### Destination Configuration

The Kamelet supports both queue and topic destinations. The destination type can be configured using the `destinationType` property, which defaults to `queue`.

### AMQP 1.0 Protocol

This sink uses the AMQP 1.0 protocol over SSL/TLS for sending messages to the broker. AMQP 1.0 is an open standard messaging protocol that provides reliable, secure, and interoperable messaging.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-ssl-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-ssl-sink.kamelet.yaml)