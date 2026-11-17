# ![kafka azure schema registry sink](_images/kamelets/kafka-azure-schema-registry-sink.svg) Azure Kafka through Eventhubs with Azure Schema Registry Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as an Avro record to an event hub in Azure Event Hubs, through its Kafka interface, with the schema kept in Azure Schema Registry.

Use it to publish Avro records to Azure Event Hubs for applications that read them with the schema of the registry. For event hubs without a schema use `azure-eventhubs-sink`; for Apicurio Registry use `kafka-apicurio-registry-not-secured-sink`.

Input: the body must be an Avro object, such as an object of the class named in `specificAvroValueType`; it is written as Avro binary. The optional `key` header (or `ce-key`) becomes the key of the record, and the optional `partition-key` header (or `ce-partitionkey`) is the number of the partition to write to. The other headers of the message, except the Camel ones, are sent as record headers.

Output: the message is unchanged.

Good to know: it logs in to Event Hubs with the connection string in `password`, and to the schema registry with the Azure credentials of the environment the integration runs in, such as the `AZURE_CLIENT_ID`, `AZURE_TENANT_ID` and `AZURE_CLIENT_SECRET` environment variables of a service principal, or a managed identity. The schemas must be in a schema group named `avro`.

## Configuration Options

The following table summarizes the configuration options available for the `kafka-azure-schema-registry-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **azureRegistryUrl** | Azure Schema Registry URL | **Required** The URL of the Azure Schema Registry, which is the address of the Event Hubs namespace that holds it, as `[https://<namespace>.servicebus.windows.net](https://\<namespace\>.servicebus.windows.net)`. | string |  | https://my-namespace.servicebus.windows.net |
| **bootstrapServers** | Bootstrap Servers | **Required** The Kafka address of the Event Hubs namespace, as `<namespace>.servicebus.windows.net:9093`. | string |  | my-namespace.servicebus.windows.net:9093 |
| **password** | Connection String | **Required** The connection string of the Event Hubs namespace, which starts with `Endpoint=sb://`. Find it in the Azure portal, under Shared access policies of the namespace. | string |  |  |
| **topic** | Event Hub Name | **Required** The name of the event hub to write the records to, which Kafka calls the topic. | string |  | orders |
| **saslMechanism** | SASL Mechanism | The login method. Keep the default `PLAIN`, which the login with the connection string in `password` needs. | string | PLAIN |  |
| **securityProtocol** | Security Protocol | How to connect to Event Hubs. Keep the default `SASL_SSL`, a login over TLS, which Event Hubs requires. The other values are `SASL_PLAINTEXT`, `PLAINTEXT` and `SSL`. | string | SASL\_SSL |  |
| **specificAvroValueType** | Specific Avro Value Type | The full name of the Java class generated from the Avro schema of the records. The class must be part of the integration. The Kamelet does not start without this option, although it is not marked as required. | string |  | com.example.Order |
| **valueSerializer** | Value Serializer | The Java class that turns the body into the value of the record. The default writes Avro with the schema from Azure Schema Registry. | string | com.microsoft.azure.schemaregistry.kafka.avro.KafkaAvroSerializer |  |

## Dependencies

At runtime, the `kafka-azure-schema-registry-sink` Kamelet relies upon the presence of the following dependencies:

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