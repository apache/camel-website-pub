# ![kafka sink](_images/kamelets/kafka-sink.svg) Kafka Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as a record to a topic in Apache Kafka, or in a Kafka-compatible service such as Amazon MSK, Confluent Cloud or Redpanda.

Use it to publish events or data for other applications to read, such as orders, sensor readings or changes from a database. To write the records with a schema kept in a schema registry, such as Confluent Schema Registry, Redpanda or Apicurio Registry, set `schemaRegistryVendor`.

Input: the body becomes the value of the record, as text. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. With `schemaRegistryVendor` and `schemaFormat` `json`, the body must be JSON text (or a Map), and the record is written with a JSON Schema; with `avro`, `confluent` and `apicurio` write a text body as an Avro string, while `aws-glue` needs an Avro record; with `protobuf`, the body must be a Protobuf message, such as an object of a class generated from the `.proto` file or a `DynamicMessage`, which a step before this sink must create in code, and JSON text fails. With `azure`, set `schemaGroup`. The optional `key` header (or `kafka-key`, `ce-key`, `ce-kafkakey`) becomes the key of the record, and the optional `partition-key` header (or `ce-partitionkey`) is the number of the partition to write to. The other headers of the message, except the Camel ones, are sent as record headers.

Output: the message is unchanged.

