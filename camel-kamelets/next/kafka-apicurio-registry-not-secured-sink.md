# ![kafka apicurio registry not secured sink](_images/kamelets/kafka-apicurio-registry-not-secured-sink.svg) Kafka Not Secured with Apicurio Registry Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as an Avro record to a topic in Apache Kafka, with the schema kept in an Apicurio Registry, and no login or TLS to either.

Use it to publish records that other applications read with the schema of the registry, on a Kafka and a registry that need no login, such as in development. When the registry is secured with Keycloak use `kafka-not-secured-apicurio-registry-sink`; for Azure Schema Registry use `kafka-azure-schema-registry-sink`; for records without a schema use `kafka-sink`.

Input: the body must be an Avro object, such as an Avro `GenericRecord` or an object of a class generated from the schema; it is written as Avro binary. A body of text is written as an Avro string, and so fails unless the schema is a string. The optional `key` header (or `ce-key`) becomes the key of the record, and the optional `partition-key` header (or `ce-partitionkey`) is the number of the partition to write to. The other headers of the message, except the Camel ones, are sent as record headers.

Output: the message is unchanged.

Good to know: The schema must already be in the registry, as the artifact `<topic>-value` (such as `orders-value`) in the default group: the Kamelet does not register it, and a message whose schema is not found fails with `ArtifactNotFoundException`. Neither Kafka nor the registry is secured: there is no login and no TLS.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-apicurio-registry-not-secured-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apicurioRegistryUrl** | Apicurio Registry URL | **Required** The URL of the API of the Apicurio Registry that holds the schemas, such as `[http://registry:8080/apis/registry/v2](http://registry:8080/apis/registry/v2)`. | string |  | http://registry.example.com:8080/apis/registry/v2 |
| **bootstrapServers** | Bootstrap Servers | **Required** The address of one or more Kafka brokers to connect to first, as `host:port`, separated by commas. The other brokers of the cluster are found from them. | string |  | broker1:9092,broker2:9092 |
| **topic** | Topic Name | **Required** The name of the topic to write the records to. | string |  | orders |
| **avroDatumProvider** | Avro Datum Provider | How the body is turned into Avro. The default `io.apicurio.registry.serde.avro.DefaultAvroDatumProvider` takes an Avro `GenericRecord` or an object of a class generated from the schema; `io.apicurio.registry.serde.avro.ReflectAvroDatumProvider` maps any Java object to Avro by reflection. | string | io.apicurio.registry.serde.avro.DefaultAvroDatumProvider |  |
| **valueSerializer** | Value Serializer | The Java class that turns the body into the value of the record. The default writes Avro with the schema from the registry. Change it only to use another serializer of the Apicurio Registry library. | string | io.apicurio.registry.serde.avro.AvroKafkaSerializer |  |

## Dependencies

At runtime, the `kafka-apicurio-registry-not-secured-sink` Kamelet relies upon the presence of the following dependencies:

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

The Kamelet uses Avro serialization with configurable datum providers. The default datum provider, `DefaultAvroDatumProvider`, takes an Avro `GenericRecord` or an object of a class generated from the schema; set `avroDatumProvider` to `io.apicurio.registry.serde.avro.ReflectAvroDatumProvider` to map any Java object by reflection.

The schema must already be in the registry, as the artifact `<topic>-value` in the default group: the Kamelet does not register it.

### Message Headers

The Kamelet supports both standard and CloudEvents headers for message keys and partition routing:

-   Message key headers: `key` or `ce-key`
    
-   Partition key headers: `partition-key` or `ce-partitionkey`
    

### Security Note

This Kamelet connects to an insecure Kafka broker without authentication. Use appropriate secured variants for production environments.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-apicurio-registry-not-secured-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-apicurio-registry-not-secured-sink.kamelet.yaml)