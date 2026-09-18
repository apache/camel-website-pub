# camel-azure-storage-datalake-source-kafka-connector source configuration

Connector Description: Consume files from Azure Storage Blob Data Lake.

When using camel-azure-storage-datalake-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-datalake-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestoragedatalakesource.CamelAzurestoragedatalakesourceSourceConnector
```

The camel-azure-storage-datalake-source source connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-datalake-source.accountName** | **Required** The Azure Storage Blob Data lake account name. |  | HIGH |
| **camel.kamelet.azure-storage-datalake-source.clientId** | **Required** The Azure Storage Blob Data lake client Id. |  | HIGH |
| **camel.kamelet.azure-storage-datalake-source.clientSecret** | **Required** The Azure Storage Blob Data lake client secret. |  | HIGH |
| **camel.kamelet.azure-storage-datalake-source.tenantId** | **Required** The Azure Storage Blob Data lake tenant id. |  | HIGH |
| **camel.kamelet.azure-storage-datalake-source.fileSystemName** | **Required** The Azure Storage Blob Data lake File system name. |  | HIGH |
| **camel.kamelet.azure-storage-datalake-source.delay** | The number of milliseconds before the next poll of the selected blob. | 500 | MEDIUM |
| **camel.kamelet.azure-storage-datalake-source.credentialType** | Determines the credential strategy to adopt. | "CLIENT\_SECRET" | MEDIUM |

The camel-azure-storage-datalake-source source connector has no converters out of the box.

The camel-azure-storage-datalake-source source connector has no transforms out of the box.

The camel-azure-storage-datalake-source source connector has no aggregation strategies out of the box.