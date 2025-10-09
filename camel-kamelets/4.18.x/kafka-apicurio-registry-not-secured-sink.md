# ![kafka apicurio registry not secured sink](_images/kamelets/kafka-apicurio-registry-not-secured-sink.svg) Kafka Not Secured with Apicurio Registry Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to Kafka topics on an insecure broker with Apicurio Registry.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-apicurio-registry-not-secured-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apicurioRegistryUrl** | Apicurio Registry URL | **Required** The Apicurio Schema Registry URL. | string |  |  |
| **bootstrapServers** | Bootstrap Servers | **Required** Comma separated list of Kafka Broker URLs. | string |  |  |
| **topic** | Topic Names | **Required** Comma separated list of Kafka topic names. | string |  |  |
| **avroDatumProvider** | Avro Datum Provider | How to write data with Avro. | string | io.apicurio.registry.serde.avro.ReflectAvroDatumProvider |  |
| **valueSerializer** | Value Serializer | Serliazer class for value that implements the Serializer interface. | string | io.apicurio.registry.serde.avro.AvroKafkaSerializer |  |

## Dependencies

At runtime, the `kafka-apicurio-registry-not-secured-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:kamelet
    
-   camel:kafka
    
-   mvn:io.apicurio:apicurio-registry-serdes-avro-serde:2.4.14.Final
    

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
            uri: "kamelet:kafka-apicurio-registry-not-secured-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kafka Not Secured with Apicurio Registry Sink Kamelet Description

### Schema Registry Integration

This Kamelet integrates with Apicurio Registry for schema management and serialization of Avro data. The registry provides centralized schema storage and versioning capabilities.

### Avro Serialization

The Kamelet uses Avro serialization with configurable datum providers for efficient data serialization. The default serializer is configured for Avro data format with reflect-based datum provider.

### Message Headers

The Kamelet supports both standard and CloudEvents headers for message keys and partition routing:

-   Message key headers: `key` or `ce-key`
    
-   Partition key headers: `partition-key` or `ce-partitionkey`
    

### Security Note

This Kamelet connects to an insecure Kafka broker without authentication. Use appropriate secured variants for production environments.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-apicurio-registry-not-secured-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-apicurio-registry-not-secured-sink.kamelet.yaml)