# camel-azure-storage-queue-source-kafka-connector source configuration

Connector Description: Receive events from Azure Storage queues.

When using camel-azure-storage-queue-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-azure-storage-queue-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.azurestoragequeuesource.CamelAzurestoragequeuesourceSourceConnector
```

The camel-azure-storage-queue-source source connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.azure-storage-queue-source.accountName** | **Required** The Azure Storage Queue account name. |  | HIGH |
| **camel.kamelet.azure-storage-queue-source.queueName** | **Required** The Azure Storage Queue container name. |  | HIGH |
| **camel.kamelet.azure-storage-queue-source.accessKey** | **Required** The Azure Storage Queue access key. |  | HIGH |
| **camel.kamelet.azure-storage-queue-source.maxMessages** | The maximum number of messages to get. You can specify a value between 1 and 32. The default is 1 (one message). If there are fewer than the maximum number of messages in the queue, then all the messages are returned. | 1 | MEDIUM |
| **camel.kamelet.azure-storage-queue-source.credentialType** | Determines the credential strategy to adopt. | "SHARED\_ACCOUNT\_KEY" | MEDIUM |

The camel-azure-storage-queue-source source connector has no converters out of the box.

The camel-azure-storage-queue-source source connector has no transforms out of the box.

The camel-azure-storage-queue-source source connector has no aggregation strategies out of the box.