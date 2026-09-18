# camel-azure-storage-files-source-kafka-connector source configuration

Connector Description: Consume files from Azure Storage File Shares.

When using camel-azure-storage-files-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-files-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestoragefilessource.CamelAzurestoragefilessourceSourceConnector
```

The camel-azure-storage-files-source source connector supports 8 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-files-source.accountName** | **Required** The Azure Storage File Share account name. |  | HIGH |
| **camel.kamelet.azure-storage-files-source.shareName** | **Required** The Azure Storage File Share share name. |  | HIGH |
| **camel.kamelet.azure-storage-files-source.sharedKey** | The Azure Storage Blob access key. |  | MEDIUM |
| **camel.kamelet.azure-storage-files-source.delay** | The number of milliseconds before the next poll of the selected blob. | 500 | MEDIUM |
| **camel.kamelet.azure-storage-files-source.deleteAfterRead** | Specifies to delete blobs after consuming them. | false | MEDIUM |
| **camel.kamelet.azure-storage-files-source.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |
| **camel.kamelet.azure-storage-files-source.directoryName** | The directory from where the consumer will start reading files. | "." | MEDIUM |
| **camel.kamelet.azure-storage-files-source.recursive** | If a directory, the consumer will look for files in all the sub-directories as well. | false | MEDIUM |

The camel-azure-storage-files-source source connector has no converters out of the box.

The camel-azure-storage-files-source source connector has no transforms out of the box.

The camel-azure-storage-files-source source connector has no aggregation strategies out of the box.