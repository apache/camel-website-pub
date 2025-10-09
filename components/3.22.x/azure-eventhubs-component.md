# Azure Event Hubs

**Since Camel 3.5**

**Both producer and consumer are supported**

The Azure Event Hubs used to integrate [Azure Event Hubs](https://azure.microsoft.com/en-us/services/event-hubs/) using [AMQP protocol](https://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol). Azure EventHubs is a highly scalable publish-subscribe service that can ingest millions of events per second and stream them to multiple consumers.

> **Note**
> Besides AMQP protocol support, Event Hubs as well supports Kafka and HTTPS protocols. Therefore, you can use as well [Camel Kafka](../4.18.x/kafka-component.md) component to produce and consume to Azure Event Hubs. You can lean more [here](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-quickstart-kafka-enabled-event-hubs).

Prerequisites

You must have a valid Windows Azure Event Hubs account. More information is available at [Azure Documentation Portal](https://docs.microsoft.com/azure/).

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-azure-eventhubs</artifactId>
    <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

```text
azure-eventhubs://[namespace/eventHubName][?options]
```

In case you supply the `connectionString`, `namespace` and `eventHubName` are not required as these options already included in the `connectionString`

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Azure Event Hubs component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amqpRetryOptions** (common) | Sets the retry policy for EventHubAsyncClient. If not specified, the default retry options are used. |  | AmqpRetryOptions |
| **amqpTransportType** (common) | 
Sets the transport type by which all the communication with Azure Event Hubs occurs. Default value is AmqpTransportType#AMQP.

Enum values:

-   Amqp
    
-   AmqpWebSockets
    





 | AMQP | AmqpTransportType |
| **configuration** (common) | The component configurations. |  | EventHubsConfiguration |
| **blobAccessKey** (consumer) | In case you chose the default BlobCheckpointStore, this sets access key for the associated azure account name to be used for authentication with azure blob services. |  | String |
| **blobAccountName** (consumer) | In case you chose the default BlobCheckpointStore, this sets Azure account name to be used for authentication with azure blob services. |  | String |
| **blobContainerName** (consumer) | In case you chose the default BlobCheckpointStore, this sets the blob container that shall be used by the BlobCheckpointStore to store the checkpoint offsets. |  | String |
| **blobStorageSharedKeyCredential** (consumer) | In case you chose the default BlobCheckpointStore, StorageSharedKeyCredential can be injected to create the azure client, this holds the important authentication information. |  | StorageSharedKeyCredential |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **checkpointBatchSize** (consumer) | Sets the batch size between each checkpoint updates. Works jointly with checkpointBatchTimeout. | 500 | int |
| **checkpointBatchTimeout** (consumer) | Sets the batch timeout between each checkpoint updates. Works jointly with checkpointBatchSize. | 5000 | int |
| **checkpointStore** (consumer) | Sets the CheckpointStore the EventProcessorClient will use for storing partition ownership and checkpoint information. Users can, optionally, provide their own implementation of CheckpointStore which will store ownership and checkpoint information. By default it set to use com.azure.messaging.eventhubs.checkpointstore.blob.BlobCheckpointStore which stores all checkpoint offsets into Azure Blob Storage. | BlobCheckpointStore | CheckpointStore |
| **consumerGroupName** (consumer) | Sets the name of the consumer group this consumer is associated with. Events are read in the context of this group. The name of the consumer group that is created by default is \\{code $Default}. | $Default | String |
| **eventPosition** (consumer) | Sets the map containing the event position to use for each partition if a checkpoint for the partition does not exist in CheckpointStore. This map is keyed off of the partition id. If there is no checkpoint in CheckpointStore and there is no entry in this map, the processing of the partition will start from \\{link EventPosition#latest() latest} position. |  | Map |
| **prefetchCount** (consumer) | Sets the count used by the receiver to control the number of events the Event Hub consumer will actively receive and queue locally without regard to whether a receive operation is currently active. | 500 | int |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **partitionId** (producer) | Sets the identifier of the Event Hub partition that the events will be sent to. If the identifier is not specified, the Event Hubs service will be responsible for routing events that are sent to an available partition. |  | String |
| **partitionKey** (producer) | Sets a hashing key to be provided for the batch of events, which instructs the Event Hubs service to map this key to a specific partition. The selection of a partition is stable for a given partition hashing key. Should any other batches of events be sent using the same exact partition hashing key, the Event Hubs service will route them all to the same partition. This should be specified only when there is a need to group events by partition, but there is flexibility into which partition they are routed. If ensuring that a batch of events is sent only to a specific partition, it is recommended that the \\{link #setPartitionId(String) identifier of the position be specified directly} when sending the batch. |  | String |
| **producerAsyncClient** (producer) | **Autowired** Sets the EventHubProducerAsyncClient.An asynchronous producer responsible for transmitting EventData to a specific Event Hub, grouped together in batches. Depending on the options specified when creating an {linkEventDataBatch}, the events may be automatically routed to an available partition or specific to a partition. Use by this component to produce the data in camel producer. |  | EventHubProducerAsyncClient |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **connectionString** (security) | Instead of supplying namespace, sharedAccessKey, sharedAccessName …​ etc, you can just supply the connection string for your eventHub. The connection string for EventHubs already include all the necessary information to connection to your EventHub. To learn on how to generate the connection string, take a look at this documentation: [https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string). |  | String |
| **sharedAccessKey** (security) | The generated value for the SharedAccessName. |  | String |
| **sharedAccessName** (security) | The name you chose for your EventHubs SAS keys. |  | String |
| **tokenCredential** (security) | Still another way of authentication (beside supplying namespace, sharedAccessKey, sharedAccessName or connection string) is through Azure-AD authentication using an implementation instance of TokenCredential. |  | TokenCredential |

## Endpoint Options

The Azure Event Hubs endpoint is configured using URI syntax:

azure-eventhubs:namespace/eventHubName

with the following path and query parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **namespace** (common) | EventHubs namespace created in Azure Portal. |  | String |
| **eventHubName** (common) | EventHubs name under a specific namespace. |  | String |

### Query Parameters (23 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **amqpRetryOptions** (common) | Sets the retry policy for EventHubAsyncClient. If not specified, the default retry options are used. |  | AmqpRetryOptions |
| **amqpTransportType** (common) | 
Sets the transport type by which all the communication with Azure Event Hubs occurs. Default value is AmqpTransportType#AMQP.

Enum values:

-   Amqp
    
-   AmqpWebSockets
    





 | AMQP | AmqpTransportType |
| **blobAccessKey** (consumer) | In case you chose the default BlobCheckpointStore, this sets access key for the associated azure account name to be used for authentication with azure blob services. |  | String |
| **blobAccountName** (consumer) | In case you chose the default BlobCheckpointStore, this sets Azure account name to be used for authentication with azure blob services. |  | String |
| **blobContainerName** (consumer) | In case you chose the default BlobCheckpointStore, this sets the blob container that shall be used by the BlobCheckpointStore to store the checkpoint offsets. |  | String |
| **blobStorageSharedKeyCredential** (consumer) | In case you chose the default BlobCheckpointStore, StorageSharedKeyCredential can be injected to create the azure client, this holds the important authentication information. |  | StorageSharedKeyCredential |
| **checkpointBatchSize** (consumer) | Sets the batch size between each checkpoint updates. Works jointly with checkpointBatchTimeout. | 500 | int |
| **checkpointBatchTimeout** (consumer) | Sets the batch timeout between each checkpoint updates. Works jointly with checkpointBatchSize. | 5000 | int |
| **checkpointStore** (consumer) | Sets the CheckpointStore the EventProcessorClient will use for storing partition ownership and checkpoint information. Users can, optionally, provide their own implementation of CheckpointStore which will store ownership and checkpoint information. By default it set to use com.azure.messaging.eventhubs.checkpointstore.blob.BlobCheckpointStore which stores all checkpoint offsets into Azure Blob Storage. | BlobCheckpointStore | CheckpointStore |
| **consumerGroupName** (consumer) | Sets the name of the consumer group this consumer is associated with. Events are read in the context of this group. The name of the consumer group that is created by default is \\{code $Default}. | $Default | String |
| **eventPosition** (consumer) | Sets the map containing the event position to use for each partition if a checkpoint for the partition does not exist in CheckpointStore. This map is keyed off of the partition id. If there is no checkpoint in CheckpointStore and there is no entry in this map, the processing of the partition will start from \\{link EventPosition#latest() latest} position. |  | Map |
| **prefetchCount** (consumer) | Sets the count used by the receiver to control the number of events the Event Hub consumer will actively receive and queue locally without regard to whether a receive operation is currently active. | 500 | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **partitionId** (producer) | Sets the identifier of the Event Hub partition that the events will be sent to. If the identifier is not specified, the Event Hubs service will be responsible for routing events that are sent to an available partition. |  | String |
| **partitionKey** (producer) | Sets a hashing key to be provided for the batch of events, which instructs the Event Hubs service to map this key to a specific partition. The selection of a partition is stable for a given partition hashing key. Should any other batches of events be sent using the same exact partition hashing key, the Event Hubs service will route them all to the same partition. This should be specified only when there is a need to group events by partition, but there is flexibility into which partition they are routed. If ensuring that a batch of events is sent only to a specific partition, it is recommended that the \\{link #setPartitionId(String) identifier of the position be specified directly} when sending the batch. |  | String |
| **producerAsyncClient** (producer) | **Autowired** Sets the EventHubProducerAsyncClient.An asynchronous producer responsible for transmitting EventData to a specific Event Hub, grouped together in batches. Depending on the options specified when creating an {linkEventDataBatch}, the events may be automatically routed to an available partition or specific to a partition. Use by this component to produce the data in camel producer. |  | EventHubProducerAsyncClient |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **connectionString** (security) | Instead of supplying namespace, sharedAccessKey, sharedAccessName …​ etc, you can just supply the connection string for your eventHub. The connection string for EventHubs already include all the necessary information to connection to your EventHub. To learn on how to generate the connection string, take a look at this documentation: [https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string). |  | String |
| **sharedAccessKey** (security) | The generated value for the SharedAccessName. |  | String |
| **sharedAccessName** (security) | The name you chose for your EventHubs SAS keys. |  | String |
| **tokenCredential** (security) | Still another way of authentication (beside supplying namespace, sharedAccessKey, sharedAccessName or connection string) is through Azure-AD authentication using an implementation instance of TokenCredential. |  | TokenCredential |

## Authentication Information

To use this component, you have 3 options in order to provide the required Azure authentication information:

-   Provide `sharedAccessName` and `sharedAccessKey` for your Azure Event Hubs account. The sharedAccessKey can be generated through your Event Hubs Azure portal.
    
-   Provide `connectionString` string, if you provide the connection string, you don’t supply `namespace`, `eventHubName`, `sharedAccessKey` and `sharedAccessName` as these data already included in the `connectionString`, therefore is the simplest option to get started. Learn more [here](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string) on how to generate the connection string.
    
-   Provide a [EventHubProducerAsyncClient](https://docs.microsoft.com/en-us/java/api/com.azure.messaging.eventhubs.eventhubproducerasyncclient?view=azure-java-stable) instance which can be provided into `producerAsyncClient`. However, this is **only possible for camel producer**, for the camel consumer, is not possible to inject the client due to some design constraint by the `EventProcessorClient`.
    
-   Provide an implementation of `com.azure.core.credential.TokenCredential` into the Camel’s Registry, e.g. using the `com.azure.identity.DefaultAzureCredentialBuilder().build();` API. See the documentation [here about Azure-AD authentication](https://docs.microsoft.com/en-us/azure/active-directory/authentication/overview-authentication).
    

## Checkpoint Store Information

A checkpoint store stores and retrieves partition ownership information and checkpoint details for each partition in a given consumer group of an event hub instance. Users are not meant to implement an CheckpointStore. Users are expected to choose existing implementations of this interface, instantiate it, and pass it to the component through `checkpointStore` option. Users are not expected to use any of the methods on a checkpoint store, these are used internally by the client.

Having said that, if the user does not pass any `CheckpointStore` implementation, the component will fallback to use [`BlobCheckpointStore`](https://docs.microsoft.com/en-us/javascript/api/@azure/eventhubs-checkpointstore-blob/blobcheckpointstore?view=azure-node-latest) to store the checkpoint info in Azure Blob Storage account. If you chose to use the default `BlobCheckpointStore`, you will need to supply the following options:

-   `blobAccountName`: It sets Azure account name to be used for authentication with azure blob services.
    
-   `blobAccessKey` : It sets access key for the associated azure account name to be used for authentication with azure blob services.
    
-   `blobContainerName` : It sets the blob container that shall be used by the BlobCheckpointStore to store the checkpoint offsets.
    

## Async Consumer and Producer

This component implements the async Consumer and producer.

This allows camel route to consume and produce events asynchronously without blocking any threads.

## Usage

For example in order consume event from EventHub, use the following snippet:

```java
from("azure-eventhubs:/camel/camelHub?sharedAccessName=SASaccountName&sharedAccessKey=SASaccessKey&blobAccountName=accountName&blobAccessKey=accessKey&blobContainerName=containerName")
  .to("file://queuedirectory");
```

## Message Headers

The Azure Event Hubs component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelAzureEventHubsPartitionKey** (common) Constant: [`PARTITION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventhubs/latest/org/apache/camel/component/azure/eventhubs/EventHubsConstants.html#PARTITION_KEY) | (producer) Overrides the hashing key to be provided for the batch of events, which instructs the Event Hubs service to map this key to a specific partition. (consumer) It sets the partition hashing key if it was set when originally publishing the event. If it exists, this value was used to compute a hash to select a partition to send the message to. This is only present on a received EventData. |  | String |
| **CamelAzureEventHubsPartitionId** (common) Constant: [`PARTITION_ID`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventhubs/latest/org/apache/camel/component/azure/eventhubs/EventHubsConstants.html#PARTITION_ID) | (producer) Overrides the identifier of the Event Hub partition that the events will be sent to. (consumer) It sets the partition id of the Event Hub. |  | String |
| **CamelAzureEventHubsOffset** (consumer) Constant: [`OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventhubs/latest/org/apache/camel/component/azure/eventhubs/EventHubsConstants.html#OFFSET) | It sets the offset of the event when it was received from the associated Event Hub partition. This is only present on a received EventData. |  | Integer |
| **CamelAzureEventHubsEnqueuedTime** (consumer) Constant: [`ENQUEUED_TIME`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventhubs/latest/org/apache/camel/component/azure/eventhubs/EventHubsConstants.html#ENQUEUED_TIME) | It sets the instant, in UTC, of when the event was enqueued in the Event Hub partition. This is only present on a received EventData. |  | Instant |
| **CamelAzureEventHubsSequenceNumber** (consumer) Constant: [`SEQUENCE_NUMBER`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventhubs/latest/org/apache/camel/component/azure/eventhubs/EventHubsConstants.html#SEQUENCE_NUMBER) | It sets the sequence number assigned to the event when it was enqueued in the associated Event Hub partition. This is unique for every message received in the Event Hub partition. This is only present on a received EventData. |  | Long |
| **CamelAzureEventHubsMetadata** (consumer) Constant: [`METADATA`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventhubs/latest/org/apache/camel/component/azure/eventhubs/EventHubsConstants.html#METADATA) | The set of free-form event properties which may be used for passing metadata associated with the event with the event body during Event Hubs operations. |  | Map |
| **CamelMessageTimestamp** (consumer) Constant: [`MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventhubs/latest/org/apache/camel/component/azure/eventhubs/EventHubsConstants.html#MESSAGE_TIMESTAMP) | The timestamp of the message. |  | long |
| **CamelAzureEventHubsCheckpointUpdatedBy** (consumer) Constant: [`CHECKPOINT_UPDATED_BY`](https://javadoc.io/doc/org.apache.camel/camel-azure-eventhubs/latest/org/apache/camel/component/azure/eventhubs/EventHubsConstants.html#CHECKPOINT_UPDATED_BY) | It sets the reason for the checkpoint to have been updated. This is only present on a received EventData. |  | String |

### Message body type

The component’s producer expects the data in the message body to be in `byte[]`. This allows the user to utilize Camel TypeConverter to marshal/unmarshal data with ease. The same goes as well for the component’s consumer, it will set the encoded data as `byte[]` in the message body.

### Automatic detection of EventHubProducerAsyncClient client in registry

The component is capable of detecting the presence of an EventHubProducerAsyncClient bean into the registry. If it’s the only instance of that type it will be used as client and you won’t have to define it as uri parameter, like the example above. This may be really useful for smarter configuration of the endpoint.

### Consumer Example

The example below will unmarshal the events that was originally produced in JSON:

```java
from("azure-eventhubs:?connectionString=RAW({{connectionString}})"&blobContainerName=containerTest&eventPosition=#eventPosition"
    +"&blobAccountName={{blobAccountName}}&blobAccessKey=RAW({{blobAccessKey}})")
.unmarshal().json(JsonLibrary.Jackson)
.to(result);
```

### Producer Example

The example below will send events as String to EventHubs:

```java
from("direct:start")
.process(exchange -> {
        exchange.getIn().setHeader(EventHubsConstants.PARTITION_ID, firstPartition);
        exchange.getIn().setBody("test event");
})
.to("azure-eventhubs:?connectionString=RAW({{connectionString}})"
```

Also, the component supports as well **aggregation** of messages by sending events as **iterable** of either Exchanges/Messages or normal data (e.g: list of Strings). For example:

```java
from("direct:start")
.process(exchange -> {
        final List<String> messages = new LinkedList<>();
        messages.add("Test String Message 1");
        messages.add("Test String Message 2");

        exchange.getIn().setHeader(EventHubsConstants.PARTITION_ID, firstPartition);
        exchange.getIn().setBody(messages);
})
.to("azure-eventhubs:?connectionString=RAW({{connectionString}})"
```

### Azure-AD Authentication example

The example below makes use of the Azure-AD authentication. See [here](https://docs.microsoft.com/en-us/java/api/overview/azure/identity-readme?view=azure-java-stable#environment-variables) about what environment variables you need to set for this to work:

```java
@BindToRegistry("myTokenCredential")
public com.azure.core.credential.TokenCredential myTokenCredential() {
    return com.azure.identity.DefaultAzureCredentialBuilder().build();
}

from("direct:start")
.to("azure-eventhubs:namespace/eventHubName?tokenCredential=#myTokenCredential)"
```

### Development Notes (Important)

When developing on this component, you will need to obtain your Azure accessKey in order to run the integration tests. In addition to the mocked unit tests you **will need to run the integration tests with every change you make or even client upgrade as the Azure client can break things even on minor versions upgrade.** To run the integration tests, on this component directory, run the following maven command:

```bash
mvn verify -DconnectionString=string -DblobAccountName=blob -DblobAccessKey=key
```

Whereby `blobAccountName` is your Azure account name and `blobAccessKey` is the access key being generated from Azure portal and `connectionString` is the eventHub connection string.

## Spring Boot Auto-Configuration

When using azure-eventhubs with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-azure-eventhubs-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 24 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.azure-eventhubs.amqp-retry-options** | Sets the retry policy for EventHubAsyncClient. If not specified, the default retry options are used. The option is a com.azure.core.amqp.AmqpRetryOptions type. |  | AmqpRetryOptions |
| **camel.component.azure-eventhubs.amqp-transport-type** | Sets the transport type by which all the communication with Azure Event Hubs occurs. Default value is AmqpTransportType#AMQP. |  | AmqpTransportType |
| **camel.component.azure-eventhubs.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.azure-eventhubs.blob-access-key** | In case you chose the default BlobCheckpointStore, this sets access key for the associated azure account name to be used for authentication with azure blob services. |  | String |
| **camel.component.azure-eventhubs.blob-account-name** | In case you chose the default BlobCheckpointStore, this sets Azure account name to be used for authentication with azure blob services. |  | String |
| **camel.component.azure-eventhubs.blob-container-name** | In case you chose the default BlobCheckpointStore, this sets the blob container that shall be used by the BlobCheckpointStore to store the checkpoint offsets. |  | String |
| **camel.component.azure-eventhubs.blob-storage-shared-key-credential** | In case you chose the default BlobCheckpointStore, StorageSharedKeyCredential can be injected to create the azure client, this holds the important authentication information. The option is a com.azure.storage.common.StorageSharedKeyCredential type. |  | StorageSharedKeyCredential |
| **camel.component.azure-eventhubs.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.azure-eventhubs.checkpoint-batch-size** | Sets the batch size between each checkpoint updates. Works jointly with checkpointBatchTimeout. | 500 | Integer |
| **camel.component.azure-eventhubs.checkpoint-batch-timeout** | Sets the batch timeout between each checkpoint updates. Works jointly with checkpointBatchSize. | 5000 | Integer |
| **camel.component.azure-eventhubs.checkpoint-store** | Sets the CheckpointStore the EventProcessorClient will use for storing partition ownership and checkpoint information. Users can, optionally, provide their own implementation of CheckpointStore which will store ownership and checkpoint information. By default it set to use com.azure.messaging.eventhubs.checkpointstore.blob.BlobCheckpointStore which stores all checkpoint offsets into Azure Blob Storage. The option is a com.azure.messaging.eventhubs.CheckpointStore type. |  | CheckpointStore |
| **camel.component.azure-eventhubs.configuration** | The component configurations. The option is a org.apache.camel.component.azure.eventhubs.EventHubsConfiguration type. |  | EventHubsConfiguration |
| **camel.component.azure-eventhubs.connection-string** | Instead of supplying namespace, sharedAccessKey, sharedAccessName …​ etc, you can just supply the connection string for your eventHub. The connection string for EventHubs already include all the necessary information to connection to your EventHub. To learn on how to generate the connection string, take a look at this documentation: [https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string). |  | String |
| **camel.component.azure-eventhubs.consumer-group-name** | Sets the name of the consumer group this consumer is associated with. Events are read in the context of this group. The name of the consumer group that is created by default is \\{code $Default}. | $Default | String |
| **camel.component.azure-eventhubs.enabled** | Whether to enable auto configuration of the azure-eventhubs component. This is enabled by default. |  | Boolean |
| **camel.component.azure-eventhubs.event-position** | Sets the map containing the event position to use for each partition if a checkpoint for the partition does not exist in CheckpointStore. This map is keyed off of the partition id. If there is no checkpoint in CheckpointStore and there is no entry in this map, the processing of the partition will start from \\{link EventPosition#latest() latest} position. |  | Map |
| **camel.component.azure-eventhubs.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.azure-eventhubs.partition-id** | Sets the identifier of the Event Hub partition that the events will be sent to. If the identifier is not specified, the Event Hubs service will be responsible for routing events that are sent to an available partition. |  | String |
| **camel.component.azure-eventhubs.partition-key** | Sets a hashing key to be provided for the batch of events, which instructs the Event Hubs service to map this key to a specific partition. The selection of a partition is stable for a given partition hashing key. Should any other batches of events be sent using the same exact partition hashing key, the Event Hubs service will route them all to the same partition. This should be specified only when there is a need to group events by partition, but there is flexibility into which partition they are routed. If ensuring that a batch of events is sent only to a specific partition, it is recommended that the \\{link #setPartitionId(String) identifier of the position be specified directly} when sending the batch. |  | String |
| **camel.component.azure-eventhubs.prefetch-count** | Sets the count used by the receiver to control the number of events the Event Hub consumer will actively receive and queue locally without regard to whether a receive operation is currently active. | 500 | Integer |
| **camel.component.azure-eventhubs.producer-async-client** | Sets the EventHubProducerAsyncClient.An asynchronous producer responsible for transmitting EventData to a specific Event Hub, grouped together in batches. Depending on the options specified when creating an {linkEventDataBatch}, the events may be automatically routed to an available partition or specific to a partition. Use by this component to produce the data in camel producer. The option is a com.azure.messaging.eventhubs.EventHubProducerAsyncClient type. |  | EventHubProducerAsyncClient |
| **camel.component.azure-eventhubs.shared-access-key** | The generated value for the SharedAccessName. |  | String |
| **camel.component.azure-eventhubs.shared-access-name** | The name you chose for your EventHubs SAS keys. |  | String |
| **camel.component.azure-eventhubs.token-credential** | Still another way of authentication (beside supplying namespace, sharedAccessKey, sharedAccessName or connection string) is through Azure-AD authentication using an implementation instance of TokenCredential. The option is a com.azure.core.credential.TokenCredential type. |  | TokenCredential |