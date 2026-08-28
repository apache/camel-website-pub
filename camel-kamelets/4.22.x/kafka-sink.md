# ![kafka sink](_images/kamelets/kafka-sink.svg) Kafka Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to Kafka topics.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **oauthClientId** | OAuth Client ID | OAuth client ID. Required when saslAuthType is OAUTH. | string |  |  |
| **oauthClientSecret** | OAuth Client Secret | OAuth client secret. Required when saslAuthType is OAUTH. | string |  |  |
| **oauthScope** | OAuth Scope | OAuth scope. Optional when saslAuthType is OAUTH. | string |  |  |
| **oauthTokenEndpointUri** | OAuth Token Endpoint | OAuth token endpoint URI. Required when saslAuthType is OAUTH. | string |  |  |
| **saslAuthType** | Authentication Type | Authentication type to use. Use NONE for no authentication, PLAIN or SCRAM\_SHA\_256/SCRAM\_SHA\_512 for username/password, SSL for certificate-based, OAUTH for OAuth 2.0, AWS\_MSK\_IAM for MSK, or KERBEROS for Kerberos. Enum values: \* NONE \* PLAIN \* SCRAM\_SHA\_256 \* SCRAM\_SHA\_512 \* SSL \* OAUTH \* AWS\_MSK\_IAM \* KERBEROS | string | NONE |  |
| **saslPassword** | Password | Password for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **saslUsername** | Username | Username for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **sslKeyPassword** | SSL Key Password | The password of the private key in the key store file. | string |  |  |
| **sslKeystoreLocation** | SSL Keystore Location | The location of the key store file. Used for mTLS authentication. | string |  |  |
| **sslKeystorePassword** | SSL Keystore Password | The password for the key store file. | string |  |  |
| **sslTruststoreLocation** | SSL Truststore Location | The location of the trust store file. | string |  |  |
| **sslTruststorePassword** | SSL Truststore Password | The password for the trust store file. | string |  |  |

## Dependencies

At runtime, the `kafka-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:kafka-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kafka Sink Kamelet Description

### Headers Support

The Kamelet is able to understand the following headers to be set:

-   `key` / `ce-key`: as message key
    
-   `partition-key` / `ce-partitionkey`: as message partition key
    

Both headers are optional.

### Authentication

This Kamelet uses Plain Login Module for authentication with username and password.

### Security Protocols

Supports multiple security protocols: - SASL\_PLAINTEXT - PLAINTEXT - SASL\_SSL - SSL

Default security protocol is SASL\_SSL with PLAIN SASL mechanism.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-sink.kamelet.yaml)