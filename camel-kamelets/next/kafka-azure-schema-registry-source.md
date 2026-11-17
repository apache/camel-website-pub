# ![kafka azure schema registry source](_images/kamelets/kafka-azure-schema-registry-source.svg) Azure Kafka through Eventhubs with Azure Schema Registry Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Receives each Avro record from event hubs in Azure Event Hubs, through its Kafka interface, with the schema kept in Azure Schema Registry.

Use it to read Avro records that other applications write to Azure Event Hubs with the schema of the registry. For many records in one message use `kafka-batch-azure-schema-registry-source`; for event hubs without a schema use `azure-eventhubs-source`.

Output: the body is the value of the record as an object of the `specificAvroValueType` class. The `kafka-topic`, `kafka-key`, `kafka-partition`, `kafka-offset` and `kafka-timestamp` (in milliseconds since 1970) headers say where the record came from. They are also set as `ce-kafkatopic`, `ce-kafkakey` and so on, and as the `CamelKafka*` headers that the Kafka actions read. The record headers become message headers, as text unless `deserializeHeaders` is false.

Good to know: it logs in to Event Hubs with the connection string in `password`, and to the schema registry with the Azure credentials of the environment the integration runs in, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables of a service principal, or a managed identity. The schemas must be in a schema group named `avro`. A new consumer group starts at the newest records, unless `autoOffsetReset` is `earliest`. Without `consumerGroup`, every start uses a new group, so the records sent while the integration was stopped are skipped.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-azure-schema-registry-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **azureRegistryUrl** | Azure Schema Registry URL | **Required** The URL of the Azure Schema Registry, which is the address of the Event Hubs namespace that holds it, as `[https://<namespace>.servicebus.windows.net](https://\<namespace\>.servicebus.windows.net)`. | string |  | https://my-namespace.servicebus.windows.net |
| **bootstrapServers** | Bootstrap Servers | **Required** The Kafka address of the Event Hubs namespace, as `<namespace>.servicebus.windows.net:9093`. | string |  | my-namespace.servicebus.windows.net:9093 |
| **password** | Connection String | **Required** The connection string of the Event Hubs namespace, which starts with `Endpoint=sb://`. Find it in the Azure portal, under Shared access policies of the namespace. | string |  |  |
| **topic** | Event Hub Names | **Required** The event hubs to read from, which Kafka calls topics, separated by commas. When `topicIsPattern` is true, a regular expression that their names must match instead. | string |  | orders |
| **allowManualCommit** | Allow Manual Commit | If true, each message carries what `kafka-manual-commit-action` needs to save the position of its record in Kafka. Set `autoCommitEnable` to false too, or the position is also saved automatically. | boolean | false |  |
| **autoCommitEnable** | Auto Commit | If true, the position reached in each partition (the offset) is saved in Kafka automatically every 5 seconds, so that a restarted integration goes on from there. Set it to false together with `allowManualCommit` true to save the position yourself with `kafka-manual-commit-action`. | boolean | true |  |
| **autoOffsetReset** | Auto Offset Reset | Where to start when the consumer group has no saved position yet: `latest` reads only the records sent from now on, `earliest` reads all the records still in the topic, and `none` fails. | string | latest | earliest |
| **consumerGroup** | Consumer Group | The name of the consumer group. Integrations with the same group share the records of the topics between them, and the group remembers the position reached, so that a restarted integration goes on where it stopped. When it is not set, a new random group is used on every start. | string |  | my-group-id |
| **deserializeHeaders** | Automatically Deserialize Headers | If true, the values of the record headers are turned into text. If false, they stay bytes. | boolean | true |  |
| **pollOnError** | Poll On Error Behavior | What to do when reading from Kafka fails: `ERROR_HANDLER` logs the error and goes on with the next records, `DISCARD` skips the records that failed, `RECONNECT` connects again and retries, `RETRY` reads the same records again, and `STOP` stops reading until the integration is restarted. Enum values: \* DISCARD \* ERROR\_HANDLER \* RECONNECT \* RETRY \* STOP | string | ERROR\_HANDLER |  |
| **saslMechanism** | SASL Mechanism | The login method. Keep the default `PLAIN`, which the login with the connection string in `password` needs. | string | PLAIN |  |
| **securityProtocol** | Security Protocol | How to connect to Event Hubs. Keep the default `SASL_SSL`, a login over TLS, which Event Hubs requires. The other values are `SASL_PLAINTEXT`, `PLAINTEXT` and `SSL`. | string | SASL\_SSL |  |
| **specificAvroValueType** | Specific Avro Value Type | The full name of the Java class generated from the Avro schema of the records, into which each record is read. The class must be part of the integration. The Kamelet does not start without this option, although it is not marked as required. | string |  | com.example.Order |
| **topicIsPattern** | Topic Is Pattern | If true, `topic` is a regular expression, such as `orders-.*`, and the Kamelet reads from every topic whose name matches it. | boolean | false |  |
| **valueDeserializer** | Value Deserializer | The Java class that turns the value of the record into the body. The default reads Avro with the schema from Azure Schema Registry. | string | com.microsoft.azure.schemaregistry.kafka.avro.KafkaAvroDeserializer |  |

## Dependencies

At runtime, the `kafka-azure-schema-registry-source` Kamelet relies upon the presence of the following dependencies:

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

The Kafka record metadata is surfaced as headers under names that are not Camel internals, so a downstream consumer does not have to read the `CamelKafka*` headers directly. Each has a `ce-` prefixed CloudEvents counterpart as well.

-   `kafka-topic` from `CamelKafkaTopic` - the topic the record was consumed from.
    
-   `kafka-key` from `CamelKafkaKey` - the record key, absent for records produced without one.
    
-   `kafka-partition` from `CamelKafkaPartition` - the partition the record came from.
    
-   `kafka-offset` from `CamelKafkaOffset` - the offset within that partition.
    
-   `kafka-timestamp` from `CamelKafkaTimestamp` - the record timestamp, in milliseconds since the epoch.
    

The `CamelKafka*` headers are left on the exchange as well, so consumers already reading them keep working.

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
      bootstrapServers: "my-registry.servicebus.windows.net:9093"
      azureRegistryUrl: "https://my-registry.servicebus.windows.net"
      password: "Endpoint=sb://my-registry.servicebus.windows.net/;SharedAccessKeyName=...;SharedAccessKey=..."
      specificAvroValueType: "com.example.Order"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-azure-schema-registry-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/kafka-azure-schema-registry-source.kamelet.yaml)