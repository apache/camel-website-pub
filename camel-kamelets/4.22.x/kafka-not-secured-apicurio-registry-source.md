# ![kafka not secured apicurio registry source](_images/kamelets/kafka-not-secured-apicurio-registry-source.svg) Kafka not secured with Apicurio Registry secured with Keycloak Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receive data from Kafka topics on an insecure broker combined with Apicurio Registry secured with Keycloak.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-not-secured-apicurio-registry-source` Kamelet:

     
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
| **consumerGroup** | Consumer Group | A string that uniquely identifies the group of consumers to which this source belongs. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | When enabled the Kamelet source will deserialize all message headers to String representation. | boolean | true |  |
| **pollOnError** | Poll On Error Behavior | What to do if kafka threw an exception while polling for new messages. There are 5 enums and the value can be one of `DISCARD`, `ERROR_HANDLER`, `RECONNECT`, `RETRY`, `STOP`. | string | ERROR\_HANDLER |  |
| **topicIsPattern** | Topic Is Pattern | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | boolean | false |  |
| **valueDeserializer** | Value Deserializer | Deserializer class for value that implements the Deserializer interface. | string | io.apicurio.registry.serde.avro.AvroKafkaDeserializer |  |

## Dependencies

At runtime, the `kafka-not-secured-apicurio-registry-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:kafka-not-secured-apicurio-registry-source"
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

## Kafka-not-secured-apicurio-registry-source Kamelet Description

### Authentication methods

This Kamelet connects to Kafka using appropriate security mechanisms based on the configuration type:

-   Security settings as indicated by the kamelet name (SSL, SCRAM, not-secured)
    
-   Schema registry integration where applicable
    
-   Bootstrap servers configuration
    

### Output format

The Kamelet consumes messages from Kafka topics and produces the message data in the configured format.

### Configuration

The Kamelet requires Kafka connection parameters:

-   `topic`: The Kafka topic to consume from
    
-   `bootstrapServers`: Comma separated list of Kafka Broker URLs
    
-   Security-specific parameters based on the authentication method
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: kafka-not-secured-apicurio-registry-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: kafka-not-secured-apicurio-registry-source
    properties:
      topic: "my-topic"
      bootstrapServers: "kafka-broker1:9092,kafka-broker2:9092"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-not-secured-apicurio-registry-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-not-secured-apicurio-registry-source.kamelet.yaml)