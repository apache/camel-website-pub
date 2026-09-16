Kamelet Catalog

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

Authentication is selected with `saslAuthType`, which defaults to `NONE`, so out of the box the Kamelet connects to an unauthenticated broker. The accepted values are `NONE`, `PLAIN`, `SCRAM_SHA_256`, `SCRAM_SHA_512`, `SSL`, `OAUTH`, `AWS_MSK_IAM` and `KERBEROS`.

Which other properties are needed depends on that choice:

-   `PLAIN`, `SCRAM_SHA_256` and `SCRAM_SHA_512` take `saslUsername` and `saslPassword`.
    
-   `OAUTH` takes `oauthClientId`, `oauthClientSecret`, `oauthTokenEndpointUri` and `oauthScope`.
    
-   `SSL` takes the keystore and truststore properties below.
    
-   `AWS_MSK_IAM` and `KERBEROS` rely on the surrounding environment rather than on Kamelet properties.
    

Resolve credentials through a Camel vault rather than plaintext properties wherever the deployment allows it.

### Configuration

Only `topic` and `bootstrapServers` are required. The Kamelet supports:

-   **topic**: Comma-separated list of Kafka topic names to consume from (required)
    
-   **bootstrapServers**: Comma-separated list of Kafka bootstrap servers (required)
    
-   **saslAuthType**: Authentication mechanism, default `NONE`
    
-   **saslUsername** / **saslPassword**: Credentials for the username and password mechanisms
    
-   **oauthClientId** / **oauthClientSecret** / **oauthTokenEndpointUri** / **oauthScope**: OAuth 2.0 settings
    
-   **sslTruststoreLocation** / **sslTruststorePassword** / **sslKeystoreLocation** / **sslKeystorePassword** / **sslKeyPassword**: TLS material
    
-   **consumerGroup**: Kafka consumer group ID for managing offsets
    
-   **autoOffsetReset**: What to do when there is no initial offset - `earliest`, `latest` or `none`, default `latest`
    
-   **autoCommitEnable**: Commit offsets automatically, default `true`
    
-   **allowManualCommit**: Enable manual commit for control over when offsets advance, default `false`
    
-   **pollOnError**: What to do when polling fails, default `ERROR_HANDLER`
    
-   **deserializeHeaders**: Deserialize the Kafka record headers onto the exchange, default `true`
    
-   **topicIsPattern**: Treat `topic` as a regular expression rather than a literal list, default `false`
    

### Output Format

The body is the Kafka record value. The record metadata is surfaced as headers under names that are not Camel internals, so a downstream consumer does not have to read the `CamelKafka*` headers directly. Each has a `ce-` prefixed CloudEvents counterpart as well.

-   `kafka-topic` from `CamelKafkaTopic` - the topic the record was consumed from, which is worth having when the Kamelet subscribes to several topics or to a pattern.
    
-   `kafka-key` from `CamelKafkaKey` - the record key, absent for records produced without one.
    
-   `kafka-partition` from `CamelKafkaPartition` - the partition the record came from.
    
-   `kafka-offset` from `CamelKafkaOffset` - the offset within that partition.
    
-   `kafka-timestamp` from `CamelKafkaTimestamp` - the record timestamp, in milliseconds since the epoch.
    

The `CamelKafka*` headers are left on the exchange as well, so consumers already reading them keep working. The Kafka record headers are passed through separately, controlled by the `deserializeHeaders` property.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: "orders,payments"
        bootstrapServers: "kafka.example.com:9092"
        saslAuthType: "PLAIN"
        saslUsername: "kafka-user"
        saslPassword: "kafka-password"
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
        saslAuthType: "PLAIN"
        saslUsername: "kafka-user"
        saslPassword: "kafka-password"
        consumerGroup: "my-consumer-group"
        autoOffsetReset: "earliest"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Security

Nothing is enabled by default: `saslAuthType` is `NONE` and no TLS material is configured, so an unconfigured binding talks to the broker in the clear. Set `saslAuthType` and the matching properties for the mechanism the broker expects, and supply the truststore and keystore properties for a TLS listener.

### Error Handling

The consumer automatically handles connection failures and will attempt to reconnect to the Kafka cluster. Failed message processing can be handled through Camel’s error handling mechanisms.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-source.kamelet.yaml)