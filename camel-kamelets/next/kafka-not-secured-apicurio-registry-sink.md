# ![kafka not secured apicurio registry sink](_images/kamelets/kafka-not-secured-apicurio-registry-sink.svg) Kafka Not Secured with Apicurio Registry secured with Keycloak Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to Kafka topics on an insecure broker with Apicurio Registry secured with Keycloak.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-not-secured-apicurio-registry-sink` Kamelet:

     
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
| **avroDatumProvider** | Avro Datum Provider | How to write data with Avro. Defaults to Apicurio’s own DefaultAvroDatumProvider, which handles GenericRecord and generated SpecificRecord classes. Set io.apicurio.registry.serde.avro.ReflectAvroDatumProvider to map arbitrary POJOs onto Avro by reflection instead. | string | io.apicurio.registry.serde.avro.DefaultAvroDatumProvider |  |
| **valueSerializer** | Value Serializer | Serliazer class for value that implements the Serializer interface. | string | io.apicurio.registry.serde.avro.AvroKafkaSerializer |  |

## Dependencies

At runtime, the `kafka-not-secured-apicurio-registry-sink` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:kafka-not-secured-apicurio-registry-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kafka Not Secured with Apicurio Registry secured with Keycloak Sink Kamelet Description

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