# ![kafka share source](_images/kamelets/kafka-share-source.svg) Kafka Share Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives each record from one or more Apache Kafka topics through a share group, which hands out the records like a queue: each record goes to one of many consumers.

Use it to share the work of a topic between many integrations or threads, more of them than the topic has partitions, such as orders or tasks that each take a while to handle, when the order of the records does not matter. To read the records in order, or to read them again from a given position, use `kafka-source`. Share groups are on by default from Kafka 4.2.

Output: the body is the value of the record, as text. With `schemaRegistryVendor`, the value is read with its schema from the registry and the body is JSON text, such as `{"id": 7, "item": "camel"}` for an Avro record. A Protobuf record is turned into JSON by the Protobuf JSON mapping, such as `{"id":7,"item":"camel"}`: the names of the fields are in lowerCamelCase (`orderNo` for `order_no`), 64-bit numbers are text, and the fields that have their default value, such as 0 or empty text, are left out. A record without a value (a tombstone) gives a message with no body. The `kafka-topic`, `kafka-key`, `kafka-partition`, `kafka-offset` and `kafka-timestamp` (in milliseconds since 1970) headers say where the record came from, and `kafka-delivery-count` how many times it has been delivered, this time included. They are also set as `ce-kafkatopic`, `ce-kafkakey` and so on, and as the `CamelKafka*` headers. The record headers become message headers, as text unless `deserializeHeaders` is false.

