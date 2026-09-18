# camel-azure-storage-files-sink-kafka-connector sink configuration

Connector Description: Upload data to Azure Storage Files Share.

When using camel-azure-storage-files-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-files-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestoragefilessink.CamelAzurestoragefilessinkSinkConnector
```

The camel-azure-storage-files-sink sink connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-files-sink.accountName** | **Required** The Azure Storage Blob account name. |  | HIGH |
| **camel.kamelet.azure-storage-files-sink.shareName** | **Required** The Azure Storage File Share share name. |  | HIGH |
| **camel.kamelet.azure-storage-files-sink.sharedKey** | The Azure Storage Blob access key. |  | MEDIUM |
| **camel.kamelet.azure-storage-files-sink.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |
| **camel.kamelet.azure-storage-files-sink.directoryName** | The directory from where the producer will upload the file. | "." | MEDIUM |

The camel-azure-storage-files-sink sink connector has no converters out of the box.

The camel-azure-storage-files-sink sink connector has no transforms out of the box.

The camel-azure-storage-files-sink sink connector has no aggregation strategies out of the box.