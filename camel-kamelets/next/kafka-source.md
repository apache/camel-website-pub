# ![kafka source](_images/kamelets/kafka-source.svg) Kafka Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives each record from one or more topics in Apache Kafka, or in a Kafka-compatible service such as Amazon MSK, Confluent Cloud or Redpanda.

Use it to react to events or data that other applications publish, such as orders, sensor readings or changes from a database. To get many records in one message use `kafka-batch-source`. When the records are written with a schema kept in a schema registry, such as Confluent Schema Registry, Redpanda or Apicurio Registry, set `schemaRegistryVendor`.

Output: the body is the value of the record, as text. With `schemaRegistryVendor`, the value is read with its schema from the registry and the body is JSON text, such as `{"id": 7, "item": "camel"}` for an Avro record. A Protobuf record is turned into JSON by the Protobuf JSON mapping, such as `{"id":7,"item":"camel"}`: the names of the fields are in lowerCamelCase (`orderNo` for `order_no`), 64-bit numbers are text, and the fields that have their default value, such as 0 or empty text, are left out. A record without a value (a tombstone) gives a message with no body. The `kafka-topic`, `kafka-key`, `kafka-partition`, `kafka-offset` and `kafka-timestamp` (in milliseconds since 1970) headers say where the record came from. They are also set as `ce-kafkatopic`, `ce-kafkakey` and so on, and as the `CamelKafka*` headers that the Kafka actions read. The record headers become message headers, as text unless `deserializeHeaders` is false.

