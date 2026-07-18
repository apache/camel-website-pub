# Pulsar

**Since Camel 2.24**

**Both producer and consumer are supported**

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-pulsar</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.y.z</version>
</dependency>
```

## URI format

pulsar:\[persistent|non-persistent\]://tenant/namespace/topic

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The Pulsar component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **authenticationClass** (common) | The Authentication FQCN to be used while creating the client from URI. |  | String |
| **authenticationParams** (common) | The Authentication Parameters to be used while creating the client from URI. |  | String |
| **configuration** (common) | Allows to pre-configure the Pulsar component with common options that the endpoints will reuse. |  | PulsarConfiguration |
| **serviceUrl** (common) | The Pulsar Service URL to point while creating the client from URI. |  | String |
| **ackGroupTimeMillis** (consumer) | Group the consumer acknowledgments for the specified time in milliseconds - defaults to 100. | 100 | long |
| **ackTimeoutMillis** (consumer) | Timeout for unacknowledged messages in milliseconds - defaults to 10000. | 10000 | long |
| **ackTimeoutRedeliveryBackoff** (consumer) | RedeliveryBackoff to use for ack timeout redelivery backoff. |  | RedeliveryBackoff |
| **allowManualAcknowledgement** (consumer) | Whether to allow manual message acknowledgements. If this option is enabled, then messages are not acknowledged automatically after successful route completion. Instead, an instance of PulsarMessageReceipt is stored as a header on the org.apache.camel.Exchange. Messages can then be acknowledged using PulsarMessageReceipt at any time before the ackTimeout occurs. | false | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerName** (consumer) | Name of the consumer when subscription is EXCLUSIVE. | sole-consumer | String |
| **consumerNamePrefix** (consumer) | Prefix to add to consumer names when a SHARED or FAILOVER subscription is used. | cons | String |
| **consumerQueueSize** (consumer) | Size of the consumer queue - defaults to 10. | 10 | int |
| **deadLetterTopic** (consumer) | Name of the topic where the messages which fail maxRedeliverCount times will be sent. Note: if not set, default topic name will be topicName-subscriptionName-DLQ. |  | String |
| **enableBatchIndexAcknowledgment** (consumer) | When enabled, allows each individual message in a batch to be acknowledged independently. By default Pulsar redelivers the entire batch when any single message in the batch is not acknowledged. This option also requires the Pulsar broker to be configured with acknowledgmentAtBatchIndexLevelEnabled=true. | false | boolean |
| **enableRetry** (consumer) | To enable retry letter topic mode. The default retry letter topic uses this format: topicname-subscriptionname-RETRY. | false | boolean |
| **keySharedPolicy** (consumer) | 
Policy to use by consumer when using key-shared subscription type.

Enum values:

-   AUTO\_SPLIT
    
-   STICKY
    





 |  | String |
| **maxRedeliverCount** (consumer) | Maximum number of times that a message will be redelivered before being sent to the dead letter queue. If this value is not set, no Dead Letter Policy will be created. |  | Integer |
| **messageListener** (consumer) | Whether to use the messageListener interface, or to receive messages using a separate thread pool. | true | boolean |
| **negativeAckRedeliveryBackoff** (consumer) | RedeliveryBackoff to use for negative ack redelivery backoff. |  | RedeliveryBackoff |
| **negativeAckRedeliveryDelayMicros** (consumer) | Set the negative acknowledgement delay. | 60000000 | long |
| **numberOfConsumers** (consumer) | Number of consumers - defaults to 1. | 1 | int |
| **numberOfConsumerThreads** (consumer) | Number of threads to receive and handle messages when using a separate thread pool. | 1 | int |
| **readCompacted** (consumer) | Enable compacted topic reading. | false | boolean |
| **retryLetterTopic** (consumer) | Name of the topic to use in retry mode. Note: if not set, default topic name will be topicName-subscriptionName-RETRY. |  | String |
| **subscriptionInitialPosition** (consumer) | 

Control the initial position in the topic of a newly created subscription. Default is latest message.

Enum values:

-   EARLIEST
    
-   LATEST
    





 | LATEST | SubscriptionInitialPosition |
| **subscriptionMode** (consumer) | 

Determines the subscription mode for the consumer. Durable subscriptions persist the cursor position if the consumer disconnects while non-durable subscriptions do not.

Enum values:

-   DURABLE
    
-   NON\_DURABLE
    





 | DURABLE | SubscriptionMode |
| **subscriptionName** (consumer) | Name of the subscription to use. | subs | String |
| **subscriptionTopicsMode** (consumer) | 

Determines to which topics this consumer should be subscribed to - Persistent, Non-Persistent, or both. Only used with pattern subscriptions.

Enum values:

-   PersistentOnly
    
-   NonPersistentOnly
    
-   AllTopics
    





 | PersistentOnly | RegexSubscriptionMode |
| **subscriptionType** (consumer) | 

Type of the subscription EXCLUSIVESHAREDFAILOVERKEY\_SHARED, defaults to EXCLUSIVE.

Enum values:

-   EXCLUSIVE
    
-   SHARED
    
-   FAILOVER
    
-   KEY\_SHARED
    





 | EXCLUSIVE | SubscriptionType |
| **topicsPattern** (consumer) | Whether the topic is a pattern (regular expression) that allows the consumer to subscribe to all matching topics in the namespace. | false | boolean |
| **pulsarMessageReceiptFactory** (consumer (advanced)) | Provide a factory to create an alternate implementation of PulsarMessageReceipt. |  | PulsarMessageReceiptFactory |
| **batcherBuilder** (producer) | 

Control batching method used by the producer.

Enum values:

-   DEFAULT
    
-   KEY\_BASED
    





 | DEFAULT | BatcherBuilder |
| **batchingEnabled** (producer) | Control whether automatic batching of messages is enabled for the producer. | true | boolean |
| **batchingMaxMessages** (producer) | The maximum size to batch messages. | 1000 | int |
| **batchingMaxPublishDelayMicros** (producer) | The maximum time period within which the messages sent will be batched if batchingEnabled is true. | 1000 | long |
| **blockIfQueueFull** (producer) | Whether to block the producing thread if pending messages queue is full or to throw a ProducerQueueIsFullError. | false | boolean |
| **chunkingEnabled** (producer) | Control whether chunking of messages is enabled for the producer. | false | boolean |
| **compressionType** (producer) | 

Compression type to use.

Enum values:

-   NONE
    
-   LZ4
    
-   ZLIB
    
-   ZSTD
    
-   SNAPPY
    





 | NONE | CompressionType |
| **hashingScheme** (producer) | 

Hashing function to use when choosing the partition to use for a particular message.

Enum values:

-   JavaStringHash
    
-   Murmur3\_32Hash
    





 | JavaStringHash | String |
| **initialSequenceId** (producer) | The first message published will have a sequence Id of initialSequenceId 1. | \-1 | long |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxPendingMessages** (producer) | Size of the pending massages queue. When the queue is full, by default, any further sends will fail unless blockIfQueueFull=true. | 1000 | int |
| **maxPendingMessagesAcrossPartitions** (producer) | **Deprecated** The maximum number of pending messages for partitioned topics. The maxPendingMessages value will be reduced if (number of partitions maxPendingMessages) exceeds this value. Partitioned topics have a pending message queue for each partition. | 50000 | int |
| **messageRouter** (producer) | Custom Message Router to use. |  | MessageRouter |
| **messageRoutingMode** (producer) | 

Message Routing Mode to use.

Enum values:

-   SinglePartition
    
-   RoundRobinPartition
    
-   CustomPartition
    





 | RoundRobinPartition | MessageRoutingMode |
| **producerName** (producer) | Name of the producer. If unset, lets Pulsar select a unique identifier. |  | String |
| **sendTimeoutMs** (producer) | Send timeout in milliseconds. | 30000 | int |
| **autoConfiguration** (advanced) | The pulsar auto configuration. |  | AutoConfiguration |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **pulsarClient** (advanced) | **Autowired** The pulsar client. |  | PulsarClient |

## Endpoint Options

The Pulsar endpoint is configured using URI syntax:

pulsar:persistence://tenant/namespace/topic

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **persistence** (common) | 
**Required** Whether the topic is persistent or non-persistent.

Enum values:

-   persistent
    
-   non-persistent
    





 |  | String |
| **tenant** (common) | **Required** The tenant. |  | String |
| **namespace** (common) | **Required** The namespace. |  | String |
| **topic** (common) | **Required** The topic. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **authenticationClass** (common) | The Authentication FQCN to be used while creating the client from URI. |  | String |
| **authenticationParams** (common) | The Authentication Parameters to be used while creating the client from URI. |  | String |
| **serviceUrl** (common) | The Pulsar Service URL to point while creating the client from URI. |  | String |
| **ackGroupTimeMillis** (consumer) | Group the consumer acknowledgments for the specified time in milliseconds - defaults to 100. | 100 | long |
| **ackTimeoutMillis** (consumer) | Timeout for unacknowledged messages in milliseconds - defaults to 10000. | 10000 | long |
| **ackTimeoutRedeliveryBackoff** (consumer) | RedeliveryBackoff to use for ack timeout redelivery backoff. |  | RedeliveryBackoff |
| **allowManualAcknowledgement** (consumer) | Whether to allow manual message acknowledgements. If this option is enabled, then messages are not acknowledged automatically after successful route completion. Instead, an instance of PulsarMessageReceipt is stored as a header on the org.apache.camel.Exchange. Messages can then be acknowledged using PulsarMessageReceipt at any time before the ackTimeout occurs. | false | boolean |
| **consumerName** (consumer) | Name of the consumer when subscription is EXCLUSIVE. | sole-consumer | String |
| **consumerNamePrefix** (consumer) | Prefix to add to consumer names when a SHARED or FAILOVER subscription is used. | cons | String |
| **consumerQueueSize** (consumer) | Size of the consumer queue - defaults to 10. | 10 | int |
| **deadLetterTopic** (consumer) | Name of the topic where the messages which fail maxRedeliverCount times will be sent. Note: if not set, default topic name will be topicName-subscriptionName-DLQ. |  | String |
| **enableBatchIndexAcknowledgment** (consumer) | When enabled, allows each individual message in a batch to be acknowledged independently. By default Pulsar redelivers the entire batch when any single message in the batch is not acknowledged. This option also requires the Pulsar broker to be configured with acknowledgmentAtBatchIndexLevelEnabled=true. | false | boolean |
| **enableRetry** (consumer) | To enable retry letter topic mode. The default retry letter topic uses this format: topicname-subscriptionname-RETRY. | false | boolean |
| **keySharedPolicy** (consumer) | 
Policy to use by consumer when using key-shared subscription type.

Enum values:

-   AUTO\_SPLIT
    
-   STICKY
    





 |  | String |
| **maxRedeliverCount** (consumer) | Maximum number of times that a message will be redelivered before being sent to the dead letter queue. If this value is not set, no Dead Letter Policy will be created. |  | Integer |
| **messageListener** (consumer) | Whether to use the messageListener interface, or to receive messages using a separate thread pool. | true | boolean |
| **negativeAckRedeliveryBackoff** (consumer) | RedeliveryBackoff to use for negative ack redelivery backoff. |  | RedeliveryBackoff |
| **negativeAckRedeliveryDelayMicros** (consumer) | Set the negative acknowledgement delay. | 60000000 | long |
| **numberOfConsumers** (consumer) | Number of consumers - defaults to 1. | 1 | int |
| **numberOfConsumerThreads** (consumer) | Number of threads to receive and handle messages when using a separate thread pool. | 1 | int |
| **readCompacted** (consumer) | Enable compacted topic reading. | false | boolean |
| **retryLetterTopic** (consumer) | Name of the topic to use in retry mode. Note: if not set, default topic name will be topicName-subscriptionName-RETRY. |  | String |
| **subscriptionInitialPosition** (consumer) | 

Control the initial position in the topic of a newly created subscription. Default is latest message.

Enum values:

-   EARLIEST
    
-   LATEST
    





 | LATEST | SubscriptionInitialPosition |
| **subscriptionMode** (consumer) | 

Determines the subscription mode for the consumer. Durable subscriptions persist the cursor position if the consumer disconnects while non-durable subscriptions do not.

Enum values:

-   DURABLE
    
-   NON\_DURABLE
    





 | DURABLE | SubscriptionMode |
| **subscriptionName** (consumer) | Name of the subscription to use. | subs | String |
| **subscriptionTopicsMode** (consumer) | 

Determines to which topics this consumer should be subscribed to - Persistent, Non-Persistent, or both. Only used with pattern subscriptions.

Enum values:

-   PersistentOnly
    
-   NonPersistentOnly
    
-   AllTopics
    





 | PersistentOnly | RegexSubscriptionMode |
| **subscriptionType** (consumer) | 

Type of the subscription EXCLUSIVESHAREDFAILOVERKEY\_SHARED, defaults to EXCLUSIVE.

Enum values:

-   EXCLUSIVE
    
-   SHARED
    
-   FAILOVER
    
-   KEY\_SHARED
    





 | EXCLUSIVE | SubscriptionType |
| **topicsPattern** (consumer) | Whether the topic is a pattern (regular expression) that allows the consumer to subscribe to all matching topics in the namespace. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **batcherBuilder** (producer) | 

Control batching method used by the producer.

Enum values:

-   DEFAULT
    
-   KEY\_BASED
    





 | DEFAULT | BatcherBuilder |
| **batchingEnabled** (producer) | Control whether automatic batching of messages is enabled for the producer. | true | boolean |
| **batchingMaxMessages** (producer) | The maximum size to batch messages. | 1000 | int |
| **batchingMaxPublishDelayMicros** (producer) | The maximum time period within which the messages sent will be batched if batchingEnabled is true. | 1000 | long |
| **blockIfQueueFull** (producer) | Whether to block the producing thread if pending messages queue is full or to throw a ProducerQueueIsFullError. | false | boolean |
| **chunkingEnabled** (producer) | Control whether chunking of messages is enabled for the producer. | false | boolean |
| **compressionType** (producer) | 

Compression type to use.

Enum values:

-   NONE
    
-   LZ4
    
-   ZLIB
    
-   ZSTD
    
-   SNAPPY
    





 | NONE | CompressionType |
| **hashingScheme** (producer) | 

Hashing function to use when choosing the partition to use for a particular message.

Enum values:

-   JavaStringHash
    
-   Murmur3\_32Hash
    





 | JavaStringHash | String |
| **initialSequenceId** (producer) | The first message published will have a sequence Id of initialSequenceId 1. | \-1 | long |
| **maxPendingMessages** (producer) | Size of the pending massages queue. When the queue is full, by default, any further sends will fail unless blockIfQueueFull=true. | 1000 | int |
| **maxPendingMessagesAcrossPartitions** (producer) | **Deprecated** The maximum number of pending messages for partitioned topics. The maxPendingMessages value will be reduced if (number of partitions maxPendingMessages) exceeds this value. Partitioned topics have a pending message queue for each partition. | 50000 | int |
| **messageRouter** (producer) | Custom Message Router to use. |  | MessageRouter |
| **messageRoutingMode** (producer) | 

Message Routing Mode to use.

Enum values:

-   SinglePartition
    
-   RoundRobinPartition
    
-   CustomPartition
    





 | RoundRobinPartition | MessageRoutingMode |
| **producerName** (producer) | Name of the producer. If unset, lets Pulsar select a unique identifier. |  | String |
| **sendTimeoutMs** (producer) | Send timeout in milliseconds. | 30000 | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Pulsar component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **properties** (consumer) Constant: [`PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#PROPERTIES) | The properties attached to the message. |  | Map |
| **producer\_name** (consumer) Constant: [`PRODUCER_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#PRODUCER_NAME) | The producer name who produced the message. |  | String |
| **sequence\_id** (consumer) Constant: [`SEQUENCE_ID`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#SEQUENCE_ID) | The sequence id associated with the message. |  | long |
| **publish\_time** (consumer) Constant: [`PUBLISH_TIME`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#PUBLISH_TIME) | The publish time of the message. |  | long |
| **message\_id** (consumer) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#MESSAGE_ID) | The unique message ID associated with the message. |  | MessageId |
| **event\_time** (consumer) Constant: [`EVENT_TIME`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#EVENT_TIME) | The event time associated with the message. |  | long |
| **key** (consumer) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#KEY) | The key of the message. |  | String |
| **key\_bytes** (consumer) Constant: [`KEY_BYTES`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#KEY_BYTES) | The bytes in key. |  | byte\[\] |
| **topic\_name** (consumer) Constant: [`TOPIC_NAME`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#TOPIC_NAME) | The topic the message was published to. |  | String |
| **message\_receipt** (consumer) Constant: [`MESSAGE_RECEIPT`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#MESSAGE_RECEIPT) | The message receipt. |  | PulsarMessageReceipt |
| **CamelPulsarProducerMessageKey** (producer) Constant: [`KEY_OUT`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#KEY_OUT) | The key of the message for routing policy. |  | String |
| **CamelPulsarProducerMessageProperties** (producer) Constant: [`PROPERTIES_OUT`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#PROPERTIES_OUT) | The properties of the message to add. |  | Map |
| **CamelPulsarProducerMessageEventTime** (producer) Constant: [`EVENT_TIME_OUT`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#EVENT_TIME_OUT) | The event time of the message message. |  | Long |
| **CamelPulsarProducerMessageDeliverAt** (producer) Constant: [`DELIVER_AT_OUT`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#DELIVER_AT_OUT) | Deliver the message only at or after the specified absolute timestamp. The timestamp is milliseconds and based on UTC (eg: System.currentTimeMillis) Note: messages are only delivered with delay when a consumer is consuming through a Shared subscription. With other subscription types, the messages will still be delivered immediately. |  | Long |
| **CamelPulsarRedeliveryCount** (consumer) Constant: [`PULSAR_REDELIVERY_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#PULSAR_REDELIVERY_COUNT) | The message redelivery count, redelivery count maintain in pulsar broker. |  | int |
| **CamelPulsarProducerMessageDeliverAfter** (producer) Constant: [`DELIVER_AFTER`](https://javadoc.io/doc/org.apache.camel/camel-pulsar/latest/org/apache/camel/component/pulsar/utils/message/PulsarMessageHeaders.html#DELIVER_AFTER) | Deliver the message after a given delayed time (millis). |  | Long |