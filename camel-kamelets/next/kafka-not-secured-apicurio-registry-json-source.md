# ![kafka not secured apicurio registry json source](_images/kamelets/kafka-not-secured-apicurio-registry-json-source.svg) Kafka not secured with Apicurio Registry secured with Keycloak for JSON schema support Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Deprecated"**

Deprecated, to be removed in a later release: receives each record written with a JSON Schema from topics in Apache Kafka, with the schema kept in an Apicurio Registry secured with Keycloak.

Use it to read JSON records that other applications write with a JSON Schema of the registry, when the registry needs a Keycloak login and Kafka needs none. For Avro records use `kafka-not-secured-apicurio-registry-source`; when the registry needs no login use `kafka-apicurio-registry-not-secured-source`. This Kamelet is deprecated and will be removed in a later release, as the Kafka Kamelets are reduced to a few.

Output: the body is the value of the record as parsed JSON. The `kafka-topic`, `kafka-key`, `kafka-partition`, `kafka-offset` and `kafka-timestamp` (in milliseconds since 1970) headers say where the record came from. They are also set as `ce-kafkatopic`, `ce-kafkakey` and so on, and as the `CamelKafka*` headers that the Kafka actions read. The record headers become message headers, as text unless `deserializeHeaders` is false.

Good to know: Kafka is not secured: it connects to the brokers with no login and no TLS. A new consumer group starts at the newest records, unless `autoOffsetReset` is `earliest`. Without `consumerGroup`, every start uses a new group, so the records sent while the integration was stopped are skipped.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-not-secured-apicurio-registry-json-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apicurioAuthClientId** | Keycloak Client ID | **Required** The ID of the Keycloak client that has access to the registry. | string |  |  |
| **apicurioAuthClientSecret** | Keycloak Client Secret | **Required** The secret of the Keycloak client `apicurioAuthClientId`, from the Credentials tab of the client in the Keycloak admin console. | string |  |  |
| **apicurioAuthPassword** | Registry Password | **Required** The password of `apicurioAuthUsername`. | string |  |  |
| **apicurioAuthRealm** | Keycloak Realm | **Required** The Keycloak realm in which the client and the user of the registry are defined. | string |  | registry |
| **apicurioAuthServiceUrl** | Keycloak URL | **Required** The URL of the Keycloak server that secures the registry. | string |  | https://keycloak.example.com |
| **apicurioAuthUsername** | Registry Username | **Required** The user name to log in to the registry with, through Keycloak. | string |  |  |
| **apicurioRegistryUrl** | Apicurio Registry URL | **Required** The URL of the API of the Apicurio Registry that holds the schemas, such as `[http://registry:8080/apis/registry/v2](http://registry:8080/apis/registry/v2)`. | string |  | http://registry.example.com:8080/apis/registry/v2 |
| **bootstrapServers** | Bootstrap Servers | **Required** The address of one or more Kafka brokers to connect to first, as `host:port`, separated by commas. The other brokers of the cluster are found from them. | string |  | broker1:9092,broker2:9092 |
| **topic** | Topic Names | **Required** The topics to read from, separated by commas. When `topicIsPattern` is true, a regular expression that the names of the topics must match instead. | string |  | orders |
| **allowManualCommit** | Allow Manual Commit | If true, each message carries what `kafka-manual-commit-action` needs to save the position of its record in Kafka. Set `autoCommitEnable` to false too, or the position is also saved automatically. | boolean | false |  |
| **autoCommitEnable** | Auto Commit | If true, the position reached in each partition (the offset) is saved in Kafka automatically every 5 seconds, so that a restarted integration goes on from there. Set it to false together with `allowManualCommit` true to save the position yourself with `kafka-manual-commit-action`. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | Where to start when the consumer group has no saved position yet: `latest` reads only the records sent from now on, `earliest` reads all the records still in the topic, and `none` fails. | string | latest | earliest |
| **consumerGroup** | Consumer Group | The name of the consumer group. Integrations with the same group share the records of the topics between them, and the group remembers the position reached, so that a restarted integration goes on where it stopped. When it is not set, a new random group is used on every start. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | If true, the values of the record headers are turned into text. If false, they stay bytes. | boolean | true |  |
| **pollOnError** | Poll On Error Behavior | What to do when reading from Kafka fails: `ERROR_HANDLER` logs the error and goes on with the next records, `DISCARD` skips the records that failed, `RECONNECT` connects again and retries, `RETRY` reads the same records again, and `STOP` stops reading until the integration is restarted. Enum values: \* DISCARD \* ERROR\_HANDLER \* RECONNECT \* RETRY \* STOP | string | ERROR\_HANDLER |  |
| **topicIsPattern** | Topic Is Pattern | If true, `topic` is a regular expression, such as `orders-.*`, and the Kamelet reads from every topic whose name matches it. | boolean | false |  |
| **valueDeserializer** | Value Deserializer | The Java class that turns the value of the record into the body. The default reads JSON checked against the JSON Schema from the registry. Change it only to use another deserializer of the Apicurio Registry library. | string | io.apicurio.registry.serde.jsonschema.JsonSchemaKafkaDeserializer |  |

