# ![kafka source](_images/kamelets/kafka-source.svg) Kafka Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from Kafka topics.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **allowManualCommit** | Allow Manual Commit | Whether to allow doing manual commits. | boolean | false |  |
| **autoCommitEnable** | Auto Commit Enable | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | string | latest |  |
| **consumerGroup** | Consumer Group | A string that uniquely identifies the group of consumers to which this source belongs. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | When enabled the Kamelet source will deserialize all message headers to String representation. | boolean | true |  |
| **oauthClientId** | OAuth Client ID | OAuth client ID. Required when saslAuthType is OAUTH. | string |  |  |
| **oauthClientSecret** | OAuth Client Secret | OAuth client secret. Required when saslAuthType is OAUTH. | string |  |  |
| **oauthScope** | OAuth Scope | OAuth scope. Optional when saslAuthType is OAUTH. | string |  |  |
| **oauthTokenEndpointUri** | OAuth Token Endpoint | OAuth token endpoint URI. Required when saslAuthType is OAUTH. | string |  |  |
| **pollOnError** | Poll On Error Behavior | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of DISCARD, ERROR\_HANDLER, RECONNECT, RETRY, STOP. | string | ERROR\_HANDLER |  |
| **saslAuthType** | Authentication Type | Authentication type to use. Use NONE for no authentication, PLAIN or SCRAM\_SHA\_256/SCRAM\_SHA\_512 for username/password, SSL for certificate-based, OAUTH for OAuth 2.0, AWS\_MSK\_IAM for MSK, or KERBEROS for Kerberos. Enum values: \* NONE \* PLAIN \* SCRAM\_SHA\_256 \* SCRAM\_SHA\_512 \* SSL \* OAUTH \* AWS\_MSK\_IAM \* KERBEROS | string | NONE |  |
| **saslPassword** | Password | Password for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **saslUsername** | Username | Username for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **sslKeyPassword** | SSL Key Password | The password of the private key in the key store file. | string |  |  |
| **sslKeystoreLocation** | SSL Keystore Location | The location of the key store file. Used for mTLS authentication. | string |  |  |
| **sslKeystorePassword** | SSL Keystore Password | The password for the key store file. | string |  |  |
| **sslTruststoreLocation** | SSL Truststore Location | The location of the trust store file. | string |  |  |
| **sslTruststorePassword** | SSL Truststore Password | The password for the trust store file. | string |  |  |
| **topicIsPattern** | Topic Is Pattern | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | boolean | false |  |

## Dependencies

At runtime, the `kafka-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:kafka-source"
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

## Kafka Source Kamelet Description

### Authentication

This Kamelet requires SASL/PLAIN authentication to connect to Kafka through a Plain Login Module. The credentials are configured through the `user` and `password` properties.

### Configuration

The Kafka Source Kamelet supports the following configurations:

-   **Topic**: Comma-separated list of Kafka topic names to consume from (required)
    
-   **Bootstrap Servers**: Comma-separated list of Kafka bootstrap servers (required)
    
-   **User**: Username for SASL/PLAIN authentication (required)
    
-   **Password**: Password for SASL/PLAIN authentication (required)
    
-   **Consumer Group**: Kafka consumer group ID for managing offsets
    
-   **Auto Offset Reset**: What to do when there is no initial offset (earliest, latest, none)
    
-   **Allow Manual Commit**: Enable manual commit for better control over message processing
    

### Output Format

The Kamelet outputs Kafka message content and includes Kafka headers and metadata such as topic, partition, offset, and timestamp.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "orders,payments"
        bootstrapServers: "kafka.example.com:9092"
        user: "kafka-user"
        password: "kafka-password"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Consumer Group

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "user-events"
        bootstrapServers: "kafka1.example.com:9092,kafka2.example.com:9092"
        user: "kafka-user"
        password: "kafka-password"
        consumerGroup: "my-consumer-group"
        autoOffsetReset: "earliest"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Security

This kamelet uses SASL/PLAIN authentication mechanism with TLS encryption enabled for secure communication with Kafka brokers.

### Error Handling

The consumer automatically handles connection failures and will attempt to reconnect to the Kafka cluster. Failed message processing can be handled through Camel’s error handling mechanisms.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-source.kamelet.yaml)