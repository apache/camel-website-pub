# camel-azure-storage-blob-sink-kafka-connector sink configuration

Connector Description: Upload data to Azure Storage Blob.

When using camel-azure-storage-blob-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-blob-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestorageblobsink.CamelAzurestorageblobsinkSinkConnector
```

The camel-azure-storage-blob-sink sink connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-blob-sink.accountName** | **Required** The Azure Storage Blob account name. |  | HIGH |
| **camel.kamelet.azure-storage-blob-sink.containerName** | **Required** The Azure Storage Blob container name. |  | HIGH |
| **camel.kamelet.azure-storage-blob-sink.accessKey** | The Azure Storage Blob access key. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-sink.clientId** | The Azure Storage Blob client Id. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-sink.clientSecret** | The Azure Storage Blob client secret. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-sink.tenantId** | The Azure Storage Blob tenant id. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-sink.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |

The camel-azure-storage-blob-sink sink connector has no converters out of the box.

The camel-azure-storage-blob-sink sink connector has no transforms out of the box.

The camel-azure-storage-blob-sink sink connector has no aggregation strategies out of the box.