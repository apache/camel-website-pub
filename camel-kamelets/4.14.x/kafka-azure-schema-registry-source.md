# ![kafka azure schema registry source](_images/kamelets/kafka-azure-schema-registry-source.svg) Azure Kafka through Eventhubs with Azure Schema Registry Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from Kafka topics on Azure Eventhubs combined with Azure Schema Registry.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-azure-schema-registry-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **azureRegistryUrl** | Azure Schema Registry URL | **Required** The Apicurio Schema Registry URL. | string |  |  |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **password** | Password | **Required** Password to authenticate to kafka. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **allowManualCommit** | Allow Manual Commit | Whether to allow doing manual commits. | boolean | false |  |
| **autoCommitEnable** | Auto Commit Enable | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | string | latest |  |
| **consumerGroup** | Consumer Group | A string that uniquely identifies the group of consumers to which this source belongs. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | When enabled the Kamelet source will deserialize all message headers to String representation. | boolean | true |  |
| **pollOnError** | Poll On Error Behavior | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | string | ERROR\_HANDLER |  |
| **saslMechanism** | SASL Mechanism | The Simple Authentication and Security Layer (SASL) Mechanism used. | string | PLAIN |  |
| **securityProtocol** | Security Protocol | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | string | SASL\_SSL |  |
| **specificAvroValueType** | Specific Avro Value Type | The Specific Type Avro will have to deal with. | string |  | com.example.Order |
| **topicIsPattern** | Topic Is Pattern | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | boolean | false |  |
| **valueDeserializer** | Value Deserializer | Deserializer class for value that implements the Deserializer interface. | string | com.microsoft.azure.schemaregistry.kafka.avro.KafkaAvroDeserializer |  |

## Dependencies

At runtime, the `kafka-azure-schema-registry-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:kafka-azure-schema-registry-source"
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

## Kafka Azure Schema Registry Source Kamelet Description

### Authentication methods

This Kamelet connects to Kafka using:

-   Azure Schema Registry for schema management
    
-   Kafka security configuration (SASL/SSL)
    
-   Azure authentication credentials
    

### Output format

The Kamelet consumes messages from Kafka topics with schema validation through Azure Schema Registry and produces the message data in the configured format.

### Configuration

The Kamelet requires Kafka and Azure Schema Registry connection parameters:

-   `topic`: The Kafka topic to consume from
    
-   `bootstrapServers`: Comma separated list of Kafka Broker URLs
    
-   `azureRegistryUrl`: The Azure Schema Registry URL
    
-   Security and authentication parameters
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kafka-azure-schema-registry-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kafka-azure-schema-registry-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-azure-schema-registry-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-azure-schema-registry-source.kamelet.yaml)