# Kafka

**Since Camel 2.13**

**Both producer and consumer are supported**

The Kafka component is used for communicating with [Apache Kafka](http://kafka.apache.org/) message broker.

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-kafka</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

kafka:topic\[?options\]

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

The Kafka component supports 109 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalProperties** (common) | Sets additional properties for either kafka consumer or kafka producer in case they can’t be set directly on the camel configurations (e.g: new Kafka properties that are not reflected yet in Camel configurations), the properties have to be prefixed with additionalProperties.. E.g: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. |  | Map |
| **brokers** (common) | URL of the Kafka brokers to use. The format is host1:port1,host2:port2, and the list can be a subset of brokers or a VIP pointing to a subset of brokers. This option is known as bootstrap.servers in the Kafka documentation. |  | String |
| **clientId** (common) | The client id is a user-specified string sent in each request to help trace calls. It should logically identify the application making the request. |  | String |
| **configuration** (common) | Allows to pre-configure the Kafka component with common options that the endpoints will reuse. |  | KafkaConfiguration |
| **headerFilterStrategy** (common) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **reconnectBackoffMaxMs** (common) | The maximum amount of time in milliseconds to wait when reconnecting to a broker that has repeatedly failed to connect. If provided, the backoff per host will increase exponentially for each consecutive connection failure, up to this maximum. After calculating the backoff increase, 20% random jitter is added to avoid connection storms. | 1000 | Integer |
| **shutdownTimeout** (common) | Timeout in milliseconds to wait gracefully for the consumer or producer to shutdown and terminate its worker threads. | 30000 | int |
| **allowManualCommit** (consumer) | Whether to allow doing manual commits via KafkaManualCommit. If this option is enabled then an instance of KafkaManualCommit is stored on the Exchange message header, which allows end users to access this API and perform manual offset commits via the Kafka consumer. | false | boolean |
| **autoCommitEnable** (consumer) | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. This committed offset will be used when the process fails as the position from which the new consumer will begin. | true | boolean |
| **autoCommitIntervalMs** (consumer) | The frequency in ms that the consumer offsets are committed to zookeeper. | 5000 | Integer |
| **autoOffsetReset** (consumer) | 
What to do when there is no initial offset in ZooKeeper or if an offset is out of range: earliest : automatically reset the offset to the earliest offset latest : automatically reset the offset to the latest offset fail: throw exception to the consumer.

Enum values:

-   latest
    
-   earliest
    
-   none
    





 | latest | String |
| **breakOnFirstError** (consumer) | This options controls what happens when a consumer is processing an exchange and it fails. If the option is false then the consumer continues to the next message and processes it. If the option is true then the consumer breaks out. Using the default NoopCommitManager will cause the consumer to not commit the offset so that the message is re-attempted. The consumer should use the KafkaManualCommit to determine the best way to handle the message. Using either the SynchCommitManager or the AsynchCommitManager the consumer will seek back to the offset of the message that caused a failure, and then re-attempt to process this message. However this can lead to endless processing of the same message if its bound to fail every time, eg a poison message. Therefore its recommended to deal with that for example by using Camel’s error handler. | false | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **checkCrcs** (consumer) | Automatically check the CRC32 of the records consumed. This ensures no on-the-wire or on-disk corruption to the messages occurred. This check adds some overhead, so it may be disabled in cases seeking extreme performance. | true | Boolean |
| **commitTimeoutMs** (consumer) | The maximum time, in milliseconds, that the code will wait for a synchronous commit to complete. | 5000 | Long |
| **consumerRequestTimeoutMs** (consumer) | The configuration controls the maximum amount of time the client will wait for the response of a request. If the response is not received before the timeout elapses the client will resend the request if necessary or fail the request if retries are exhausted. | 30000 | Integer |
| **consumersCount** (consumer) | The number of consumers that connect to kafka server. Each consumer is run on a separate thread, that retrieves and process the incoming data. | 1 | int |
| **fetchMaxBytes** (consumer) | The maximum amount of data the server should return for a fetch request This is not an absolute maximum, if the first message in the first non-empty partition of the fetch is larger than this value, the message will still be returned to ensure that the consumer can make progress. The maximum message size accepted by the broker is defined via message.max.bytes (broker config) or max.message.bytes (topic config). Note that the consumer performs multiple fetches in parallel. | 52428800 | Integer |
| **fetchMinBytes** (consumer) | The minimum amount of data the server should return for a fetch request. If insufficient data is available the request will wait for that much data to accumulate before answering the request. | 1 | Integer |
| **fetchWaitMaxMs** (consumer) | The maximum amount of time the server will block before answering the fetch request if there isn’t sufficient data to immediately satisfy fetch.min.bytes. | 500 | Integer |
| **groupId** (consumer) | A string that uniquely identifies the group of consumer processes to which this consumer belongs. By setting the same group id multiple processes indicate that they are all part of the same consumer group. This option is required for consumers. |  | String |
| **groupInstanceId** (consumer) | A unique identifier of the consumer instance provided by the end user. Only non-empty strings are permitted. If set, the consumer is treated as a static member, which means that only one instance with this ID is allowed in the consumer group at any time. This can be used in combination with a larger session timeout to avoid group rebalances caused by transient unavailability (e.g. process restarts). If not set, the consumer will join the group as a dynamic member, which is the traditional behavior. |  | String |
| **headerDeserializer** (consumer) | To use a custom KafkaHeaderDeserializer to deserialize kafka headers values. |  | KafkaHeaderDeserializer |
| **heartbeatIntervalMs** (consumer) | The expected time between heartbeats to the consumer coordinator when using Kafka’s group management facilities. Heartbeats are used to ensure that the consumer’s session stays active and to facilitate rebalancing when new consumers join or leave the group. The value must be set lower than session.timeout.ms, but typically should be set no higher than 1/3 of that value. It can be adjusted even lower to control the expected time for normal rebalances. | 3000 | Integer |
| **keyDeserializer** (consumer) | Deserializer class for key that implements the Deserializer interface. | org.apache.kafka.common.serialization.StringDeserializer | String |
| **maxPartitionFetchBytes** (consumer) | The maximum amount of data per-partition the server will return. The maximum total memory used for a request will be #partitions max.partition.fetch.bytes. This size must be at least as large as the maximum message size the server allows or else it is possible for the producer to send messages larger than the consumer can fetch. If that happens, the consumer can get stuck trying to fetch a large message on a certain partition. | 1048576 | Integer |
| **maxPollIntervalMs** (consumer) | The maximum delay between invocations of poll() when using consumer group management. This places an upper bound on the amount of time that the consumer can be idle before fetching more records. If poll() is not called before expiration of this timeout, then the consumer is considered failed and the group will rebalance in order to reassign the partitions to another member. |  | Integer |
| **maxPollRecords** (consumer) | The maximum number of records returned in a single call to poll(). | 500 | Integer |
| **offsetRepository** (consumer) | The offset repository to use in order to locally store the offset of each partition of the topic. Defining one will disable the autocommit. |  | StateRepository |
| **partitionAssignor** (consumer) | The class name of the partition assignment strategy that the client will use to distribute partition ownership amongst consumer instances when group management is used. | org.apache.kafka.clients.consumer.RangeAssignor | String |
| **pollOnError** (consumer) | 

What to do if kafka threw an exception while polling for new messages. Will by default use the value from the component configuration unless an explicit value has been configured on the endpoint level. DISCARD will discard the message and continue to poll next message. ERROR\_HANDLER will use Camel’s error handler to process the exception, and afterwards continue to poll next message. RECONNECT will re-connect the consumer and try poll the message again RETRY will let the consumer retry polling the same message again STOP will stop the consumer (have to be manually started/restarted if the consumer should be able to consume messages again).

Enum values:

-   DISCARD
    
-   ERROR\_HANDLER
    
-   RECONNECT
    
-   RETRY
    
-   STOP
    





 | ERROR\_HANDLER | PollOnError |
| **pollTimeoutMs** (consumer) | The timeout used when polling the KafkaConsumer. | 5000 | Long |
| **seekTo** (consumer) | 

Set if KafkaConsumer will read from beginning or end on startup: SeekPolicy.BEGINNING: read from beginning. SeekPolicy.END: read from end.

Enum values:

-   BEGINNING
    
-   END
    





 |  | SeekPolicy |
| **sessionTimeoutMs** (consumer) | The timeout used to detect failures when using Kafka’s group management facilities. | 45000 | Integer |
| **specificAvroReader** (consumer) | This enables the use of a specific Avro reader for use with the Confluent Platform schema registry and the io.confluent.kafka.serializers.KafkaAvroDeserializer. This option is only available in the Confluent Platform (not standard Apache Kafka). | false | boolean |
| **topicIsPattern** (consumer) | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | false | boolean |
| **valueDeserializer** (consumer) | Deserializer class for value that implements the Deserializer interface. | org.apache.kafka.common.serialization.StringDeserializer | String |
| **createConsumerBackoffInterval** (consumer (advanced)) | The delay in millis seconds to wait before trying again to create the kafka consumer (kafka-client). | 5000 | long |
| **createConsumerBackoffMaxAttempts** (consumer (advanced)) | Maximum attempts to create the kafka consumer (kafka-client), before eventually giving up and failing. Error during creating the consumer may be fatal due to invalid configuration and as such recovery is not possible. However, one part of the validation is DNS resolution of the bootstrap broker hostnames. This may be a temporary networking problem, and could potentially be recoverable. While other errors are fatal such as some invalid kafka configurations. Unfortunately kafka-client does not separate this kind of errors. Camel will by default retry forever, and therefore never give up. If you want to give up after many attempts then set this option and Camel will then when giving up terminate the consumer. You can manually restart the consumer by stopping and starting the route, to try again. |  | int |
| **isolationLevel** (consumer (advanced)) | 

Controls how to read messages written transactionally. If set to read\_committed, consumer.poll() will only return transactional messages which have been committed. If set to read\_uncommitted (the default), consumer.poll() will return all messages, even transactional messages which have been aborted. Non-transactional messages will be returned unconditionally in either mode. Messages will always be returned in offset order. Hence, in read\_committed mode, consumer.poll() will only return messages up to the last stable offset (LSO), which is the one less than the offset of the first open transaction. In particular any messages appearing after messages belonging to ongoing transactions will be withheld until the relevant transaction has been completed. As a result, read\_committed consumers will not be able to read up to the high watermark when there are in flight transactions. Further, when in read\_committed the seekToEnd method will return the LSO.

Enum values:

-   read\_uncommitted
    
-   read\_committed
    





 | read\_uncommitted | String |
| **kafkaManualCommitFactory** (consumer (advanced)) | **Autowired** Factory to use for creating KafkaManualCommit instances. This allows to plugin a custom factory to create custom KafkaManualCommit instances in case special logic is needed when doing manual commits that deviates from the default implementation that comes out of the box. |  | KafkaManualCommitFactory |
| **pollExceptionStrategy** (consumer (advanced)) | **Autowired** To use a custom strategy with the consumer to control how to handle exceptions thrown from the Kafka broker while pooling messages. |  | PollExceptionStrategy |
| **subscribeConsumerBackoffInterval** (consumer (advanced)) | The delay in millis seconds to wait before trying again to subscribe to the kafka broker. | 5000 | long |
| **subscribeConsumerBackoffMaxAttempts** (consumer (advanced)) | Maximum number the kafka consumer will attempt to subscribe to the kafka broker, before eventually giving up and failing. Error during subscribing the consumer to the kafka topic could be temporary errors due to network issues, and could potentially be recoverable. Camel will by default retry forever, and therefore never give up. If you want to give up after many attempts then set this option and Camel will then when giving up terminate the consumer. You can manually restart the consumer by stopping and starting the route, to try again. |  | int |
| **batchWithIndividualHeaders** (producer) | If this feature is enabled and a single element of a batch is an Exchange or Message, the producer will generate individual kafka header values for it by using the batch Message to determine the values. Normal behaviour consists in always using the same header values (which are determined by the parent Exchange which contains the Iterable or Iterator). | false | boolean |
| **bufferMemorySize** (producer) | The total bytes of memory the producer can use to buffer records waiting to be sent to the server. If records are sent faster than they can be delivered to the server the producer will either block or throw an exception based on the preference specified by block.on.buffer.full.This setting should correspond roughly to the total memory the producer will use, but is not a hard bound since not all memory the producer uses is used for buffering. Some additional memory will be used for compression (if compression is enabled) as well as for maintaining in-flight requests. | 33554432 | Integer |
| **compressionCodec** (producer) | 

This parameter allows you to specify the compression codec for all data generated by this producer. Valid values are none, gzip, snappy, lz4 and zstd.

Enum values:

-   none
    
-   gzip
    
-   snappy
    
-   lz4
    
-   zstd
    





 | none | String |
| **connectionMaxIdleMs** (producer) | Close idle connections after the number of milliseconds specified by this config. | 540000 | Integer |
| **deliveryTimeoutMs** (producer) | An upper bound on the time to report success or failure after a call to send() returns. This limits the total time that a record will be delayed prior to sending, the time to await acknowledgement from the broker (if expected), and the time allowed for retriable send failures. | 120000 | Integer |
| **enableIdempotence** (producer) | When set to 'true', the producer will ensure that exactly one copy of each message is written in the stream. If 'false', producer retries due to broker failures, etc., may write duplicates of the retried message in the stream. Note that enabling idempotence requires max.in.flight.requests.per.connection to be less than or equal to 5 (with message ordering preserved for any allowable value), retries to be greater than 0, and acks must be 'all'. Idempotence is enabled by default if no conflicting configurations are set. If conflicting configurations are set and idempotence is not explicitly enabled, idempotence is disabled. If idempotence is explicitly enabled and conflicting configurations are set, a ConfigException is thrown. | true | boolean |
| **headerSerializer** (producer) | To use a custom KafkaHeaderSerializer to serialize kafka headers values. |  | KafkaHeaderSerializer |
| **key** (producer) | The record key (or null if no key is specified). If this option has been configured then it take precedence over header KafkaConstants#KEY. |  | String |
| **keySerializer** (producer) | The serializer class for keys (defaults to the same as for messages if nothing is given). | org.apache.kafka.common.serialization.StringSerializer | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **lingerMs** (producer) | The producer groups together any records that arrive in between request transmissions into a single batched request. Normally this occurs only under load when records arrive faster than they can be sent out. However in some circumstances the client may want to reduce the number of requests even under moderate load. This setting accomplishes this by adding a small amount of artificial delay that is, rather than immediately sending out a record the producer will wait for up to the given delay to allow other records to be sent so that the sends can be batched together. This can be thought of as analogous to Nagle’s algorithm in TCP. This setting gives the upper bound on the delay for batching: once we get batch.size worth of records for a partition it will be sent immediately regardless of this setting, however if we have fewer than this many bytes accumulated for this partition we will 'linger' for the specified time waiting for more records to show up. This setting defaults to 0 (i.e. no delay). Setting linger.ms=5, for example, would have the effect of reducing the number of requests sent but would add up to 5ms of latency to records sent in the absence of load. | 0 | Integer |
| **maxBlockMs** (producer) | The configuration controls how long the KafkaProducer’s send(), partitionsFor(), initTransactions(), sendOffsetsToTransaction(), commitTransaction() and abortTransaction() methods will block. For send() this timeout bounds the total time waiting for both metadata fetch and buffer allocation (blocking in the user-supplied serializers or partitioner is not counted against this timeout). For partitionsFor() this timeout bounds the time spent waiting for metadata if it is unavailable. The transaction-related methods always block, but may timeout if the transaction coordinator could not be discovered or did not respond within the timeout. | 60000 | Integer |
| **maxInFlightRequest** (producer) | The maximum number of unacknowledged requests the client will send on a single connection before blocking. Note that if this setting is set to be greater than 1 and there are failed sends, there is a risk of message re-ordering due to retries (i.e., if retries are enabled). | 5 | Integer |
| **maxRequestSize** (producer) | The maximum size of a request. This is also effectively a cap on the maximum record size. Note that the server has its own cap on record size which may be different from this. This setting will limit the number of record batches the producer will send in a single request to avoid sending huge requests. | 1048576 | Integer |
| **metadataMaxAgeMs** (producer) | The period of time in milliseconds after which we force a refresh of metadata even if we haven’t seen any partition leadership changes to proactively discover any new brokers or partitions. | 300000 | Integer |
| **metricReporters** (producer) | A list of classes to use as metrics reporters. Implementing the MetricReporter interface allows plugging in classes that will be notified of new metric creation. The JmxReporter is always included to register JMX statistics. |  | String |
| **metricsSampleWindowMs** (producer) | The window of time a metrics sample is computed over. | 30000 | Integer |
| **noOfMetricsSample** (producer) | The number of samples maintained to compute metrics. | 2 | Integer |
| **partitioner** (producer) | The partitioner class for partitioning messages amongst sub-topics. The default partitioner is based on the hash of the key. | org.apache.kafka.clients.producer.internals.DefaultPartitioner | String |
| **partitionKey** (producer) | The partition to which the record will be sent (or null if no partition was specified). If this option has been configured then it take precedence over header KafkaConstants#PARTITION\_KEY. |  | Integer |
| **producerBatchSize** (producer) | The producer will attempt to batch records together into fewer requests whenever multiple records are being sent to the same partition. This helps performance on both the client and the server. This configuration controls the default batch size in bytes. No attempt will be made to batch records larger than this size.Requests sent to brokers will contain multiple batches, one for each partition with data available to be sent.A small batch size will make batching less common and may reduce throughput (a batch size of zero will disable batching entirely). A very large batch size may use memory a bit more wastefully as we will always allocate a buffer of the specified batch size in anticipation of additional records. | 16384 | Integer |
| **queueBufferingMaxMessages** (producer) | The maximum number of unsent messages that can be queued up the producer when using async mode before either the producer must be blocked or data must be dropped. | 10000 | Integer |
| **receiveBufferBytes** (producer) | The size of the TCP receive buffer (SO\_RCVBUF) to use when reading data. | 65536 | Integer |
| **reconnectBackoffMs** (producer) | The amount of time to wait before attempting to reconnect to a given host. This avoids repeatedly connecting to a host in a tight loop. This backoff applies to all requests sent by the consumer to the broker. | 50 | Integer |
| **recordMetadata** (producer) | Whether the producer should store the RecordMetadata results from sending to Kafka. The results are stored in a List containing the RecordMetadata metadata’s. The list is stored on a header with the key KafkaConstants#KAFKA\_RECORDMETA. | true | boolean |
| **requestRequiredAcks** (producer) | 

The number of acknowledgments the producer requires the leader to have received before considering a request complete. This controls the durability of records that are sent. The following settings are allowed: acks=0 If set to zero then the producer will not wait for any acknowledgment from the server at all. The record will be immediately added to the socket buffer and considered sent. No guarantee can be made that the server has received the record in this case, and the retries configuration will not take effect (as the client won’t generally know of any failures). The offset given back for each record will always be set to -1. acks=1 This will mean the leader will write the record to its local log but will respond without awaiting full acknowledgement from all followers. In this case should the leader fail immediately after acknowledging the record but before the followers have replicated it then the record will be lost. acks=all This means the leader will wait for the full set of in-sync replicas to acknowledge the record. This guarantees that the record will not be lost as long as at least one in-sync replica remains alive. This is the strongest available guarantee. This is equivalent to the acks=-1 setting. Note that enabling idempotence requires this config value to be 'all'. If conflicting configurations are set and idempotence is not explicitly enabled, idempotence is disabled.

Enum values:

-   all
    
-   \-1
    
-   0
    
-   1
    





 | all | String |
| **requestTimeoutMs** (producer) | The amount of time the broker will wait trying to meet the request.required.acks requirement before sending back an error to the client. | 30000 | Integer |
| **retries** (producer) | Setting a value greater than zero will cause the client to resend any record whose send fails with a potentially transient error. Note that this retry is no different than if the client resent the record upon receiving the error. Produce requests will be failed before the number of retries has been exhausted if the timeout configured by delivery.timeout.ms expires first before successful acknowledgement. Users should generally prefer to leave this config unset and instead use delivery.timeout.ms to control retry behavior. Enabling idempotence requires this config value to be greater than 0. If conflicting configurations are set and idempotence is not explicitly enabled, idempotence is disabled. Allowing retries while setting enable.idempotence to false and max.in.flight.requests.per.connection to 1 will potentially change the ordering of records because if two batches are sent to a single partition, and the first fails and is retried but the second succeeds, then the records in the second batch may appear first. |  | Integer |
| **retryBackoffMs** (producer) | Before each retry, the producer refreshes the metadata of relevant topics to see if a new leader has been elected. Since leader election takes a bit of time, this property specifies the amount of time that the producer waits before refreshing the metadata. | 100 | Integer |
| **sendBufferBytes** (producer) | Socket write buffer size. | 131072 | Integer |
| **useIterator** (producer) | Sets whether sending to kafka should send the message body as a single record, or use a java.util.Iterator to send multiple records to kafka (if the message body can be iterated). | true | boolean |
| **valueSerializer** (producer) | The serializer class for messages. | org.apache.kafka.common.serialization.StringSerializer | String |
| **workerPool** (producer) | To use a custom worker pool for continue routing Exchange after kafka server has acknowledge the message that was sent to it from KafkaProducer using asynchronous non-blocking processing. If using this option then you must handle the lifecycle of the thread pool to shut the pool down when no longer needed. |  | ExecutorService |
| **workerPoolCoreSize** (producer) | Number of core threads for the worker pool for continue routing Exchange after kafka server has acknowledge the message that was sent to it from KafkaProducer using asynchronous non-blocking processing. | 10 | Integer |
| **workerPoolMaxSize** (producer) | Maximum number of threads for the worker pool for continue routing Exchange after kafka server has acknowledge the message that was sent to it from KafkaProducer using asynchronous non-blocking processing. | 20 | Integer |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **kafkaClientFactory** (advanced) | **Autowired** Factory to use for creating org.apache.kafka.clients.consumer.KafkaConsumer and org.apache.kafka.clients.producer.KafkaProducer instances. This allows to configure a custom factory to create instances with logic that extends the vanilla Kafka clients. |  | KafkaClientFactory |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **schemaRegistryURL** (confluent) | URL of the Confluent Platform schema registry servers to use. The format is host1:port1,host2:port2. This is known as schema.registry.url in the Confluent Platform documentation. This option is only available in the Confluent Platform (not standard Apache Kafka). |  | String |
| **interceptorClasses** (monitoring) | Sets interceptors for producer or consumers. Producer interceptors have to be classes implementing org.apache.kafka.clients.producer.ProducerInterceptor Consumer interceptors have to be classes implementing org.apache.kafka.clients.consumer.ConsumerInterceptor Note that if you use Producer interceptor on a consumer it will throw a class cast exception in runtime. |  | String |
| **kerberosBeforeReloginMinTime** (security) | Login thread sleep time between refresh attempts. | 60000 | Integer |
| **kerberosInitCmd** (security) | Kerberos kinit command path. Default is /usr/bin/kinit. | /usr/bin/kinit | String |
| **kerberosPrincipalToLocalRules** (security) | A list of rules for mapping from principal names to short names (typically operating system usernames). The rules are evaluated in order and the first rule that matches a principal name is used to map it to a short name. Any later rules in the list are ignored. By default, principal names of the form {username}/{hostname}{REALM} are mapped to {username}. For more details on the format please see the security authorization and acls documentation (at the Apache Kafka project). Multiple values can be separated by comma. | DEFAULT | String |
| **kerberosRenewJitter** (security) | Percentage of random jitter added to the renewal time. | 0.05 | Double |
| **kerberosRenewWindowFactor** (security) | Login thread will sleep until the specified window factor of time from last refresh to ticket’s expiry has been reached, at which time it will try to renew the ticket. | 0.8 | Double |
| **saslJaasConfig** (security) | Expose the kafka sasl.jaas.config parameter Example: org.apache.kafka.common.security.plain.PlainLoginModule required username=USERNAME password=PASSWORD;. |  | String |
| **saslKerberosServiceName** (security) | The Kerberos principal name that Kafka runs as. This can be defined either in Kafka’s JAAS config or in Kafka’s config. |  | String |
| **saslMechanism** (security) | The Simple Authentication and Security Layer (SASL) Mechanism used. For the valid values see [http://www.iana.org/assignments/sasl-mechanisms/sasl-mechanisms.xhtml](http://www.iana.org/assignments/sasl-mechanisms/sasl-mechanisms.xhtml). | GSSAPI | String |
| **securityProtocol** (security) | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | PLAINTEXT | String |
| **sslCipherSuites** (security) | A list of cipher suites. This is a named combination of authentication, encryption, MAC and key exchange algorithm used to negotiate the security settings for a network connection using TLS or SSL network protocol. By default all the available cipher suites are supported. |  | String |
| **sslContextParameters** (security) | SSL configuration using a Camel SSLContextParameters object. If configured it’s applied before the other SSL endpoint parameters. NOTE: Kafka only supports loading keystore from file locations, so prefix the location with file: in the KeyStoreParameters.resource option. |  | SSLContextParameters |
| **sslEnabledProtocols** (security) | The list of protocols enabled for SSL connections. The default is TLSv1.2,TLSv1.3 when running with Java 11 or newer, TLSv1.2 otherwise. With the default value for Java 11, clients and servers will prefer TLSv1.3 if both support it and fallback to TLSv1.2 otherwise (assuming both support at least TLSv1.2). This default should be fine for most cases. Also see the config documentation for SslProtocol. |  | String |
| **sslEndpointAlgorithm** (security) | The endpoint identification algorithm to validate server hostname using server certificate. Use none or false to disable server hostname verification. | https | String |
| **sslKeymanagerAlgorithm** (security) | The algorithm used by key manager factory for SSL connections. Default value is the key manager factory algorithm configured for the Java Virtual Machine. | SunX509 | String |
| **sslKeyPassword** (security) | The password of the private key in the key store file or the PEM key specified in sslKeystoreKey. This is required for clients only if two-way authentication is configured. |  | String |
| **sslKeystoreLocation** (security) | The location of the key store file. This is optional for client and can be used for two-way authentication for client. |  | String |
| **sslKeystorePassword** (security) | The store password for the key store file. This is optional for client and only needed if sslKeystoreLocation' is configured. Key store password is not supported for PEM format. |  | String |
| **sslKeystoreType** (security) | The file format of the key store file. This is optional for client. Default value is JKS. | JKS | String |
| **sslProtocol** (security) | The SSL protocol used to generate the SSLContext. The default is TLSv1.3 when running with Java 11 or newer, TLSv1.2 otherwise. This value should be fine for most use cases. Allowed values in recent JVMs are TLSv1.2 and TLSv1.3. TLS, TLSv1.1, SSL, SSLv2 and SSLv3 may be supported in older JVMs, but their usage is discouraged due to known security vulnerabilities. With the default value for this config and sslEnabledProtocols, clients will downgrade to TLSv1.2 if the server does not support TLSv1.3. If this config is set to TLSv1.2, clients will not use TLSv1.3 even if it is one of the values in sslEnabledProtocols and the server only supports TLSv1.3. |  | String |
| **sslProvider** (security) | The name of the security provider used for SSL connections. Default value is the default security provider of the JVM. |  | String |
| **sslTrustmanagerAlgorithm** (security) | The algorithm used by trust manager factory for SSL connections. Default value is the trust manager factory algorithm configured for the Java Virtual Machine. | PKIX | String |
| **sslTruststoreLocation** (security) | The location of the trust store file. |  | String |
| **sslTruststorePassword** (security) | The password for the trust store file. If a password is not set, trust store file configured will still be used, but integrity checking is disabled. Trust store password is not supported for PEM format. |  | String |
| **sslTruststoreType** (security) | The file format of the trust store file. Default value is JKS. | JKS | String |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Kafka endpoint is configured using URI syntax:

kafka:topic

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **topic** (common) | **Required** Name of the topic to use. On the consumer you can use comma to separate multiple topics. A producer can only send a message to a single topic. |  | String |

### Query Parameters (103 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalProperties** (common) | Sets additional properties for either kafka consumer or kafka producer in case they can’t be set directly on the camel configurations (e.g: new Kafka properties that are not reflected yet in Camel configurations), the properties have to be prefixed with additionalProperties.. E.g: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. |  | Map |
| **brokers** (common) | URL of the Kafka brokers to use. The format is host1:port1,host2:port2, and the list can be a subset of brokers or a VIP pointing to a subset of brokers. This option is known as bootstrap.servers in the Kafka documentation. |  | String |
| **clientId** (common) | The client id is a user-specified string sent in each request to help trace calls. It should logically identify the application making the request. |  | String |
| **headerFilterStrategy** (common) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **reconnectBackoffMaxMs** (common) | The maximum amount of time in milliseconds to wait when reconnecting to a broker that has repeatedly failed to connect. If provided, the backoff per host will increase exponentially for each consecutive connection failure, up to this maximum. After calculating the backoff increase, 20% random jitter is added to avoid connection storms. | 1000 | Integer |
| **shutdownTimeout** (common) | Timeout in milliseconds to wait gracefully for the consumer or producer to shutdown and terminate its worker threads. | 30000 | int |
| **allowManualCommit** (consumer) | Whether to allow doing manual commits via KafkaManualCommit. If this option is enabled then an instance of KafkaManualCommit is stored on the Exchange message header, which allows end users to access this API and perform manual offset commits via the Kafka consumer. | false | boolean |
| **autoCommitEnable** (consumer) | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. This committed offset will be used when the process fails as the position from which the new consumer will begin. | true | boolean |
| **autoCommitIntervalMs** (consumer) | The frequency in ms that the consumer offsets are committed to zookeeper. | 5000 | Integer |
| **autoOffsetReset** (consumer) | 
What to do when there is no initial offset in ZooKeeper or if an offset is out of range: earliest : automatically reset the offset to the earliest offset latest : automatically reset the offset to the latest offset fail: throw exception to the consumer.

Enum values:

-   latest
    
-   earliest
    
-   none
    





 | latest | String |
| **breakOnFirstError** (consumer) | This options controls what happens when a consumer is processing an exchange and it fails. If the option is false then the consumer continues to the next message and processes it. If the option is true then the consumer breaks out. Using the default NoopCommitManager will cause the consumer to not commit the offset so that the message is re-attempted. The consumer should use the KafkaManualCommit to determine the best way to handle the message. Using either the SynchCommitManager or the AsynchCommitManager the consumer will seek back to the offset of the message that caused a failure, and then re-attempt to process this message. However this can lead to endless processing of the same message if its bound to fail every time, eg a poison message. Therefore its recommended to deal with that for example by using Camel’s error handler. | false | boolean |
| **checkCrcs** (consumer) | Automatically check the CRC32 of the records consumed. This ensures no on-the-wire or on-disk corruption to the messages occurred. This check adds some overhead, so it may be disabled in cases seeking extreme performance. | true | Boolean |
| **commitTimeoutMs** (consumer) | The maximum time, in milliseconds, that the code will wait for a synchronous commit to complete. | 5000 | Long |
| **consumerRequestTimeoutMs** (consumer) | The configuration controls the maximum amount of time the client will wait for the response of a request. If the response is not received before the timeout elapses the client will resend the request if necessary or fail the request if retries are exhausted. | 30000 | Integer |
| **consumersCount** (consumer) | The number of consumers that connect to kafka server. Each consumer is run on a separate thread, that retrieves and process the incoming data. | 1 | int |
| **fetchMaxBytes** (consumer) | The maximum amount of data the server should return for a fetch request This is not an absolute maximum, if the first message in the first non-empty partition of the fetch is larger than this value, the message will still be returned to ensure that the consumer can make progress. The maximum message size accepted by the broker is defined via message.max.bytes (broker config) or max.message.bytes (topic config). Note that the consumer performs multiple fetches in parallel. | 52428800 | Integer |
| **fetchMinBytes** (consumer) | The minimum amount of data the server should return for a fetch request. If insufficient data is available the request will wait for that much data to accumulate before answering the request. | 1 | Integer |
| **fetchWaitMaxMs** (consumer) | The maximum amount of time the server will block before answering the fetch request if there isn’t sufficient data to immediately satisfy fetch.min.bytes. | 500 | Integer |
| **groupId** (consumer) | A string that uniquely identifies the group of consumer processes to which this consumer belongs. By setting the same group id multiple processes indicate that they are all part of the same consumer group. This option is required for consumers. |  | String |
| **groupInstanceId** (consumer) | A unique identifier of the consumer instance provided by the end user. Only non-empty strings are permitted. If set, the consumer is treated as a static member, which means that only one instance with this ID is allowed in the consumer group at any time. This can be used in combination with a larger session timeout to avoid group rebalances caused by transient unavailability (e.g. process restarts). If not set, the consumer will join the group as a dynamic member, which is the traditional behavior. |  | String |
| **headerDeserializer** (consumer) | To use a custom KafkaHeaderDeserializer to deserialize kafka headers values. |  | KafkaHeaderDeserializer |
| **heartbeatIntervalMs** (consumer) | The expected time between heartbeats to the consumer coordinator when using Kafka’s group management facilities. Heartbeats are used to ensure that the consumer’s session stays active and to facilitate rebalancing when new consumers join or leave the group. The value must be set lower than session.timeout.ms, but typically should be set no higher than 1/3 of that value. It can be adjusted even lower to control the expected time for normal rebalances. | 3000 | Integer |
| **keyDeserializer** (consumer) | Deserializer class for key that implements the Deserializer interface. | org.apache.kafka.common.serialization.StringDeserializer | String |
| **maxPartitionFetchBytes** (consumer) | The maximum amount of data per-partition the server will return. The maximum total memory used for a request will be #partitions max.partition.fetch.bytes. This size must be at least as large as the maximum message size the server allows or else it is possible for the producer to send messages larger than the consumer can fetch. If that happens, the consumer can get stuck trying to fetch a large message on a certain partition. | 1048576 | Integer |
| **maxPollIntervalMs** (consumer) | The maximum delay between invocations of poll() when using consumer group management. This places an upper bound on the amount of time that the consumer can be idle before fetching more records. If poll() is not called before expiration of this timeout, then the consumer is considered failed and the group will rebalance in order to reassign the partitions to another member. |  | Integer |
| **maxPollRecords** (consumer) | The maximum number of records returned in a single call to poll(). | 500 | Integer |
| **offsetRepository** (consumer) | The offset repository to use in order to locally store the offset of each partition of the topic. Defining one will disable the autocommit. |  | StateRepository |
| **partitionAssignor** (consumer) | The class name of the partition assignment strategy that the client will use to distribute partition ownership amongst consumer instances when group management is used. | org.apache.kafka.clients.consumer.RangeAssignor | String |
| **pollOnError** (consumer) | 

What to do if kafka threw an exception while polling for new messages. Will by default use the value from the component configuration unless an explicit value has been configured on the endpoint level. DISCARD will discard the message and continue to poll next message. ERROR\_HANDLER will use Camel’s error handler to process the exception, and afterwards continue to poll next message. RECONNECT will re-connect the consumer and try poll the message again RETRY will let the consumer retry polling the same message again STOP will stop the consumer (have to be manually started/restarted if the consumer should be able to consume messages again).

Enum values:

-   DISCARD
    
-   ERROR\_HANDLER
    
-   RECONNECT
    
-   RETRY
    
-   STOP
    





 | ERROR\_HANDLER | PollOnError |
| **pollTimeoutMs** (consumer) | The timeout used when polling the KafkaConsumer. | 5000 | Long |
| **seekTo** (consumer) | 

Set if KafkaConsumer will read from beginning or end on startup: SeekPolicy.BEGINNING: read from beginning. SeekPolicy.END: read from end.

Enum values:

-   BEGINNING
    
-   END
    





 |  | SeekPolicy |
| **sessionTimeoutMs** (consumer) | The timeout used to detect failures when using Kafka’s group management facilities. | 45000 | Integer |
| **specificAvroReader** (consumer) | This enables the use of a specific Avro reader for use with the Confluent Platform schema registry and the io.confluent.kafka.serializers.KafkaAvroDeserializer. This option is only available in the Confluent Platform (not standard Apache Kafka). | false | boolean |
| **topicIsPattern** (consumer) | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | false | boolean |
| **valueDeserializer** (consumer) | Deserializer class for value that implements the Deserializer interface. | org.apache.kafka.common.serialization.StringDeserializer | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **isolationLevel** (consumer (advanced)) | 

Controls how to read messages written transactionally. If set to read\_committed, consumer.poll() will only return transactional messages which have been committed. If set to read\_uncommitted (the default), consumer.poll() will return all messages, even transactional messages which have been aborted. Non-transactional messages will be returned unconditionally in either mode. Messages will always be returned in offset order. Hence, in read\_committed mode, consumer.poll() will only return messages up to the last stable offset (LSO), which is the one less than the offset of the first open transaction. In particular any messages appearing after messages belonging to ongoing transactions will be withheld until the relevant transaction has been completed. As a result, read\_committed consumers will not be able to read up to the high watermark when there are in flight transactions. Further, when in read\_committed the seekToEnd method will return the LSO.

Enum values:

-   read\_uncommitted
    
-   read\_committed
    





 | read\_uncommitted | String |
| **kafkaManualCommitFactory** (consumer (advanced)) | Factory to use for creating KafkaManualCommit instances. This allows to plugin a custom factory to create custom KafkaManualCommit instances in case special logic is needed when doing manual commits that deviates from the default implementation that comes out of the box. |  | KafkaManualCommitFactory |
| **batchWithIndividualHeaders** (producer) | If this feature is enabled and a single element of a batch is an Exchange or Message, the producer will generate individual kafka header values for it by using the batch Message to determine the values. Normal behaviour consists in always using the same header values (which are determined by the parent Exchange which contains the Iterable or Iterator). | false | boolean |
| **bufferMemorySize** (producer) | The total bytes of memory the producer can use to buffer records waiting to be sent to the server. If records are sent faster than they can be delivered to the server the producer will either block or throw an exception based on the preference specified by block.on.buffer.full.This setting should correspond roughly to the total memory the producer will use, but is not a hard bound since not all memory the producer uses is used for buffering. Some additional memory will be used for compression (if compression is enabled) as well as for maintaining in-flight requests. | 33554432 | Integer |
| **compressionCodec** (producer) | 

This parameter allows you to specify the compression codec for all data generated by this producer. Valid values are none, gzip, snappy, lz4 and zstd.

Enum values:

-   none
    
-   gzip
    
-   snappy
    
-   lz4
    
-   zstd
    





 | none | String |
| **connectionMaxIdleMs** (producer) | Close idle connections after the number of milliseconds specified by this config. | 540000 | Integer |
| **deliveryTimeoutMs** (producer) | An upper bound on the time to report success or failure after a call to send() returns. This limits the total time that a record will be delayed prior to sending, the time to await acknowledgement from the broker (if expected), and the time allowed for retriable send failures. | 120000 | Integer |
| **enableIdempotence** (producer) | When set to 'true', the producer will ensure that exactly one copy of each message is written in the stream. If 'false', producer retries due to broker failures, etc., may write duplicates of the retried message in the stream. Note that enabling idempotence requires max.in.flight.requests.per.connection to be less than or equal to 5 (with message ordering preserved for any allowable value), retries to be greater than 0, and acks must be 'all'. Idempotence is enabled by default if no conflicting configurations are set. If conflicting configurations are set and idempotence is not explicitly enabled, idempotence is disabled. If idempotence is explicitly enabled and conflicting configurations are set, a ConfigException is thrown. | true | boolean |
| **headerSerializer** (producer) | To use a custom KafkaHeaderSerializer to serialize kafka headers values. |  | KafkaHeaderSerializer |
| **key** (producer) | The record key (or null if no key is specified). If this option has been configured then it take precedence over header KafkaConstants#KEY. |  | String |
| **keySerializer** (producer) | The serializer class for keys (defaults to the same as for messages if nothing is given). | org.apache.kafka.common.serialization.StringSerializer | String |
| **lingerMs** (producer) | The producer groups together any records that arrive in between request transmissions into a single batched request. Normally this occurs only under load when records arrive faster than they can be sent out. However in some circumstances the client may want to reduce the number of requests even under moderate load. This setting accomplishes this by adding a small amount of artificial delay that is, rather than immediately sending out a record the producer will wait for up to the given delay to allow other records to be sent so that the sends can be batched together. This can be thought of as analogous to Nagle’s algorithm in TCP. This setting gives the upper bound on the delay for batching: once we get batch.size worth of records for a partition it will be sent immediately regardless of this setting, however if we have fewer than this many bytes accumulated for this partition we will 'linger' for the specified time waiting for more records to show up. This setting defaults to 0 (i.e. no delay). Setting linger.ms=5, for example, would have the effect of reducing the number of requests sent but would add up to 5ms of latency to records sent in the absence of load. | 0 | Integer |
| **maxBlockMs** (producer) | The configuration controls how long the KafkaProducer’s send(), partitionsFor(), initTransactions(), sendOffsetsToTransaction(), commitTransaction() and abortTransaction() methods will block. For send() this timeout bounds the total time waiting for both metadata fetch and buffer allocation (blocking in the user-supplied serializers or partitioner is not counted against this timeout). For partitionsFor() this timeout bounds the time spent waiting for metadata if it is unavailable. The transaction-related methods always block, but may timeout if the transaction coordinator could not be discovered or did not respond within the timeout. | 60000 | Integer |
| **maxInFlightRequest** (producer) | The maximum number of unacknowledged requests the client will send on a single connection before blocking. Note that if this setting is set to be greater than 1 and there are failed sends, there is a risk of message re-ordering due to retries (i.e., if retries are enabled). | 5 | Integer |
| **maxRequestSize** (producer) | The maximum size of a request. This is also effectively a cap on the maximum record size. Note that the server has its own cap on record size which may be different from this. This setting will limit the number of record batches the producer will send in a single request to avoid sending huge requests. | 1048576 | Integer |
| **metadataMaxAgeMs** (producer) | The period of time in milliseconds after which we force a refresh of metadata even if we haven’t seen any partition leadership changes to proactively discover any new brokers or partitions. | 300000 | Integer |
| **metricReporters** (producer) | A list of classes to use as metrics reporters. Implementing the MetricReporter interface allows plugging in classes that will be notified of new metric creation. The JmxReporter is always included to register JMX statistics. |  | String |
| **metricsSampleWindowMs** (producer) | The window of time a metrics sample is computed over. | 30000 | Integer |
| **noOfMetricsSample** (producer) | The number of samples maintained to compute metrics. | 2 | Integer |
| **partitioner** (producer) | The partitioner class for partitioning messages amongst sub-topics. The default partitioner is based on the hash of the key. | org.apache.kafka.clients.producer.internals.DefaultPartitioner | String |
| **partitionKey** (producer) | The partition to which the record will be sent (or null if no partition was specified). If this option has been configured then it take precedence over header KafkaConstants#PARTITION\_KEY. |  | Integer |
| **producerBatchSize** (producer) | The producer will attempt to batch records together into fewer requests whenever multiple records are being sent to the same partition. This helps performance on both the client and the server. This configuration controls the default batch size in bytes. No attempt will be made to batch records larger than this size.Requests sent to brokers will contain multiple batches, one for each partition with data available to be sent.A small batch size will make batching less common and may reduce throughput (a batch size of zero will disable batching entirely). A very large batch size may use memory a bit more wastefully as we will always allocate a buffer of the specified batch size in anticipation of additional records. | 16384 | Integer |
| **queueBufferingMaxMessages** (producer) | The maximum number of unsent messages that can be queued up the producer when using async mode before either the producer must be blocked or data must be dropped. | 10000 | Integer |
| **receiveBufferBytes** (producer) | The size of the TCP receive buffer (SO\_RCVBUF) to use when reading data. | 65536 | Integer |
| **reconnectBackoffMs** (producer) | The amount of time to wait before attempting to reconnect to a given host. This avoids repeatedly connecting to a host in a tight loop. This backoff applies to all requests sent by the consumer to the broker. | 50 | Integer |
| **recordMetadata** (producer) | Whether the producer should store the RecordMetadata results from sending to Kafka. The results are stored in a List containing the RecordMetadata metadata’s. The list is stored on a header with the key KafkaConstants#KAFKA\_RECORDMETA. | true | boolean |
| **requestRequiredAcks** (producer) | 

The number of acknowledgments the producer requires the leader to have received before considering a request complete. This controls the durability of records that are sent. The following settings are allowed: acks=0 If set to zero then the producer will not wait for any acknowledgment from the server at all. The record will be immediately added to the socket buffer and considered sent. No guarantee can be made that the server has received the record in this case, and the retries configuration will not take effect (as the client won’t generally know of any failures). The offset given back for each record will always be set to -1. acks=1 This will mean the leader will write the record to its local log but will respond without awaiting full acknowledgement from all followers. In this case should the leader fail immediately after acknowledging the record but before the followers have replicated it then the record will be lost. acks=all This means the leader will wait for the full set of in-sync replicas to acknowledge the record. This guarantees that the record will not be lost as long as at least one in-sync replica remains alive. This is the strongest available guarantee. This is equivalent to the acks=-1 setting. Note that enabling idempotence requires this config value to be 'all'. If conflicting configurations are set and idempotence is not explicitly enabled, idempotence is disabled.

Enum values:

-   all
    
-   \-1
    
-   0
    
-   1
    





 | all | String |
| **requestTimeoutMs** (producer) | The amount of time the broker will wait trying to meet the request.required.acks requirement before sending back an error to the client. | 30000 | Integer |
| **retries** (producer) | Setting a value greater than zero will cause the client to resend any record whose send fails with a potentially transient error. Note that this retry is no different than if the client resent the record upon receiving the error. Produce requests will be failed before the number of retries has been exhausted if the timeout configured by delivery.timeout.ms expires first before successful acknowledgement. Users should generally prefer to leave this config unset and instead use delivery.timeout.ms to control retry behavior. Enabling idempotence requires this config value to be greater than 0. If conflicting configurations are set and idempotence is not explicitly enabled, idempotence is disabled. Allowing retries while setting enable.idempotence to false and max.in.flight.requests.per.connection to 1 will potentially change the ordering of records because if two batches are sent to a single partition, and the first fails and is retried but the second succeeds, then the records in the second batch may appear first. |  | Integer |
| **retryBackoffMs** (producer) | Before each retry, the producer refreshes the metadata of relevant topics to see if a new leader has been elected. Since leader election takes a bit of time, this property specifies the amount of time that the producer waits before refreshing the metadata. | 100 | Integer |
| **sendBufferBytes** (producer) | Socket write buffer size. | 131072 | Integer |
| **useIterator** (producer) | Sets whether sending to kafka should send the message body as a single record, or use a java.util.Iterator to send multiple records to kafka (if the message body can be iterated). | true | boolean |
| **valueSerializer** (producer) | The serializer class for messages. | org.apache.kafka.common.serialization.StringSerializer | String |
| **workerPool** (producer) | To use a custom worker pool for continue routing Exchange after kafka server has acknowledge the message that was sent to it from KafkaProducer using asynchronous non-blocking processing. If using this option then you must handle the lifecycle of the thread pool to shut the pool down when no longer needed. |  | ExecutorService |
| **workerPoolCoreSize** (producer) | Number of core threads for the worker pool for continue routing Exchange after kafka server has acknowledge the message that was sent to it from KafkaProducer using asynchronous non-blocking processing. | 10 | Integer |
| **workerPoolMaxSize** (producer) | Maximum number of threads for the worker pool for continue routing Exchange after kafka server has acknowledge the message that was sent to it from KafkaProducer using asynchronous non-blocking processing. | 20 | Integer |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **kafkaClientFactory** (advanced) | Factory to use for creating org.apache.kafka.clients.consumer.KafkaConsumer and org.apache.kafka.clients.producer.KafkaProducer instances. This allows to configure a custom factory to create instances with logic that extends the vanilla Kafka clients. |  | KafkaClientFactory |
| **synchronous** (advanced) | Sets whether synchronous processing should be strictly used. | false | boolean |
| **schemaRegistryURL** (confluent) | URL of the Confluent Platform schema registry servers to use. The format is host1:port1,host2:port2. This is known as schema.registry.url in the Confluent Platform documentation. This option is only available in the Confluent Platform (not standard Apache Kafka). |  | String |
| **interceptorClasses** (monitoring) | Sets interceptors for producer or consumers. Producer interceptors have to be classes implementing org.apache.kafka.clients.producer.ProducerInterceptor Consumer interceptors have to be classes implementing org.apache.kafka.clients.consumer.ConsumerInterceptor Note that if you use Producer interceptor on a consumer it will throw a class cast exception in runtime. |  | String |
| **kerberosBeforeReloginMinTime** (security) | Login thread sleep time between refresh attempts. | 60000 | Integer |
| **kerberosInitCmd** (security) | Kerberos kinit command path. Default is /usr/bin/kinit. | /usr/bin/kinit | String |
| **kerberosPrincipalToLocalRules** (security) | A list of rules for mapping from principal names to short names (typically operating system usernames). The rules are evaluated in order and the first rule that matches a principal name is used to map it to a short name. Any later rules in the list are ignored. By default, principal names of the form {username}/{hostname}{REALM} are mapped to {username}. For more details on the format please see the security authorization and acls documentation (at the Apache Kafka project). Multiple values can be separated by comma. | DEFAULT | String |
| **kerberosRenewJitter** (security) | Percentage of random jitter added to the renewal time. | 0.05 | Double |
| **kerberosRenewWindowFactor** (security) | Login thread will sleep until the specified window factor of time from last refresh to ticket’s expiry has been reached, at which time it will try to renew the ticket. | 0.8 | Double |
| **saslJaasConfig** (security) | Expose the kafka sasl.jaas.config parameter Example: org.apache.kafka.common.security.plain.PlainLoginModule required username=USERNAME password=PASSWORD;. |  | String |
| **saslKerberosServiceName** (security) | The Kerberos principal name that Kafka runs as. This can be defined either in Kafka’s JAAS config or in Kafka’s config. |  | String |
| **saslMechanism** (security) | The Simple Authentication and Security Layer (SASL) Mechanism used. For the valid values see [http://www.iana.org/assignments/sasl-mechanisms/sasl-mechanisms.xhtml](http://www.iana.org/assignments/sasl-mechanisms/sasl-mechanisms.xhtml). | GSSAPI | String |
| **securityProtocol** (security) | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | PLAINTEXT | String |
| **sslCipherSuites** (security) | A list of cipher suites. This is a named combination of authentication, encryption, MAC and key exchange algorithm used to negotiate the security settings for a network connection using TLS or SSL network protocol. By default all the available cipher suites are supported. |  | String |
| **sslContextParameters** (security) | SSL configuration using a Camel SSLContextParameters object. If configured it’s applied before the other SSL endpoint parameters. NOTE: Kafka only supports loading keystore from file locations, so prefix the location with file: in the KeyStoreParameters.resource option. |  | SSLContextParameters |
| **sslEnabledProtocols** (security) | The list of protocols enabled for SSL connections. The default is TLSv1.2,TLSv1.3 when running with Java 11 or newer, TLSv1.2 otherwise. With the default value for Java 11, clients and servers will prefer TLSv1.3 if both support it and fallback to TLSv1.2 otherwise (assuming both support at least TLSv1.2). This default should be fine for most cases. Also see the config documentation for SslProtocol. |  | String |
| **sslEndpointAlgorithm** (security) | The endpoint identification algorithm to validate server hostname using server certificate. Use none or false to disable server hostname verification. | https | String |
| **sslKeymanagerAlgorithm** (security) | The algorithm used by key manager factory for SSL connections. Default value is the key manager factory algorithm configured for the Java Virtual Machine. | SunX509 | String |
| **sslKeyPassword** (security) | The password of the private key in the key store file or the PEM key specified in sslKeystoreKey. This is required for clients only if two-way authentication is configured. |  | String |
| **sslKeystoreLocation** (security) | The location of the key store file. This is optional for client and can be used for two-way authentication for client. |  | String |
| **sslKeystorePassword** (security) | The store password for the key store file. This is optional for client and only needed if sslKeystoreLocation' is configured. Key store password is not supported for PEM format. |  | String |
| **sslKeystoreType** (security) | The file format of the key store file. This is optional for client. Default value is JKS. | JKS | String |
| **sslProtocol** (security) | The SSL protocol used to generate the SSLContext. The default is TLSv1.3 when running with Java 11 or newer, TLSv1.2 otherwise. This value should be fine for most use cases. Allowed values in recent JVMs are TLSv1.2 and TLSv1.3. TLS, TLSv1.1, SSL, SSLv2 and SSLv3 may be supported in older JVMs, but their usage is discouraged due to known security vulnerabilities. With the default value for this config and sslEnabledProtocols, clients will downgrade to TLSv1.2 if the server does not support TLSv1.3. If this config is set to TLSv1.2, clients will not use TLSv1.3 even if it is one of the values in sslEnabledProtocols and the server only supports TLSv1.3. |  | String |
| **sslProvider** (security) | The name of the security provider used for SSL connections. Default value is the default security provider of the JVM. |  | String |
| **sslTrustmanagerAlgorithm** (security) | The algorithm used by trust manager factory for SSL connections. Default value is the trust manager factory algorithm configured for the Java Virtual Machine. | PKIX | String |
| **sslTruststoreLocation** (security) | The location of the trust store file. |  | String |
| **sslTruststorePassword** (security) | The password for the trust store file. If a password is not set, trust store file configured will still be used, but integrity checking is disabled. Trust store password is not supported for PEM format. |  | String |
| **sslTruststoreType** (security) | The file format of the trust store file. Default value is JKS. | JKS | String |

For more information about Producer/Consumer configuration:

[http://kafka.apache.org/documentation.html#newconsumerconfigs](http://kafka.apache.org/documentation.html#newconsumerconfigs) [http://kafka.apache.org/documentation.html#producerconfigs](http://kafka.apache.org/documentation.html#producerconfigs)

## Message Headers

The Kafka component supports 13 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **kafka.PARTITION\_KEY** (producer) Constant: [`PARTITION_KEY`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#PARTITION_KEY) | Explicitly specify the partition. |  | Integer |
| **kafka.PARTITION** (consumer) Constant: [`PARTITION`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#PARTITION) | The partition where the message was stored. |  | Integer |
| **kafka.KEY** (common) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#KEY) | **Required** Producer: The key of the message in order to ensure that all related message goes in the same partition. Consumer: The key of the message if configured. |  | Object |
| **kafka.TOPIC** (consumer) Constant: [`TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#TOPIC) | The topic from where the message originated. |  | String |
| **kafka.OVERRIDE\_TOPIC** (producer) Constant: [`OVERRIDE_TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#OVERRIDE_TOPIC) | The topic to which send the message (override and takes precedence), and the header is not preserved. |  | String |
| **kafka.OFFSET** (consumer) Constant: [`OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#OFFSET) | The offset of the message. |  | Long |
| **kafka.HEADERS** (consumer) Constant: [`HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#HEADERS) | The record headers. |  | Headers |
| **kafka.LAST\_RECORD\_BEFORE\_COMMIT** (consumer) Constant: [`LAST_RECORD_BEFORE_COMMIT`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#LAST_RECORD_BEFORE_COMMIT) | Whether or not it’s the last record before commit (only available if autoCommitEnable endpoint parameter is false). |  | Boolean |
| **kafka.LAST\_POLL\_RECORD** (consumer) Constant: [`LAST_POLL_RECORD`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#LAST_POLL_RECORD) | Indicates the last record within the current poll request (only available if autoCommitEnable endpoint parameter is false or allowManualCommit is true). |  | Boolean |
| **kafka.TIMESTAMP** (consumer) Constant: [`TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#TIMESTAMP) | The timestamp of the message. |  | Long |
| **kafka.OVERRIDE\_TIMESTAMP** (producer) Constant: [`OVERRIDE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#OVERRIDE_TIMESTAMP) | The ProducerRecord also has an associated timestamp. If the user did provide a timestamp, the producer will stamp the record with the provided timestamp and the header is not preserved. |  | Long |
| **org.apache.kafka.clients.producer.RecordMetadata** (producer) Constant: [`KAFKA_RECORDMETA`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#KAFKA_RECORDMETA) | The metadata (only configured if recordMetadata endpoint parameter is true). |  | List |
| **CamelKafkaManualCommit** (consumer) Constant: [`MANUAL_COMMIT`](https://javadoc.io/doc/org.apache.camel/camel-kafka/latest/org/apache/camel/component/kafka/KafkaConstants.html#MANUAL_COMMIT) | Can be used for forcing manual offset commit when using Kafka consumer. |  | KafkaManualCommit |

If you want to send a message to a dynamic topic then use `KafkaConstants.OVERRIDE_TOPIC` as it is used as a one-time header that is not send along the message, as it is removed in the producer.

## Consumer error handling

While kafka consumer is polling messages from the kafka broker, then errors can happen. This section describes what happens and what you can configure.

The consumer may throw exception when invoking the Kafka `poll` API. For example, if the message cannot be de-serialized due invalid data, and many other kind of errors. Those errors are in the form of `KafkaException` which are either _retryable_ or not. The exceptions which can be retried (`RetriableException`) will be retried again (with a poll timeout in between). All other kind of exceptions are handled according to the _pollOnError_ configuration. This configuration has the following values:

-   DISCARD will discard the message and continue to poll next message.
    
-   ERROR\_HANDLER will use Camel’s error handler to process the exception, and afterwards continue to poll next message.
    
-   RECONNECT will re-connect the consumer and try poll the message again.
    
-   RETRY will let the consumer retry polling the same message again
    
-   STOP will stop the consumer (have to be manually started/restarted if the consumer should be able to consume messages again).
    

The default is **ERROR\_HANDLER** which will let Camel’s error handler (if any configured) process the caused exception. Afterwards continue to poll the next message. This behavior is similar to the _bridgeErrorHandler_ option that Camel components have.

For advanced control a custom implementation of `org.apache.camel.component.kafka.PollExceptionStrategy` can be configured on the component level, which allows to control which exceptions causes which of the strategies above.

## Consumer error handling (advanced)

By default Camel will poll using the **ERROR\_HANDLER** to process exceptions. How Camel handles a message that results in an exception can be altered using the `breakOnFirstError` attribute in the configuration. Instead of continuing to poll next message, Camel will instead commit the offset so that the message that caused the exception will be retried. This is similar to the **RETRY** polling strategy above.

```java
KafkaComponent kafka = new KafkaComponent();
kafka.setBreakOnFirstError(true);
...
camelContext.addComponent("kafka", kafka);
```

It is recommended that you read the section below "Using manual commit with Kafka consumer" to understand how `breakOnFirstError` will work based on the `CommitManager` that is configured.

## Samples

### Consuming messages from Kafka

Here is the minimal route you need in order to read messages from Kafka.

```java
from("kafka:test?brokers=localhost:9092")
    .log("Message received from Kafka : ${body}")
    .log("    on the topic ${headers[kafka.TOPIC]}")
    .log("    on the partition ${headers[kafka.PARTITION]}")
    .log("    with the offset ${headers[kafka.OFFSET]}")
    .log("    with the key ${headers[kafka.KEY]}")
```

If you need to consume messages from multiple topics you can use a comma separated list of topic names.

```java
from("kafka:test,test1,test2?brokers=localhost:9092")
    .log("Message received from Kafka : ${body}")
    .log("    on the topic ${headers[kafka.TOPIC]}")
    .log("    on the partition ${headers[kafka.PARTITION]}")
    .log("    with the offset ${headers[kafka.OFFSET]}")
    .log("    with the key ${headers[kafka.KEY]}")
```

It’s also possible to subscribe to multiple topics giving a pattern as the topic name and using the `topicIsPattern` option.

```java
from("kafka:test*?brokers=localhost:9092&topicIsPattern=true")
    .log("Message received from Kafka : ${body}")
    .log("    on the topic ${headers[kafka.TOPIC]}")
    .log("    on the partition ${headers[kafka.PARTITION]}")
    .log("    with the offset ${headers[kafka.OFFSET]}")
    .log("    with the key ${headers[kafka.KEY]}")
```

When consuming messages from Kafka you can use your own offset management and not delegate this management to Kafka. In order to keep the offsets the component needs a `StateRepository` implementation such as `FileStateRepository`. This bean should be available in the registry. Here how to use it :

```java
// Create the repository in which the Kafka offsets will be persisted
FileStateRepository repository = FileStateRepository.fileStateRepository(new File("/path/to/repo.dat"));

// Bind this repository into the Camel registry
Registry registry = createCamelRegistry();
registry.bind("offsetRepo", repository);

// Configure the camel context
DefaultCamelContext camelContext = new DefaultCamelContext(registry);
camelContext.addRoutes(new RouteBuilder() {
    @Override
    public void configure() throws Exception {
        from("kafka:" + TOPIC + "?brokers=localhost:{{kafkaPort}}" +
                     // Setup the topic and broker address
                     "&groupId=A" +
                     // The consumer processor group ID
                     "&autoOffsetReset=earliest" +
                     // Ask to start from the beginning if we have unknown offset
                     "&offsetRepository=#offsetRepo")
                     // Keep the offsets in the previously configured repository
                .to("mock:result");
    }
});
```

### Producing messages to Kafka

Here is the minimal route you need in order to write messages to Kafka.

```java
from("direct:start")
    .setBody(constant("Message from Camel"))          // Message to send
    .setHeader(KafkaConstants.KEY, constant("Camel")) // Key of the message
    .to("kafka:test?brokers=localhost:9092");
```

## SSL configuration

You have 2 different ways to configure the SSL communication on the Kafka component.

The first way is through the many SSL endpoint parameters:

```java
from("kafka:" + TOPIC + "?brokers=localhost:{{kafkaPort}}" +
             "&groupId=A" +
             "&sslKeystoreLocation=/path/to/keystore.jks" +
             "&sslKeystorePassword=changeit" +
             "&sslKeyPassword=changeit" +
             "&securityProtocol=SSL")
        .to("mock:result");
```

The second way is to use the `sslContextParameters` endpoint parameter:

```java
// Configure the SSLContextParameters object
KeyStoreParameters ksp = new KeyStoreParameters();
ksp.setResource("/path/to/keystore.jks");
ksp.setPassword("changeit");
KeyManagersParameters kmp = new KeyManagersParameters();
kmp.setKeyStore(ksp);
kmp.setKeyPassword("changeit");
SSLContextParameters scp = new SSLContextParameters();
scp.setKeyManagers(kmp);

// Bind this SSLContextParameters into the Camel registry
Registry registry = createCamelRegistry();
registry.bind("ssl", scp);

// Configure the camel context
DefaultCamelContext camelContext = new DefaultCamelContext(registry);
camelContext.addRoutes(new RouteBuilder() {
    @Override
    public void configure() throws Exception {
        from("kafka:" + TOPIC + "?brokers=localhost:{{kafkaPort}}" +
                     // Setup the topic and broker address
                     "&groupId=A" +
                     // The consumer processor group ID
                     "&sslContextParameters=#ssl" +
                     // The security protocol
                     "&securityProtocol=SSL)
                     // Reference the SSL configuration
                .to("mock:result");
    }
});
```

## Using the Kafka idempotent repository

The `camel-kafka` library provides a Kafka topic-based idempotent repository. This repository stores broadcasts all changes to idempotent state (add/remove) in a Kafka topic, and populates a local in-memory cache for each repository’s process instance through event sourcing. The topic used must be unique per idempotent repository instance. The mechanism does not have any requirements about the number of topic partitions; as the repository consumes from all partitions at the same time. It also does not have any requirements about the replication factor of the topic. Each repository instance that uses the topic (e.g. typically on different machines running in parallel) controls its own consumer group, so in a cluster of 10 Camel processes using the same topic each will control its own offset. On startup, the instance subscribes to the topic, rewinds the offset to the beginning and rebuilds the cache to the latest state. The cache will not be considered warmed up until one poll of `pollDurationMs` in length returns 0 records. Startup will not be completed until either the cache has warmed up, or 30 seconds go by; if the latter happens the idempotent repository may be in an inconsistent state until its consumer catches up to the end of the topic. Be mindful of the format of the header used for the uniqueness check. By default, it uses Strings as the data types. When using primitive numeric formats, the header must be deserialized accordingly. Check the samples below for examples.

A `KafkaIdempotentRepository` has the following properties:

 
| Property | Description |
| --- | --- |
| `topic` | The name of the Kafka topic to use to broadcast changes. (required) |
| `bootstrapServers` | The `bootstrap.servers` property on the internal Kafka producer and consumer. Use this as shorthand if not setting `consumerConfig` and `producerConfig`. If used, this component will apply sensible default configurations for the producer and consumer. |
| `producerConfig` | Sets the properties that will be used by the Kafka producer that broadcasts changes. Overrides `bootstrapServers`, so must define the Kafka `bootstrap.servers` property itself |
| `consumerConfig` | Sets the properties that will be used by the Kafka consumer that populates the cache from the topic. Overrides `bootstrapServers`, so must define the Kafka `bootstrap.servers` property itself |
| `maxCacheSize` | How many of the most recently used keys should be stored in memory (default 1000). |
| `pollDurationMs` | The poll duration of the Kafka consumer. The local caches are updated immediately. This value will affect how far behind other peers that update their caches from the topic are relative to the idempotent consumer instance that sent the cache action message. The default value of this is 100 ms.  
If setting this value explicitly, be aware that there is a tradeoff between the remote cache liveness and the volume of network traffic between this repository’s consumer and the Kafka brokers. The cache warmup process also depends on there being one poll that fetches nothing - this indicates that the stream has been consumed up to the current point. If the poll duration is excessively long for the rate at which messages are sent on the topic, there exists a possibility that the cache cannot be warmed up and will operate in an inconsistent state relative to its peers until it catches up. |
| `groupId` | The groupId to assign to the idempotent consumer. If not specified it will be randomize. |

The repository can be instantiated by defining the `topic` and `bootstrapServers`, or the `producerConfig` and `consumerConfig` property sets can be explicitly defined to enable features such as SSL/SASL. To use, this repository must be placed in the Camel registry, either manually or by registration as a bean in Spring/Blueprint, as it is `CamelContext` aware.

Sample usage is as follows:

```java
KafkaIdempotentRepository kafkaIdempotentRepository = new KafkaIdempotentRepository("idempotent-db-inserts", "localhost:9091");

SimpleRegistry registry = new SimpleRegistry();
registry.put("insertDbIdemRepo", kafkaIdempotentRepository); // must be registered in the registry, to enable access to the CamelContext
CamelContext context = new CamelContext(registry);

// later in RouteBuilder...
from("direct:performInsert")
    .idempotentConsumer(header("id")).idempotentRepository("insertDbIdemRepo")
        // once-only insert into database
    .end()
```

In XML:

```xml
<!-- simple -->
<bean id="insertDbIdemRepo"
  class="org.apache.camel.processor.idempotent.kafka.KafkaIdempotentRepository">
  <property name="topic" value="idempotent-db-inserts"/>
  <property name="bootstrapServers" value="localhost:9091"/>
</bean>

<!-- complex -->
<bean id="insertDbIdemRepo"
  class="org.apache.camel.processor.idempotent.kafka.KafkaIdempotentRepository">
  <property name="topic" value="idempotent-db-inserts"/>
  <property name="maxCacheSize" value="10000"/>
  <property name="consumerConfig">
    <props>
      <prop key="bootstrap.servers">localhost:9091</prop>
    </props>
  </property>
  <property name="producerConfig">
    <props>
      <prop key="bootstrap.servers">localhost:9091</prop>
    </props>
  </property>
</bean>
```

There are 3 alternatives to choose from when using idempotency with numeric identifiers. The first one is to use the static method `numericHeader` method from `org.apache.camel.component.kafka.serde.KafkaSerdeHelper` to perform the conversion for you:

```java
from("direct:performInsert")
    .idempotentConsumer(numericHeader("id")).idempotentRepository("insertDbIdemRepo")
        // once-only insert into database
    .end()
```

Alternatively, it is possible to use a custom serializer configured via the route URL to perform the conversion:

```java
public class CustomHeaderDeserializer extends DefaultKafkaHeaderDeserializer {
    private static final Logger LOG = LoggerFactory.getLogger(CustomHeaderDeserializer.class);

    @Override
    public Object deserialize(String key, byte[] value) {
        if (key.equals("id")) {
            BigInteger bi = new BigInteger(value);

            return String.valueOf(bi.longValue());
        } else {
            return super.deserialize(key, value);
        }
    }
}
```

Lastly, it is also possible to do so in a processor:

```java
from(from).routeId("foo")
    .process(exchange -> {
        byte[] id = exchange.getIn().getHeader("id", byte[].class);

        BigInteger bi = new BigInteger(id);
        exchange.getIn().setHeader("id", String.valueOf(bi.longValue()));
    })
    .idempotentConsumer(header("id"))
    .idempotentRepository("kafkaIdempotentRepository")
    .to(to);
```

## Using manual commit with Kafka consumer

By default, the Kafka consumer will use auto commit, where the offset will be committed automatically in the background using a given interval.

In case you want to force manual commits, you can use `KafkaManualCommit` API from the Camel Exchange, stored on the message header. This requires to turn on manual commits by either setting the option `allowManualCommit` to `true` on the `KafkaComponent` or on the endpoint, for example:

```java
KafkaComponent kafka = new KafkaComponent();
kafka.setAutoCommitEnable(false);
kafka.setAllowManualCommit(true);
...
camelContext.addComponent("kafka", kafka);
```

By default this will use the `NoopCommitManager` behind the scenes. In order to commit an offset you will required you to use the `KafkaManualCommit` from Java code such as a Camel `Processor`:

```java
public void process(Exchange exchange) {
    KafkaManualCommit manual =
        exchange.getIn().getHeader(KafkaConstants.MANUAL_COMMIT, KafkaManualCommit.class);
    manual.commit();
}
```

The `KafkaManualCommit` will force a synchronous commit which will block until the commit is acknowledged on Kafka, or if it fails an exception is thrown. You can use an asynchronous commit as well by configuring the `KafkaManualCommitFactory` with the `DefaultKafkaManualAsyncCommitFactory` implementation.

Then the commit will be done in the next consumer loop using the kafka asynchronous commit api.

If you want to use a custom implementation of `KafkaManualCommit` then you can configure a custom `KafkaManualCommitFactory` on the `KafkaComponent` that creates instances of your custom implementation.

When configuring a consumer to use manual commit and a specific `CommitManager` it is important to understand how these influence the behavior of `breakOnFirstError`

```java
KafkaComponent kafka = new KafkaComponent();
kafka.setAutoCommitEnable(false);
kafka.setAllowManualCommit(true);
kafka.setBreakOnFirstError(true);
kafka.setKafkaManualCommitFactory(new DefaultKafkaManualCommitFactory());
...
camelContext.addComponent("kafka", kafka);
```

When the `CommitManager` is left to the default `NoopCommitManager` then `breakOnFirstError` will not automatically commit the offset so that the message with an error is retried. The consumer must manage that in the route using `KafkaManualCommit`.

When the `CommitManager` is changed to either the synch or asynch manager then `breakOnFirstError` will automatically commit the offset so that the message with an error is retried. This message will be continually retried until it can be processed without an error.

**Note 1**: records from a partition must be processed and committed by the same thread as the consumer. This means that certain EIPs, async or concurrent operations in the DSL, may cause the commit to fail. In such circumstances, tyring to commit the transaction will cause the Kafka client to throw a `java.util.ConcurrentModificationException` exception with the message `KafkaConsumer is not safe for multi-threaded access`. To prevent this from happening, redesign your route to avoid those operations.

\*Note 2: this is mostly useful with aggregation’s completion timeout strategies.

## Pausable Consumers

The Kafka component supports pausable consumers. This type of consumer can pause consuming data based on conditions external to the component itself (such as an external system being unavailable).

```java
from("kafka:topic")
    .pausable(new KafkaConsumerListener(), () -> canContinue())
    .routeId("pausable-route")
    .process(exchange -> LOG.info("Got record from Kafka: {}", exchange.getMessage().getBody()))
    .to("some:destination");
```

In this example, consuming messages can pause (by calling the Kafka’s Consumer pause method) if the result from `canContinue` is false.

## Kafka Headers propagation

When consuming messages from Kafka, headers will be propagated to camel exchange headers automatically. Producing flow backed by same behaviour - camel headers of particular exchange will be propagated to kafka message headers.

Since kafka headers allows only `byte[]` values, in order camel exchange header to be propagated its value should be serialized to `bytes[]`, otherwise header will be skipped. Following header value types are supported: `String`, `Integer`, `Long`, `Double`, `Boolean`, `byte[]`. Note: all headers propagated **from** kafka **to** camel exchange will contain `byte[]` value by default. In order to override default functionality uri parameters can be set: `headerDeserializer` for `from` route and `headerSerializer` for `to` route. Example:

```java
from("kafka:my_topic?headerDeserializer=#myDeserializer")
...
.to("kafka:my_topic?headerSerializer=#mySerializer")
```

By default, all headers are being filtered by `KafkaHeaderFilterStrategy`. Strategy filters out headers which start with `Camel` or `org.apache.camel` prefixes. Default strategy can be overridden by using `headerFilterStrategy` uri parameter in both `to` and `from` routes:

```java
from("kafka:my_topic?headerFilterStrategy=#myStrategy")
...
.to("kafka:my_topic?headerFilterStrategy=#myStrategy")
```

`myStrategy` object should be subclass of `HeaderFilterStrategy` and must be placed in the Camel registry, either manually or by registration as a bean in Spring/Blueprint, as it is `CamelContext` aware.

## Kafka Transaction

You need to add `transactional.id`, `enable.idempotence` and `retries` in `additional-properties` to enable kafka transaction with the producer.

```java
from("direct:transaction")
.to("kafka:my_topic?additional-properties[transactional.id]=1234&additional-properties[enable.idempotence]=true&additional-properties[retries]=5");
```

At the end of exchange routing, the kafka producer would commit the transaction or abort it if there is an Exception throwing or the exchange is `RollbackOnly`. Since Kafka does not support transactions in multi threads, it will throw `ProducerFencedException` if there is another producer with the same `transaction.id` to make the transactional request.

It would work with JTA `camel-jta` by using `transacted()` and if it involves some resources (SQL or JMS) which supports XA, then they would work in tandem, where they both will either commit or rollback at the end of the exchange routing. In some cases, if the JTA transaction manager fails to commit (during the 2PC processing), but kafka transaction has been committed before and there is no chance to rollback the changes since the kafka transaction does not support JTA/XA spec. There is still a risk with the data consistency.

## Setting Kerberos config file

Since kafka clients do not expose a way to configure the `krb5.conf` file directly through their API, you can, if necessary, do this using the JVM system properties.

Through command line:

```bash
java -jar myroute.jar -Djava.security.krb5.conf=/path/to/krb5.conf
```

Through java code:

```java
public class MyRoute extends RouteBuilder {
    static {
        System.setProperty("java.security.krb5.conf", "/path/to/krb5.conf");
    }

    // your route

}
```

> **Warning**
> Keep in mind that once using system properties that config will be applied to whole JVM so all routes will be affected by this.

## Spring Boot Auto-Configuration

When using kafka with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-kafka-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 110 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.kafka.additional-properties** | Sets additional properties for either kafka consumer or kafka producer in case they can’t be set directly on the camel configurations (e.g: new Kafka properties that are not reflected yet in Camel configurations), the properties have to be prefixed with additionalProperties.. E.g: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. |  | Map |
| **camel.component.kafka.allow-manual-commit** | Whether to allow doing manual commits via KafkaManualCommit. If this option is enabled then an instance of KafkaManualCommit is stored on the Exchange message header, which allows end users to access this API and perform manual offset commits via the Kafka consumer. | false | Boolean |
| **camel.component.kafka.auto-commit-enable** | If true, periodically commit to ZooKeeper the offset of messages already fetched by the consumer. This committed offset will be used when the process fails as the position from which the new consumer will begin. | true | Boolean |
| **camel.component.kafka.auto-commit-interval-ms** | The frequency in ms that the consumer offsets are committed to zookeeper. | 5000 | Integer |
| **camel.component.kafka.auto-offset-reset** | What to do when there is no initial offset in ZooKeeper or if an offset is out of range: earliest : automatically reset the offset to the earliest offset latest : automatically reset the offset to the latest offset fail: throw exception to the consumer. | latest | String |
| **camel.component.kafka.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kafka.batch-with-individual-headers** | If this feature is enabled and a single element of a batch is an Exchange or Message, the producer will generate individual kafka header values for it by using the batch Message to determine the values. Normal behaviour consists in always using the same header values (which are determined by the parent Exchange which contains the Iterable or Iterator). | false | Boolean |
| **camel.component.kafka.break-on-first-error** | This options controls what happens when a consumer is processing an exchange and it fails. If the option is false then the consumer continues to the next message and processes it. If the option is true then the consumer breaks out. Using the default NoopCommitManager will cause the consumer to not commit the offset so that the message is re-attempted. The consumer should use the KafkaManualCommit to determine the best way to handle the message. Using either the SynchCommitManager or the AsynchCommitManager the consumer will seek back to the offset of the message that caused a failure, and then re-attempt to process this message. However this can lead to endless processing of the same message if its bound to fail every time, eg a poison message. Therefore its recommended to deal with that for example by using Camel’s error handler. | false | Boolean |
| **camel.component.kafka.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kafka.brokers** | URL of the Kafka brokers to use. The format is host1:port1,host2:port2, and the list can be a subset of brokers or a VIP pointing to a subset of brokers. This option is known as bootstrap.servers in the Kafka documentation. |  | String |
| **camel.component.kafka.buffer-memory-size** | The total bytes of memory the producer can use to buffer records waiting to be sent to the server. If records are sent faster than they can be delivered to the server the producer will either block or throw an exception based on the preference specified by block.on.buffer.full.This setting should correspond roughly to the total memory the producer will use, but is not a hard bound since not all memory the producer uses is used for buffering. Some additional memory will be used for compression (if compression is enabled) as well as for maintaining in-flight requests. | 33554432 | Integer |
| **camel.component.kafka.check-crcs** | Automatically check the CRC32 of the records consumed. This ensures no on-the-wire or on-disk corruption to the messages occurred. This check adds some overhead, so it may be disabled in cases seeking extreme performance. | true | Boolean |
| **camel.component.kafka.client-id** | The client id is a user-specified string sent in each request to help trace calls. It should logically identify the application making the request. |  | String |
| **camel.component.kafka.commit-timeout-ms** | The maximum time, in milliseconds, that the code will wait for a synchronous commit to complete. The option is a java.lang.Long type. | 5000 | Long |
| **camel.component.kafka.compression-codec** | This parameter allows you to specify the compression codec for all data generated by this producer. Valid values are none, gzip, snappy, lz4 and zstd. | none | String |
| **camel.component.kafka.configuration** | Allows to pre-configure the Kafka component with common options that the endpoints will reuse. The option is a org.apache.camel.component.kafka.KafkaConfiguration type. |  | KafkaConfiguration |
| **camel.component.kafka.connection-max-idle-ms** | Close idle connections after the number of milliseconds specified by this config. | 540000 | Integer |
| **camel.component.kafka.consumer-request-timeout-ms** | The configuration controls the maximum amount of time the client will wait for the response of a request. If the response is not received before the timeout elapses the client will resend the request if necessary or fail the request if retries are exhausted. | 30000 | Integer |
| **camel.component.kafka.consumers-count** | The number of consumers that connect to kafka server. Each consumer is run on a separate thread, that retrieves and process the incoming data. | 1 | Integer |
| **camel.component.kafka.create-consumer-backoff-interval** | The delay in millis seconds to wait before trying again to create the kafka consumer (kafka-client). | 5000 | Long |
| **camel.component.kafka.create-consumer-backoff-max-attempts** | Maximum attempts to create the kafka consumer (kafka-client), before eventually giving up and failing. Error during creating the consumer may be fatal due to invalid configuration and as such recovery is not possible. However, one part of the validation is DNS resolution of the bootstrap broker hostnames. This may be a temporary networking problem, and could potentially be recoverable. While other errors are fatal such as some invalid kafka configurations. Unfortunately kafka-client does not separate this kind of errors. Camel will by default retry forever, and therefore never give up. If you want to give up after many attempts then set this option and Camel will then when giving up terminate the consumer. You can manually restart the consumer by stopping and starting the route, to try again. |  | Integer |
| **camel.component.kafka.delivery-timeout-ms** | An upper bound on the time to report success or failure after a call to send() returns. This limits the total time that a record will be delayed prior to sending, the time to await acknowledgement from the broker (if expected), and the time allowed for retriable send failures. | 120000 | Integer |
| **camel.component.kafka.enable-idempotence** | When set to 'true', the producer will ensure that exactly one copy of each message is written in the stream. If 'false', producer retries due to broker failures, etc., may write duplicates of the retried message in the stream. Note that enabling idempotence requires max.in.flight.requests.per.connection to be less than or equal to 5 (with message ordering preserved for any allowable value), retries to be greater than 0, and acks must be 'all'. Idempotence is enabled by default if no conflicting configurations are set. If conflicting configurations are set and idempotence is not explicitly enabled, idempotence is disabled. If idempotence is explicitly enabled and conflicting configurations are set, a ConfigException is thrown. | true | Boolean |
| **camel.component.kafka.enabled** | Whether to enable auto configuration of the kafka component. This is enabled by default. |  | Boolean |
| **camel.component.kafka.fetch-max-bytes** | The maximum amount of data the server should return for a fetch request This is not an absolute maximum, if the first message in the first non-empty partition of the fetch is larger than this value, the message will still be returned to ensure that the consumer can make progress. The maximum message size accepted by the broker is defined via message.max.bytes (broker config) or max.message.bytes (topic config). Note that the consumer performs multiple fetches in parallel. | 52428800 | Integer |
| **camel.component.kafka.fetch-min-bytes** | The minimum amount of data the server should return for a fetch request. If insufficient data is available the request will wait for that much data to accumulate before answering the request. | 1 | Integer |
| **camel.component.kafka.fetch-wait-max-ms** | The maximum amount of time the server will block before answering the fetch request if there isn’t sufficient data to immediately satisfy fetch.min.bytes. | 500 | Integer |
| **camel.component.kafka.group-id** | A string that uniquely identifies the group of consumer processes to which this consumer belongs. By setting the same group id multiple processes indicate that they are all part of the same consumer group. This option is required for consumers. |  | String |
| **camel.component.kafka.group-instance-id** | A unique identifier of the consumer instance provided by the end user. Only non-empty strings are permitted. If set, the consumer is treated as a static member, which means that only one instance with this ID is allowed in the consumer group at any time. This can be used in combination with a larger session timeout to avoid group rebalances caused by transient unavailability (e.g. process restarts). If not set, the consumer will join the group as a dynamic member, which is the traditional behavior. |  | String |
| **camel.component.kafka.header-deserializer** | To use a custom KafkaHeaderDeserializer to deserialize kafka headers values. The option is a org.apache.camel.component.kafka.serde.KafkaHeaderDeserializer type. |  | KafkaHeaderDeserializer |
| **camel.component.kafka.header-filter-strategy** | To use a custom HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.kafka.header-serializer** | To use a custom KafkaHeaderSerializer to serialize kafka headers values. The option is a org.apache.camel.component.kafka.serde.KafkaHeaderSerializer type. |  | KafkaHeaderSerializer |
| **camel.component.kafka.heartbeat-interval-ms** | The expected time between heartbeats to the consumer coordinator when using Kafka’s group management facilities. Heartbeats are used to ensure that the consumer’s session stays active and to facilitate rebalancing when new consumers join or leave the group. The value must be set lower than session.timeout.ms, but typically should be set no higher than 1/3 of that value. It can be adjusted even lower to control the expected time for normal rebalances. | 3000 | Integer |
| **camel.component.kafka.interceptor-classes** | Sets interceptors for producer or consumers. Producer interceptors have to be classes implementing org.apache.kafka.clients.producer.ProducerInterceptor Consumer interceptors have to be classes implementing org.apache.kafka.clients.consumer.ConsumerInterceptor Note that if you use Producer interceptor on a consumer it will throw a class cast exception in runtime. |  | String |
| **camel.component.kafka.isolation-level** | Controls how to read messages written transactionally. If set to read\_committed, consumer.poll() will only return transactional messages which have been committed. If set to read\_uncommitted (the default), consumer.poll() will return all messages, even transactional messages which have been aborted. Non-transactional messages will be returned unconditionally in either mode. Messages will always be returned in offset order. Hence, in read\_committed mode, consumer.poll() will only return messages up to the last stable offset (LSO), which is the one less than the offset of the first open transaction. In particular any messages appearing after messages belonging to ongoing transactions will be withheld until the relevant transaction has been completed. As a result, read\_committed consumers will not be able to read up to the high watermark when there are in flight transactions. Further, when in read\_committed the seekToEnd method will return the LSO. | read\_uncommitted | String |
| **camel.component.kafka.kafka-client-factory** | Factory to use for creating org.apache.kafka.clients.consumer.KafkaConsumer and org.apache.kafka.clients.producer.KafkaProducer instances. This allows to configure a custom factory to create instances with logic that extends the vanilla Kafka clients. The option is a org.apache.camel.component.kafka.KafkaClientFactory type. |  | KafkaClientFactory |
| **camel.component.kafka.kafka-manual-commit-factory** | Factory to use for creating KafkaManualCommit instances. This allows to plugin a custom factory to create custom KafkaManualCommit instances in case special logic is needed when doing manual commits that deviates from the default implementation that comes out of the box. The option is a org.apache.camel.component.kafka.consumer.KafkaManualCommitFactory type. |  | KafkaManualCommitFactory |
| **camel.component.kafka.kerberos-before-relogin-min-time** | Login thread sleep time between refresh attempts. | 60000 | Integer |
| **camel.component.kafka.kerberos-init-cmd** | Kerberos kinit command path. Default is /usr/bin/kinit. | /usr/bin/kinit | String |
| **camel.component.kafka.kerberos-principal-to-local-rules** | A list of rules for mapping from principal names to short names (typically operating system usernames). The rules are evaluated in order and the first rule that matches a principal name is used to map it to a short name. Any later rules in the list are ignored. By default, principal names of the form {username}/{hostname}{REALM} are mapped to {username}. For more details on the format please see the security authorization and acls documentation (at the Apache Kafka project). Multiple values can be separated by comma. | DEFAULT | String |
| **camel.component.kafka.kerberos-renew-jitter** | Percentage of random jitter added to the renewal time. |  | Double |
| **camel.component.kafka.kerberos-renew-window-factor** | Login thread will sleep until the specified window factor of time from last refresh to ticket’s expiry has been reached, at which time it will try to renew the ticket. |  | Double |
| **camel.component.kafka.key** | The record key (or null if no key is specified). If this option has been configured then it take precedence over header KafkaConstants#KEY. |  | String |
| **camel.component.kafka.key-deserializer** | Deserializer class for key that implements the Deserializer interface. | org.apache.kafka.common.serialization.StringDeserializer | String |
| **camel.component.kafka.key-serializer** | The serializer class for keys (defaults to the same as for messages if nothing is given). | org.apache.kafka.common.serialization.StringSerializer | String |
| **camel.component.kafka.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kafka.linger-ms** | The producer groups together any records that arrive in between request transmissions into a single batched request. Normally this occurs only under load when records arrive faster than they can be sent out. However in some circumstances the client may want to reduce the number of requests even under moderate load. This setting accomplishes this by adding a small amount of artificial delay that is, rather than immediately sending out a record the producer will wait for up to the given delay to allow other records to be sent so that the sends can be batched together. This can be thought of as analogous to Nagle’s algorithm in TCP. This setting gives the upper bound on the delay for batching: once we get batch.size worth of records for a partition it will be sent immediately regardless of this setting, however if we have fewer than this many bytes accumulated for this partition we will 'linger' for the specified time waiting for more records to show up. This setting defaults to 0 (i.e. no delay). Setting linger.ms=5, for example, would have the effect of reducing the number of requests sent but would add up to 5ms of latency to records sent in the absence of load. | 0 | Integer |
| **camel.component.kafka.max-block-ms** | The configuration controls how long the KafkaProducer’s send(), partitionsFor(), initTransactions(), sendOffsetsToTransaction(), commitTransaction() and abortTransaction() methods will block. For send() this timeout bounds the total time waiting for both metadata fetch and buffer allocation (blocking in the user-supplied serializers or partitioner is not counted against this timeout). For partitionsFor() this timeout bounds the time spent waiting for metadata if it is unavailable. The transaction-related methods always block, but may timeout if the transaction coordinator could not be discovered or did not respond within the timeout. | 60000 | Integer |
| **camel.component.kafka.max-in-flight-request** | The maximum number of unacknowledged requests the client will send on a single connection before blocking. Note that if this setting is set to be greater than 1 and there are failed sends, there is a risk of message re-ordering due to retries (i.e., if retries are enabled). | 5 | Integer |
| **camel.component.kafka.max-partition-fetch-bytes** | The maximum amount of data per-partition the server will return. The maximum total memory used for a request will be #partitions max.partition.fetch.bytes. This size must be at least as large as the maximum message size the server allows or else it is possible for the producer to send messages larger than the consumer can fetch. If that happens, the consumer can get stuck trying to fetch a large message on a certain partition. | 1048576 | Integer |
| **camel.component.kafka.max-poll-interval-ms** | The maximum delay between invocations of poll() when using consumer group management. This places an upper bound on the amount of time that the consumer can be idle before fetching more records. If poll() is not called before expiration of this timeout, then the consumer is considered failed and the group will rebalance in order to reassign the partitions to another member. The option is a java.lang.Integer type. |  | Integer |
| **camel.component.kafka.max-poll-records** | The maximum number of records returned in a single call to poll(). | 500 | Integer |
| **camel.component.kafka.max-request-size** | The maximum size of a request. This is also effectively a cap on the maximum record size. Note that the server has its own cap on record size which may be different from this. This setting will limit the number of record batches the producer will send in a single request to avoid sending huge requests. | 1048576 | Integer |
| **camel.component.kafka.metadata-max-age-ms** | The period of time in milliseconds after which we force a refresh of metadata even if we haven’t seen any partition leadership changes to proactively discover any new brokers or partitions. | 300000 | Integer |
| **camel.component.kafka.metric-reporters** | A list of classes to use as metrics reporters. Implementing the MetricReporter interface allows plugging in classes that will be notified of new metric creation. The JmxReporter is always included to register JMX statistics. |  | String |
| **camel.component.kafka.metrics-sample-window-ms** | The window of time a metrics sample is computed over. | 30000 | Integer |
| **camel.component.kafka.no-of-metrics-sample** | The number of samples maintained to compute metrics. | 2 | Integer |
| **camel.component.kafka.offset-repository** | The offset repository to use in order to locally store the offset of each partition of the topic. Defining one will disable the autocommit. The option is a org.apache.camel.spi.StateRepository<java.lang.String, java.lang.String> type. |  | StateRepository |
| **camel.component.kafka.partition-assignor** | The class name of the partition assignment strategy that the client will use to distribute partition ownership amongst consumer instances when group management is used. | org.apache.kafka.clients.consumer.RangeAssignor | String |
| **camel.component.kafka.partition-key** | The partition to which the record will be sent (or null if no partition was specified). If this option has been configured then it take precedence over header KafkaConstants#PARTITION\_KEY. |  | Integer |
| **camel.component.kafka.partitioner** | The partitioner class for partitioning messages amongst sub-topics. The default partitioner is based on the hash of the key. | org.apache.kafka.clients.producer.internals.DefaultPartitioner | String |
| **camel.component.kafka.poll-exception-strategy** | To use a custom strategy with the consumer to control how to handle exceptions thrown from the Kafka broker while pooling messages. The option is a org.apache.camel.component.kafka.PollExceptionStrategy type. |  | PollExceptionStrategy |
| **camel.component.kafka.poll-on-error** | What to do if kafka threw an exception while polling for new messages. Will by default use the value from the component configuration unless an explicit value has been configured on the endpoint level. DISCARD will discard the message and continue to poll next message. ERROR\_HANDLER will use Camel’s error handler to process the exception, and afterwards continue to poll next message. RECONNECT will re-connect the consumer and try poll the message again RETRY will let the consumer retry polling the same message again STOP will stop the consumer (have to be manually started/restarted if the consumer should be able to consume messages again). |  | PollOnError |
| **camel.component.kafka.poll-timeout-ms** | The timeout used when polling the KafkaConsumer. The option is a java.lang.Long type. | 5000 | Long |
| **camel.component.kafka.producer-batch-size** | The producer will attempt to batch records together into fewer requests whenever multiple records are being sent to the same partition. This helps performance on both the client and the server. This configuration controls the default batch size in bytes. No attempt will be made to batch records larger than this size.Requests sent to brokers will contain multiple batches, one for each partition with data available to be sent.A small batch size will make batching less common and may reduce throughput (a batch size of zero will disable batching entirely). A very large batch size may use memory a bit more wastefully as we will always allocate a buffer of the specified batch size in anticipation of additional records. | 16384 | Integer |
| **camel.component.kafka.queue-buffering-max-messages** | The maximum number of unsent messages that can be queued up the producer when using async mode before either the producer must be blocked or data must be dropped. | 10000 | Integer |
| **camel.component.kafka.receive-buffer-bytes** | The size of the TCP receive buffer (SO\_RCVBUF) to use when reading data. | 65536 | Integer |
| **camel.component.kafka.reconnect-backoff-max-ms** | The maximum amount of time in milliseconds to wait when reconnecting to a broker that has repeatedly failed to connect. If provided, the backoff per host will increase exponentially for each consecutive connection failure, up to this maximum. After calculating the backoff increase, 20% random jitter is added to avoid connection storms. | 1000 | Integer |
| **camel.component.kafka.reconnect-backoff-ms** | The amount of time to wait before attempting to reconnect to a given host. This avoids repeatedly connecting to a host in a tight loop. This backoff applies to all requests sent by the consumer to the broker. | 50 | Integer |
| **camel.component.kafka.record-metadata** | Whether the producer should store the RecordMetadata results from sending to Kafka. The results are stored in a List containing the RecordMetadata metadata’s. The list is stored on a header with the key KafkaConstants#KAFKA\_RECORDMETA. | true | Boolean |
| **camel.component.kafka.request-required-acks** | The number of acknowledgments the producer requires the leader to have received before considering a request complete. This controls the durability of records that are sent. The following settings are allowed: acks=0 If set to zero then the producer will not wait for any acknowledgment from the server at all. The record will be immediately added to the socket buffer and considered sent. No guarantee can be made that the server has received the record in this case, and the retries configuration will not take effect (as the client won’t generally know of any failures). The offset given back for each record will always be set to -1. acks=1 This will mean the leader will write the record to its local log but will respond without awaiting full acknowledgement from all followers. In this case should the leader fail immediately after acknowledging the record but before the followers have replicated it then the record will be lost. acks=all This means the leader will wait for the full set of in-sync replicas to acknowledge the record. This guarantees that the record will not be lost as long as at least one in-sync replica remains alive. This is the strongest available guarantee. This is equivalent to the acks=-1 setting. Note that enabling idempotence requires this config value to be 'all'. If conflicting configurations are set and idempotence is not explicitly enabled, idempotence is disabled. | all | String |
| **camel.component.kafka.request-timeout-ms** | The amount of time the broker will wait trying to meet the request.required.acks requirement before sending back an error to the client. | 30000 | Integer |
| **camel.component.kafka.retries** | Setting a value greater than zero will cause the client to resend any record whose send fails with a potentially transient error. Note that this retry is no different than if the client resent the record upon receiving the error. Produce requests will be failed before the number of retries has been exhausted if the timeout configured by delivery.timeout.ms expires first before successful acknowledgement. Users should generally prefer to leave this config unset and instead use delivery.timeout.ms to control retry behavior. Enabling idempotence requires this config value to be greater than 0. If conflicting configurations are set and idempotence is not explicitly enabled, idempotence is disabled. Allowing retries while setting enable.idempotence to false and max.in.flight.requests.per.connection to 1 will potentially change the ordering of records because if two batches are sent to a single partition, and the first fails and is retried but the second succeeds, then the records in the second batch may appear first. |  | Integer |
| **camel.component.kafka.retry-backoff-ms** | Before each retry, the producer refreshes the metadata of relevant topics to see if a new leader has been elected. Since leader election takes a bit of time, this property specifies the amount of time that the producer waits before refreshing the metadata. | 100 | Integer |
| **camel.component.kafka.sasl-jaas-config** | Expose the kafka sasl.jaas.config parameter Example: org.apache.kafka.common.security.plain.PlainLoginModule required username=USERNAME password=PASSWORD;. |  | String |
| **camel.component.kafka.sasl-kerberos-service-name** | The Kerberos principal name that Kafka runs as. This can be defined either in Kafka’s JAAS config or in Kafka’s config. |  | String |
| **camel.component.kafka.sasl-mechanism** | The Simple Authentication and Security Layer (SASL) Mechanism used. For the valid values see [http://www.iana.org/assignments/sasl-mechanisms/sasl-mechanisms.xhtml](http://www.iana.org/assignments/sasl-mechanisms/sasl-mechanisms.xhtml). | GSSAPI | String |
| **camel.component.kafka.schema-registry-u-r-l** | URL of the Confluent Platform schema registry servers to use. The format is host1:port1,host2:port2. This is known as schema.registry.url in the Confluent Platform documentation. This option is only available in the Confluent Platform (not standard Apache Kafka). |  | String |
| **camel.component.kafka.security-protocol** | Protocol used to communicate with brokers. SASL\_PLAINTEXT, PLAINTEXT, SASL\_SSL and SSL are supported. | PLAINTEXT | String |
| **camel.component.kafka.seek-to** | Set if KafkaConsumer will read from beginning or end on startup: SeekPolicy.BEGINNING: read from beginning. SeekPolicy.END: read from end. |  | SeekPolicy |
| **camel.component.kafka.send-buffer-bytes** | Socket write buffer size. | 131072 | Integer |
| **camel.component.kafka.session-timeout-ms** | The timeout used to detect failures when using Kafka’s group management facilities. | 45000 | Integer |
| **camel.component.kafka.shutdown-timeout** | Timeout in milliseconds to wait gracefully for the consumer or producer to shutdown and terminate its worker threads. | 30000 | Integer |
| **camel.component.kafka.specific-avro-reader** | This enables the use of a specific Avro reader for use with the Confluent Platform schema registry and the io.confluent.kafka.serializers.KafkaAvroDeserializer. This option is only available in the Confluent Platform (not standard Apache Kafka). | false | Boolean |
| **camel.component.kafka.ssl-cipher-suites** | A list of cipher suites. This is a named combination of authentication, encryption, MAC and key exchange algorithm used to negotiate the security settings for a network connection using TLS or SSL network protocol. By default all the available cipher suites are supported. |  | String |
| **camel.component.kafka.ssl-context-parameters** | SSL configuration using a Camel SSLContextParameters object. If configured it’s applied before the other SSL endpoint parameters. NOTE: Kafka only supports loading keystore from file locations, so prefix the location with file: in the KeyStoreParameters.resource option. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.kafka.ssl-enabled-protocols** | The list of protocols enabled for SSL connections. The default is TLSv1.2,TLSv1.3 when running with Java 11 or newer, TLSv1.2 otherwise. With the default value for Java 11, clients and servers will prefer TLSv1.3 if both support it and fallback to TLSv1.2 otherwise (assuming both support at least TLSv1.2). This default should be fine for most cases. Also see the config documentation for SslProtocol. |  | String |
| **camel.component.kafka.ssl-endpoint-algorithm** | The endpoint identification algorithm to validate server hostname using server certificate. Use none or false to disable server hostname verification. | https | String |
| **camel.component.kafka.ssl-key-password** | The password of the private key in the key store file or the PEM key specified in sslKeystoreKey. This is required for clients only if two-way authentication is configured. |  | String |
| **camel.component.kafka.ssl-keymanager-algorithm** | The algorithm used by key manager factory for SSL connections. Default value is the key manager factory algorithm configured for the Java Virtual Machine. | SunX509 | String |
| **camel.component.kafka.ssl-keystore-location** | The location of the key store file. This is optional for client and can be used for two-way authentication for client. |  | String |
| **camel.component.kafka.ssl-keystore-password** | The store password for the key store file. This is optional for client and only needed if sslKeystoreLocation' is configured. Key store password is not supported for PEM format. |  | String |
| **camel.component.kafka.ssl-keystore-type** | The file format of the key store file. This is optional for client. Default value is JKS. | JKS | String |
| **camel.component.kafka.ssl-protocol** | The SSL protocol used to generate the SSLContext. The default is TLSv1.3 when running with Java 11 or newer, TLSv1.2 otherwise. This value should be fine for most use cases. Allowed values in recent JVMs are TLSv1.2 and TLSv1.3. TLS, TLSv1.1, SSL, SSLv2 and SSLv3 may be supported in older JVMs, but their usage is discouraged due to known security vulnerabilities. With the default value for this config and sslEnabledProtocols, clients will downgrade to TLSv1.2 if the server does not support TLSv1.3. If this config is set to TLSv1.2, clients will not use TLSv1.3 even if it is one of the values in sslEnabledProtocols and the server only supports TLSv1.3. |  | String |
| **camel.component.kafka.ssl-provider** | The name of the security provider used for SSL connections. Default value is the default security provider of the JVM. |  | String |
| **camel.component.kafka.ssl-trustmanager-algorithm** | The algorithm used by trust manager factory for SSL connections. Default value is the trust manager factory algorithm configured for the Java Virtual Machine. | PKIX | String |
| **camel.component.kafka.ssl-truststore-location** | The location of the trust store file. |  | String |
| **camel.component.kafka.ssl-truststore-password** | The password for the trust store file. If a password is not set, trust store file configured will still be used, but integrity checking is disabled. Trust store password is not supported for PEM format. |  | String |
| **camel.component.kafka.ssl-truststore-type** | The file format of the trust store file. Default value is JKS. | JKS | String |
| **camel.component.kafka.subscribe-consumer-backoff-interval** | The delay in millis seconds to wait before trying again to subscribe to the kafka broker. | 5000 | Long |
| **camel.component.kafka.subscribe-consumer-backoff-max-attempts** | Maximum number the kafka consumer will attempt to subscribe to the kafka broker, before eventually giving up and failing. Error during subscribing the consumer to the kafka topic could be temporary errors due to network issues, and could potentially be recoverable. Camel will by default retry forever, and therefore never give up. If you want to give up after many attempts then set this option and Camel will then when giving up terminate the consumer. You can manually restart the consumer by stopping and starting the route, to try again. |  | Integer |
| **camel.component.kafka.synchronous** | Sets whether synchronous processing should be strictly used. | false | Boolean |
| **camel.component.kafka.topic-is-pattern** | Whether the topic is a pattern (regular expression). This can be used to subscribe to dynamic number of topics matching the pattern. | false | Boolean |
| **camel.component.kafka.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.kafka.use-iterator** | Sets whether sending to kafka should send the message body as a single record, or use a java.util.Iterator to send multiple records to kafka (if the message body can be iterated). | true | Boolean |
| **camel.component.kafka.value-deserializer** | Deserializer class for value that implements the Deserializer interface. | org.apache.kafka.common.serialization.StringDeserializer | String |
| **camel.component.kafka.value-serializer** | The serializer class for messages. | org.apache.kafka.common.serialization.StringSerializer | String |
| **camel.component.kafka.worker-pool** | To use a custom worker pool for continue routing Exchange after kafka server has acknowledge the message that was sent to it from KafkaProducer using asynchronous non-blocking processing. If using this option then you must handle the lifecycle of the thread pool to shut the pool down when no longer needed. The option is a java.util.concurrent.ExecutorService type. |  | ExecutorService |
| **camel.component.kafka.worker-pool-core-size** | Number of core threads for the worker pool for continue routing Exchange after kafka server has acknowledge the message that was sent to it from KafkaProducer using asynchronous non-blocking processing. | 10 | Integer |
| **camel.component.kafka.worker-pool-max-size** | Maximum number of threads for the worker pool for continue routing Exchange after kafka server has acknowledge the message that was sent to it from KafkaProducer using asynchronous non-blocking processing. | 20 | Integer |