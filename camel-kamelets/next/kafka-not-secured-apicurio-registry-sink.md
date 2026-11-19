# ![kafka not secured apicurio registry sink](_images/kamelets/kafka-not-secured-apicurio-registry-sink.svg) Kafka Not Secured with Apicurio Registry secured with Keycloak Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Deprecated"**

Deprecated, to be removed in a later release: sends each message as an Avro record to a topic in Apache Kafka, with the schema kept in an Apicurio Registry secured with Keycloak.

Use it to publish records that other applications read with the schema of the registry, when the registry needs a Keycloak login and Kafka needs none. When the registry needs no login use `kafka-apicurio-registry-not-secured-sink`; for records without a schema use `kafka-sink`. This Kamelet is deprecated and will be removed in a later release, as the Kafka Kamelets are reduced to a few.

Input: the body must be an Avro object, such as an Avro `GenericRecord` or an object of a class generated from the schema; it is written as Avro binary. A body of text is written as an Avro string, and so fails unless the schema is a string. The optional `key` header (or `ce-key`) becomes the key of the record, and the optional `partition-key` header (or `ce-partitionkey`) is the number of the partition to write to. The other headers of the message, except the Camel ones, are sent as record headers.

Output: the message is unchanged.

Good to know: The schema must already be in the registry, as the artifact `<topic>-value` (such as `orders-value`) in the default group: the Kamelet does not register it, and a message whose schema is not found fails with `ArtifactNotFoundException`. Kafka is not secured: it connects to the brokers with no login and no TLS. Headers that start with `CamelKafka`, except `CamelKafkaKey` and `CamelKafkaOverrideTopic`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-not-secured-apicurio-registry-sink` Kamelet:

     
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
| **topic** | Topic Name | **Required** The name of the topic to write the records to. | string |  | orders |
| **avroDatumProvider** | Avro Datum Provider | How the body is turned into Avro. The default `io.apicurio.registry.serde.avro.DefaultAvroDatumProvider` takes an Avro `GenericRecord` or an object of a class generated from the schema; `io.apicurio.registry.serde.avro.ReflectAvroDatumProvider` maps any Java object to Avro by reflection. | string | io.apicurio.registry.serde.avro.DefaultAvroDatumProvider |  |
| **valueSerializer** | Value Serializer | The Java class that turns the body into the value of the record. The default writes Avro with the schema from the registry. Change it only to use another serializer of the Apicurio Registry library. | string | io.apicurio.registry.serde.avro.AvroKafkaSerializer |  |

## Dependencies

At runtime, the `kafka-not-secured-apicurio-registry-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:kafka-not-secured-apicurio-registry-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kafka Not Secured with Apicurio Registry secured with Keycloak Sink Kamelet Description

> **Note**
> This Kamelet is deprecated and will be removed in a later release, as the Kafka Kamelets are reduced to a few.

### Schema Registry Security

This Kamelet integrates with Apicurio Registry that is secured with Keycloak authentication. While the Kafka broker connection is not secured, the schema registry access requires proper authentication.

### Keycloak Authentication

The Kamelet supports OAuth2/OpenID Connect authentication through Keycloak for accessing the Apicurio Registry. Configuration includes:

-   Keycloak service URL and realm
    
-   Client ID and client secret
    
-   Username and password for authentication
    

### Avro Serialization

Uses Apicurio Registry’s Avro serializer with configurable datum providers for efficient schema-based data serialization.

### Security Considerations

While the Kafka broker connection is not secured, the schema registry authentication ensures that only authorized applications can access and modify schemas.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-not-secured-apicurio-registry-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-not-secured-apicurio-registry-sink.kamelet.yaml)