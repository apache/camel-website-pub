# ![kafka source](_images/kamelets/kafka-source.svg) Kafka Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each record from one or more topics in Apache Kafka, or in a Kafka-compatible service such as Amazon MSK, Confluent Cloud or Redpanda.

Use it to react to events or data that other applications publish, such as orders, sensor readings or changes from a database. To get many records in one message use `kafka-batch-source`. When the records are written with a schema kept in a schema registry, use one of the `kafka-**-registry-**` sources instead.

Output: the body is the value of the record, as text. A record without a value (a tombstone) gives a message with no body. The `kafka-topic`, `kafka-key`, `kafka-partition`, `kafka-offset` and `kafka-timestamp` (in milliseconds since 1970) headers say where the record came from. They are also set as `ce-kafkatopic`, `ce-kafkakey` and so on, and as the `CamelKafka*` headers that the Kafka actions read. The record headers become message headers, as text unless `deserializeHeaders` is false.

Good to know: `saslAuthType` has no default and must be set; `NONE` connects with no login and no TLS. A new consumer group starts at the newest records, unless `autoOffsetReset` is `earliest`. Without `consumerGroup`, every start uses a new group, so the records sent while the integration was stopped are skipped.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** The address of one or more Kafka brokers to connect to first, as `host:port`, separated by commas. The other brokers of the cluster are found from them. | string |  | broker1:9092,broker2:9092 |
| **saslAuthType** | Authentication Type | **Required** How to log in to Kafka. It has no default and must be set. `NONE` connects with no login and no TLS, as a local Kafka expects; `PLAIN`, `SCRAM_SHA_256` and `SCRAM_SHA_512` log in with `saslUsername` and `saslPassword`; `SSL` connects over TLS and logs in with the client certificate in `sslKeystoreLocation`, when set; `OAUTH` logs in with the `oauth` options; `AWS_MSK_IAM` (Amazon MSK) and `KERBEROS` take their credentials from the environment the integration runs in. All types except `NONE` connect over TLS. Enum values: \* NONE \* PLAIN \* SCRAM\_SHA\_256 \* SCRAM\_SHA\_512 \* SSL \* OAUTH \* AWS\_MSK\_IAM \* KERBEROS | string |  |  |
| **topic** | Topic Names | **Required** The topics to read from, separated by commas. When `topicIsPattern` is true, a regular expression that the names of the topics must match instead. | string |  | orders |
| **allowManualCommit** | Allow Manual Commit | If true, each message carries what `kafka-manual-commit-action` needs to save the position of its record in Kafka. Set `autoCommitEnable` to false too, or the position is also saved automatically. | boolean | false |  |
| **autoCommitEnable** | Auto Commit | If true, the position reached in each partition (the offset) is saved in Kafka automatically every 5 seconds, so that a restarted integration goes on from there. Set it to false together with `allowManualCommit` true to save the position yourself with `kafka-manual-commit-action`. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | Where to start when the consumer group has no saved position yet: `latest` reads only the records sent from now on, `earliest` reads all the records still in the topic, and `none` fails. | string | latest | earliest |
| **consumerGroup** | Consumer Group | The name of the consumer group. Integrations with the same group share the records of the topics between them, and the group remembers the position reached, so that a restarted integration goes on where it stopped. When it is not set, a new random group is used on every start. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | If true, the values of the record headers are turned into text. If false, they stay bytes. | boolean | true |  |
| **oauthClientId** | OAuth Client ID | The ID of the client registered with the OAuth 2.0 provider. Required when `saslAuthType` is `OAUTH`. | string |  |  |
| **oauthClientSecret** | OAuth Client Secret | The secret of the OAuth client `oauthClientId`, from the OAuth 2.0 provider. Required when `saslAuthType` is `OAUTH`. | string |  |  |
| **oauthScope** | OAuth Scope | The scope to ask the OAuth 2.0 provider for, when it requires one. Only used when `saslAuthType` is `OAUTH`. | string |  | kafka |
| **oauthTokenEndpointUri** | OAuth Token URL | The URL of the OAuth 2.0 provider where the Kamelet gets its access token. Required when `saslAuthType` is `OAUTH`. | string |  | https://auth.example.com/oauth2/token |
| **pollOnError** | Poll On Error Behavior | What to do when reading from Kafka fails: `ERROR_HANDLER` logs the error and goes on with the next records, `DISCARD` skips the records that failed, `RECONNECT` connects again and retries, `RETRY` reads the same records again, and `STOP` stops reading until the integration is restarted. Enum values: \* DISCARD \* ERROR\_HANDLER \* RECONNECT \* RETRY \* STOP | string | ERROR\_HANDLER |  |
| **saslPassword** | Password | The password of `saslUsername`. Required when `saslAuthType` is `PLAIN`, `SCRAM_SHA_256` or `SCRAM_SHA_512`. | string |  |  |
| **saslUsername** | Username | The user name to log in to Kafka with. Required when `saslAuthType` is `PLAIN`, `SCRAM_SHA_256` or `SCRAM_SHA_512`. | string |  |  |
| **sslKeyPassword** | SSL Key Password | The password of the private key in the key store file in `sslKeystoreLocation`. | string |  |  |
| **sslKeystoreLocation** | SSL Keystore Location | The path of a key store file, in JKS format, with the certificate and private key of the client. Needed only to log in with a client certificate (mutual TLS), usually with `saslAuthType` `SSL`. | string |  | /etc/kafka/keystore.jks |
| **sslKeystorePassword** | SSL Keystore Password | The password of the key store file in `sslKeystoreLocation`. | string |  |  |
| **sslTruststoreLocation** | SSL Truststore Location | The path of a trust store file, in JKS format, with the certificates to trust the brokers by. Needed only when the brokers use a certificate that Java does not trust by default, such as a self-signed one. | string |  | /etc/kafka/truststore.jks |
| **sslTruststorePassword** | SSL Truststore Password | The password of the trust store file in `sslTruststoreLocation`. | string |  |  |
| **topicIsPattern** | Topic Is Pattern | If true, `topic` is a regular expression, such as `orders-.*`, and the Kamelet reads from every topic whose name matches it. | boolean | false |  |

