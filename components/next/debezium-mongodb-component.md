# Debezium MongoDB Connector

**Since Camel 3.0**

**Only consumer is supported**

The Debezium MongoDB component is wrapper around [Debezium](https://debezium.io/) using [Debezium Engine](https://debezium.io/documentation/reference/1.9/development/engine.md), which enables Change Data Capture from MongoDB database using Debezium without the need for Kafka or Kafka Connect.

> **Note**
> The Debezium MongoDB connector uses MongoDB’s oplog to capture the changes. The connector works only with the MongoDB replica sets or with sharded clusters, where each shard is a separate replica set. Therefore, you will need to have your MongoDB instance running either in replica set mode or sharded clusters mode.

> **Note**
> **Note on handling failures:** per [Debezium Embedded Engine](https://debezium.io/documentation/reference/1.9/development/engine.html#_handling_failures) documentation, the engines are actively recording source offsets and periodically flush these offsets to a persistent storage. Therefore, when the application is restarted or crashed, the engine will resume from the last recorded offset. This means that, at normal operation, your downstream routes will receive each event exactly once. However, in case of an application crash (not having a graceful shutdown), the application will resume from the last recorded offset, which may result in receiving duplicate events immediately after the restart. Therefore, your downstream routes should be tolerant enough of such a case and deduplicate events if needed.

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-debezium-mongodb</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

debezium-mongodb:name\[?options\]

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

The Debezium MongoDB Connector component supports 88 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalProperties** (common) | Additional properties for debezium components in case they can’t be set directly on the camel configurations (e.g: setting Kafka Connect properties needed by Debezium engine, for example setting KafkaOffsetBackingStore), the properties have to be prefixed with additionalProperties.. E.g: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. This is a multi-value option with prefix: additionalProperties. |  | Map |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **configuration** (consumer) | Allow pre-configured Configurations to be set. |  | MongoDbConnectorEmbeddedDebeziumConfiguration |
| **internalKeyConverter** (consumer) | The Converter class that should be used to serialize and deserialize key data for offsets. The default is JSON converter. | org.apache.kafka.connect.json.JsonConverter | String |
| **internalValueConverter** (consumer) | The Converter class that should be used to serialize and deserialize value data for offsets. The default is JSON converter. | org.apache.kafka.connect.json.JsonConverter | String |
| **offsetCommitPolicy** (consumer) | The name of the Java class of the commit policy. It defines when offsets commit has to be triggered based on the number of events processed and the time elapsed since the last commit. This class must implement the interface 'OffsetCommitPolicy'. The default is a periodic commit policy based upon time intervals. |  | String |
| **offsetCommitTimeoutMs** (consumer) | Maximum number of milliseconds to wait for records to flush and partition offset data to be committed to offset storage before cancelling the process and restoring the offset data to be committed in a future attempt. The default is 5 seconds. | 5000 | long |
| **offsetFlushIntervalMs** (consumer) | Interval at which to try committing offsets. The default is 1 minute. | 60000 | long |
| **offsetStorage** (consumer) | The name of the Java class that is responsible for persistence of connector offsets. | org.apache.kafka.connect.storage.FileOffsetBackingStore | String |
| **offsetStorageFileName** (consumer) | Path to file where offsets are to be stored. Required when offset.storage is set to the FileOffsetBackingStore. |  | String |
| **offsetStoragePartitions** (consumer) | The number of partitions used when creating the offset storage topic. Required when offset.storage is set to the 'KafkaOffsetBackingStore'. |  | int |
| **offsetStorageReplicationFactor** (consumer) | Replication factor used when creating the offset storage topic. Required when offset.storage is set to the KafkaOffsetBackingStore. |  | int |
| **offsetStorageTopic** (consumer) | The name of the Kafka topic where offsets are to be stored. Required when offset.storage is set to the KafkaOffsetBackingStore. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **captureMode** (mongodb) | The method used to capture changes from MongoDB server. Options include: 'change\_streams' to capture changes via MongoDB Change Streams, update events do not contain full documents; 'change\_streams\_update\_full' (the default) to capture changes via MongoDB Change Streams, update events contain full documents. | change\_streams\_update\_full | String |
| **collectionExcludeList** (mongodb) | A comma-separated list of regular expressions or literals that match the collection names for which changes are to be excluded. |  | String |
| **collectionIncludeList** (mongodb) | A comma-separated list of regular expressions or literals that match the collection names for which changes are to be captured. |  | String |
| **connectionValidationTimeoutMs** (mongodb) | The maximum time in milliseconds to wait for connection validation to complete. Defaults to 60 seconds. | 1m | long |
| **converters** (mongodb) | Optional list of custom converters that would be used instead of default ones. The converters are defined using '.type' config option and configured using options '.'. |  | String |
| **cursorMaxAwaitTimeMs** (mongodb) | The maximum processing time in milliseconds to wait for the oplog cursor to process a single poll request. |  | int |
| **customMetricTags** (mongodb) | The custom metric tags will accept key-value pairs to customize the MBean object name which should be appended the end of regular name, each key would represent a tag for the MBean object name, and the corresponding value would be the value of that tag the key is. For example: k1=v1,k2=v2. |  | String |
| **customSanitizePattern** (mongodb) | Regular expression identifying configuration keys whose values should be masked. When set, this custom pattern replaces Debeziums default password masking pattern. | .\*secret$|.\*password$|.\*sasl\\.jaas\\.config$|.\*basic\\.auth\\.user\\.info|.\*registry\\.auth\\.client-secret|.\*credentials\\.json$ | String |
| **databaseExcludeList** (mongodb) | A comma-separated list of regular expressions or literals that match the database names for which changes are to be excluded. |  | String |
| **databaseIncludeList** (mongodb) | A comma-separated list of regular expressions or literals that match the database names for which changes are to be captured. |  | String |
| **errorsMaxRetries** (mongodb) | The maximum number of retries on connection errors before failing (-1 = no limit, 0 = disabled, 0 = num of retries). | \-1 | int |
| **eventProcessingFailureHandlingMode** (mongodb) | Specify how failures during processing of events (i.e. when encountering a corrupted event) should be handled, including: 'fail' (the default) an exception indicating the problematic event and its position is raised, causing the connector to be stopped; 'warn' the problematic event and its position will be logged and the event will be skipped; 'ignore' the problematic event will be skipped. | fail | String |
| **executorShutdownTimeoutMs** (mongodb) | The maximum time in milliseconds to wait for task executor to shut down. | 4s | long |
| **extendedHeadersEnabled** (mongodb) | Enable/Disable Debezium context headers that provides essential metadata for tracking and identifying the source of CDC events in downstream processing systems. | true | boolean |
| **fieldExcludeList** (mongodb) | A comma-separated list of the fully-qualified names of fields that should be excluded from change event message values. |  | String |
| **fieldRenames** (mongodb) | A comma-separated list of the fully-qualified replacements of fields that should be used to rename fields in change event message values. Fully-qualified replacements for fields are of the form databaseName.collectionName.fieldName.nestedFieldName:newNestedFieldName, where databaseName and collectionName may contain the wildcard () which matches any characters, the colon character (:) is used to determine rename mapping of field. |  | String |
| **guardrailCollectionsLimitAction** (mongodb) | Specify the action to take when a guardrail collections limit is exceeded: 'warn' (the default) logs a warning message and continues processing; 'fail' stops the connector with an error. | warn | String |
| **guardrailCollectionsMax** (mongodb) | The maximum number of collections or tables that can be captured by the connector. When this limit is exceeded, the action specified by 'guardrail.collections.limit.action' will be taken. Set to 0 to disable this guardrail. | 0 | int |
| **heartbeatIntervalMs** (mongodb) | Length of an interval in milli-seconds in in which the connector periodically sends heartbeat messages to a heartbeat topic. Use 0 to disable heartbeat messages. Disabled by default. | 0ms | int |
| **heartbeatTopicsPrefix** (mongodb) | The prefix that is used to name heartbeat topics.Defaults to \_\_debezium-heartbeat. | \_\_debezium-heartbeat | String |
| **incrementalSnapshotWatermarkingStrategy** (mongodb) | Specify the strategy used for watermarking during an incremental snapshot: 'insert\_insert' both open and close signal is written into signal data collection (default); 'insert\_delete' only open signal is written on signal data collection, the close will delete the relative open signal;. | INSERT\_INSERT | String |
| **maxBatchSize** (mongodb) | Maximum size of each batch of source records. Defaults to 2048. | 2048 | int |
| **maxQueueSize** (mongodb) | Maximum size of the queue for change events read from the database log but not yet recorded or forwarded. Defaults to 8192, and should always be larger than the maximum batch size. | 8192 | int |
| **maxQueueSizeInBytes** (mongodb) | Maximum size of the queue in bytes for change events read from the database log but not yet recorded or forwarded. Defaults to 0. Mean the feature is not enabled. | 0 | long |
| **mongodbAuthsource** (mongodb) | Database containing user credentials. | admin | String |
| **mongodbConnectionString** (mongodb) | Database connection string. |  | String |
| **mongodbConnectTimeoutMs** (mongodb) | The connection timeout, given in milliseconds. Defaults to 10 seconds (10,000 ms). | 10s | int |
| **mongodbHeartbeatFrequencyMs** (mongodb) | The frequency that the cluster monitor attempts to reach each server. Defaults to 10 seconds (10,000 ms). | 10s | int |
| **mongodbPassword** (mongodb) | **Required** Password to be used when connecting to MongoDB, if necessary. |  | String |
| **mongodbPollIntervalMs** (mongodb) | Interval for looking for new, removed, or changed replica sets, given in milliseconds. Defaults to 30 seconds (30,000 ms). | 30s | long |
| **mongodbServerSelectionTimeoutMs** (mongodb) | The server selection timeout, given in milliseconds. Defaults to 10 seconds (10,000 ms). | 30s | int |
| **mongodbSocketTimeoutMs** (mongodb) | The socket timeout, given in milliseconds. Defaults to 0 ms. | 0ms | int |
| **mongodbSslEnabled** (mongodb) | Should connector use SSL to connect to MongoDB instances. | false | boolean |
| **mongodbSslInvalidHostnameAllowed** (mongodb) | Whether invalid host names are allowed when using SSL. If true the connection will not prevent man-in-the-middle attacks. | false | boolean |
| **mongodbUser** (mongodb) | Database user for connecting to MongoDB, if necessary. |  | String |
| **notificationEnabledChannels** (mongodb) | List of notification channels names that are enabled. |  | String |
| **notificationSinkTopicName** (mongodb) | The name of the topic for the notifications. This is required in case 'sink' is in the list of enabled channels. |  | String |
| **openlineageIntegrationConfigFilePath** (mongodb) | Path to OpenLineage file configuration. See [https://openlineage.io/docs/client/java/configuration](https://openlineage.io/docs/client/java/configuration). | ./openlineage.yml | String |
| **openlineageIntegrationDatasetKafkaBootstrapServers** (mongodb) | The Kafka bootstrap server address used as input/output namespace/. |  | String |
| **openlineageIntegrationEnabled** (mongodb) | Enable Debezium to emit data lineage metadata through OpenLineage API. | false | boolean |
| **openlineageIntegrationJobDescription** (mongodb) | The job’s description emitted by Debezium. | Debezium change data capture job | String |
| **openlineageIntegrationJobNamespace** (mongodb) | The job’s namespace emitted by Debezium. |  | String |
| **openlineageIntegrationJobOwners** (mongodb) | The job’s owners emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **openlineageIntegrationJobTags** (mongodb) | The job’s tags emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **pollIntervalMs** (mongodb) | Time to wait for new change events to appear after receiving no events, given in milliseconds. Defaults to 500 ms. | 500ms | long |
| **postProcessors** (mongodb) | Optional list of post processors. The processors are defined using '.type' config option and configured using options ''. |  | String |
| **provideTransactionMetadata** (mongodb) | Enables transaction metadata extraction together with event counting. | false | boolean |
| **queryFetchSize** (mongodb) | The maximum number of records that should be loaded into memory while streaming. A value of '0' uses the default JDBC fetch size. | 0 | int |
| **retriableRestartConnectorWaitMs** (mongodb) | Time to wait before restarting connector after retriable exception occurs. Defaults to 10000ms. | 10s | long |
| **schemaHistoryInternalFileFilename** (mongodb) | The path to the file that will be used to record the database schema history. |  | String |
| **schemaNameAdjustmentMode** (mongodb) | Specify how schema names should be adjusted for compatibility with the message converter used by the connector, including: 'avro' replaces the characters that cannot be used in the Avro type name with underscore; 'avro\_unicode' replaces the underscore or characters that cannot be used in the Avro type name with corresponding unicode like \_uxxxx. Note: \_ is an escape sequence like backslash in Java;'none' does not apply any adjustment (default). | none | String |
| **signalDataCollection** (mongodb) | The name of the data collection that is used to send signals/commands to Debezium. For multi-partition mode connectors, multiple signal data collections can be specified as a comma-separated list. Signaling is disabled when not set. |  | String |
| **signalEnabledChannels** (mongodb) | List of channels names that are enabled. Source channel is enabled by default. | source | String |
| **signalPollIntervalMs** (mongodb) | Interval for looking for new signals in registered channels, given in milliseconds. Defaults to 5 seconds. | 5s | long |
| **skippedOperations** (mongodb) | The comma-separated list of operations to skip during streaming, defined as: 'c' for inserts/create; 'u' for updates; 'd' for deletes, 't' for truncates, and 'none' to indicate nothing skipped. By default, only truncate operations will be skipped. | t | String |
| **snapshotCollectionFilterOverrides** (mongodb) | This property contains a comma-separated list of ., for which the initial snapshot may be a subset of data present in the data source. The subset would be defined by mongodb filter query specified as value for property snapshot.collection.filter.override.. |  | String |
| **snapshotDelayMs** (mongodb) | A delay period before a snapshot will begin, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **snapshotFetchSize** (mongodb) | The maximum number of records that should be loaded into memory while performing a snapshot. |  | int |
| **snapshotIncludeCollectionList** (mongodb) | This setting must be set to specify a list of tables/collections whose snapshot must be taken on creating or restarting the connector. |  | String |
| **snapshotMaxThreads** (mongodb) | The maximum number of threads used to perform the snapshot. Defaults to 1. | 1 | int |
| **snapshotMaxThreadsMultiplier** (mongodb) | The factor used to scale the number of snapshot chunks per table. The default behavior is to take 'row\_count/snapshot.max.threads' to compute the number of rows per chunks. This may not be ideal for larger tables, and using the multiplier, the formula is adjusted to increase the number of chunks by using 'row\_count/(snapshot.max.threads snapshot.max.threads.multiplier). | 1 | int |
| **snapshotMode** (mongodb) | The criteria for running a snapshot upon startup of the connector. Select one of the following snapshot options: 'initial' (default): If the connector does not detect any offsets for the logical server name, it runs a snapshot that captures the current full state of the configured tables. After the snapshot completes, the connector begins to stream changes from the oplog. 'never': The connector does not run a snapshot. Upon first startup, the connector immediately begins reading from the beginning of the oplog. | initial | String |
| **snapshotModeConfigurationBasedSnapshotData** (mongodb) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnDataError** (mongodb) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnSchemaError** (mongodb) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotSchema** (mongodb) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedStartStream** (mongodb) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the stream should start or not after snapshot. | false | boolean |
| **snapshotModeCustomName** (mongodb) | When 'snapshot.mode' is set as custom, this setting must be set to specify a the name of the custom implementation provided in the 'name()' method. The implementations must implement the 'Snapshotter' interface and is called on each app boot to determine whether to do a snapshot. |  | String |
| **sourceinfoStructMaker** (mongodb) | The name of the SourceInfoStructMaker class that returns SourceInfo schema and struct. | io.debezium.connector.mongodb.MongoDbSourceInfoStructMaker | String |
| **streamingDelayMs** (mongodb) | A delay period after the snapshot is completed and the streaming begins, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **tombstonesOnDelete** (mongodb) | Whether delete operations should be represented by a delete event and a subsequent tombstone event (true) or only by a delete event (false). Emitting the tombstone event (the default behavior) allows Kafka to completely delete all events pertaining to the given key once the source record got deleted. | false | boolean |
| **topicNamingStrategy** (mongodb) | The name of the TopicNamingStrategy class that should be used to determine the topic name for data change, schema change, transaction, heartbeat event etc. | io.debezium.schema.SchemaTopicNamingStrategy | String |
| **topicPrefix** (mongodb) | **Required** Topic prefix that identifies and provides a namespace for the particular database server/cluster is capturing changes. The topic prefix should be unique across all other connectors, since it is used as a prefix for all Kafka topic names that receive events emitted by this connector. Only alphanumeric characters, hyphens, dots and underscores must be accepted. |  | String |
| **transactionMetadataFactory** (mongodb) | Class to make transaction context & transaction struct/schemas. | io.debezium.pipeline.txmetadata.DefaultTransactionMetadataFactory | String |

## Endpoint Options

The Debezium MongoDB Connector endpoint is configured using URI syntax:

debezium-mongodb:name

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (consumer) | **Required** Unique name for the connector. Attempting to register again with the same name will fail. |  | String |

### Query Parameters (88 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalProperties** (common) | Additional properties for debezium components in case they can’t be set directly on the camel configurations (e.g: setting Kafka Connect properties needed by Debezium engine, for example setting KafkaOffsetBackingStore), the properties have to be prefixed with additionalProperties.. E.g: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. This is a multi-value option with prefix: additionalProperties. |  | Map |
| **internalKeyConverter** (consumer) | The Converter class that should be used to serialize and deserialize key data for offsets. The default is JSON converter. | org.apache.kafka.connect.json.JsonConverter | String |
| **internalValueConverter** (consumer) | The Converter class that should be used to serialize and deserialize value data for offsets. The default is JSON converter. | org.apache.kafka.connect.json.JsonConverter | String |
| **offsetCommitPolicy** (consumer) | The name of the Java class of the commit policy. It defines when offsets commit has to be triggered based on the number of events processed and the time elapsed since the last commit. This class must implement the interface 'OffsetCommitPolicy'. The default is a periodic commit policy based upon time intervals. |  | String |
| **offsetCommitTimeoutMs** (consumer) | Maximum number of milliseconds to wait for records to flush and partition offset data to be committed to offset storage before cancelling the process and restoring the offset data to be committed in a future attempt. The default is 5 seconds. | 5000 | long |
| **offsetFlushIntervalMs** (consumer) | Interval at which to try committing offsets. The default is 1 minute. | 60000 | long |
| **offsetStorage** (consumer) | The name of the Java class that is responsible for persistence of connector offsets. | org.apache.kafka.connect.storage.FileOffsetBackingStore | String |
| **offsetStorageFileName** (consumer) | Path to file where offsets are to be stored. Required when offset.storage is set to the FileOffsetBackingStore. |  | String |
| **offsetStoragePartitions** (consumer) | The number of partitions used when creating the offset storage topic. Required when offset.storage is set to the 'KafkaOffsetBackingStore'. |  | int |
| **offsetStorageReplicationFactor** (consumer) | Replication factor used when creating the offset storage topic. Required when offset.storage is set to the KafkaOffsetBackingStore. |  | int |
| **offsetStorageTopic** (consumer) | The name of the Kafka topic where offsets are to be stored. Required when offset.storage is set to the KafkaOffsetBackingStore. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **captureMode** (mongodb) | The method used to capture changes from MongoDB server. Options include: 'change\_streams' to capture changes via MongoDB Change Streams, update events do not contain full documents; 'change\_streams\_update\_full' (the default) to capture changes via MongoDB Change Streams, update events contain full documents. | change\_streams\_update\_full | String |
| **collectionExcludeList** (mongodb) | A comma-separated list of regular expressions or literals that match the collection names for which changes are to be excluded. |  | String |
| **collectionIncludeList** (mongodb) | A comma-separated list of regular expressions or literals that match the collection names for which changes are to be captured. |  | String |
| **connectionValidationTimeoutMs** (mongodb) | The maximum time in milliseconds to wait for connection validation to complete. Defaults to 60 seconds. | 1m | long |
| **converters** (mongodb) | Optional list of custom converters that would be used instead of default ones. The converters are defined using '.type' config option and configured using options '.'. |  | String |
| **cursorMaxAwaitTimeMs** (mongodb) | The maximum processing time in milliseconds to wait for the oplog cursor to process a single poll request. |  | int |
| **customMetricTags** (mongodb) | The custom metric tags will accept key-value pairs to customize the MBean object name which should be appended the end of regular name, each key would represent a tag for the MBean object name, and the corresponding value would be the value of that tag the key is. For example: k1=v1,k2=v2. |  | String |
| **customSanitizePattern** (mongodb) | Regular expression identifying configuration keys whose values should be masked. When set, this custom pattern replaces Debeziums default password masking pattern. | .\*secret$|.\*password$|.\*sasl\\.jaas\\.config$|.\*basic\\.auth\\.user\\.info|.\*registry\\.auth\\.client-secret|.\*credentials\\.json$ | String |
| **databaseExcludeList** (mongodb) | A comma-separated list of regular expressions or literals that match the database names for which changes are to be excluded. |  | String |
| **databaseIncludeList** (mongodb) | A comma-separated list of regular expressions or literals that match the database names for which changes are to be captured. |  | String |
| **errorsMaxRetries** (mongodb) | The maximum number of retries on connection errors before failing (-1 = no limit, 0 = disabled, 0 = num of retries). | \-1 | int |
| **eventProcessingFailureHandlingMode** (mongodb) | Specify how failures during processing of events (i.e. when encountering a corrupted event) should be handled, including: 'fail' (the default) an exception indicating the problematic event and its position is raised, causing the connector to be stopped; 'warn' the problematic event and its position will be logged and the event will be skipped; 'ignore' the problematic event will be skipped. | fail | String |
| **executorShutdownTimeoutMs** (mongodb) | The maximum time in milliseconds to wait for task executor to shut down. | 4s | long |
| **extendedHeadersEnabled** (mongodb) | Enable/Disable Debezium context headers that provides essential metadata for tracking and identifying the source of CDC events in downstream processing systems. | true | boolean |
| **fieldExcludeList** (mongodb) | A comma-separated list of the fully-qualified names of fields that should be excluded from change event message values. |  | String |
| **fieldRenames** (mongodb) | A comma-separated list of the fully-qualified replacements of fields that should be used to rename fields in change event message values. Fully-qualified replacements for fields are of the form databaseName.collectionName.fieldName.nestedFieldName:newNestedFieldName, where databaseName and collectionName may contain the wildcard () which matches any characters, the colon character (:) is used to determine rename mapping of field. |  | String |
| **guardrailCollectionsLimitAction** (mongodb) | Specify the action to take when a guardrail collections limit is exceeded: 'warn' (the default) logs a warning message and continues processing; 'fail' stops the connector with an error. | warn | String |
| **guardrailCollectionsMax** (mongodb) | The maximum number of collections or tables that can be captured by the connector. When this limit is exceeded, the action specified by 'guardrail.collections.limit.action' will be taken. Set to 0 to disable this guardrail. | 0 | int |
| **heartbeatIntervalMs** (mongodb) | Length of an interval in milli-seconds in in which the connector periodically sends heartbeat messages to a heartbeat topic. Use 0 to disable heartbeat messages. Disabled by default. | 0ms | int |
| **heartbeatTopicsPrefix** (mongodb) | The prefix that is used to name heartbeat topics.Defaults to \_\_debezium-heartbeat. | \_\_debezium-heartbeat | String |
| **incrementalSnapshotWatermarkingStrategy** (mongodb) | Specify the strategy used for watermarking during an incremental snapshot: 'insert\_insert' both open and close signal is written into signal data collection (default); 'insert\_delete' only open signal is written on signal data collection, the close will delete the relative open signal;. | INSERT\_INSERT | String |
| **maxBatchSize** (mongodb) | Maximum size of each batch of source records. Defaults to 2048. | 2048 | int |
| **maxQueueSize** (mongodb) | Maximum size of the queue for change events read from the database log but not yet recorded or forwarded. Defaults to 8192, and should always be larger than the maximum batch size. | 8192 | int |
| **maxQueueSizeInBytes** (mongodb) | Maximum size of the queue in bytes for change events read from the database log but not yet recorded or forwarded. Defaults to 0. Mean the feature is not enabled. | 0 | long |
| **mongodbAuthsource** (mongodb) | Database containing user credentials. | admin | String |
| **mongodbConnectionString** (mongodb) | Database connection string. |  | String |
| **mongodbConnectTimeoutMs** (mongodb) | The connection timeout, given in milliseconds. Defaults to 10 seconds (10,000 ms). | 10s | int |
| **mongodbHeartbeatFrequencyMs** (mongodb) | The frequency that the cluster monitor attempts to reach each server. Defaults to 10 seconds (10,000 ms). | 10s | int |
| **mongodbPassword** (mongodb) | **Required** Password to be used when connecting to MongoDB, if necessary. |  | String |
| **mongodbPollIntervalMs** (mongodb) | Interval for looking for new, removed, or changed replica sets, given in milliseconds. Defaults to 30 seconds (30,000 ms). | 30s | long |
| **mongodbServerSelectionTimeoutMs** (mongodb) | The server selection timeout, given in milliseconds. Defaults to 10 seconds (10,000 ms). | 30s | int |
| **mongodbSocketTimeoutMs** (mongodb) | The socket timeout, given in milliseconds. Defaults to 0 ms. | 0ms | int |
| **mongodbSslEnabled** (mongodb) | Should connector use SSL to connect to MongoDB instances. | false | boolean |
| **mongodbSslInvalidHostnameAllowed** (mongodb) | Whether invalid host names are allowed when using SSL. If true the connection will not prevent man-in-the-middle attacks. | false | boolean |
| **mongodbUser** (mongodb) | Database user for connecting to MongoDB, if necessary. |  | String |
| **notificationEnabledChannels** (mongodb) | List of notification channels names that are enabled. |  | String |
| **notificationSinkTopicName** (mongodb) | The name of the topic for the notifications. This is required in case 'sink' is in the list of enabled channels. |  | String |
| **openlineageIntegrationConfigFilePath** (mongodb) | Path to OpenLineage file configuration. See [https://openlineage.io/docs/client/java/configuration](https://openlineage.io/docs/client/java/configuration). | ./openlineage.yml | String |
| **openlineageIntegrationDatasetKafkaBootstrapServers** (mongodb) | The Kafka bootstrap server address used as input/output namespace/. |  | String |
| **openlineageIntegrationEnabled** (mongodb) | Enable Debezium to emit data lineage metadata through OpenLineage API. | false | boolean |
| **openlineageIntegrationJobDescription** (mongodb) | The job’s description emitted by Debezium. | Debezium change data capture job | String |
| **openlineageIntegrationJobNamespace** (mongodb) | The job’s namespace emitted by Debezium. |  | String |
| **openlineageIntegrationJobOwners** (mongodb) | The job’s owners emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **openlineageIntegrationJobTags** (mongodb) | The job’s tags emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **pollIntervalMs** (mongodb) | Time to wait for new change events to appear after receiving no events, given in milliseconds. Defaults to 500 ms. | 500ms | long |
| **postProcessors** (mongodb) | Optional list of post processors. The processors are defined using '.type' config option and configured using options ''. |  | String |
| **provideTransactionMetadata** (mongodb) | Enables transaction metadata extraction together with event counting. | false | boolean |
| **queryFetchSize** (mongodb) | The maximum number of records that should be loaded into memory while streaming. A value of '0' uses the default JDBC fetch size. | 0 | int |
| **retriableRestartConnectorWaitMs** (mongodb) | Time to wait before restarting connector after retriable exception occurs. Defaults to 10000ms. | 10s | long |
| **schemaHistoryInternalFileFilename** (mongodb) | The path to the file that will be used to record the database schema history. |  | String |
| **schemaNameAdjustmentMode** (mongodb) | Specify how schema names should be adjusted for compatibility with the message converter used by the connector, including: 'avro' replaces the characters that cannot be used in the Avro type name with underscore; 'avro\_unicode' replaces the underscore or characters that cannot be used in the Avro type name with corresponding unicode like \_uxxxx. Note: \_ is an escape sequence like backslash in Java;'none' does not apply any adjustment (default). | none | String |
| **signalDataCollection** (mongodb) | The name of the data collection that is used to send signals/commands to Debezium. For multi-partition mode connectors, multiple signal data collections can be specified as a comma-separated list. Signaling is disabled when not set. |  | String |
| **signalEnabledChannels** (mongodb) | List of channels names that are enabled. Source channel is enabled by default. | source | String |
| **signalPollIntervalMs** (mongodb) | Interval for looking for new signals in registered channels, given in milliseconds. Defaults to 5 seconds. | 5s | long |
| **skippedOperations** (mongodb) | The comma-separated list of operations to skip during streaming, defined as: 'c' for inserts/create; 'u' for updates; 'd' for deletes, 't' for truncates, and 'none' to indicate nothing skipped. By default, only truncate operations will be skipped. | t | String |
| **snapshotCollectionFilterOverrides** (mongodb) | This property contains a comma-separated list of ., for which the initial snapshot may be a subset of data present in the data source. The subset would be defined by mongodb filter query specified as value for property snapshot.collection.filter.override.. |  | String |
| **snapshotDelayMs** (mongodb) | A delay period before a snapshot will begin, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **snapshotFetchSize** (mongodb) | The maximum number of records that should be loaded into memory while performing a snapshot. |  | int |
| **snapshotIncludeCollectionList** (mongodb) | This setting must be set to specify a list of tables/collections whose snapshot must be taken on creating or restarting the connector. |  | String |
| **snapshotMaxThreads** (mongodb) | The maximum number of threads used to perform the snapshot. Defaults to 1. | 1 | int |
| **snapshotMaxThreadsMultiplier** (mongodb) | The factor used to scale the number of snapshot chunks per table. The default behavior is to take 'row\_count/snapshot.max.threads' to compute the number of rows per chunks. This may not be ideal for larger tables, and using the multiplier, the formula is adjusted to increase the number of chunks by using 'row\_count/(snapshot.max.threads snapshot.max.threads.multiplier). | 1 | int |
| **snapshotMode** (mongodb) | The criteria for running a snapshot upon startup of the connector. Select one of the following snapshot options: 'initial' (default): If the connector does not detect any offsets for the logical server name, it runs a snapshot that captures the current full state of the configured tables. After the snapshot completes, the connector begins to stream changes from the oplog. 'never': The connector does not run a snapshot. Upon first startup, the connector immediately begins reading from the beginning of the oplog. | initial | String |
| **snapshotModeConfigurationBasedSnapshotData** (mongodb) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnDataError** (mongodb) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnSchemaError** (mongodb) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotSchema** (mongodb) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedStartStream** (mongodb) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the stream should start or not after snapshot. | false | boolean |
| **snapshotModeCustomName** (mongodb) | When 'snapshot.mode' is set as custom, this setting must be set to specify a the name of the custom implementation provided in the 'name()' method. The implementations must implement the 'Snapshotter' interface and is called on each app boot to determine whether to do a snapshot. |  | String |
| **sourceinfoStructMaker** (mongodb) | The name of the SourceInfoStructMaker class that returns SourceInfo schema and struct. | io.debezium.connector.mongodb.MongoDbSourceInfoStructMaker | String |
| **streamingDelayMs** (mongodb) | A delay period after the snapshot is completed and the streaming begins, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **tombstonesOnDelete** (mongodb) | Whether delete operations should be represented by a delete event and a subsequent tombstone event (true) or only by a delete event (false). Emitting the tombstone event (the default behavior) allows Kafka to completely delete all events pertaining to the given key once the source record got deleted. | false | boolean |
| **topicNamingStrategy** (mongodb) | The name of the TopicNamingStrategy class that should be used to determine the topic name for data change, schema change, transaction, heartbeat event etc. | io.debezium.schema.SchemaTopicNamingStrategy | String |
| **topicPrefix** (mongodb) | **Required** Topic prefix that identifies and provides a namespace for the particular database server/cluster is capturing changes. The topic prefix should be unique across all other connectors, since it is used as a prefix for all Kafka topic names that receive events emitted by this connector. Only alphanumeric characters, hyphens, dots and underscores must be accepted. |  | String |
| **transactionMetadataFactory** (mongodb) | Class to make transaction context & transaction struct/schemas. | io.debezium.pipeline.txmetadata.DefaultTransactionMetadataFactory | String |

## Message Headers

The Debezium MongoDB Connector component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDebeziumSourceMetadata** (consumer) Constant: [`HEADER_SOURCE_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-debezium-mongodb/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_SOURCE_METADATA) | The metadata about the source event, for example table name, database name, log position, etc, please refer to the Debezium documentation for more info. |  | Map |
| **CamelDebeziumIdentifier** (consumer) Constant: [`HEADER_IDENTIFIER`](https://javadoc.io/doc/org.apache.camel/camel-debezium-mongodb/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_IDENTIFIER) | The identifier of the connector, normally is this format {server-name}.{database-name}.{table-name}. |  | String |
| **CamelDebeziumKey** (consumer) Constant: [`HEADER_KEY`](https://javadoc.io/doc/org.apache.camel/camel-debezium-mongodb/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_KEY) | The key of the event, normally is the table Primary Key. |  | Struct |
| **CamelDebeziumOperation** (consumer) Constant: [`HEADER_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-debezium-mongodb/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_OPERATION) | If presents, the type of event operation. Values for the connector are c for create (or insert), u for update, d for delete or r for read (in the case of a initial sync) or in case of a snapshot event. |  | String |
| **CamelDebeziumTimestamp** (consumer) Constant: [`HEADER_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-debezium-mongodb/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_TIMESTAMP) | If presents, the time (using the system clock in the JVM) at which the connector processed the event. |  | Long |
| **CamelDebeziumBefore** (consumer) Constant: [`HEADER_BEFORE`](https://javadoc.io/doc/org.apache.camel/camel-debezium-mongodb/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_BEFORE) | If presents, contains the state of the row before the event occurred. |  | Struct |
| **CamelDebeziumDdlSQL** (consumer) Constant: [`HEADER_DDL_SQL`](https://javadoc.io/doc/org.apache.camel/camel-debezium-mongodb/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_DDL_SQL) | If presents, the ddl sql text of the event. |  | String |

For more information about configuration: [https://debezium.io/documentation/reference/0.10/operations/embedded.html#engine-properties](https://debezium.io/documentation/reference/0.10/operations/embedded.html#engine-properties) [https://debezium.io/documentation/reference/0.10/connectors/mongodb.html#connector-properties](https://debezium.io/documentation/reference/0.10/connectors/mongodb.html#connector-properties)

**Note**: Debezium Mongodb uses MongoDB’s oplog to populate the CDC events, the update events in MongoDB’s oplog don’t have the before or after states of the changed document, so there’s no way for the Debezium connector to provide this information, therefore header key `CamelDebeziumBefore` is not available in this component.

## Usage

### Message body

If the message body is not `null` (in case of tombstones), it contains the state of the row after the event occurred. It is in `String` JSON format, and you can unmarshal using Camel JSON Data Format.

See below for more details.

## Examples

### Consuming events

Here is a basic route that you can use to listen to Debezium events from MongoDB connector:

```java
from("debezium-mongodb:dbz-test-1?offsetStorageFileName=/usr/offset-file-1.dat&mongodbHosts=rs0/localhost:27017&mongodbUser=debezium&mongodbPassword=dbz&mongodbName=dbserver1&databaseHistoryFileFilename=/usr/history-file-1.dat")
    .log("Event received from Debezium : ${body}")
    .log("    with this identifier ${headers.CamelDebeziumIdentifier}")
    .log("    with these source metadata ${headers.CamelDebeziumSourceMetadata}")
    .log("    the event occurred upon this operation '${headers.CamelDebeziumSourceOperation}'")
    .log("    on this database '${headers.CamelDebeziumSourceMetadata[db]}' and this table '${headers.CamelDebeziumSourceMetadata[table]}'")
    .log("    with the key ${headers.CamelDebeziumKey}")
    .choice()
        .when(header(DebeziumConstants.HEADER_OPERATION).in("c", "u", "r"))
            .unmarshal().json()
            .log("Event received from Debezium : ${body}")
         .end()
    .end();
```

By default, the component will emit the events in the body String JSON format in case of `u`, `c` or `r` operations. This can be easily converted to JSON using Camel JSON Data Format e.g.: `.unmarshal().json()` like the above example. In case of operation `d`, the body will be `null`.

> **Important**
> This component is a thin wrapper around Debezium Engine as mentioned. Therefore, before using this component in production, you need to understand how Debezium works and how configurations can reflect the expected behavior. This is especially true in regard to [handling failures](https://debezium.io/documentation/reference/1.8/operations/embedded.html#_handling_failures).

## Spring Boot Auto-Configuration

When using debezium-mongodb with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-debezium-mongodb-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 89 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.debezium-mongodb.additional-properties** | Additional properties for debezium components in case they can’t be set directly on the camel configurations (e.g: setting Kafka Connect properties needed by Debezium engine, for example setting KafkaOffsetBackingStore), the properties have to be prefixed with additionalProperties.. E.g: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. This is a multi-value option with prefix: additionalProperties. |  | Map |
| **camel.component.debezium-mongodb.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.debezium-mongodb.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.debezium-mongodb.capture-mode** | The method used to capture changes from MongoDB server. Options include: 'change\_streams' to capture changes via MongoDB Change Streams, update events do not contain full documents; 'change\_streams\_update\_full' (the default) to capture changes via MongoDB Change Streams, update events contain full documents. | change\_streams\_update\_full | String |
| **camel.component.debezium-mongodb.collection-exclude-list** | A comma-separated list of regular expressions or literals that match the collection names for which changes are to be excluded. |  | String |
| **camel.component.debezium-mongodb.collection-include-list** | A comma-separated list of regular expressions or literals that match the collection names for which changes are to be captured. |  | String |
| **camel.component.debezium-mongodb.configuration** | Allow pre-configured Configurations to be set. The option is a org.apache.camel.component.debezium.mongodb.configuration.MongoDbConnectorEmbeddedDebeziumConfiguration type. |  | MongoDbConnectorEmbeddedDebeziumConfiguration |
| **camel.component.debezium-mongodb.connection-validation-timeout-ms** | The maximum time in milliseconds to wait for connection validation to complete. Defaults to 60 seconds. The option is a long type. | 60000 | Long |
| **camel.component.debezium-mongodb.converters** | Optional list of custom converters that would be used instead of default ones. The converters are defined using '.type' config option and configured using options '.'. |  | String |
| **camel.component.debezium-mongodb.cursor-max-await-time-ms** | The maximum processing time in milliseconds to wait for the oplog cursor to process a single poll request. The option is a int type. |  | Integer |
| **camel.component.debezium-mongodb.custom-metric-tags** | The custom metric tags will accept key-value pairs to customize the MBean object name which should be appended the end of regular name, each key would represent a tag for the MBean object name, and the corresponding value would be the value of that tag the key is. For example: k1=v1,k2=v2. |  | String |
| **camel.component.debezium-mongodb.custom-sanitize-pattern** | Regular expression identifying configuration keys whose values should be masked. When set, this custom pattern replaces Debeziums default password masking pattern. | \\.jaas.config$|.\*basic.auth.user.info|.\*registry.auth.client-secret|.\*credentials.json$ | String |
| **camel.component.debezium-mongodb.database-exclude-list** | A comma-separated list of regular expressions or literals that match the database names for which changes are to be excluded. |  | String |
| **camel.component.debezium-mongodb.database-include-list** | A comma-separated list of regular expressions or literals that match the database names for which changes are to be captured. |  | String |
| **camel.component.debezium-mongodb.enabled** | Whether to enable auto configuration of the debezium-mongodb component. This is enabled by default. |  | Boolean |
| **camel.component.debezium-mongodb.errors-max-retries** | The maximum number of retries on connection errors before failing (-1 = no limit, 0 = disabled, 0 = num of retries). | \-1 | Integer |
| **camel.component.debezium-mongodb.event-processing-failure-handling-mode** | Specify how failures during processing of events (i.e. when encountering a corrupted event) should be handled, including: 'fail' (the default) an exception indicating the problematic event and its position is raised, causing the connector to be stopped; 'warn' the problematic event and its position will be logged and the event will be skipped; 'ignore' the problematic event will be skipped. | fail | String |
| **camel.component.debezium-mongodb.executor-shutdown-timeout-ms** | The maximum time in milliseconds to wait for task executor to shut down. The option is a long type. | 4000 | Long |
| **camel.component.debezium-mongodb.extended-headers-enabled** | Enable/Disable Debezium context headers that provides essential metadata for tracking and identifying the source of CDC events in downstream processing systems. | true | Boolean |
| **camel.component.debezium-mongodb.field-exclude-list** | A comma-separated list of the fully-qualified names of fields that should be excluded from change event message values. |  | String |
| **camel.component.debezium-mongodb.field-renames** | A comma-separated list of the fully-qualified replacements of fields that should be used to rename fields in change event message values. Fully-qualified replacements for fields are of the form databaseName.collectionName.fieldName.nestedFieldName:newNestedFieldName, where databaseName and collectionName may contain the wildcard () which matches any characters, the colon character (:) is used to determine rename mapping of field. |  | String |
| **camel.component.debezium-mongodb.guardrail-collections-limit-action** | Specify the action to take when a guardrail collections limit is exceeded: 'warn' (the default) logs a warning message and continues processing; 'fail' stops the connector with an error. | warn | String |
| **camel.component.debezium-mongodb.guardrail-collections-max** | The maximum number of collections or tables that can be captured by the connector. When this limit is exceeded, the action specified by 'guardrail.collections.limit.action' will be taken. Set to 0 to disable this guardrail. | 0 | Integer |
| **camel.component.debezium-mongodb.heartbeat-interval-ms** | Length of an interval in milli-seconds in in which the connector periodically sends heartbeat messages to a heartbeat topic. Use 0 to disable heartbeat messages. Disabled by default. The option is a int type. | 0 | Integer |
| **camel.component.debezium-mongodb.heartbeat-topics-prefix** | The prefix that is used to name heartbeat topics.Defaults to \_\_debezium-heartbeat. | \_\_debezium-heartbeat | String |
| **camel.component.debezium-mongodb.incremental-snapshot-watermarking-strategy** | Specify the strategy used for watermarking during an incremental snapshot: 'insert\_insert' both open and close signal is written into signal data collection (default); 'insert\_delete' only open signal is written on signal data collection, the close will delete the relative open signal;. | INSERT\_INSERT | String |
| **camel.component.debezium-mongodb.internal-key-converter** | The Converter class that should be used to serialize and deserialize key data for offsets. The default is JSON converter. | org.apache.kafka.connect.json.JsonConverter | String |
| **camel.component.debezium-mongodb.internal-value-converter** | The Converter class that should be used to serialize and deserialize value data for offsets. The default is JSON converter. | org.apache.kafka.connect.json.JsonConverter | String |
| **camel.component.debezium-mongodb.max-batch-size** | Maximum size of each batch of source records. Defaults to 2048. | 2048 | Integer |
| **camel.component.debezium-mongodb.max-queue-size** | Maximum size of the queue for change events read from the database log but not yet recorded or forwarded. Defaults to 8192, and should always be larger than the maximum batch size. | 8192 | Integer |
| **camel.component.debezium-mongodb.max-queue-size-in-bytes** | Maximum size of the queue in bytes for change events read from the database log but not yet recorded or forwarded. Defaults to 0. Mean the feature is not enabled. | 0 | Long |
| **camel.component.debezium-mongodb.mongodb-authsource** | Database containing user credentials. | admin | String |
| **camel.component.debezium-mongodb.mongodb-connect-timeout-ms** | The connection timeout, given in milliseconds. Defaults to 10 seconds (10,000 ms). The option is a int type. | 10000 | Integer |
| **camel.component.debezium-mongodb.mongodb-connection-string** | Database connection string. |  | String |
| **camel.component.debezium-mongodb.mongodb-heartbeat-frequency-ms** | The frequency that the cluster monitor attempts to reach each server. Defaults to 10 seconds (10,000 ms). The option is a int type. | 10000 | Integer |
| **camel.component.debezium-mongodb.mongodb-password** | Password to be used when connecting to MongoDB, if necessary. |  | String |
| **camel.component.debezium-mongodb.mongodb-poll-interval-ms** | Interval for looking for new, removed, or changed replica sets, given in milliseconds. Defaults to 30 seconds (30,000 ms). The option is a long type. | 30000 | Long |
| **camel.component.debezium-mongodb.mongodb-server-selection-timeout-ms** | The server selection timeout, given in milliseconds. Defaults to 10 seconds (10,000 ms). The option is a int type. | 30000 | Integer |
| **camel.component.debezium-mongodb.mongodb-socket-timeout-ms** | The socket timeout, given in milliseconds. Defaults to 0 ms. The option is a int type. | 0 | Integer |
| **camel.component.debezium-mongodb.mongodb-ssl-enabled** | Should connector use SSL to connect to MongoDB instances. | false | Boolean |
| **camel.component.debezium-mongodb.mongodb-ssl-invalid-hostname-allowed** | Whether invalid host names are allowed when using SSL. If true the connection will not prevent man-in-the-middle attacks. | false | Boolean |
| **camel.component.debezium-mongodb.mongodb-user** | Database user for connecting to MongoDB, if necessary. |  | String |
| **camel.component.debezium-mongodb.notification-enabled-channels** | List of notification channels names that are enabled. |  | String |
| **camel.component.debezium-mongodb.notification-sink-topic-name** | The name of the topic for the notifications. This is required in case 'sink' is in the list of enabled channels. |  | String |
| **camel.component.debezium-mongodb.offset-commit-policy** | The name of the Java class of the commit policy. It defines when offsets commit has to be triggered based on the number of events processed and the time elapsed since the last commit. This class must implement the interface 'OffsetCommitPolicy'. The default is a periodic commit policy based upon time intervals. |  | String |
| **camel.component.debezium-mongodb.offset-commit-timeout-ms** | Maximum number of milliseconds to wait for records to flush and partition offset data to be committed to offset storage before cancelling the process and restoring the offset data to be committed in a future attempt. The default is 5 seconds. The option is a long type. | 5000 | Long |
| **camel.component.debezium-mongodb.offset-flush-interval-ms** | Interval at which to try committing offsets. The default is 1 minute. The option is a long type. | 60000 | Long |
| **camel.component.debezium-mongodb.offset-storage** | The name of the Java class that is responsible for persistence of connector offsets. | org.apache.kafka.connect.storage.FileOffsetBackingStore | String |
| **camel.component.debezium-mongodb.offset-storage-file-name** | Path to file where offsets are to be stored. Required when offset.storage is set to the FileOffsetBackingStore. |  | String |
| **camel.component.debezium-mongodb.offset-storage-partitions** | The number of partitions used when creating the offset storage topic. Required when offset.storage is set to the 'KafkaOffsetBackingStore'. |  | Integer |
| **camel.component.debezium-mongodb.offset-storage-replication-factor** | Replication factor used when creating the offset storage topic. Required when offset.storage is set to the KafkaOffsetBackingStore. |  | Integer |
| **camel.component.debezium-mongodb.offset-storage-topic** | The name of the Kafka topic where offsets are to be stored. Required when offset.storage is set to the KafkaOffsetBackingStore. |  | String |
| **camel.component.debezium-mongodb.openlineage-integration-config-file-path** | Path to OpenLineage file configuration. See [https://openlineage.io/docs/client/java/configuration](https://openlineage.io/docs/client/java/configuration). | ./openlineage.yml | String |
| **camel.component.debezium-mongodb.openlineage-integration-dataset-kafka-bootstrap-servers** | The Kafka bootstrap server address used as input/output namespace/. |  | String |
| **camel.component.debezium-mongodb.openlineage-integration-enabled** | Enable Debezium to emit data lineage metadata through OpenLineage API. | false | Boolean |
| **camel.component.debezium-mongodb.openlineage-integration-job-description** | The job’s description emitted by Debezium. | Debezium change data capture job | String |
| **camel.component.debezium-mongodb.openlineage-integration-job-namespace** | The job’s namespace emitted by Debezium. |  | String |
| **camel.component.debezium-mongodb.openlineage-integration-job-owners** | The job’s owners emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **camel.component.debezium-mongodb.openlineage-integration-job-tags** | The job’s tags emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **camel.component.debezium-mongodb.poll-interval-ms** | Time to wait for new change events to appear after receiving no events, given in milliseconds. Defaults to 500 ms. The option is a long type. | 500 | Long |
| **camel.component.debezium-mongodb.post-processors** | Optional list of post processors. The processors are defined using '.type' config option and configured using options ''. |  | String |
| **camel.component.debezium-mongodb.provide-transaction-metadata** | Enables transaction metadata extraction together with event counting. | false | Boolean |
| **camel.component.debezium-mongodb.query-fetch-size** | The maximum number of records that should be loaded into memory while streaming. A value of '0' uses the default JDBC fetch size. | 0 | Integer |
| **camel.component.debezium-mongodb.retriable-restart-connector-wait-ms** | Time to wait before restarting connector after retriable exception occurs. Defaults to 10000ms. The option is a long type. | 10000 | Long |
| **camel.component.debezium-mongodb.schema-history-internal-file-filename** | The path to the file that will be used to record the database schema history. |  | String |
| **camel.component.debezium-mongodb.schema-name-adjustment-mode** | Specify how schema names should be adjusted for compatibility with the message converter used by the connector, including: 'avro' replaces the characters that cannot be used in the Avro type name with underscore; 'avro\_unicode' replaces the underscore or characters that cannot be used in the Avro type name with corresponding unicode like \_uxxxx. Note: \_ is an escape sequence like backslash in Java;'none' does not apply any adjustment (default). | none | String |
| **camel.component.debezium-mongodb.signal-data-collection** | The name of the data collection that is used to send signals/commands to Debezium. For multi-partition mode connectors, multiple signal data collections can be specified as a comma-separated list. Signaling is disabled when not set. |  | String |
| **camel.component.debezium-mongodb.signal-enabled-channels** | List of channels names that are enabled. Source channel is enabled by default. | source | String |
| **camel.component.debezium-mongodb.signal-poll-interval-ms** | Interval for looking for new signals in registered channels, given in milliseconds. Defaults to 5 seconds. The option is a long type. | 5000 | Long |
| **camel.component.debezium-mongodb.skipped-operations** | The comma-separated list of operations to skip during streaming, defined as: 'c' for inserts/create; 'u' for updates; 'd' for deletes, 't' for truncates, and 'none' to indicate nothing skipped. By default, only truncate operations will be skipped. | t | String |
| **camel.component.debezium-mongodb.snapshot-collection-filter-overrides** | This property contains a comma-separated list of ., for which the initial snapshot may be a subset of data present in the data source. The subset would be defined by mongodb filter query specified as value for property snapshot.collection.filter.override.. |  | String |
| **camel.component.debezium-mongodb.snapshot-delay-ms** | A delay period before a snapshot will begin, given in milliseconds. Defaults to 0 ms. The option is a long type. | 0 | Long |
| **camel.component.debezium-mongodb.snapshot-fetch-size** | The maximum number of records that should be loaded into memory while performing a snapshot. |  | Integer |
| **camel.component.debezium-mongodb.snapshot-include-collection-list** | This setting must be set to specify a list of tables/collections whose snapshot must be taken on creating or restarting the connector. |  | String |
| **camel.component.debezium-mongodb.snapshot-max-threads** | The maximum number of threads used to perform the snapshot. Defaults to 1. | 1 | Integer |
| **camel.component.debezium-mongodb.snapshot-max-threads-multiplier** | The factor used to scale the number of snapshot chunks per table. The default behavior is to take 'row\_count/snapshot.max.threads' to compute the number of rows per chunks. This may not be ideal for larger tables, and using the multiplier, the formula is adjusted to increase the number of chunks by using 'row\_count/(snapshot.max.threads snapshot.max.threads.multiplier). | 1 | Integer |
| **camel.component.debezium-mongodb.snapshot-mode** | The criteria for running a snapshot upon startup of the connector. Select one of the following snapshot options: 'initial' (default): If the connector does not detect any offsets for the logical server name, it runs a snapshot that captures the current full state of the configured tables. After the snapshot completes, the connector begins to stream changes from the oplog. 'never': The connector does not run a snapshot. Upon first startup, the connector immediately begins reading from the beginning of the oplog. | initial | String |
| **camel.component.debezium-mongodb.snapshot-mode-configuration-based-snapshot-data** | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not. | false | Boolean |
| **camel.component.debezium-mongodb.snapshot-mode-configuration-based-snapshot-on-data-error** | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not in case of error. | false | Boolean |
| **camel.component.debezium-mongodb.snapshot-mode-configuration-based-snapshot-on-schema-error** | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not in case of error. | false | Boolean |
| **camel.component.debezium-mongodb.snapshot-mode-configuration-based-snapshot-schema** | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not. | false | Boolean |
| **camel.component.debezium-mongodb.snapshot-mode-configuration-based-start-stream** | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the stream should start or not after snapshot. | false | Boolean |
| **camel.component.debezium-mongodb.snapshot-mode-custom-name** | When 'snapshot.mode' is set as custom, this setting must be set to specify a the name of the custom implementation provided in the 'name()' method. The implementations must implement the 'Snapshotter' interface and is called on each app boot to determine whether to do a snapshot. |  | String |
| **camel.component.debezium-mongodb.sourceinfo-struct-maker** | The name of the SourceInfoStructMaker class that returns SourceInfo schema and struct. | io.debezium.connector.mongodb.MongoDbSourceInfoStructMaker | String |
| **camel.component.debezium-mongodb.streaming-delay-ms** | A delay period after the snapshot is completed and the streaming begins, given in milliseconds. Defaults to 0 ms. The option is a long type. | 0 | Long |
| **camel.component.debezium-mongodb.tombstones-on-delete** | Whether delete operations should be represented by a delete event and a subsequent tombstone event (true) or only by a delete event (false). Emitting the tombstone event (the default behavior) allows Kafka to completely delete all events pertaining to the given key once the source record got deleted. | false | Boolean |
| **camel.component.debezium-mongodb.topic-naming-strategy** | The name of the TopicNamingStrategy class that should be used to determine the topic name for data change, schema change, transaction, heartbeat event etc. | io.debezium.schema.SchemaTopicNamingStrategy | String |
| **camel.component.debezium-mongodb.topic-prefix** | Topic prefix that identifies and provides a namespace for the particular database server/cluster is capturing changes. The topic prefix should be unique across all other connectors, since it is used as a prefix for all Kafka topic names that receive events emitted by this connector. Only alphanumeric characters, hyphens, dots and underscores must be accepted. |  | String |
| **camel.component.debezium-mongodb.transaction-metadata-factory** | Class to make transaction context & transaction struct/schemas. | io.debezium.pipeline.txmetadata.DefaultTransactionMetadataFactory | String |