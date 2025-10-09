# ![kafka ssl source](_images/kamelets/kafka-ssl-source.svg) Kafka SSL Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from Kafka topics with SSL/TLS support

## Configuration Options

The following table summarizes the configuration options available for the `kafka-ssl-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **sslKeyPassword** | SSL Key Password | **Required** The password of the private key in the key store file. | string |  |  |
| **sslTruststoreLocation** | SSL Truststore Location | **Required** The location of the trust store file. | string |  |  |
| **sslTruststorePassword** | SSL Truststore Password | **Required** The store password for the trust store file. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **allowManualCommit** | Allow Manual Commit | Whether to allow doing manual commits. | boolean | false |  |
| **autoCommitEnable** | Auto Commit Enable | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | string | latest |  |
| **consumerGroup** | Consumer Group | A string that uniquely identifies the group of consumers to which this source belongs. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | When enabled the Kamelet source will deserialize all message headers to String representation. | boolean | true |  |
| **pollOnError** | Poll On Error Behavior | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | string | ERROR\_HANDLER |  |
| **saslJaasConfig** | JAAS Configuration | Java Authentication and Authorization Service (JAAS) for Simple Authentication and Security Layer (SASL) configuration. | string |  |  |
| **saslMechanism** | SASL Mechanism | The Simple Authentication and Security Layer (SASL) Mechanism used. | string | GSSAPI |  |
| **securityProtocol** | Security Protocol | Protocol used to communicate with brokers. `SASL_PLAINTEXT`, `PLAINTEXT`, `SASL_SSL` and `SSL` are supported. | string | SSL |  |
| **sslEnabledProtocols** | SSL Enabled Protocols | The list of protocols enabled for SSL connections. TLSv1.2, TLSv1.1 and TLSv1 are enabled by default. | string | TLSv1.2,TLSv1.1,TLSv1 |  |
| **sslEndpointAlgorithm** | SSL Endpoint Algorithm | The endpoint identification algorithm to validate server hostname using server certificate. Use none or false to disable server hostname verification. | string | https |  |
| **sslKeystoreLocation** | SSL Keystore Location | The location of the key store file. This is optional for client and can be used for two-way authentication for client. | string |  |  |
| **sslKeystorePassword** | SSL Keystore Password | The store password for the key store file.This is optional for client and only needed if ssl.keystore.location is configured. | string |  |  |
| **sslProtocol** | SSL Protocol | The SSL protocol used to generate the SSLContext. Default setting is TLS, which is fine for most cases. Allowed values in recent JVMs are TLS, TLSv1.1 and TLSv1.2. SSL, SSLv2 and SSLv3 may be supported in older JVMs, but their usage is discouraged due to known security vulnerabilities. | string | TLSv1.2 |  |
| **topicIsPattern** | Topic Is Pattern | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | boolean | false |  |

## Dependencies

At runtime, the `kafka-ssl-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:kafka-ssl-source"
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

## Kafka-ssl-source Kamelet Description

### Authentication methods

This Kamelet connects to Kafka using appropriate security mechanisms based on the configuration type:

-   Security settings as indicated by the kamelet name (SSL, SCRAM, not-secured)
    
-   Schema registry integration where applicable
    
-   Bootstrap servers configuration
    

### Output format

The Kamelet consumes messages from Kafka topics and produces the message data in the configured format.

### Configuration

The Kamelet requires Kafka connection parameters:

-   `topic`: The Kafka topic to consume from
    
-   `bootstrapServers`: Comma separated list of Kafka Broker URLs
    
-   Security-specific parameters based on the authentication method
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kafka-ssl-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kafka-ssl-source
    properties:
      topic: "my-topic"
      bootstrapServers: "kafka-broker1:9092,kafka-broker2:9092"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-ssl-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-ssl-source.kamelet.yaml)