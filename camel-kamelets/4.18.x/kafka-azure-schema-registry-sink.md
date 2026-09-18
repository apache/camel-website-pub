# ![kafka azure schema registry sink](_images/kamelets/kafka-azure-schema-registry-sink.svg) Azure Kafka through Eventhubs with Azure Schema Registry Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to Kafka topics on Azure Eventhubs combined with Azure Schema Registry.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-azure-schema-registry-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **azureRegistryUrl** | Azure Schema Registry URL | **Required** The Apicurio Schema Registry URL. | string |  |  |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **password** | Password | **Required** Password to authenticate to kafka. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **saslMechanism** | SASL Mechanism | The Simple Authentication and Security Layer (SASL) Mechanism used. | string | PLAIN |  |
| **securityProtocol** | Security Protocol | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | string | SASL\_SSL |  |
| **specificAvroValueType** | Specific Avro Value Type | The Specific Type Avro will have to deal with. | string |  | com.example.Order |
| **valueSerializer** | Value Deserializer | Deserializer class for value that implements the Deserializer interface. | string | com.microsoft.azure.schemaregistry.kafka.avro.KafkaAvroSerializer |  |

## Dependencies

At runtime, the `kafka-azure-schema-registry-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kafka
    
-   camel:kamelet
    
-   camel:azure-schema-registry
    
-   mvn:com.microsoft.azure:azure-schemaregistry-kafka-avro:1.1.4
    
-   mvn:com.azure:azure-data-schemaregistry-apacheavro:1.1.30
    
-   mvn:com.azure:azure-identity:1.18.1
    

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
            uri: "kamelet:kafka-azure-schema-registry-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Azure Kafka through Eventhubs with Azure Schema Registry Sink Kamelet Description

### Azure Integration

This Kamelet connects to Azure Event Hubs using Kafka protocol and integrates with Azure Schema Registry for schema management. It provides a bridge between Kafka-based applications and Azure’s messaging services.

### Authentication

The Kamelet uses SASL authentication with connection string-based credentials. The security protocol defaults to SASL\_SSL for secure communication with Azure Event Hubs.

### Schema Registry

Integration with Azure Schema Registry provides centralized schema management for Avro data serialization. The Kamelet requires configuration of the specific Avro value type to be processed.

### Azure Credentials

The Kamelet uses DefaultAzureCredential for authentication to Azure Schema Registry, supporting various Azure authentication methods including managed identity and service principal authentication.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-azure-schema-registry-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-azure-schema-registry-sink.kamelet.yaml)