Good to know: `saslAuthType` has no default and must be set; `NONE` connects with no login and no TLS. A new consumer group starts at the newest records, unless `autoOffsetReset` is `earliest`. Without `consumerGroup`, every start uses a new group, so the records sent while the integration was stopped are skipped. With `schemaRegistryVendor`, the integration needs the serde jars of the vendor, which Camel JBang downloads by itself; for `confluent` add the Confluent Maven repository, as in `camel run --repos=confluent`. With `aws-glue` and `azure`, the serde logs in with the credentials of the environment the integration runs in: the AWS default credentials chain, or the Azure `DefaultAzureCredential` (such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` variables). To log in to a `confluent` or `apicurio` registry, set `schemaRegistryUsername` and `schemaRegistryPassword` (for Confluent Cloud, the API key and secret of the Schema Registry), or the OAuth2 client credentials `schemaRegistryOauthClientId`, `schemaRegistryOauthClientSecret` and `schemaRegistryOauthTokenEndpoint`, such as of a Keycloak client; these options are not used with `aws-glue` and `azure`, and setting one fails at startup. Kafka only calls an OAuth2 token endpoint that is listed in the JVM system property `org.apache.kafka.sasl.oauthbearer.allowed.urls`, such as with `camel run --jvm-args=-Dorg.apache.kafka.sasl.oauthbearer.allowed.urls=https://idp.example.com/oauth2/token`; without it, the integration fails to start with `The URL cannot be accessed due to restrictions`. This applies to `schemaRegistryOauthTokenEndpoint` and to the `oauthTokenEndpointUri` of `saslAuthType` `OAUTH`.

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
| **oauthTokenEndpointUri** | OAuth Token URL | The URL of the OAuth 2.0 provider where the Kamelet gets its access token. Required when `saslAuthType` is `OAUTH`. The URL must also be listed in the JVM system property `org.apache.kafka.sasl.oauthbearer.allowed.urls`, or the integration fails to start. | string |  | https://auth.example.com/oauth2/token |
| **pollOnError** | Poll On Error Behavior | What to do when reading from Kafka fails: `ERROR_HANDLER` logs the error and goes on with the next records, `DISCARD` skips the records that failed, `RECONNECT` connects again and retries, `RETRY` reads the same records again, and `STOP` stops reading until the integration is restarted. Enum values: \* DISCARD \* ERROR\_HANDLER \* RECONNECT \* RETRY \* STOP | string | ERROR\_HANDLER |  |
| **saslPassword** | Password | The password of `saslUsername`. Required when `saslAuthType` is `PLAIN`, `SCRAM_SHA_256` or `SCRAM_SHA_512`. | string |  |  |
| **saslUsername** | Username | The user name to log in to Kafka with. Required when `saslAuthType` is `PLAIN`, `SCRAM_SHA_256` or `SCRAM_SHA_512`. | string |  |  |
| **schemaFormat** | Schema Format | The format of the record values in the schema registry: `avro`, `json` (JSON Schema) or `protobuf` (Protocol Buffers). With `apicurio`, use `avro` or `protobuf`; with `azure`, use `avro`. Only used when `schemaRegistryVendor` is set. Enum values: \* avro \* json \* protobuf | string | avro |  |
| **schemaRegistryName** | Schema Registry Name | The name of the registry in AWS Glue. When not set, it is `default-registry`. Only used when `schemaRegistryVendor` is `aws-glue`. | string |  |  |
| **schemaRegistryOauthClientId** | Schema Registry OAuth Client ID | The OAuth2 client id, to log in to a `confluent` or `apicurio` schema registry with client credentials. | string |  |  |
| **schemaRegistryOauthClientSecret** | Schema Registry OAuth Client Secret | The OAuth2 client secret of `schemaRegistryOauthClientId`. | string |  |  |
| **schemaRegistryOauthScope** | Schema Registry OAuth Scope | The OAuth2 scope to ask for when logging in to the schema registry with client credentials (optional). | string |  |  |
| **schemaRegistryOauthTokenEndpoint** | Schema Registry OAuth Token Endpoint | The token endpoint of the OAuth2 server, to log in to a `confluent` or `apicurio` schema registry with client credentials, such as the token endpoint of a Keycloak realm. The URL must also be listed in the JVM system property `org.apache.kafka.sasl.oauthbearer.allowed.urls`, or the integration fails to start. | string |  | http://keycloak:8080/realms/registry/protocol/openid-connect/token |
| **schemaRegistryPassword** | Schema Registry Password | The password of `schemaRegistryUsername`. For Confluent Cloud, the API secret of the Schema Registry. | string |  |  |
| **schemaRegistryRegion** | Schema Registry Region | The AWS region of the AWS Glue Schema Registry, such as `eu-west-1`. When not set, the region is taken from the environment, such as the `AWS_REGION` variable. Only used when `schemaRegistryVendor` is `aws-glue`. | string |  |  |
| **schemaRegistryUrl** | Schema Registry URL | The URL of the schema registry: for `confluent` such as `[http://localhost:8081](http://localhost:8081)`; for `apicurio` the URL of the registry API, such as `[http://localhost:8080/apis/registry/v3](http://localhost:8080/apis/registry/v3)`; for `azure` the fully qualified name of the Event Hubs namespace, such as `my-namespace.servicebus.windows.net`. Required when `schemaRegistryVendor` is set, except for `aws-glue`, where it can override the endpoint of the Glue service. | string |  |  |
| **schemaRegistryUsername** | Schema Registry Username | The username to log in to a `confluent` or `apicurio` schema registry, with `schemaRegistryPassword`. For Confluent Cloud, the API key of the Schema Registry. | string |  |  |
| **schemaRegistryVendor** | Schema Registry Vendor | The schema registry that holds the schemas of the record values: `confluent`, also for registries with the Confluent API such as Redpanda and Karapace; `apicurio` (Apicurio Registry 3.x); `aws-glue` (AWS Glue Schema Registry); or `azure` (Azure Schema Registry of Event Hubs). It sets the value deserializer and the registry properties, and its jars must be added to the integration (see below). Leave it unset when the records do not use a schema registry. Enum values: \* confluent \* apicurio \* aws-glue \* azure | string |  |  |
| **sslKeyPassword** | SSL Key Password | The password of the private key in the key store file in `sslKeystoreLocation`. | string |  |  |
| **sslKeystoreLocation** | SSL Keystore Location | The path of a key store file, in JKS format, with the certificate and private key of the client. Needed only to log in with a client certificate (mutual TLS), usually with `saslAuthType` `SSL`. | string |  | /etc/kafka/keystore.jks |
| **sslKeystorePassword** | SSL Keystore Password | The password of the key store file in `sslKeystoreLocation`. | string |  |  |
| **sslTruststoreLocation** | SSL Truststore Location | The path of a trust store file, in JKS format, with the certificates to trust the brokers by. Needed only when the brokers use a certificate that Java does not trust by default, such as a self-signed one. | string |  | /etc/kafka/truststore.jks |
| **sslTruststorePassword** | SSL Truststore Password | The password of the trust store file in `sslTruststoreLocation`. | string |  |  |
| **topicIsPattern** | Topic Is Pattern | If true, `topic` is a regular expression, such as `orders-.*`, and the Kamelet reads from every topic whose name matches it. | boolean | false |  |

## Dependencies

At runtime, the `kafka-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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
    
-   **schemaRegistryVendor** / **schemaRegistryUrl** / **schemaFormat** / **schemaRegistryRegion** / **schemaRegistryName**: Read the records with their schema from a schema registry, see below
    

### Output Format

The body is the Kafka record value. The record metadata is surfaced as headers under names that are not Camel internals, so a downstream consumer does not have to read the `CamelKafka*` headers directly. Each has a `ce-` prefixed CloudEvents counterpart as well.

-   `kafka-topic` from `CamelKafkaTopic` - the topic the record was consumed from, which is worth having when the Kamelet subscribes to several topics or to a pattern.
    
-   `kafka-key` from `CamelKafkaKey` - the record key, absent for records produced without one.
    
-   `kafka-partition` from `CamelKafkaPartition` - the partition the record came from.
    
-   `kafka-offset` from `CamelKafkaOffset` - the offset within that partition.
    
-   `kafka-timestamp` from `CamelKafkaTimestamp` - the record timestamp, in milliseconds since the epoch.
    

The `CamelKafka*` headers are left on the exchange as well, so consumers already reading them keep working. The Kafka record headers are passed through separately, controlled by the `deserializeHeaders` property.

### Schema registry

When the records are written with a schema kept in a schema registry, set `schemaRegistryVendor`, `schemaRegistryUrl` and, for JSON Schema or Protobuf, `schemaFormat: json` or `schemaFormat: protobuf` (the default is `avro`). The Kamelet reads each value with its schema and turns it into JSON text, so the next step gets text as without a registry: an Avro record becomes, for example, `{"id": 7, "item": "camel"}`. A Protobuf record is turned into JSON by the Protobuf JSON mapping, such as `{"id":7,"item":"camel"}`: the names of the fields are in lowerCamelCase (`orderNo` for `order_no`), 64-bit numbers are text, and the fields that have their default value, such as 0 or empty text, are left out.

  
| `schemaRegistryVendor` | `schemaFormat` | Registry |
| --- | --- | --- |
| `confluent` | `avro`, `json`, `protobuf` | Confluent Schema Registry, and the registries with the same API, such as the one of Redpanda and Karapace. `schemaRegistryUrl` is the URL of the registry, such as `[http://localhost:8081](http://localhost:8081)`. |
| `apicurio` | `avro`, `protobuf` | Apicurio Registry 3.x. `schemaRegistryUrl` is the URL of the registry API, such as `[http://localhost:8080/apis/registry/v3](http://localhost:8080/apis/registry/v3)`. |
| `aws-glue` | `avro`, `json`, `protobuf` | AWS Glue Schema Registry. Set `schemaRegistryRegion`, unless the environment has the region (such as `AWS_REGION`), and `schemaRegistryName`, unless the registry is `default-registry`. `schemaRegistryUrl` is not needed. The AWS credentials are taken from the AWS default credentials chain. |
| `azure` | `avro` | Azure Schema Registry of Event Hubs. `schemaRegistryUrl` is the fully qualified name of the namespace, such as `my-namespace.servicebus.windows.net`. The sink needs `schemaGroup`. The credentials are taken by the Azure `DefaultAzureCredential`, such as from the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` variables. |

The serde jars of the vendor are not part of the Kamelet. Camel JBang downloads them by itself; the Confluent jars are in the Confluent Maven repository, not in Maven Central, so run with `--repos=confluent`. In a Maven project, add the jar of the vendor and format, such as `io.confluent:kafka-avro-serializer`, and for Confluent the repository `[https://packages.confluent.io/maven/](https://packages.confluent.io/maven/)`. To log in to a `confluent` or `apicurio` registry, set `schemaRegistryUsername` and `schemaRegistryPassword` (basic auth), or `schemaRegistryOauthTokenEndpoint`, `schemaRegistryOauthClientId`, `schemaRegistryOauthClientSecret` and, if needed, `schemaRegistryOauthScope` (OAuth2). `azure` and `aws-glue` log in with the credentials of the environment.

```yaml
- route:
    from:
      uri: "kamelet:kafka-source"
      parameters:
        topic: orders
        bootstrapServers: "localhost:9092"
        saslAuthType: NONE
        schemaRegistryVendor: confluent
        schemaRegistryUrl: "http://localhost:8081"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

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