# ![kafka batch azure schema registry source](_images/kamelets/kafka-batch-azure-schema-registry-source.svg) Azure Kafka Batch through Eventhubs with Azure Schema Registry Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from Kafka topics in batch on Azure Eventhubs combined with Azure Schema Registry and commit them manually through KafkaManualCommit or auto commit.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-batch-azure-schema-registry-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **azureRegistryUrl** | Azure Schema Registry URL | **Required** The Apicurio Schema Registry URL. | string |  |  |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **password** | Password | **Required** Password to authenticate to kafka. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **allowManualCommit** | Allow Manual Commit | Whether to allow doing manual commits. | boolean | false |  |
| **autoCommitEnable** | Auto Commit Enable | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | string | latest |  |
| **batchSize** | Batch Dimension | The maximum number of records returned in a single call to poll(). | integer | 500 |  |
| **batchingIntervalMs** | Batching Interval | In consumer batching mode, then this option is specifying a time in millis, to trigger batch completion eager when the current batch size has not reached the maximum size defined by maxPollRecords. Notice the trigger is not exact at the given interval, as this can only happen between kafka polls (see pollTimeoutMs option). | integer |  |  |
| **consumerGroup** | Consumer Group | A string that uniquely identifies the group of consumers to which this source belongs. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | When enabled the Kamelet source will deserialize all message headers to String representation. | boolean | true |  |
| **maxPollIntervalMs** | Max Poll Interval | The maximum delay between invocations of poll() when using consumer group management. | integer |  |  |
| **pollOnError** | Poll On Error Behavior | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | string | ERROR\_HANDLER |  |
| **pollTimeout** | Poll Timeout Interval | The timeout used when polling the KafkaConsumer. | integer | 5000 |  |
| **saslMechanism** | SASL Mechanism | The Simple Authentication and Security Layer (SASL) Mechanism used. | string | PLAIN |  |
| **securityProtocol** | Security Protocol | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | string | SASL\_SSL |  |
| **specificAvroValueType** | Specific Avro Value Type | The Specific Type Avro will have to deal with. | string |  | com.example.Order |
| **topicIsPattern** | Topic Is Pattern | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | boolean | false |  |
| **valueDeserializer** | Value Deserializer | Deserializer class for value that implements the Deserializer interface. | string | com.microsoft.azure.schemaregistry.kafka.avro.KafkaAvroDeserializer |  |

## Dependencies

At runtime, the `kafka-batch-azure-schema-registry-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kafka
    
-   camel:core
    
-   camel:kamelet
    
-   camel:azure-schema-registry
    
-   mvn:com.microsoft.azure:azure-schemaregistry-kafka-avro:1.1.2
    
-   mvn:com.azure:azure-data-schemaregistry-apacheavro:1.1.26
    
-   mvn:com.azure:azure-identity:1.16.2
    

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
      uri: "kamelet:kafka-batch-azure-schema-registry-source"
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

## Kafka Batch Azure Schema Registry Source Kamelet Description

### Authentication methods

This Kamelet connects to Kafka using:

-   Azure Schema Registry for schema management
    
-   Kafka security configuration (SASL/SSL)
    
-   Batch consumption mode for processing multiple messages
    

### Output format

The Kamelet consumes messages in batches from Kafka topics with schema validation through Azure Schema Registry and produces the batch data in the configured format.

### Configuration

The Kamelet requires Kafka and Azure Schema Registry connection parameters:

-   `topic`: The Kafka topic to consume from
    
-   `bootstrapServers`: Comma separated list of Kafka Broker URLs
    
-   `azureRegistryUrl`: The Azure Schema Registry URL
    
-   Security and batch processing parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kafka-batch-azure-schema-registry-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kafka-batch-azure-schema-registry-source
    properties:
      topic: "my-topic"
      bootstrapServers: "kafka-broker1:9092,kafka-broker2:9092"
      azureRegistryUrl: "https://my-registry.servicebus.windows.net"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-azure-schema-registry-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-batch-azure-schema-registry-source.kamelet.yaml)