## Dependencies

At runtime, the `kafka-not-secured-apicurio-registry-json-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kafka
    
-   camel:kamelet
    
-   mvn:io.apicurio:apicurio-registry-serdes-jsonschema-serde:2.5.11.Final
    

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
      uri: "kamelet:kafka-not-secured-apicurio-registry-json-source"
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

## Kafka-not-secured-apicurio-registry-json-source Kamelet Description

> **Note**
> This Kamelet is deprecated and will be removed in a later release, as the Kafka Kamelets are reduced to a few.

### Authentication methods

This Kamelet connects to Kafka with no login and no TLS. It logs in to the Apicurio Registry through Keycloak, with the `apicurioAuth*` options.

### Output format

The Kamelet reads records written with a JSON Schema schema kept in the Apicurio Registry.

The Kafka record metadata is surfaced as headers under names that are not Camel internals, so a downstream consumer does not have to read the `CamelKafka*` headers directly. Each has a `ce-` prefixed CloudEvents counterpart as well.

-   `kafka-topic` from `CamelKafkaTopic` - the topic the record was consumed from.
    
-   `kafka-key` from `CamelKafkaKey` - the record key, absent for records produced without one.
    
-   `kafka-partition` from `CamelKafkaPartition` - the partition the record came from.
    
-   `kafka-offset` from `CamelKafkaOffset` - the offset within that partition.
    
-   `kafka-timestamp` from `CamelKafkaTimestamp` - the record timestamp, in milliseconds since the epoch.
    

The `CamelKafka*` headers are left on the exchange as well, so consumers already reading them keep working.

### Configuration

The Kamelet requires Kafka connection parameters:

-   `topic`: The Kafka topic to consume from
    
-   `bootstrapServers`: Comma separated list of Kafka Broker URLs
    
-   `apicurioRegistryUrl`: The Apicurio Schema Registry URL
    
-   The `apicurioAuth*` options of the Keycloak login to the registry
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kafka-not-secured-apicurio-registry-json-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kafka-not-secured-apicurio-registry-json-source
    properties:
      topic: "my-topic"
      bootstrapServers: "kafka-broker1:9092,kafka-broker2:9092"
      apicurioRegistryUrl: "http://apicurio-registry:8080/apis/registry/v2"
      apicurioAuthServiceUrl: "https://keycloak.example.com"
      apicurioAuthRealm: "registry"
      apicurioAuthClientId: "registry-client"
      apicurioAuthClientSecret: "client-secret"
      apicurioAuthUsername: "registry-user"
      apicurioAuthPassword: "registry-password"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-not-secured-apicurio-registry-json-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-not-secured-apicurio-registry-json-source.kamelet.yaml)