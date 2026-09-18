# camel-azure-storage-datalake-sink-kafka-connector sink configuration

Connector Description: Send data to Azure Storage Blob Data Lake.

When using camel-azure-storage-datalake-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-datalake-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestoragedatalakesink.CamelAzurestoragedatalakesinkSinkConnector
```

The camel-azure-storage-datalake-sink sink connector supports 6 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-datalake-sink.accountName** | **Required** The Azure Storage Blob Data lake account name. |  | HIGH |
| **camel.kamelet.azure-storage-datalake-sink.clientId** | **Required** The Azure Storage Blob Data lake client Id. |  | HIGH |
| **camel.kamelet.azure-storage-datalake-sink.clientSecret** | **Required** The Azure Storage Blob Data lake client secret. |  | HIGH |
| **camel.kamelet.azure-storage-datalake-sink.tenantId** | **Required** The Azure Storage Blob Data lake tenant id. |  | HIGH |
| **camel.kamelet.azure-storage-datalake-sink.fileSystemName** | **Required** The Azure Storage Blob Data lake File system name. |  | HIGH |
| **camel.kamelet.azure-storage-datalake-sink.credentialType** | Determines the credential strategy to adopt. | "CLIENT\_SECRET" | MEDIUM |

The camel-azure-storage-datalake-sink sink connector has no converters out of the box.

The camel-azure-storage-datalake-sink sink connector has no transforms out of the box.

The camel-azure-storage-datalake-sink sink connector has no aggregation strategies out of the box.