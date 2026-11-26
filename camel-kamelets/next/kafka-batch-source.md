# ![kafka batch source](_images/kamelets/kafka-batch-source.svg) Kafka Batch Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives records from one or more topics in Apache Kafka in batches, as one message that holds a list of up to `batchSize` records.

Use it to handle many records at once, for example to write them to a database in one go, or to save the position in Kafka only once a whole batch was handled. To handle one record at a time use `kafka-source`. When the records are written with a schema kept in a schema registry, such as Confluent Schema Registry, Redpanda or Apicurio Registry, set `schemaRegistryVendor`.

Output: the body is a List with one entry per record, up to `batchSize`. Each entry is a Camel `Exchange` for one record, not a message: a step reads the value of the record, as text, with `getMessage().getBody()` on the entry, such as `${body[0].getMessage().getBody()}`. With `schemaRegistryVendor`, each value is read with its schema from the registry and is JSON text, such as `{"id": 7, "item": "camel"}` for an Avro record; a record without a value (a tombstone) gives an entry with no body. A Protobuf record is turned into JSON by the Protobuf JSON mapping, such as `{"id":7,"item":"camel"}`: the names of the fields are in lowerCamelCase (`orderNo` for `order_no`), 64-bit numbers are text, and the fields that have their default value, such as 0 or empty text, are left out. The message of the entry also has the key, offset and timestamp of the record in its `CamelKafkaKey`, `CamelKafkaOffset` and `CamelKafkaTimestamp` headers, and the record headers, as bytes. The message itself has the `CamelKafkaTopic` and `CamelKafkaPartition` headers. The `kafka-topic`, `kafka-key` and other headers of `kafka-source` are not set.

