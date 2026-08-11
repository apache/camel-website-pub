# Debezium SQL Server Connector

**Since Camel 3.0**

**Only consumer is supported**

The Debezium SQL Server component is wrapper around [Debezium](https://debezium.io/) using [Debezium Engine](https://debezium.io/documentation/reference/0.10/operations/embedded.md), which enables Change Data Capture from SQL Server database using Debezium without the need for Kafka or Kafka Connect.

> **Note**
> **Note on handling failures:** per [Debezium Embedded Engine](https://debezium.io/documentation/reference/1.9/development/engine.html#_handling_failures) documentation, the engines are actively recording source offsets and periodically flush these offsets to a persistent storage. Therefore, when the application is restarted or crashed, the engine will resume from the last recorded offset. This means that, at normal operation, your downstream routes will receive each event exactly once. However, in case of an application crash (not having a graceful shutdown), the application will resume from the last recorded offset, which may result in receiving duplicate events immediately after the restart. Therefore, your downstream routes should be tolerant enough of such a case and deduplicate events if needed.

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-debezium-sqlserver</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

debezium-sqlserver:name\[?options\]

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

The Debezium SQL Server Connector component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalProperties** (common) | Additional properties for debezium components in case they can’t be set directly on the camel configurations (e.g: setting Kafka Connect properties needed by Debezium engine, for example setting KafkaOffsetBackingStore), the properties have to be prefixed with additionalProperties.. E.g: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. This is a multi-value option with prefix: additionalProperties. |  | Map |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **configuration** (consumer) | Allow pre-configured Configurations to be set. |  | SqlServerConnectorEmbeddedDebeziumConfiguration |
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
| **binaryHandlingMode** (sqlserver) | Specify how binary (blob, binary, etc.) columns should be represented in change events, including: 'bytes' represents binary data as byte array (default); 'base64' represents binary data as base64-encoded string; 'base64-url-safe' represents binary data as base64-url-safe-encoded string; 'hex' represents binary data as hex-encoded (base16) string. | bytes | String |
| **columnExcludeList** (sqlserver) | Regular expressions matching columns to exclude from change events. |  | String |
| **columnIncludeList** (sqlserver) | Regular expressions matching columns to include in change events. |  | String |
| **columnPropagateSourceType** (sqlserver) | A comma-separated list of regular expressions matching fully-qualified names of columns that adds the columns original type and original length as parameters to the corresponding field schemas in the emitted change records. |  | String |
| **connectionValidationTimeoutMs** (sqlserver) | The maximum time in milliseconds to wait for connection validation to complete. Defaults to 60 seconds. | 1m | long |
| **converters** (sqlserver) | Optional list of custom converters that would be used instead of default ones. The converters are defined using '.type' config option and configured using options '.'. |  | String |
| **customMetricTags** (sqlserver) | The custom metric tags will accept key-value pairs to customize the MBean object name which should be appended the end of regular name, each key would represent a tag for the MBean object name, and the corresponding value would be the value of that tag the key is. For example: k1=v1,k2=v2. |  | String |
| **customSanitizePattern** (sqlserver) | Regular expression identifying configuration keys whose values should be masked. When set, this custom pattern replaces Debeziums default password masking pattern. | .\*secret$|.\*password$|.\*sasl\\.jaas\\.config$|.\*basic\\.auth\\.user\\.info|.\*registry\\.auth\\.client-secret|.\*credentials\\.json$|.\*connectionstring$|.\*connection\\.string$ | String |
| **databaseHostname** (sqlserver) | Resolvable hostname or IP address of the database server. |  | String |
| **databaseInstance** (sqlserver) | The SQL Server instance name. |  | String |
| **databaseNames** (sqlserver) | The names of the databases from which the connector should capture changes. |  | String |
| **databasePassword** (sqlserver) | **Required** Password of the database user to be used when connecting to the database. |  | String |
| **databasePort** (sqlserver) | Port of the database server. | 1433 | int |
| **databaseQueryTimeoutMs** (sqlserver) | Time to wait for a query to execute, given in milliseconds. Defaults to 600 seconds (600,000 ms); zero means there is no limit. | 10m | int |
| **databaseUser** (sqlserver) | Name of the database user to be used when connecting to the database. |  | String |
| **dataQueryMode** (sqlserver) | Controls how the connector queries CDC data. The default is 'direct', which makes the connector to query the change tables directly. The value of 'function' means the data is queried by means of calling cdc.fn\_cdc\_get\_all\_changes\_# function. | direct | String |
| **datatypePropagateSourceType** (sqlserver) | A comma-separated list of regular expressions matching the database-specific data type names that adds the data type’s original type and original length as parameters to the corresponding field schemas in the emitted change records. |  | String |
| **decimalHandlingMode** (sqlserver) | Specify how DECIMAL and NUMERIC columns should be represented in change events, including: 'precise' (the default) uses java.math.BigDecimal to represent values, which are encoded in the change events using a binary representation and Kafka Connect’s 'org.apache.kafka.connect.data.Decimal' type; 'string' uses string to represent values; 'double' represents values using Java’s 'double', which may not offer the precision but will be far easier to use in consumers. | precise | String |
| **errorsMaxRetries** (sqlserver) | The maximum number of retries on connection errors before failing (-1 = no limit, 0 = disabled, 0 = num of retries). | \-1 | int |
| **eventProcessingFailureHandlingMode** (sqlserver) | Specify how failures during processing of events (i.e. when encountering a corrupted event) should be handled, including: 'fail' (the default) an exception indicating the problematic event and its position is raised, causing the connector to be stopped; 'warn' the problematic event and its position will be logged and the event will be skipped; 'ignore' the problematic event will be skipped. | fail | String |
| **executorShutdownTimeoutMs** (sqlserver) | The maximum time in milliseconds to wait for task executor to shut down. | 4s | long |
| **extendedHeadersEnabled** (sqlserver) | Enable/Disable Debezium context headers that provides essential metadata for tracking and identifying the source of CDC events in downstream processing systems. | true | boolean |
| **guardrailCollectionsLimitAction** (sqlserver) | Specify the action to take when a guardrail collections limit is exceeded: 'warn' (the default) logs a warning message and continues processing; 'fail' stops the connector with an error. | warn | String |
| **guardrailCollectionsMax** (sqlserver) | The maximum number of collections or tables that can be captured by the connector. When this limit is exceeded, the action specified by 'guardrail.collections.limit.action' will be taken. Set to 0 to disable this guardrail. | 0 | int |
| **heartbeatActionQuery** (sqlserver) | The query executed with every heartbeat. |  | String |
| **heartbeatIntervalMs** (sqlserver) | Length of an interval in milli-seconds in in which the connector periodically sends heartbeat messages to a heartbeat topic. Use 0 to disable heartbeat messages. Disabled by default. | 0ms | int |
| **heartbeatTopicsPrefix** (sqlserver) | The prefix that is used to name heartbeat topics.Defaults to \_\_debezium-heartbeat. | \_\_debezium-heartbeat | String |
| **includeSchemaChanges** (sqlserver) | Whether the connector should publish changes in the database schema to a Kafka topic with the same name as the database server ID. Each schema change will be recorded using a key that contains the database name and whose value include logical description of the new schema and optionally the DDL statement(s). The default is 'true'. This is independent of how the connector internally records database schema history. | true | boolean |
| **includeSchemaComments** (sqlserver) | Whether the connector parse table and column’s comment to metadata object. Note: Enable this option will bring the implications on memory usage. The number and size of ColumnImpl objects is what largely impacts how much memory is consumed by the Debezium connectors, and adding a String to each of them can potentially be quite heavy. The default is 'false'. | false | boolean |
| **incrementalSnapshotAllowSchemaChanges** (sqlserver) | Detect schema change during an incremental snapshot and re-select a current chunk to avoid locking DDLs. Note that changes to a primary key are not supported and can cause incorrect results if performed during an incremental snapshot. Another limitation is that if a schema change affects only columns' default values, then the change won’t be detected until the DDL is processed from the binlog stream. This doesn’t affect the snapshot events' values, but the schema of snapshot events may have outdated defaults. | false | boolean |
| **incrementalSnapshotChunkSize** (sqlserver) | The maximum size of chunk (number of documents/rows) for incremental snapshotting. | 1024 | int |
| **incrementalSnapshotOptionRecompile** (sqlserver) | Add OPTION(RECOMPILE) on each SELECT statement during the incremental snapshot process. This prevents parameter sniffing but can cause CPU pressure on the source database. | false | boolean |
| **incrementalSnapshotWatermarkingStrategy** (sqlserver) | Specify the strategy used for watermarking during an incremental snapshot: 'insert\_insert' both open and close signal is written into signal data collection (default); 'insert\_delete' only open signal is written on signal data collection, the close will delete the relative open signal;. | INSERT\_INSERT | String |
| **legacySnapshotMaxThreads** (sqlserver) | When enabled, uses the legacy table-per-thread parallel snapshot algorithm. When set to false (the default), tables are split into chunks and processed across all snapshot threads, allowing for higher concurrency for snapshots. | false | boolean |
| **maxBatchSize** (sqlserver) | Maximum size of each batch of source records. Defaults to 2048. | 2048 | int |
| **maxIterationTransactions** (sqlserver) | This property can be used to reduce the connector memory usage footprint when changes are streamed from multiple tables per database. | 500 | int |
| **maxQueueSize** (sqlserver) | Maximum size of the queue for change events read from the database log but not yet recorded or forwarded. Defaults to 8192, and should always be larger than the maximum batch size. | 8192 | int |
| **maxQueueSizeInBytes** (sqlserver) | Maximum size of the queue in bytes for change events read from the database log but not yet recorded or forwarded. Defaults to 0. Mean the feature is not enabled. | 0 | long |
| **memoryManagementSchemasClass** (sqlserver) | The fully-qualified class name of the storage implementation for schema metadata. The class must implement io.debezium.relational.TableMappingStorage. Defaults to io.debezium.relational.ConcurrentMapTableMappingStorage for in-memory storage. | io.debezium.relational.ConcurrentMapTableMappingStorage | String |
| **memoryManagementTablesClass** (sqlserver) | The fully-qualified class name of the storage implementation for table metadata. The class must implement io.debezium.relational.TableMappingStorage. Defaults to io.debezium.relational.ConcurrentMapTableMappingStorage for in-memory storage. | io.debezium.relational.ConcurrentMapTableMappingStorage | String |
| **messageKeyColumns** (sqlserver) | A semicolon-separated list of expressions that match fully-qualified tables and column(s) to be used as message key. Each expression must match the pattern ':', where the table names could be defined as (DB\_NAME.TABLE\_NAME) or (SCHEMA\_NAME.TABLE\_NAME), depending on the specific connector, and the key columns are a comma-separated list of columns representing the custom key. For any table without an explicit key configuration the table’s primary key column(s) will be used as message key. Example: dbserver1.inventory.orderlines:orderId,orderLineId;dbserver1.inventory.orders:id. |  | String |
| **notificationEnabledChannels** (sqlserver) | List of notification channels names that are enabled. |  | String |
| **notificationSinkTopicName** (sqlserver) | The name of the topic for the notifications. This is required in case 'sink' is in the list of enabled channels. |  | String |
| **openlineageIntegrationConfigFilePath** (sqlserver) | Path to OpenLineage file configuration. See [https://openlineage.io/docs/client/java/configuration](https://openlineage.io/docs/client/java/configuration). | ./openlineage.yml | String |
| **openlineageIntegrationDatasetKafkaBootstrapServers** (sqlserver) | The Kafka bootstrap server address used as input/output namespace/. |  | String |
| **openlineageIntegrationEnabled** (sqlserver) | Enable Debezium to emit data lineage metadata through OpenLineage API. | false | boolean |
| **openlineageIntegrationJobDescription** (sqlserver) | The job’s description emitted by Debezium. | Debezium change data capture job | String |
| **openlineageIntegrationJobNamespace** (sqlserver) | The job’s namespace emitted by Debezium. |  | String |
| **openlineageIntegrationJobOwners** (sqlserver) | The job’s owners emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **openlineageIntegrationJobTags** (sqlserver) | The job’s tags emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **pollIntervalMs** (sqlserver) | Time to wait for new change events to appear after receiving no events, given in milliseconds. Defaults to 500 ms. | 500ms | long |
| **postProcessors** (sqlserver) | Optional list of post processors. The processors are defined using '.type' config option and configured using options ''. |  | String |
| **provideTransactionMetadata** (sqlserver) | Enables transaction metadata extraction together with event counting. | false | boolean |
| **retriableRestartConnectorWaitMs** (sqlserver) | Time to wait before restarting connector after retriable exception occurs. Defaults to 10000ms. | 10s | long |
| **schemaHistoryInternal** (sqlserver) | The name of the SchemaHistory class that should be used to store and recover database schema changes. The configuration properties for the history are prefixed with the 'schema.history.internal.' string. | io.debezium.storage.kafka.history.KafkaSchemaHistory | String |
| **schemaHistoryInternalFileFilename** (sqlserver) | The path to the file that will be used to record the database schema history. |  | String |
| **schemaHistoryInternalSkipUnparseableDdl** (sqlserver) | Controls the action Debezium will take when it meets a DDL statement in binlog, that it cannot parse.By default the connector will stop operating but by changing the setting it can ignore the statements which it cannot parse. If skipping is enabled then Debezium can miss metadata changes. | false | boolean |
| **schemaHistoryInternalStoreOnlyCapturedDatabasesDdl** (sqlserver) | Controls what DDL will Debezium store in database schema history. By default (false) Debezium will store all incoming DDL statements. If set to true, then only DDL that manipulates a table from captured schema/database will be stored. | false | boolean |
| **schemaHistoryInternalStoreOnlyCapturedTablesDdl** (sqlserver) | Controls what DDL will Debezium store in database schema history. By default (false) Debezium will store all incoming DDL statements. If set to true, then only DDL that manipulates a captured table will be stored. | false | boolean |
| **schemaNameAdjustmentMode** (sqlserver) | Specify how schema names should be adjusted for compatibility with the message converter used by the connector, including: 'avro' replaces the characters that cannot be used in the Avro type name with underscore; 'avro\_unicode' replaces the underscore or characters that cannot be used in the Avro type name with corresponding unicode like \_uxxxx. Note: \_ is an escape sequence like backslash in Java;'none' does not apply any adjustment (default). | none | String |
| **signalDataCollection** (sqlserver) | The name of the data collection that is used to send signals/commands to Debezium. For multi-partition mode connectors, multiple signal data collections can be specified as a comma-separated list. Signaling is disabled when not set. |  | String |
| **signalEnabledChannels** (sqlserver) | List of channels names that are enabled. Source channel is enabled by default. | source | String |
| **signalPollIntervalMs** (sqlserver) | Interval for looking for new signals in registered channels, given in milliseconds. Defaults to 5 seconds. | 5s | long |
| **skippedOperations** (sqlserver) | The comma-separated list of operations to skip during streaming, defined as: 'c' for inserts/create; 'u' for updates; 'd' for deletes, 't' for truncates, and 'none' to indicate nothing skipped. By default, only truncate operations will be skipped. | t | String |
| **snapshotDelayMs** (sqlserver) | A delay period before a snapshot will begin, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **snapshotFetchSize** (sqlserver) | The maximum number of records that should be loaded into memory while performing a snapshot. |  | int |
| **snapshotIncludeCollectionList** (sqlserver) | This setting must be set to specify a list of tables/collections whose snapshot must be taken on creating or restarting the connector. |  | String |
| **snapshotIsolationMode** (sqlserver) | Controls which transaction isolation level is used and how long the connector locks the captured tables. The default is 'repeatable\_read', which means that repeatable read isolation level is used. In addition, type of acquired lock during schema snapshot depends on snapshot.locking.mode property. Using a value of 'exclusive' ensures that the connector holds the type of lock specified with snapshot.locking.mode property (and thus prevents any reads and updates) for all captured tables during the entire snapshot duration. When 'snapshot' is specified, connector runs the initial snapshot in SNAPSHOT isolation level, which guarantees snapshot consistency. In addition, neither table nor row-level locks are held. When 'read\_committed' is specified, connector runs the initial snapshot in READ COMMITTED isolation level. No long-running locks are taken, so that initial snapshot does not prevent other transactions from updating table rows. Snapshot consistency is not guaranteed.In 'read\_uncommitted' mode neither table nor row-level locks are acquired, but connector does not guarantee snapshot consistency. | repeatable\_read | String |
| **snapshotLockTimeoutMs** (sqlserver) | The maximum number of millis to wait for table locks at the beginning of a snapshot. If locks cannot be acquired in this time frame, the snapshot will be aborted. Defaults to 10 seconds. | 10s | long |
| **snapshotMaxThreads** (sqlserver) | The maximum number of threads used to perform the snapshot. Defaults to 1. | 1 | int |
| **snapshotMaxThreadsMultiplier** (sqlserver) | The factor used to scale the number of snapshot chunks per table. The default behavior is to take 'row\_count/snapshot.max.threads' to compute the number of rows per chunks. This may not be ideal for larger tables, and using the multiplier, the formula is adjusted to increase the number of chunks by using 'row\_count/(snapshot.max.threads snapshot.max.threads.multiplier). | 1 | int |
| **snapshotMode** (sqlserver) | The criteria for running a snapshot upon startup of the connector. Select one of the following snapshot options: 'initial' (default): If the connector does not detect any offsets for the logical server name, it runs a snapshot that captures the current full state of the configured tables. After the snapshot completes, the connector begins to stream changes from the transaction log.; 'initial\_only': The connector performs a snapshot as it does for the 'initial' option, but after the connector completes the snapshot, it stops, and does not stream changes from the transaction log.; 'schema\_only': If the connector does not detect any offsets for the logical server name, it runs a snapshot that captures only the schema (table structures), but not any table data. After the snapshot completes, the connector begins to stream changes from the transaction log. | initial | String |
| **snapshotModeConfigurationBasedSnapshotData** (sqlserver) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnDataError** (sqlserver) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnSchemaError** (sqlserver) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotSchema** (sqlserver) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedStartStream** (sqlserver) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the stream should start or not after snapshot. | false | boolean |
| **snapshotModeCustomName** (sqlserver) | When 'snapshot.mode' is set as custom, this setting must be set to specify a the name of the custom implementation provided in the 'name()' method. The implementations must implement the 'Snapshotter' interface and is called on each app boot to determine whether to do a snapshot. |  | String |
| **snapshotSelectStatementOverrides** (sqlserver) | This property contains a comma-separated list of fully-qualified tables (DB\_NAME.TABLE\_NAME) or (SCHEMA\_NAME.TABLE\_NAME), depending on the specific connectors. Select statements for the individual tables are specified in further configuration properties, one for each table, identified by the id 'snapshot.select.statement.overrides.DB\_NAME.TABLE\_NAME' or 'snapshot.select.statement.overrides.SCHEMA\_NAME.TABLE\_NAME', respectively. The value of those properties is the select statement to use when retrieving data from the specific table during snapshotting. A possible use case for large append-only tables is setting a specific point where to start (resume) snapshotting, in case a previous snapshotting was interrupted. |  | String |
| **snapshotTablesOrderByRowCount** (sqlserver) | Controls the order in which tables are processed in the initial snapshot. A descending value will order the tables by row count descending. A ascending value will order the tables by row count ascending. A value of disabled (the default) will disable ordering by row count. | disabled | String |
| **sourceinfoStructMaker** (sqlserver) | The name of the SourceInfoStructMaker class that returns SourceInfo schema and struct. | io.debezium.connector.sqlserver.SqlServerSourceInfoStructMaker | String |
| **statisticsMetricsEnabled** (sqlserver) | Enable to collect various kind of statistics, like latencies in record processing, and derived data like quantiles. By default collecting statistics is enabled. | true | boolean |
| **streamingDelayMs** (sqlserver) | A delay period after the snapshot is completed and the streaming begins, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **streamingFetchSize** (sqlserver) | Specifies the maximum number of rows that should be read in one go from each table while streaming. The connector will read the table contents in multiple batches of this size. Defaults to 0 which means no limit. | 0 | int |
| **tableExcludeList** (sqlserver) | A comma-separated list of regular expressions that match the fully-qualified names of tables to be excluded from monitoring. |  | String |
| **tableIgnoreBuiltin** (sqlserver) | Flag specifying whether built-in tables should be ignored. | true | boolean |
| **tableIncludeList** (sqlserver) | The tables for which changes are to be captured. |  | String |
| **timePrecisionMode** (sqlserver) | Time, date, and timestamps can be represented with different kinds of precisions, including: 'adaptive' (the default) bases the precision of time, date, and timestamp values on the database column’s precision; 'adaptive\_time\_microseconds' like 'adaptive' mode, but TIME fields always use microseconds precision; 'connect' always represents time, date, and timestamp values using Kafka Connect’s built-in representations for Time, Date, and Timestamp, which uses millisecond precision regardless of the database columns' precision; 'isostring' represents time, date, and timestamp values as ISO-8601 formatted strings at the UTC time zone; 'microseconds' always represents time, date, and timestamp values using microsecond precision; 'nanoseconds' always represents time, date, and timestamp values using nanosecond precision. | adaptive | String |
| **tombstonesOnDelete** (sqlserver) | Whether delete operations should be represented by a delete event and a subsequent tombstone event (true) or only by a delete event (false). Emitting the tombstone event (the default behavior) allows Kafka to completely delete all events pertaining to the given key once the source record got deleted. | false | boolean |
| **topicNamingStrategy** (sqlserver) | The name of the TopicNamingStrategy class that should be used to determine the topic name for data change, schema change, transaction, heartbeat event etc. | io.debezium.schema.SchemaTopicNamingStrategy | String |
| **topicPrefix** (sqlserver) | **Required** Topic prefix that identifies and provides a namespace for the particular database server/cluster is capturing changes. The topic prefix should be unique across all other connectors, since it is used as a prefix for all Kafka topic names that receive events emitted by this connector. Only alphanumeric characters, hyphens, dots and underscores must be accepted. |  | String |
| **transactionMetadataFactory** (sqlserver) | Class to make transaction context & transaction struct/schemas. | io.debezium.pipeline.txmetadata.DefaultTransactionMetadataFactory | String |

## Endpoint Options

The Debezium SQL Server Connector endpoint is configured using URI syntax:

debezium-sqlserver:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (consumer) | **Required** Unique name for the connector. Attempting to register again with the same name will fail. |  | String |

### Query Parameters

   
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
| **binaryHandlingMode** (sqlserver) | Specify how binary (blob, binary, etc.) columns should be represented in change events, including: 'bytes' represents binary data as byte array (default); 'base64' represents binary data as base64-encoded string; 'base64-url-safe' represents binary data as base64-url-safe-encoded string; 'hex' represents binary data as hex-encoded (base16) string. | bytes | String |
| **columnExcludeList** (sqlserver) | Regular expressions matching columns to exclude from change events. |  | String |
| **columnIncludeList** (sqlserver) | Regular expressions matching columns to include in change events. |  | String |
| **columnPropagateSourceType** (sqlserver) | A comma-separated list of regular expressions matching fully-qualified names of columns that adds the columns original type and original length as parameters to the corresponding field schemas in the emitted change records. |  | String |
| **connectionValidationTimeoutMs** (sqlserver) | The maximum time in milliseconds to wait for connection validation to complete. Defaults to 60 seconds. | 1m | long |
| **converters** (sqlserver) | Optional list of custom converters that would be used instead of default ones. The converters are defined using '.type' config option and configured using options '.'. |  | String |
| **customMetricTags** (sqlserver) | The custom metric tags will accept key-value pairs to customize the MBean object name which should be appended the end of regular name, each key would represent a tag for the MBean object name, and the corresponding value would be the value of that tag the key is. For example: k1=v1,k2=v2. |  | String |
| **customSanitizePattern** (sqlserver) | Regular expression identifying configuration keys whose values should be masked. When set, this custom pattern replaces Debeziums default password masking pattern. | .\*secret$|.\*password$|.\*sasl\\.jaas\\.config$|.\*basic\\.auth\\.user\\.info|.\*registry\\.auth\\.client-secret|.\*credentials\\.json$|.\*connectionstring$|.\*connection\\.string$ | String |
| **databaseHostname** (sqlserver) | Resolvable hostname or IP address of the database server. |  | String |
| **databaseInstance** (sqlserver) | The SQL Server instance name. |  | String |
| **databaseNames** (sqlserver) | The names of the databases from which the connector should capture changes. |  | String |
| **databasePassword** (sqlserver) | **Required** Password of the database user to be used when connecting to the database. |  | String |
| **databasePort** (sqlserver) | Port of the database server. | 1433 | int |
| **databaseQueryTimeoutMs** (sqlserver) | Time to wait for a query to execute, given in milliseconds. Defaults to 600 seconds (600,000 ms); zero means there is no limit. | 10m | int |
| **databaseUser** (sqlserver) | Name of the database user to be used when connecting to the database. |  | String |
| **dataQueryMode** (sqlserver) | Controls how the connector queries CDC data. The default is 'direct', which makes the connector to query the change tables directly. The value of 'function' means the data is queried by means of calling cdc.fn\_cdc\_get\_all\_changes\_# function. | direct | String |
| **datatypePropagateSourceType** (sqlserver) | A comma-separated list of regular expressions matching the database-specific data type names that adds the data type’s original type and original length as parameters to the corresponding field schemas in the emitted change records. |  | String |
| **decimalHandlingMode** (sqlserver) | Specify how DECIMAL and NUMERIC columns should be represented in change events, including: 'precise' (the default) uses java.math.BigDecimal to represent values, which are encoded in the change events using a binary representation and Kafka Connect’s 'org.apache.kafka.connect.data.Decimal' type; 'string' uses string to represent values; 'double' represents values using Java’s 'double', which may not offer the precision but will be far easier to use in consumers. | precise | String |
| **errorsMaxRetries** (sqlserver) | The maximum number of retries on connection errors before failing (-1 = no limit, 0 = disabled, 0 = num of retries). | \-1 | int |
| **eventProcessingFailureHandlingMode** (sqlserver) | Specify how failures during processing of events (i.e. when encountering a corrupted event) should be handled, including: 'fail' (the default) an exception indicating the problematic event and its position is raised, causing the connector to be stopped; 'warn' the problematic event and its position will be logged and the event will be skipped; 'ignore' the problematic event will be skipped. | fail | String |
| **executorShutdownTimeoutMs** (sqlserver) | The maximum time in milliseconds to wait for task executor to shut down. | 4s | long |
| **extendedHeadersEnabled** (sqlserver) | Enable/Disable Debezium context headers that provides essential metadata for tracking and identifying the source of CDC events in downstream processing systems. | true | boolean |
| **guardrailCollectionsLimitAction** (sqlserver) | Specify the action to take when a guardrail collections limit is exceeded: 'warn' (the default) logs a warning message and continues processing; 'fail' stops the connector with an error. | warn | String |
| **guardrailCollectionsMax** (sqlserver) | The maximum number of collections or tables that can be captured by the connector. When this limit is exceeded, the action specified by 'guardrail.collections.limit.action' will be taken. Set to 0 to disable this guardrail. | 0 | int |
| **heartbeatActionQuery** (sqlserver) | The query executed with every heartbeat. |  | String |
| **heartbeatIntervalMs** (sqlserver) | Length of an interval in milli-seconds in in which the connector periodically sends heartbeat messages to a heartbeat topic. Use 0 to disable heartbeat messages. Disabled by default. | 0ms | int |
| **heartbeatTopicsPrefix** (sqlserver) | The prefix that is used to name heartbeat topics.Defaults to \_\_debezium-heartbeat. | \_\_debezium-heartbeat | String |
| **includeSchemaChanges** (sqlserver) | Whether the connector should publish changes in the database schema to a Kafka topic with the same name as the database server ID. Each schema change will be recorded using a key that contains the database name and whose value include logical description of the new schema and optionally the DDL statement(s). The default is 'true'. This is independent of how the connector internally records database schema history. | true | boolean |
| **includeSchemaComments** (sqlserver) | Whether the connector parse table and column’s comment to metadata object. Note: Enable this option will bring the implications on memory usage. The number and size of ColumnImpl objects is what largely impacts how much memory is consumed by the Debezium connectors, and adding a String to each of them can potentially be quite heavy. The default is 'false'. | false | boolean |
| **incrementalSnapshotAllowSchemaChanges** (sqlserver) | Detect schema change during an incremental snapshot and re-select a current chunk to avoid locking DDLs. Note that changes to a primary key are not supported and can cause incorrect results if performed during an incremental snapshot. Another limitation is that if a schema change affects only columns' default values, then the change won’t be detected until the DDL is processed from the binlog stream. This doesn’t affect the snapshot events' values, but the schema of snapshot events may have outdated defaults. | false | boolean |
| **incrementalSnapshotChunkSize** (sqlserver) | The maximum size of chunk (number of documents/rows) for incremental snapshotting. | 1024 | int |
| **incrementalSnapshotOptionRecompile** (sqlserver) | Add OPTION(RECOMPILE) on each SELECT statement during the incremental snapshot process. This prevents parameter sniffing but can cause CPU pressure on the source database. | false | boolean |
| **incrementalSnapshotWatermarkingStrategy** (sqlserver) | Specify the strategy used for watermarking during an incremental snapshot: 'insert\_insert' both open and close signal is written into signal data collection (default); 'insert\_delete' only open signal is written on signal data collection, the close will delete the relative open signal;. | INSERT\_INSERT | String |
| **legacySnapshotMaxThreads** (sqlserver) | When enabled, uses the legacy table-per-thread parallel snapshot algorithm. When set to false (the default), tables are split into chunks and processed across all snapshot threads, allowing for higher concurrency for snapshots. | false | boolean |
| **maxBatchSize** (sqlserver) | Maximum size of each batch of source records. Defaults to 2048. | 2048 | int |
| **maxIterationTransactions** (sqlserver) | This property can be used to reduce the connector memory usage footprint when changes are streamed from multiple tables per database. | 500 | int |
| **maxQueueSize** (sqlserver) | Maximum size of the queue for change events read from the database log but not yet recorded or forwarded. Defaults to 8192, and should always be larger than the maximum batch size. | 8192 | int |
| **maxQueueSizeInBytes** (sqlserver) | Maximum size of the queue in bytes for change events read from the database log but not yet recorded or forwarded. Defaults to 0. Mean the feature is not enabled. | 0 | long |
| **memoryManagementSchemasClass** (sqlserver) | The fully-qualified class name of the storage implementation for schema metadata. The class must implement io.debezium.relational.TableMappingStorage. Defaults to io.debezium.relational.ConcurrentMapTableMappingStorage for in-memory storage. | io.debezium.relational.ConcurrentMapTableMappingStorage | String |
| **memoryManagementTablesClass** (sqlserver) | The fully-qualified class name of the storage implementation for table metadata. The class must implement io.debezium.relational.TableMappingStorage. Defaults to io.debezium.relational.ConcurrentMapTableMappingStorage for in-memory storage. | io.debezium.relational.ConcurrentMapTableMappingStorage | String |
| **messageKeyColumns** (sqlserver) | A semicolon-separated list of expressions that match fully-qualified tables and column(s) to be used as message key. Each expression must match the pattern ':', where the table names could be defined as (DB\_NAME.TABLE\_NAME) or (SCHEMA\_NAME.TABLE\_NAME), depending on the specific connector, and the key columns are a comma-separated list of columns representing the custom key. For any table without an explicit key configuration the table’s primary key column(s) will be used as message key. Example: dbserver1.inventory.orderlines:orderId,orderLineId;dbserver1.inventory.orders:id. |  | String |
| **notificationEnabledChannels** (sqlserver) | List of notification channels names that are enabled. |  | String |
| **notificationSinkTopicName** (sqlserver) | The name of the topic for the notifications. This is required in case 'sink' is in the list of enabled channels. |  | String |
| **openlineageIntegrationConfigFilePath** (sqlserver) | Path to OpenLineage file configuration. See [https://openlineage.io/docs/client/java/configuration](https://openlineage.io/docs/client/java/configuration). | ./openlineage.yml | String |
| **openlineageIntegrationDatasetKafkaBootstrapServers** (sqlserver) | The Kafka bootstrap server address used as input/output namespace/. |  | String |
| **openlineageIntegrationEnabled** (sqlserver) | Enable Debezium to emit data lineage metadata through OpenLineage API. | false | boolean |
| **openlineageIntegrationJobDescription** (sqlserver) | The job’s description emitted by Debezium. | Debezium change data capture job | String |
| **openlineageIntegrationJobNamespace** (sqlserver) | The job’s namespace emitted by Debezium. |  | String |
| **openlineageIntegrationJobOwners** (sqlserver) | The job’s owners emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **openlineageIntegrationJobTags** (sqlserver) | The job’s tags emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **pollIntervalMs** (sqlserver) | Time to wait for new change events to appear after receiving no events, given in milliseconds. Defaults to 500 ms. | 500ms | long |
| **postProcessors** (sqlserver) | Optional list of post processors. The processors are defined using '.type' config option and configured using options ''. |  | String |
| **provideTransactionMetadata** (sqlserver) | Enables transaction metadata extraction together with event counting. | false | boolean |
| **retriableRestartConnectorWaitMs** (sqlserver) | Time to wait before restarting connector after retriable exception occurs. Defaults to 10000ms. | 10s | long |
| **schemaHistoryInternal** (sqlserver) | The name of the SchemaHistory class that should be used to store and recover database schema changes. The configuration properties for the history are prefixed with the 'schema.history.internal.' string. | io.debezium.storage.kafka.history.KafkaSchemaHistory | String |
| **schemaHistoryInternalFileFilename** (sqlserver) | The path to the file that will be used to record the database schema history. |  | String |
| **schemaHistoryInternalSkipUnparseableDdl** (sqlserver) | Controls the action Debezium will take when it meets a DDL statement in binlog, that it cannot parse.By default the connector will stop operating but by changing the setting it can ignore the statements which it cannot parse. If skipping is enabled then Debezium can miss metadata changes. | false | boolean |
| **schemaHistoryInternalStoreOnlyCapturedDatabasesDdl** (sqlserver) | Controls what DDL will Debezium store in database schema history. By default (false) Debezium will store all incoming DDL statements. If set to true, then only DDL that manipulates a table from captured schema/database will be stored. | false | boolean |
| **schemaHistoryInternalStoreOnlyCapturedTablesDdl** (sqlserver) | Controls what DDL will Debezium store in database schema history. By default (false) Debezium will store all incoming DDL statements. If set to true, then only DDL that manipulates a captured table will be stored. | false | boolean |
| **schemaNameAdjustmentMode** (sqlserver) | Specify how schema names should be adjusted for compatibility with the message converter used by the connector, including: 'avro' replaces the characters that cannot be used in the Avro type name with underscore; 'avro\_unicode' replaces the underscore or characters that cannot be used in the Avro type name with corresponding unicode like \_uxxxx. Note: \_ is an escape sequence like backslash in Java;'none' does not apply any adjustment (default). | none | String |
| **signalDataCollection** (sqlserver) | The name of the data collection that is used to send signals/commands to Debezium. For multi-partition mode connectors, multiple signal data collections can be specified as a comma-separated list. Signaling is disabled when not set. |  | String |
| **signalEnabledChannels** (sqlserver) | List of channels names that are enabled. Source channel is enabled by default. | source | String |
| **signalPollIntervalMs** (sqlserver) | Interval for looking for new signals in registered channels, given in milliseconds. Defaults to 5 seconds. | 5s | long |
| **skippedOperations** (sqlserver) | The comma-separated list of operations to skip during streaming, defined as: 'c' for inserts/create; 'u' for updates; 'd' for deletes, 't' for truncates, and 'none' to indicate nothing skipped. By default, only truncate operations will be skipped. | t | String |
| **snapshotDelayMs** (sqlserver) | A delay period before a snapshot will begin, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **snapshotFetchSize** (sqlserver) | The maximum number of records that should be loaded into memory while performing a snapshot. |  | int |
| **snapshotIncludeCollectionList** (sqlserver) | This setting must be set to specify a list of tables/collections whose snapshot must be taken on creating or restarting the connector. |  | String |
| **snapshotIsolationMode** (sqlserver) | Controls which transaction isolation level is used and how long the connector locks the captured tables. The default is 'repeatable\_read', which means that repeatable read isolation level is used. In addition, type of acquired lock during schema snapshot depends on snapshot.locking.mode property. Using a value of 'exclusive' ensures that the connector holds the type of lock specified with snapshot.locking.mode property (and thus prevents any reads and updates) for all captured tables during the entire snapshot duration. When 'snapshot' is specified, connector runs the initial snapshot in SNAPSHOT isolation level, which guarantees snapshot consistency. In addition, neither table nor row-level locks are held. When 'read\_committed' is specified, connector runs the initial snapshot in READ COMMITTED isolation level. No long-running locks are taken, so that initial snapshot does not prevent other transactions from updating table rows. Snapshot consistency is not guaranteed.In 'read\_uncommitted' mode neither table nor row-level locks are acquired, but connector does not guarantee snapshot consistency. | repeatable\_read | String |
| **snapshotLockTimeoutMs** (sqlserver) | The maximum number of millis to wait for table locks at the beginning of a snapshot. If locks cannot be acquired in this time frame, the snapshot will be aborted. Defaults to 10 seconds. | 10s | long |
| **snapshotMaxThreads** (sqlserver) | The maximum number of threads used to perform the snapshot. Defaults to 1. | 1 | int |
| **snapshotMaxThreadsMultiplier** (sqlserver) | The factor used to scale the number of snapshot chunks per table. The default behavior is to take 'row\_count/snapshot.max.threads' to compute the number of rows per chunks. This may not be ideal for larger tables, and using the multiplier, the formula is adjusted to increase the number of chunks by using 'row\_count/(snapshot.max.threads snapshot.max.threads.multiplier). | 1 | int |
| **snapshotMode** (sqlserver) | The criteria for running a snapshot upon startup of the connector. Select one of the following snapshot options: 'initial' (default): If the connector does not detect any offsets for the logical server name, it runs a snapshot that captures the current full state of the configured tables. After the snapshot completes, the connector begins to stream changes from the transaction log.; 'initial\_only': The connector performs a snapshot as it does for the 'initial' option, but after the connector completes the snapshot, it stops, and does not stream changes from the transaction log.; 'schema\_only': If the connector does not detect any offsets for the logical server name, it runs a snapshot that captures only the schema (table structures), but not any table data. After the snapshot completes, the connector begins to stream changes from the transaction log. | initial | String |
| **snapshotModeConfigurationBasedSnapshotData** (sqlserver) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnDataError** (sqlserver) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnSchemaError** (sqlserver) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotSchema** (sqlserver) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedStartStream** (sqlserver) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the stream should start or not after snapshot. | false | boolean |
| **snapshotModeCustomName** (sqlserver) | When 'snapshot.mode' is set as custom, this setting must be set to specify a the name of the custom implementation provided in the 'name()' method. The implementations must implement the 'Snapshotter' interface and is called on each app boot to determine whether to do a snapshot. |  | String |
| **snapshotSelectStatementOverrides** (sqlserver) | This property contains a comma-separated list of fully-qualified tables (DB\_NAME.TABLE\_NAME) or (SCHEMA\_NAME.TABLE\_NAME), depending on the specific connectors. Select statements for the individual tables are specified in further configuration properties, one for each table, identified by the id 'snapshot.select.statement.overrides.DB\_NAME.TABLE\_NAME' or 'snapshot.select.statement.overrides.SCHEMA\_NAME.TABLE\_NAME', respectively. The value of those properties is the select statement to use when retrieving data from the specific table during snapshotting. A possible use case for large append-only tables is setting a specific point where to start (resume) snapshotting, in case a previous snapshotting was interrupted. |  | String |
| **snapshotTablesOrderByRowCount** (sqlserver) | Controls the order in which tables are processed in the initial snapshot. A descending value will order the tables by row count descending. A ascending value will order the tables by row count ascending. A value of disabled (the default) will disable ordering by row count. | disabled | String |
| **sourceinfoStructMaker** (sqlserver) | The name of the SourceInfoStructMaker class that returns SourceInfo schema and struct. | io.debezium.connector.sqlserver.SqlServerSourceInfoStructMaker | String |
| **statisticsMetricsEnabled** (sqlserver) | Enable to collect various kind of statistics, like latencies in record processing, and derived data like quantiles. By default collecting statistics is enabled. | true | boolean |
| **streamingDelayMs** (sqlserver) | A delay period after the snapshot is completed and the streaming begins, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **streamingFetchSize** (sqlserver) | Specifies the maximum number of rows that should be read in one go from each table while streaming. The connector will read the table contents in multiple batches of this size. Defaults to 0 which means no limit. | 0 | int |
| **tableExcludeList** (sqlserver) | A comma-separated list of regular expressions that match the fully-qualified names of tables to be excluded from monitoring. |  | String |
| **tableIgnoreBuiltin** (sqlserver) | Flag specifying whether built-in tables should be ignored. | true | boolean |
| **tableIncludeList** (sqlserver) | The tables for which changes are to be captured. |  | String |
| **timePrecisionMode** (sqlserver) | Time, date, and timestamps can be represented with different kinds of precisions, including: 'adaptive' (the default) bases the precision of time, date, and timestamp values on the database column’s precision; 'adaptive\_time\_microseconds' like 'adaptive' mode, but TIME fields always use microseconds precision; 'connect' always represents time, date, and timestamp values using Kafka Connect’s built-in representations for Time, Date, and Timestamp, which uses millisecond precision regardless of the database columns' precision; 'isostring' represents time, date, and timestamp values as ISO-8601 formatted strings at the UTC time zone; 'microseconds' always represents time, date, and timestamp values using microsecond precision; 'nanoseconds' always represents time, date, and timestamp values using nanosecond precision. | adaptive | String |
| **tombstonesOnDelete** (sqlserver) | Whether delete operations should be represented by a delete event and a subsequent tombstone event (true) or only by a delete event (false). Emitting the tombstone event (the default behavior) allows Kafka to completely delete all events pertaining to the given key once the source record got deleted. | false | boolean |
| **topicNamingStrategy** (sqlserver) | The name of the TopicNamingStrategy class that should be used to determine the topic name for data change, schema change, transaction, heartbeat event etc. | io.debezium.schema.SchemaTopicNamingStrategy | String |
| **topicPrefix** (sqlserver) | **Required** Topic prefix that identifies and provides a namespace for the particular database server/cluster is capturing changes. The topic prefix should be unique across all other connectors, since it is used as a prefix for all Kafka topic names that receive events emitted by this connector. Only alphanumeric characters, hyphens, dots and underscores must be accepted. |  | String |
| **transactionMetadataFactory** (sqlserver) | Class to make transaction context & transaction struct/schemas. | io.debezium.pipeline.txmetadata.DefaultTransactionMetadataFactory | String |

## Message Headers

The Debezium SQL Server Connector component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDebeziumSourceMetadata** (consumer) Constant: [`HEADER_SOURCE_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-debezium-sqlserver/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_SOURCE_METADATA) | The metadata about the source event, for example table name, database name, log position, etc, please refer to the Debezium documentation for more info. |  | Map |
| **CamelDebeziumIdentifier** (consumer) Constant: [`HEADER_IDENTIFIER`](https://javadoc.io/doc/org.apache.camel/camel-debezium-sqlserver/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_IDENTIFIER) | The identifier of the connector, normally is this format {server-name}.{database-name}.{table-name}. |  | String |
| **CamelDebeziumKey** (consumer) Constant: [`HEADER_KEY`](https://javadoc.io/doc/org.apache.camel/camel-debezium-sqlserver/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_KEY) | The key of the event, normally is the table Primary Key. |  | Struct |
| **CamelDebeziumOperation** (consumer) Constant: [`HEADER_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-debezium-sqlserver/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_OPERATION) | If presents, the type of event operation. Values for the connector are c for create (or insert), u for update, d for delete or r for read (in the case of a initial sync) or in case of a snapshot event. |  | String |
| **CamelDebeziumTimestamp** (consumer) Constant: [`HEADER_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-debezium-sqlserver/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_TIMESTAMP) | If presents, the time (using the system clock in the JVM) at which the connector processed the event. |  | Long |
| **CamelDebeziumBefore** (consumer) Constant: [`HEADER_BEFORE`](https://javadoc.io/doc/org.apache.camel/camel-debezium-sqlserver/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_BEFORE) | If presents, contains the state of the row before the event occurred. |  | Struct |
| **CamelDebeziumDdlSQL** (consumer) Constant: [`HEADER_DDL_SQL`](https://javadoc.io/doc/org.apache.camel/camel-debezium-sqlserver/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_DDL_SQL) | If presents, the ddl sql text of the event. |  | String |

For more information about configuration: [https://debezium.io/documentation/reference/0.10/operations/embedded.html#engine-properties](https://debezium.io/documentation/reference/0.10/operations/embedded.html#engine-properties) [https://debezium.io/documentation/reference/0.10/connectors/sqlserver.html#connector-properties](https://debezium.io/documentation/reference/0.10/connectors/sqlserver.html#connector-properties)

## Usage

### Message body

If the message body is not `null` (in case of tombstones), it contains the state of the row after the event occurred. It is one of two formats:

-   `Struct`
    
-   `Map` (if you use the included Type Converter from `Struct` to `Map`)
    

See below for more details.

## Examples

### Consuming events

Here is a very simple route that you can use in order to listen to Debezium events from SQL Server connector.

-   Java
    
-   XML
    
-   YAML
    

```java
from("debezium-sqlserver:dbz-test-1?offsetStorageFileName=/usr/offset-file-1.dat&databaseHostname=localhost&databaseUser=debezium&databasePassword=dbz&databaseServerName=my-app-connector&databaseHistoryFileFilename=/usr/history-file-1.dat")
    .log("Event received from Debezium : ${body}")
    .log("    with this identifier ${headers.CamelDebeziumIdentifier}")
    .log("    with these source metadata ${headers.CamelDebeziumSourceMetadata}")
    .log("    the event occurred upon this operation '${headers.CamelDebeziumSourceOperation}'")
    .log("    on this database '${headers.CamelDebeziumSourceMetadata[db]}' and this table '${headers.CamelDebeziumSourceMetadata[table]}'")
    .log("    with the key ${headers.CamelDebeziumKey}")
    .log("    the previous value is ${headers.CamelDebeziumBefore}");
```

```xml
<route>
  <from uri="debezium-sqlserver:dbz-test-1?offsetStorageFileName=/usr/offset-file-1.dat&amp;databaseHostname=localhost&amp;databaseUser=debezium&amp;databasePassword=dbz&amp;databaseServerName=my-app-connector&amp;databaseHistoryFileFilename=/usr/history-file-1.dat"/>
  <log message="Event received from Debezium : ${body}"/>
  <log message="    with this identifier ${headers.CamelDebeziumIdentifier}"/>
  <log message="    with these source metadata ${headers.CamelDebeziumSourceMetadata}"/>
  <log message="    the event occurred upon this operation '${headers.CamelDebeziumSourceOperation}'"/>
  <log message="    on this database '${headers.CamelDebeziumSourceMetadata[db]}' and this table '${headers.CamelDebeziumSourceMetadata[table]}'"/>
  <log message="    with the key ${headers.CamelDebeziumKey}"/>
  <log message="    the previous value is ${headers.CamelDebeziumBefore}"/>
</route>
```

```yaml
- route:
    from:
      uri: debezium-sqlserver:dbz-test-1
      parameters:
        offsetStorageFileName: /usr/offset-file-1.dat
        databaseHostname: localhost
        databaseUser: debezium
        databasePassword: dbz
        databaseServerName: my-app-connector
        databaseHistoryFileFilename: /usr/history-file-1.dat
      steps:
        - log:
            message: "Event received from Debezium : ${body}"
        - log:
            message: "    with this identifier ${headers.CamelDebeziumIdentifier}"
        - log:
            message: "    with these source metadata ${headers.CamelDebeziumSourceMetadata}"
        - log:
            message: "    the event occurred upon this operation '${headers.CamelDebeziumSourceOperation}'"
        - log:
            message: "    on this database '${headers.CamelDebeziumSourceMetadata[db]}' and this table '${headers.CamelDebeziumSourceMetadata[table]}'"
        - log:
            message: "    with the key ${headers.CamelDebeziumKey}"
        - log:
            message: "    the previous value is ${headers.CamelDebeziumBefore}"
```

By default, the component will emit the events in the body and `CamelDebeziumBefore` header as [`Struct`](https://kafka.apache.org/22/javadoc/org/apache/kafka/connect/data/Struct.md) data type, the reasoning behind this, is to perceive the schema information in case is needed. However, the component as well contains a [Type Converter](../../manual/type-converter.md) that converts from default output type of [`Struct`](https://kafka.apache.org/22/javadoc/org/apache/kafka/connect/data/Struct.md) to `Map` in order to leverage Camel’s rich [Data Format](../../manual/data-format.md) types which many of them work out of box with `Map` data type. To use it, you can either add `Map.class` type when you access the message (e.g., `exchange.getIn().getBody(Map.class)`), or you can convert the body always to `Map` from the route builder by adding `.convertBodyTo(Map.class)` to your Camel Route DSL after `from` statement.

We mentioned above the schema, which can be used in case you need to perform advance data transformation and the schema is needed for that. If you choose not to convert your body to `Map`, you can obtain the schema information as [`Schema`](https://kafka.apache.org/22/javadoc/org/apache/kafka/connect/data/Schema.md) type from `Struct` like this:

_Java-only: accessing the Struct schema from a processor_

```java
from("debezium-sqlserver:[name]?[options]])
    .process(exchange -> {
        final Struct bodyValue = exchange.getIn().getBody(Struct.class);
        final Schema schemaValue = bodyValue.schema();

        log.info("Body value is : {}", bodyValue);
        log.info("With Schema : {}", schemaValue);
        log.info("And fields of : {}", schemaValue.fields());
        log.info("Field name has `{}` type", schemaValue.field("name").schema());
    });
```

> **Important**
> This component is a thin wrapper around Debezium Engine as mentioned. Therefore, before using this component in production, you need to understand how Debezium works and how configurations can reflect the expected behavior. This is especially true in regard to [handling failures](https://debezium.io/documentation/reference/1.9/operations/embedded.html#_handling_failures).