## Dependencies

At runtime, the `kafka-source` Kamelet relies upon the presence of the following dependencies:

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

Authentication is selected with `saslAuthType`, which is required and has no default, so the choice is always explicit. The accepted values are `NONE`, `PLAIN`, `SCRAM_SHA_256`, `SCRAM_SHA_512`, `SSL`, `OAUTH`, `AWS_MSK_IAM` and `KERBEROS`. `NONE` is a valid choice and connects to an unauthenticated broker over a plaintext connection — it just has to be asked for rather than inherited.

Which other properties are needed depends on that choice:

-   `PLAIN`, `SCRAM_SHA_256` and `SCRAM_SHA_512` take `saslUsername` and `saslPassword`.
    
-   `OAUTH` takes `oauthClientId`, `oauthClientSecret`, `oauthTokenEndpointUri` and `oauthScope`.
    
-   `SSL` takes the keystore and truststore properties below.
    
-   `AWS_MSK_IAM` and `KERBEROS` rely on the surrounding environment rather than on Kamelet properties.
    

Resolve credentials through a Camel vault rather than plaintext properties wherever the deployment allows it.

### Configuration

`topic`, `bootstrapServers` and `saslAuthType` are required. The Kamelet supports:

-   **topic**: Comma-separated list of Kafka topic names to consume from (required)
    
-   **bootstrapServers**: Comma-separated list of Kafka bootstrap servers (required)
    
-   **saslAuthType**: Authentication mechanism, no default (required)
    
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

`saslAuthType` has no default, so the security of the connection is always chosen explicitly. With `NONE` the Kamelet talks to the broker in the clear, with no login. All the other types connect over TLS; supply the truststore properties when the brokers use a certificate that Java does not trust by default, and the keystore properties to log in with a client certificate.

### Error Handling

The consumer automatically handles connection failures and will attempt to reconnect to the Kafka cluster. Failed message processing can be handled through Camel’s error handling mechanisms.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-source.kamelet.yaml)