# ![kafka batch apicurio registry source](_images/kamelets/kafka-batch-apicurio-registry-source.svg) Kafka Batch with Apicurio Registry secured with Keycloak Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Deprecated"**

Deprecated, to be removed in a later release: receives Avro records from topics in Apache Kafka in batches, with the schema kept in an Apicurio Registry secured with Keycloak.

Use it to read many Avro records at once, when the registry needs a Keycloak login and Kafka needs none. For one record at a time use `kafka-not-secured-apicurio-registry-source`; when the registry needs no login use `kafka-batch-apicurio-registry-not-secured-source`. This Kamelet is deprecated and will be removed in a later release, as the Kafka Kamelets are reduced to a few.

Output: the body is a List with one entry per record, up to `batchSize`. Each entry is a message of its own, with the value of the record as its body (an Avro `GenericRecord`, whose text form is JSON), and the key, offset and timestamp of the record in its `CamelKafkaKey`, `CamelKafkaOffset` and `CamelKafkaTimestamp` headers. The record headers are in the entries too, as bytes. The message itself has the `CamelKafkaTopic` and `CamelKafkaPartition` headers. The `kafka-topic`, `kafka-key` and other headers of `kafka-source` are not set.

Good to know: Kafka is not secured: it connects to the brokers with no login and no TLS. To save the position in Kafka only once a batch was handled, set `allowManualCommit` to true and `autoCommitEnable` to false, and end the flow with `kafka-batch-manual-commit-action`.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-batch-apicurio-registry-source` Kamelet:

     
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
| **allowManualCommit** | Allow Manual Commit | If true, each message carries what `kafka-batch-manual-commit-action` needs to save the position of its records in Kafka. Set `autoCommitEnable` to false too, or the position is also saved automatically. | boolean | false |  |
| **autoCommitEnable** | Auto Commit | If true, the position reached in each partition (the offset) is saved in Kafka automatically every 5 seconds, so that a restarted integration goes on from there. Set it to false together with `allowManualCommit` true to save the position yourself with `kafka-batch-manual-commit-action`. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | Where to start when the consumer group has no saved position yet: `latest` reads only the records sent from now on, `earliest` reads all the records still in the topic, and `none` fails. | string | latest | earliest |
| **avroDatumProvider** | Avro Datum Provider | How the Avro value is turned into the body. The default `io.apicurio.registry.serde.avro.DefaultAvroDatumProvider` gives an Avro `GenericRecord`; `io.apicurio.registry.serde.avro.ReflectAvroDatumProvider` maps the Avro value onto Java objects by reflection. | string | io.apicurio.registry.serde.avro.DefaultAvroDatumProvider |  |
| **batchSize** | Batch Size | The largest number of records in one message. A message holds fewer when fewer records are waiting. | integer | 500 |  |
| **batchingIntervalMs** | Batching Interval | When set, a batch that has not reached `batchSize` is sent on after about this many milliseconds. It is checked only between two reads, so it can take up to `pollTimeout` longer. | integer |  | 10000 |
| **consumerGroup** | Consumer Group | The name of the consumer group. Integrations with the same group share the records of the topics between them, and the group remembers the position reached, so that a restarted integration goes on where it stopped. When it is not set, a new random group is used on every start. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | Meant to turn the values of the record headers into text. In a batch it has no effect: the record headers of the entries of the list stay bytes. | boolean | true |  |
| **maxPollIntervalMs** | Max Poll Interval | The longest time, in milliseconds, that the integration may take to handle one batch. When it takes longer, Kafka considers it failed and gives its partitions to another member of the consumer group. When it is not set, the Kafka default of 300000 (5 minutes) applies. | integer |  | 600000 |
| **pollOnError** | Poll On Error Behavior | What to do when reading from Kafka fails: `ERROR_HANDLER` logs the error and goes on with the next records, `DISCARD` skips the records that failed, `RECONNECT` connects again and retries, `RETRY` reads the same records again, and `STOP` stops reading until the integration is restarted. Enum values: \* DISCARD \* ERROR\_HANDLER \* RECONNECT \* RETRY \* STOP | string | ERROR\_HANDLER |  |
| **pollTimeout** | Poll Timeout | How long one read from Kafka waits for new records, in milliseconds. | integer | 5000 |  |
| **topicIsPattern** | Topic Is Pattern | If true, `topic` is a regular expression, such as `orders-.*`, and the Kamelet reads from every topic whose name matches it. | boolean | false |  |
| **valueDeserializer** | Value Deserializer | The Java class that turns the value of the record into the body. The default reads Avro with the schema from the registry. Change it only to use another deserializer of the Apicurio Registry library. | string | io.apicurio.registry.serde.avro.AvroKafkaDeserializer |  |

## Dependencies

At runtime, the `kafka-batch-apicurio-registry-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kafka
    
-   camel:kamelet
    
-   mvn:io.quarkus:quarkus-apicurio-registry-avro:3.24.2
    

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
      uri: "kamelet:kafka-batch-apicurio-registry-source"
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

## Kafka Batch Apicurio Registry Source Kamelet Description

> **Note**
> This Kamelet is deprecated and will be removed in a later release, as the Kafka Kamelets are reduced to a few.

### Authentication methods

This Kamelet connects to Kafka using:

-   No login and no TLS to Kafka; a Keycloak login to the registry
    
-   Apicurio Schema Registry for schema management
    
-   Batch consumption mode for processing multiple messages
    

### Output format

The Kamelet consumes messages in batches from Kafka topics with schema validation through Apicurio Registry and produces the batch data in the configured format.

### Configuration

The Kamelet requires Kafka and Apicurio Registry connection parameters:

-   `topic`: The Kafka topic to consume from
    
-   `bootstrapServers`: Comma separated list of Kafka Broker URLs
    
-   `apicurioRegistryUrl`: The Apicurio Schema Registry URL
    
-   Security and batch processing parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kafka-batch-apicurio-registry-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kafka-batch-apicurio-registry-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-apicurio-registry-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-apicurio-registry-source.kamelet.yaml)