Good to know: each record is acknowledged on its own once the integration has handled it, and a record that was handled is not delivered again. A record whose handling fails is released by default: Kafka delivers it again, to this or another consumer, up to `group.share.delivery.count.limit` times in all (5 by default, a broker setting), and then drops it. Set `onFailure` to `REJECT` to drop it at once, or to `ACCEPT` to count it as handled. To decide for one record, set the header `CamelKafkaShareAcknowledge` to `ACCEPT`, `RELEASE` or `REJECT` in the integration, such as `REJECT` when `kafka-delivery-count` is too high; a record header of that name is not used. A record that takes longer to handle than the lock of the broker (`group.share.record.lock.duration.ms`, 30 seconds by default) is delivered to another consumer as well. A new share group starts at the newest records: the records sent before it first reads a topic are skipped. Set `autoOffsetReset` to `earliest` to read them: when the Kamelet starts, it sets the group setting `share.auto.offset.reset` on the broker, which needs the `ALTER_CONFIGS` permission on the group, and the Kamelet does not start when that fails. The setting only decides where the group starts on a partition it has not read yet, and it applies to all the consumers of the group. A Kafka of a single broker needs the broker settings `share.coordinator.state.topic.replication.factor=1` and `share.coordinator.state.topic.min.isr=1`, or the share group gets no records, with no error. `saslAuthType` has no default and must be set; `NONE` connects with no login and no TLS. With `schemaRegistryVendor`, the integration needs the serde jars of the vendor, which Camel JBang downloads by itself; for `confluent` add the Confluent Maven repository, as in `camel run --repos=confluent`. With `aws-glue` and `azure`, the serde logs in with the credentials of the environment the integration runs in: the AWS default credentials chain, or the Azure `DefaultAzureCredential`. To log in to a `confluent` or `apicurio` registry, set `schemaRegistryUsername` and `schemaRegistryPassword`, or the OAuth2 client credentials `schemaRegistryOauthClientId`, `schemaRegistryOauthClientSecret` and `schemaRegistryOauthTokenEndpoint`. Kafka only calls an OAuth2 token endpoint that is listed in the JVM system property `org.apache.kafka.sasl.oauthbearer.allowed.urls`; without it, the integration fails to start. This applies to `schemaRegistryOauthTokenEndpoint` and to the `oauthTokenEndpointUri` of `saslAuthType` `OAUTH`.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-share-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** The address of one or more Kafka brokers to connect to first, as `host:port`, separated by commas. The other brokers of the cluster are found from them. | string |  | broker1:9092,broker2:9092 |
| **saslAuthType** | Authentication Type | **Required** How to log in to Kafka. It has no default and must be set. `NONE` connects with no login and no TLS, as a local Kafka expects; `PLAIN`, `SCRAM_SHA_256` and `SCRAM_SHA_512` log in with `saslUsername` and `saslPassword`; `SSL` connects over TLS and logs in with the client certificate in `sslKeystoreLocation`, when set; `OAUTH` logs in with the `oauth` options; `AWS_MSK_IAM` (Amazon MSK) and `KERBEROS` take their credentials from the environment the integration runs in. All types except `NONE` connect over TLS. Enum values: \* NONE \* PLAIN \* SCRAM\_SHA\_256 \* SCRAM\_SHA\_512 \* SSL \* OAUTH \* AWS\_MSK\_IAM \* KERBEROS | string |  |  |
| **shareGroup** | Share Group | **Required** The name of the share group. All the consumers with the same share group, in this and in other integrations, share the records of the topics: each record goes to one of them. The group remembers which records were handled, so that a restarted integration goes on where it stopped. | string |  | order-workers |
| **topic** | Topic Names | **Required** The topics to read from, separated by commas. A share group cannot read the topics whose names match a regular expression. | string |  | orders |
| **autoOffsetReset** | Auto Offset Reset | Where a new share group starts reading a topic: `earliest` (the oldest records), `latest` (the records sent from now on, as Kafka does when it is not set) or `by_duration:` followed by an ISO-8601 duration, such as `by_duration:PT1H` for the records of the last hour. It is set on the group when the Kamelet starts, and needs the `ALTER_CONFIGS` permission on the group. When it is not set, the group setting is left as it is. | string |  | earliest |
| **consumersCount** | Consumers Count | How many consumers of the share group this Kamelet runs, each on its own thread, so that this many records are handled at the same time. Unlike a consumer group, it is not limited by the number of partitions of the topics. | integer | 1 |  |
| **deserializeHeaders** | Automatically Deserialize Headers | If true, the values of the record headers are turned into text. If false, they stay bytes. | boolean | true |  |
| **oauthClientId** | OAuth Client ID | The ID of the client registered with the OAuth 2.0 provider. Required when `saslAuthType` is `OAUTH`. | string |  |  |
| **oauthClientSecret** | OAuth Client Secret | The secret of the OAuth client `oauthClientId`, from the OAuth 2.0 provider. Required when `saslAuthType` is `OAUTH`. | string |  |  |
| **oauthScope** | OAuth Scope | The scope to ask the OAuth 2.0 provider for, when it requires one. Only used when `saslAuthType` is `OAUTH`. | string |  | kafka |
| **oauthTokenEndpointUri** | OAuth Token URL | The URL of the OAuth 2.0 provider where the Kamelet gets its access token. Required when `saslAuthType` is `OAUTH`. The URL must also be listed in the JVM system property `org.apache.kafka.sasl.oauthbearer.allowed.urls`, or the integration fails to start. | string |  | https://auth.example.com/oauth2/token |
| **onFailure** | On Failure | What to do with a record whose handling failed: `RELEASE` gives it back to Kafka, which delivers it again, to this or another consumer, until the delivery limit of the broker is reached; `REJECT` drops it, and it is not delivered again; `ACCEPT` counts it as handled, and it is not delivered again. Enum values: \* ACCEPT \* RELEASE \* REJECT | string | RELEASE |  |
| **pollOnError** | Poll On Error Behavior | What to do when reading from Kafka fails: `ERROR_HANDLER` logs the error and reads again, `DISCARD` and `RETRY` read again, `RECONNECT` connects again, and `STOP` stops reading until the integration is restarted. A record whose handling fails is not a read error: see `onFailure`. Enum values: \* DISCARD \* ERROR\_HANDLER \* RECONNECT \* RETRY \* STOP | string | ERROR\_HANDLER |  |
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

## Dependencies

At runtime, the `kafka-share-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kafka
    
-   camel:kafka-share
    
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
      uri: "kamelet:kafka-share-source"
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-share-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-share-source.kamelet.yaml)