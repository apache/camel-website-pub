# camel-azure-storage-queue-sink-kafka-connector sink configuration

Connector Description: Send events to Azure Storage queues.

When using camel-azure-storage-queue-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-queue-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestoragequeuesink.CamelAzurestoragequeuesinkSinkConnector
```

The camel-azure-storage-queue-sink sink connector supports 4 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-queue-sink.accountName** | **Required** The Azure Storage Queue account name. |  | HIGH |
| **camel.kamelet.azure-storage-queue-sink.queueName** | **Required** The Azure Storage Queue container name. |  | HIGH |
| **camel.kamelet.azure-storage-queue-sink.accessKey** | **Required** The Azure Storage Queue access key. |  | HIGH |
| **camel.kamelet.azure-storage-queue-sink.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |

The camel-azure-storage-queue-sink sink connector has no converters out of the box.

The camel-azure-storage-queue-sink sink connector has no transforms out of the box.

The camel-azure-storage-queue-sink sink connector has no aggregation strategies out of the box.