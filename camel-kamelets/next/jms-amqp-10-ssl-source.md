# ![jms amqp 10 ssl source](_images/kamelets/jms-amqp-10-ssl-source.svg) JMS - AMQP 1.0 SSL Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Consume data from any AMQP 1.0 compliant message broker over an SSL/TLS connection by using the Apache Qpid JMS client. SSL transport options can be configured as query parameters on the remoteURI (e.g. transport.trustStoreLocation, transport.trustStorePassword, transport.keyStoreLocation, transport.keyStorePassword, transport.verifyHost, transport.trustAll).

## Configuration Options

The following table summarizes the configuration options available for the `jms-amqp-10-ssl-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **destinationName** | Destination Name | **Required** The JMS destination name. | string |  |  |
| **remoteURI** | Broker URL | **Required** The JMS URL with amqps scheme and SSL transport options as query parameters. | string |  | amqps://my-host:5671?transport.trustStoreLocation=/path/to/truststore.jks&transport.trustStorePassword=changeit |
| **destinationType** | Destination Type | The JMS destination type (queue or topic). | string | queue |  |

## Dependencies

At runtime, the `jms-amqp-10-ssl-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:jms-amqp-10-ssl-source"
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

## JMS AMQP 1.0 SSL Source Kamelet Description

### Authentication methods

This Kamelet supports AMQP 1.0 authentication mechanisms over SSL/TLS including:

-   SASL authentication with username and password
    
-   Connection to AMQP 1.0 brokers over SSL/TLS
    

### SSL/TLS Configuration

SSL transport options are configured as query parameters on the `remoteURI`. Common options include:

-   `transport.trustStoreLocation`: Path to the truststore file
    
-   `transport.trustStorePassword`: Password for the truststore
    
-   `transport.keyStoreLocation`: Path to the keystore file
    
-   `transport.keyStorePassword`: Password for the keystore
    
-   `transport.verifyHost`: Verify hostname matches certificate (default: true)
    
-   `transport.trustAll`: Trust server certificate implicitly (default: false)
    

### Output format

The Kamelet consumes messages from JMS AMQP 1.0 queues over SSL/TLS and produces the message data in the configured format.

### Configuration

The Kamelet requires connection parameters for the AMQP 1.0 broker:

-   `remoteURI`: The AMQPS broker URI with SSL transport options
    
-   `destinationName`: The destination queue or topic name
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: jms-amqp-10-ssl-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: jms-amqp-10-ssl-source
    properties:
      remoteURI: "amqps://broker.example.com:5671?transport.trustStoreLocation=/path/to/truststore.jks&transport.trustStorePassword=changeit"
      destinationName: "my-queue"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-ssl-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/jms-amqp-10-ssl-source.kamelet.yaml)