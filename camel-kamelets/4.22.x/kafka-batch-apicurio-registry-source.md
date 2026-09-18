# ![kafka batch apicurio registry source](_images/kamelets/kafka-batch-apicurio-registry-source.svg) Kafka Batch with Apicurio Registry secured with Keycloak Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from Kafka topics in batch on an insecure broker combined with Apicurio Registry secured with Keycloak and commit them manually through KafkaManualCommit or auto commit.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-batch-apicurio-registry-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apicurioAuthClientId** | Apicurio Registry Auth Client ID | **Required** The Client ID in Keycloak instance securing the Apicurio Registry. | string |  |  |
| **apicurioAuthClientSecret** | Apicurio Registry Auth Client Secret | **Required** The Client Secret in Keycloak instance securing the Apicurio Registry. | string |  |  |
| **apicurioAuthPassword** | Apicurio Registry Auth Password | **Required** The Password in Keycloak instance securing the Apicurio Registry. | string |  |  |
| **apicurioAuthRealm** | Apicurio Registry Auth Realm | **Required** The Realm in Keycloak instance securing the Apicurio Registry. | string |  |  |
| **apicurioAuthServiceUrl** | Apicurio Registry Auth Service URL | **Required** The URL for Keycloak instance securing the Apicurio Registry. | string |  | http://my-keycloak.com:8080/ |
| **apicurioAuthUsername** | Apicurio Registry Auth Username | **Required** The Username in Keycloak instance securing the Apicurio Registry. | string |  |  |
| **apicurioRegistryUrl** | Apicurio Registry URL | **Required** The Apicurio Schema Registry URL. | string |  |  |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **allowManualCommit** | Allow Manual Commit | Whether to allow doing manual commits. | boolean | false |  |
| **autoCommitEnable** | Auto Commit Enable | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | string | latest |  |
| **avroDatumProvider** | Avro Datum Provider | How to read data with Avro. | string | io.apicurio.registry.serde.avro.ReflectAvroDatumProvider |  |
| **batchSize** | Batch Dimension | The maximum number of records returned in a single call to poll(). | integer | 500 |  |
| **batchingIntervalMs** | Batching Interval | In consumer batching mode, then this option is specifying a time in millis, to trigger batch completion eager when the current batch size has not reached the maximum size defined by maxPollRecords. Notice the trigger is not exact at the given interval, as this can only happen between kafka polls (see pollTimeoutMs option). | integer |  |  |
| **consumerGroup** | Consumer Group | A string that uniquely identifies the group of consumers to which this source belongs. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | When enabled the Kamelet source will deserialize all message headers to String representation. | boolean | true |  |
| **maxPollIntervalMs** | Max Poll Interval | The maximum delay between invocations of poll() when using consumer group management. | integer |  |  |
| **pollOnError** | Poll On Error Behavior | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | string | ERROR\_HANDLER |  |
| **pollTimeout** | Poll Timeout Interval | The timeout used when polling the KafkaConsumer. | integer | 5000 |  |
| **topicIsPattern** | Topic Is Pattern | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | boolean | false |  |
| **valueDeserializer** | Value Deserializer | Deserializer class for value that implements the Deserializer interface. | string | io.apicurio.registry.serde.avro.AvroKafkaDeserializer |  |

## Dependencies

At runtime, the `kafka-batch-apicurio-registry-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kafka
    
-   camel:core
    
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

### Authentication methods

This Kamelet connects to Kafka using:

-   Security mechanisms (SASL/SSL)
    
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
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-apicurio-registry-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-apicurio-registry-source.kamelet.yaml)