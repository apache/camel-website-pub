# camel-azure-storage-blob-append-sink-kafka-connector sink configuration

Connector Description: Upload data in append mode to Azure Storage Blob.

When using camel-azure-storage-blob-append-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-blob-append-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestorageblobappendsink.CamelAzurestorageblobappendsinkSinkConnector
```

The camel-azure-storage-blob-append-sink sink connector supports 4 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-blob-append-sink.accountName** | **Required** The Azure Storage Blob account name. |  | HIGH |
| **camel.kamelet.azure-storage-blob-append-sink.containerName** | **Required** The Azure Storage Blob container name. |  | HIGH |
| **camel.kamelet.azure-storage-blob-append-sink.accessKey** | The Azure Storage Blob access key. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-append-sink.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |

The camel-azure-storage-blob-append-sink sink connector has no converters out of the box.

The camel-azure-storage-blob-append-sink sink connector has no transforms out of the box.

The camel-azure-storage-blob-append-sink sink connector has no aggregation strategies out of the box.