# ![kafka apicurio registry not secured source](_images/kamelets/kafka-apicurio-registry-not-secured-source.svg) Kafka Not Secured with Apicurio Registry Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from Kafka topics on an insecure broker combined with Apicurio Registry.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-apicurio-registry-not-secured-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apicurioRegistryUrl** | Apicurio Registry URL | **Required** The Apicurio Schema Registry URL. | string |  |  |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **allowManualCommit** | Allow Manual Commit | Whether to allow doing manual commits. | boolean | false |  |
| **autoCommitEnable** | Auto Commit Enable | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | What to do when there is no initial offset. There are 3 enums and the value can be one of latest, earliest, none. | string | latest |  |
| **consumerGroup** | Consumer Group | A string that uniquely identifies the group of consumers to which this source belongs. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | When enabled the Kamelet source will deserialize all message headers to String representation. | boolean | true |  |
| **pollOnError** | Poll On Error Behavior | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | string | ERROR\_HANDLER |  |
| **topicIsPattern** | Topic Is Pattern | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | boolean | false |  |
| **valueDeserializer** | Value Deserializer | Deserializer class for value that implements the Deserializer interface. | string | io.apicurio.registry.serde.jsonschema.JsonSchemaKafkaDeserializer |  |

## Dependencies

At runtime, the `kafka-apicurio-registry-not-secured-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kafka
    
-   camel:core
    
-   camel:kamelet
    
-   mvn:io.quarkus:quarkus-apicurio-registry-json-schema:3.15.1
    

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
      uri: "kamelet:kafka-apicurio-registry-not-secured-source"
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

## Kafka Apicurio Registry Not Secured Source Kamelet Description

### Authentication methods

This Kamelet connects to Kafka using:

-   No security (not secured setup)
    
-   Apicurio Schema Registry for schema management
    
-   Bootstrap servers configuration
    

### Output format

The Kamelet consumes messages from Kafka topics with schema validation through Apicurio Registry and produces the message data in the configured format.

### Configuration

The Kamelet requires Kafka and Apicurio Registry connection parameters:

-   `topic`: The Kafka topic to consume from
    
-   `bootstrapServers`: Comma separated list of Kafka Broker URLs
    
-   `apicurioRegistryUrl`: The Apicurio Schema Registry URL
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kafka-apicurio-registry-not-secured-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kafka-apicurio-registry-not-secured-source
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-apicurio-registry-not-secured-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-apicurio-registry-not-secured-source.kamelet.yaml)