Good to know: `saslAuthType` has no default and must be set; `NONE` connects with no login and no TLS, as a local Kafka expects. A managed Kafka service needs one of the other types. With `schemaRegistryVendor`, the integration needs the serde jars of the vendor, which Camel JBang downloads by itself; for `confluent` add the Confluent Maven repository, as in `camel run --repos=confluent`. With `aws-glue` and `azure`, the serde logs in with the credentials of the environment the integration runs in: the AWS default credentials chain, or the Azure `DefaultAzureCredential` (such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` variables). To log in to a `confluent` or `apicurio` registry, set `schemaRegistryUsername` and `schemaRegistryPassword` (for Confluent Cloud, the API key and secret of the Schema Registry), or the OAuth2 client credentials `schemaRegistryOauthClientId`, `schemaRegistryOauthClientSecret` and `schemaRegistryOauthTokenEndpoint`, such as of a Keycloak client; these options are not used with `aws-glue` and `azure`, and setting one fails at startup. Kafka only calls an OAuth2 token endpoint that is listed in the JVM system property `org.apache.kafka.sasl.oauthbearer.allowed.urls`, such as with `camel run --jvm-args=-Dorg.apache.kafka.sasl.oauthbearer.allowed.urls=https://idp.example.com/oauth2/token`; without it, the integration fails to start with `The URL cannot be accessed due to restrictions`. This applies to `schemaRegistryOauthTokenEndpoint` and to the `oauthTokenEndpointUri` of `saslAuthType` `OAUTH`. The sink registers a schema made from the message, which with `json` accepts any JSON object; it does not check the message against a schema that is already registered for the topic. Headers that start with `CamelKafka`, except `CamelKafkaKey` and `CamelKafkaOverrideTopic`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **bootstrapServers** | Bootstrap Servers | **Required** The address of one or more Kafka brokers to connect to first, as `host:port`, separated by commas. The other brokers of the cluster are found from them. | string |  | broker1:9092,broker2:9092 |
| **saslAuthType** | Authentication Type | **Required** How to log in to Kafka. It has no default and must be set. `NONE` connects with no login and no TLS, as a local Kafka expects; `PLAIN`, `SCRAM_SHA_256` and `SCRAM_SHA_512` log in with `saslUsername` and `saslPassword`; `SSL` connects over TLS and logs in with the client certificate in `sslKeystoreLocation`, when set; `OAUTH` logs in with the `oauth` options; `AWS_MSK_IAM` (Amazon MSK) and `KERBEROS` take their credentials from the environment the integration runs in. All types except `NONE` connect over TLS. Enum values: \* NONE \* PLAIN \* SCRAM\_SHA\_256 \* SCRAM\_SHA\_512 \* SSL \* OAUTH \* AWS\_MSK\_IAM \* KERBEROS | string |  |  |
| **topic** | Topic Name | **Required** The name of the topic to write the records to. | string |  | orders |
| **oauthClientId** | OAuth Client ID | OAuth client ID. Required when saslAuthType is OAUTH. | string |  |  |
| **oauthClientSecret** | OAuth Client Secret | OAuth client secret. Required when saslAuthType is OAUTH. | string |  |  |
| **oauthScope** | OAuth Scope | OAuth scope. Optional when saslAuthType is OAUTH. | string |  |  |
| **oauthTokenEndpointUri** | OAuth Token Endpoint | OAuth token endpoint URI. Required when saslAuthType is OAUTH. The URL must also be listed in the JVM system property `org.apache.kafka.sasl.oauthbearer.allowed.urls`, or the integration fails to start. | string |  |  |
| **saslPassword** | Password | Password for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **saslUsername** | Username | Username for SASL authentication. Required when saslAuthType is PLAIN, SCRAM\_SHA\_256, or SCRAM\_SHA\_512. | string |  |  |
| **schemaFormat** | Schema Format | The format of the record values in the schema registry: `avro`, `json` (JSON Schema) or `protobuf` (Protocol Buffers). With `apicurio`, use `avro` or `protobuf`; with `azure`, use `avro`. Only used when `schemaRegistryVendor` is set. Enum values: \* avro \* json \* protobuf | string | avro |  |
| **schemaGroup** | Schema Group | The schema group in the Azure Schema Registry that the schemas of the records are registered in. Required when `schemaRegistryVendor` is `azure`. | string |  |  |
| **schemaRegistryName** | Schema Registry Name | The name of the registry in AWS Glue. When not set, it is `default-registry`. Only used when `schemaRegistryVendor` is `aws-glue`. | string |  |  |
| **schemaRegistryOauthClientId** | Schema Registry OAuth Client ID | The OAuth2 client id, to log in to a `confluent` or `apicurio` schema registry with client credentials. | string |  |  |
| **schemaRegistryOauthClientSecret** | Schema Registry OAuth Client Secret | The OAuth2 client secret of `schemaRegistryOauthClientId`. | string |  |  |
| **schemaRegistryOauthScope** | Schema Registry OAuth Scope | The OAuth2 scope to ask for when logging in to the schema registry with client credentials (optional). | string |  |  |
| **schemaRegistryOauthTokenEndpoint** | Schema Registry OAuth Token Endpoint | The token endpoint of the OAuth2 server, to log in to a `confluent` or `apicurio` schema registry with client credentials, such as the token endpoint of a Keycloak realm. The URL must also be listed in the JVM system property `org.apache.kafka.sasl.oauthbearer.allowed.urls`, or the integration fails to start. | string |  | http://keycloak:8080/realms/registry/protocol/openid-connect/token |
| **schemaRegistryPassword** | Schema Registry Password | The password of `schemaRegistryUsername`. For Confluent Cloud, the API secret of the Schema Registry. | string |  |  |
| **schemaRegistryRegion** | Schema Registry Region | The AWS region of the AWS Glue Schema Registry, such as `eu-west-1`. When not set, the region is taken from the environment, such as the `AWS_REGION` variable. Only used when `schemaRegistryVendor` is `aws-glue`. | string |  |  |
| **schemaRegistryUrl** | Schema Registry URL | The URL of the schema registry: for `confluent` such as `[http://localhost:8081](http://localhost:8081)`; for `apicurio` the URL of the registry API, such as `[http://localhost:8080/apis/registry/v3](http://localhost:8080/apis/registry/v3)`; for `azure` the fully qualified name of the Event Hubs namespace, such as `my-namespace.servicebus.windows.net`. Required when `schemaRegistryVendor` is set, except for `aws-glue`, where it can override the endpoint of the Glue service. | string |  |  |
| **schemaRegistryUsername** | Schema Registry Username | The username to log in to a `confluent` or `apicurio` schema registry, with `schemaRegistryPassword`. For Confluent Cloud, the API key of the Schema Registry. | string |  |  |
| **schemaRegistryVendor** | Schema Registry Vendor | The schema registry that holds the schemas of the record values: `confluent`, also for registries with the Confluent API such as Redpanda and Karapace; `apicurio` (Apicurio Registry 3.x); `aws-glue` (AWS Glue Schema Registry); or `azure` (Azure Schema Registry of Event Hubs). It sets the value serializer and the registry properties, and its jars must be added to the integration (see below). Leave it unset when the records do not use a schema registry. Enum values: \* confluent \* apicurio \* aws-glue \* azure | string |  |  |
| **sslKeyPassword** | SSL Key Password | The password of the private key in the key store file. | string |  |  |
| **sslKeystoreLocation** | SSL Keystore Location | The location of the key store file. Used for mTLS authentication. | string |  |  |
| **sslKeystorePassword** | SSL Keystore Password | The password for the key store file. | string |  |  |
| **sslTruststoreLocation** | SSL Truststore Location | The location of the trust store file. | string |  |  |
| **sslTruststorePassword** | SSL Truststore Password | The password for the trust store file. | string |  |  |

## Dependencies

At runtime, the `kafka-sink` Kamelet relies upon the presence of the following dependencies:

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

### Authentication

The `saslAuthType` option chooses how the Kamelet logs in to Kafka. The options that each type needs are listed below; leave the others empty.

 
| `saslAuthType` | Options to set |
| --- | --- |
| `NONE` | None. No login and no TLS, as a local Kafka expects. |
| `PLAIN`, `SCRAM_SHA_256`, `SCRAM_SHA_512` | `saslUsername` and `saslPassword`. |
| `SSL` | `sslTruststoreLocation` and `sslTruststorePassword`; for mutual TLS also `sslKeystoreLocation`, `sslKeystorePassword` and `sslKeyPassword`. |
| `OAUTH` | `oauthClientId`, `oauthClientSecret` and `oauthTokenEndpointUri`; `oauthScope` when the provider asks for one. |
| `AWS_MSK_IAM` | None in the Kamelet: the AWS credentials are taken from the environment the integration runs in. |
| `KERBEROS` | None in the Kamelet: Kerberos is configured in the environment the integration runs in. |

### Schema registry

To write the records with a schema kept in a schema registry, set `schemaRegistryVendor`, `schemaRegistryUrl` and `schemaFormat` (the default is `avro`). With `json`, the body must be JSON text (or a Map); the Kamelet turns it into an object, and the record is written with a JSON Schema made from it, which accepts any JSON object. With `avro`, `confluent` and `apicurio` write a text body as an Avro string, while `aws-glue` needs an Avro record, which a step must create in code. With `protobuf`, the body must be a Protobuf message, such as an object of a class generated from the `.proto` file or a `DynamicMessage`, which a step must create in code; JSON text fails. With `azure`, also set `schemaGroup`. The sink registers the schema it makes, and does not check the message against a schema that is already registered for the topic.

  
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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: '{"id": 42, "item": "book"}'
        contentType: application/json
      steps:
        - to:
            uri: "kamelet:kafka-sink"
            parameters:
              bootstrapServers: "localhost:9092"
              topic: orders
              saslAuthType: NONE
              schemaRegistryVendor: confluent
              schemaRegistryUrl: "http://localhost:8081"
              schemaFormat: json
```

### Usage example

The route below sends a JSON order every ten seconds to the `orders` topic, with the order number as the record key.

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: '{"id": 42, "item": "book"}'
        contentType: application/json
      steps:
        - setHeader:
            name: key
            constant: "42"
        - to:
            uri: "kamelet:kafka-sink"
            parameters:
              bootstrapServers: "localhost:9092"
              topic: orders
              saslAuthType: NONE
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-sink.kamelet.yaml)