Good to know: `saslAuthType` has no default and must be set; `NONE` connects with no login and no TLS. To save the position in Kafka only once a batch was handled, set `allowManualCommit` to true and `autoCommitEnable` to false, and end the flow with `kafka-batch-manual-commit-action`. A new consumer group starts at the newest records, unless `autoOffsetReset` is `earliest`. Without `consumerGroup`, every start uses a new group, so the records sent while the integration was stopped are skipped. With `schemaRegistryVendor`, the integration needs the serde jars of the vendor, which Camel JBang downloads by itself; for `confluent` add the Confluent Maven repository, as in `camel run --repos=confluent`. With `aws-glue` and `azure`, the serde logs in with the credentials of the environment the integration runs in: the AWS default credentials chain, or the Azure `DefaultAzureCredential` (such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` variables). To log in to a `confluent` or `apicurio` registry, set `schemaRegistryUsername` and `schemaRegistryPassword` (for Confluent Cloud, the API key and secret of the Schema Registry), or the OAuth2 client credentials `schemaRegistryOauthClientId`, `schemaRegistryOauthClientSecret` and `schemaRegistryOauthTokenEndpoint`, such as of a Keycloak client; these options are not used with `aws-glue` and `azure`, and setting one fails at startup. Kafka only calls an OAuth2 token endpoint that is listed in the JVM system property `org.apache.kafka.sasl.oauthbearer.allowed.urls`, such as with `camel run --jvm-args=-Dorg.apache.kafka.sasl.oauthbearer.allowed.urls=https://idp.example.com/oauth2/token`; without it, the integration fails to start with `The URL cannot be accessed due to restrictions`. This applies to `schemaRegistryOauthTokenEndpoint` and to the `oauthTokenEndpointUri` of `saslAuthType` `OAUTH`.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-batch-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** The address of one or more Kafka brokers to connect to first, as `host:port`, separated by commas. The other brokers of the cluster are found from them. | string |  | broker1:9092,broker2:9092 |
| **saslAuthType** | Authentication Type | **Required** How to log in to Kafka. It has no default and must be set. `NONE` connects with no login and no TLS, as a local Kafka expects; `PLAIN`, `SCRAM_SHA_256` and `SCRAM_SHA_512` log in with `saslUsername` and `saslPassword`; `SSL` connects over TLS and logs in with the client certificate in `sslKeystoreLocation`, when set; `OAUTH` logs in with the `oauth` options; `AWS_MSK_IAM` (Amazon MSK) and `KERBEROS` take their credentials from the environment the integration runs in. All types except `NONE` connect over TLS. Enum values: \* NONE \* PLAIN \* SCRAM\_SHA\_256 \* SCRAM\_SHA\_512 \* SSL \* OAUTH \* AWS\_MSK\_IAM \* KERBEROS | string |  |  |
| **topic** | Topic Names | **Required** The topics to read from, separated by commas. When `topicIsPattern` is true, a regular expression that the names of the topics must match instead. | string |  | orders |
| **allowManualCommit** | Allow Manual Commit | If true, each message carries what `kafka-batch-manual-commit-action` needs to save the position of its records in Kafka. Set `autoCommitEnable` to false too, or the position is also saved automatically. | boolean | false |  |
| **autoCommitEnable** | Auto Commit | If true, the position reached in each partition (the offset) is saved in Kafka automatically every 5 seconds, so that a restarted integration goes on from there. Set it to false together with `allowManualCommit` true to save the position yourself with `kafka-batch-manual-commit-action`. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | Where to start when the consumer group has no saved position yet: `latest` reads only the records sent from now on, `earliest` reads all the records still in the topic, and `none` fails. | string | latest | earliest |
| **batchSize** | Batch Size | The largest number of records in one message. A message holds fewer when fewer records are waiting. | integer | 500 |  |
| **batchingIntervalMs** | Batching Interval | When set, a batch that has not reached `batchSize` is sent on after about this many milliseconds. It is checked only between two reads, so it can take up to `pollTimeout` longer. | integer |  | 10000 |
| **consumerGroup** | Consumer Group | The name of the consumer group. Integrations with the same group share the records of the topics between them, and the group remembers the position reached, so that a restarted integration goes on where it stopped. When it is not set, a new random group is used on every start. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | Meant to turn the values of the record headers into text. In a batch it has no effect: the record headers of the entries of the list stay bytes. | boolean | true |  |
| **maxPollIntervalMs** | Max Poll Interval | The longest time, in milliseconds, that the integration may take to handle one batch. When it takes longer, Kafka considers it failed and gives its partitions to another member of the consumer group. When it is not set, the Kafka default of 300000 (5 minutes) applies. | integer |  | 600000 |
| **oauthClientId** | OAuth Client ID | The ID of the client registered with the OAuth 2.0 provider. Required when `saslAuthType` is `OAUTH`. | string |  |  |
| **oauthClientSecret** | OAuth Client Secret | The secret of the OAuth client `oauthClientId`, from the OAuth 2.0 provider. Required when `saslAuthType` is `OAUTH`. | string |  |  |
| **oauthScope** | OAuth Scope | The scope to ask the OAuth 2.0 provider for, when it requires one. Only used when `saslAuthType` is `OAUTH`. | string |  | kafka |
| **oauthTokenEndpointUri** | OAuth Token URL | The URL of the OAuth 2.0 provider where the Kamelet gets its access token. Required when `saslAuthType` is `OAUTH`. The URL must also be listed in the JVM system property `org.apache.kafka.sasl.oauthbearer.allowed.urls`, or the integration fails to start. | string |  | https://auth.example.com/oauth2/token |
| **pollOnError** | Poll On Error Behavior | What to do when reading from Kafka fails: `ERROR_HANDLER` logs the error and goes on with the next records, `DISCARD` skips the records that failed, `RECONNECT` connects again and retries, `RETRY` reads the same records again, and `STOP` stops reading until the integration is restarted. Enum values: \* DISCARD \* ERROR\_HANDLER \* RECONNECT \* RETRY \* STOP | string | ERROR\_HANDLER |  |
| **pollTimeout** | Poll Timeout | How long one read from Kafka waits for new records, in milliseconds. | integer | 5000 |  |
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

At runtime, the `kafka-batch-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:kafka-batch-source"
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

## Kafka-batch-source Kamelet Description

### Authentication methods

The `saslAuthType` option chooses how the Kamelet logs in to Kafka, as for `kafka-source`. It has no default and must be set; `NONE` connects with no login and no TLS, as a local Kafka expects.

### Output format

Each message holds a batch: its body is a List with one entry per record, up to `batchSize`. Each entry has the value of the record as its body, and the record’s key, offset, timestamp and headers as its headers. To save the position in Kafka only once a batch was handled, set `allowManualCommit` to true and `autoCommitEnable` to false, and end the flow with `kafka-batch-manual-commit-action`.

### Configuration

The Kamelet requires Kafka connection parameters:

-   `topic`: The Kafka topic to consume from
    
-   `bootstrapServers`: Comma separated list of Kafka Broker URLs
    
-   `saslAuthType`: How to log in to Kafka, such as `NONE` for a local Kafka
    
-   Security-specific parameters based on the authentication method
    

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:kafka-batch-source"
      parameters:
        topic: "my-topic"
        bootstrapServers: "kafka-broker1:9092,kafka-broker2:9092"
        saslAuthType: "NONE"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-source.kamelet.yaml)