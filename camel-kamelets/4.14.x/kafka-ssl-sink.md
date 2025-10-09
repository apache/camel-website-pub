# ![kafka ssl sink](_images/kamelets/kafka-ssl-sink.svg) Kafka SSL Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to Kafka topics wit TLS/SSL support.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-ssl-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Brokers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **sslKeyPassword** | SSL Key Password | **Required** The password of the private key in the key store file. | string |  |  |
| **sslKeystoreLocation** | SSL Keystore Location | **Required** The location of the key store file. This is optional for client and can be used for two-way authentication for client. | string |  |  |
| **sslKeystorePassword** | SSL Keystore Password | **Required** The store password for the key store file.This is optional for client and only needed if ssl.keystore.location is configured. | string |  |  |
| **sslTruststoreLocation** | SSL Truststore Location | **Required** The location of the trust store file. | string |  |  |
| **sslTruststorePassword** | SSL Truststore Password | **Required** The store password for the trust store file. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **saslMechanism** | SASL Mechanism | The Simple Authentication and Security Layer (SASL) Mechanism used. | string | GSSAPI |  |
| **securityProtocol** | Security Protocol | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | string | SSL |  |
| **sslEnabledProtocols** | SSL Enabled Protocols | The list of protocols enabled for SSL connections. TLSv1.2, TLSv1.1 and TLSv1 are enabled by default. | string | TLSv1.2,TLSv1.1,TLSv1 |  |
| **sslEndpointAlgorithm** | SSL Endpoint Algorithm | The endpoint identification algorithm to validate server hostname using server certificate. Use none or false to disable server hostname verification. | string | https |  |
| **sslProtocol** | SSL Protocol | The SSL protocol used to generate the SSLContext. Default setting is TLS, which is fine for most cases. Allowed values in recent JVMs are TLS, TLSv1.1 and TLSv1.2. SSL, SSLv2 and SSLv3 may be supported in older JVMs, but their usage is discouraged due to known security vulnerabilities. | string | TLSv1.2 |  |

## Dependencies

At runtime, the `kafka-ssl-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:kafka-ssl-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kafka SSL Sink Kamelet Description

### TLS/SSL Encryption

This Kamelet provides secure communication with Kafka brokers using TLS/SSL encryption. It supports both one-way and mutual (two-way) SSL authentication.

### Certificate Configuration

Requires configuration of SSL keystores and truststores:

-   Keystore: Contains the client’s private key and certificate (for mutual authentication)
    
-   Truststore: Contains trusted certificate authorities and broker certificates
    
-   Password protection for both keystores and private keys
    

### SSL Protocol Support

Supports modern TLS protocols (TLSv1.2 by default) with configurable enabled protocols. Older SSL versions are discouraged due to security vulnerabilities.

### Hostname Verification

Includes endpoint identification algorithm for server hostname verification using server certificates, ensuring protection against man-in-the-middle attacks.

### Production Security

Designed for production environments requiring strong encryption and certificate-based authentication. Provides comprehensive security for sensitive data transmission.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-ssl-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-ssl-sink.kamelet.yaml)