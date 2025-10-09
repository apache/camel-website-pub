# camel-azure-storage-blob-changefeed-source-kafka-connector source configuration

Connector Description: Consume events from an Azure Storage Blob change feed.

When using camel-azure-storage-blob-changefeed-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-blob-changefeed-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestorageblobchangefeedsource.CamelAzurestorageblobchangefeedsourceSourceConnector
```

The camel-azure-storage-blob-changefeed-source source connector supports 7 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-blob-changefeed-source.period** | **Required** The interval (in milliseconds) between fetches to the Azure Storage change feed. | 10000 | HIGH |
| **camel.kamelet.azure-storage-blob-changefeed-source.accountName** | **Required** The Azure Storage Blob account name. |  | HIGH |
| **camel.kamelet.azure-storage-blob-changefeed-source.accessKey** | The Azure Storage Blob access Key. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-changefeed-source.clientId** | The Azure Storage Blob client Id. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-changefeed-source.clientSecret** | The Azure Storage Blob client secret. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-changefeed-source.tenantId** | The Azure Storage Blob tenant id. |  | MEDIUM |
| **camel.kamelet.azure-storage-blob-changefeed-source.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |

The camel-azure-storage-blob-changefeed-source source connector has no converters out of the box.

The camel-azure-storage-blob-changefeed-source source connector has no transforms out of the box.

The camel-azure-storage-blob-changefeed-source source connector has no aggregation strategies out of the box.