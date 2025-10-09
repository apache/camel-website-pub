# camel-azure-storage-blob-source-kafka-connector source configuration

Connector Description: Consume files from Azure Storage Blob.

When using camel-azure-storage-blob-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-blob-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestorageblobsource.CamelAzurestorageblobsourceSourceConnector
```

The camel-azure-storage-blob-source source connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-blob-source.accountName** | **Required** The Azure Storage Blob account name. |  | HIGH |
| **camel.kamelet.azure-storage-blob-source.containerName** | **Required** The Azure Storage Blob container name. |  | HIGH |
| **camel.kamelet.azure-storage-blob-source.accessKey** | The Azure Storage Blob access key. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-source.clientId** | The Azure Storage Blob client Id. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-source.clientSecret** | The Azure Storage Blob client secret. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-source.tenantId** | The Azure Storage Blob tenant id. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-source.delay** | The number of milliseconds before the next poll of the selected blob. | 500 | MEDIUM |
| **camel.kamelet.azure-storage-blob-source.deleteAfterRead** | Specifies to delete blobs after consuming them. | false | MEDIUM |
| **camel.kamelet.azure-storage-blob-source.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |

The camel-azure-storage-blob-source source connector has no converters out of the box.

The camel-azure-storage-blob-source source connector has no transforms out of the box.

The camel-azure-storage-blob-source source connector has no aggregation strategies out of the box.