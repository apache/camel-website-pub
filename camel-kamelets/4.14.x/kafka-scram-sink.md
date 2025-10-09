# ![kafka scram sink](_images/kamelets/kafka-scram-sink.svg) Kafka Scram Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Send data to Kafka topics through SCRAM login module.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-scram-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **password** | Password | **Required** Password to authenticate to kafka. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **user** | Username | **Required** Username to authenticate to Kafka . | string |  |  |
| **saslMechanism** | SASL Mechanism | The Simple Authentication and Security Layer (SASL) Mechanism used. | string | SCRAM-SHA-512 |  |
| **securityProtocol** | Security Protocol | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | string | SASL\_SSL |  |

## Dependencies

At runtime, the `kafka-scram-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kafka
    
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
            uri: "kamelet:kafka-scram-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kafka Scram Sink Kamelet Description

### SCRAM Authentication

This Kamelet uses SCRAM (Salted Challenge Response Authentication Mechanism) for secure authentication with Kafka brokers. SCRAM provides a secure method for username/password authentication.

### Authentication Mechanism

The Kamelet supports SCRAM-SHA-512 by default, which provides strong cryptographic security. The authentication mechanism can be configured based on the Kafka broker’s security configuration.

### Security Protocol

Uses SASL\_SSL security protocol by default, ensuring both authentication and encryption for data in transit. This provides comprehensive security for Kafka communications.

### Credential Management

Requires username and password credentials that should be securely managed and rotated according to security best practices.

### Production Ready

This Kamelet is suitable for production environments requiring secure authentication without the complexity of certificate-based authentication.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-scram-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-scram-sink.kamelet.yaml)