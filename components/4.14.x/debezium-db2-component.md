# Debezium DB2 Connector

**Since Camel 3.17**

**Only consumer is supported**

The Debezium db2 component is wrapper around [Debezium](https://debezium.io/) using [Debezium Engine](https://debezium.io/documentation/reference/1.8/operations/embedded.md), which enables Change Data Capture from db2 database using Debezium without the need for Kafka or Kafka Connect.

> **Note**
> **Note on handling failures:** per [Debezium Embedded Engine](https://debezium.io/documentation/reference/1.9/development/engine.html#_handling_failures) documentation, the engines are actively recording source offsets and periodically flush these offsets to a persistent storage. Therefore, when the application is restarted or crashed, the engine will resume from the last recorded offset. This means that, at normal operation, your downstream routes will receive each event exactly once. However, in case of an application crash (not having a graceful shutdown), the application will resume from the last recorded offset, which may result in receiving duplicate events immediately after the restart. Therefore, your downstream routes should be tolerant enough of such a case and deduplicate events if needed.

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-debezium-db2</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

debezium-db2:name\[?options\]

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

The Debezium DB2 Connector component supports 89 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **additionalProperties** (common) | Additional properties for debezium components in case they can’t be set directly on the camel configurations (e.g: setting Kafka Connect properties needed by Debezium engine, for example setting KafkaOffsetBackingStore), the properties have to be prefixed with additionalProperties.. E.g: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. This is a multi-value option with prefix: additionalProperties. |  | Map |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **configuration** (consumer) | Allow pre-configured Configurations to be set. |  | Db2ConnectorEmbeddedDebeziumConfiguration |
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
| **cdcChangeTablesSchema** (db2) | The name of the schema where CDC change tables are located; defaults to 'ASNCDC'. | ASNCDC | String |
| **cdcControlSchema** (db2) | The name of the schema where CDC control structures are located; defaults to 'ASNCDC'. | ASNCDC | String |
| **columnExcludeList** (db2) | Regular expressions matching columns to exclude from change events. |  | String |
| **columnIncludeList** (db2) | Regular expressions matching columns to include in change events. |  | String |
| **columnPropagateSourceType** (db2) | A comma-separated list of regular expressions matching fully-qualified names of columns that adds the columns original type and original length as parameters to the corresponding field schemas in the emitted change records. |  | String |
| **connectionValidationTimeoutMs** (db2) | The maximum time in milliseconds to wait for connection validation to complete. Defaults to 60 seconds. | 1m | long |
| **converters** (db2) | Optional list of custom converters that would be used instead of default ones. The converters are defined using '.type' config option and configured using options '.'. |  | String |
| **customMetricTags** (db2) | The custom metric tags will accept key-value pairs to customize the MBean object name which should be appended the end of regular name, each key would represent a tag for the MBean object name, and the corresponding value would be the value of that tag the key is. For example: k1=v1,k2=v2. |  | String |
| **databaseDbname** (db2) | The name of the database from which the connector should capture changes. |  | String |
| **databaseHostname** (db2) | Resolvable hostname or IP address of the database server. |  | String |
| **databasePassword** (db2) | **Required** Password of the database user to be used when connecting to the database. |  | String |
| **databasePort** (db2) | Port of the database server. | 50000 | int |
| **databaseUser** (db2) | Name of the database user to be used when connecting to the database. |  | String |
| **datatypePropagateSourceType** (db2) | A comma-separated list of regular expressions matching the database-specific data type names that adds the data type’s original type and original length as parameters to the corresponding field schemas in the emitted change records. |  | String |
| **db2Platform** (db2) | Informs connector which Db2 implementation platform it is connected to. The default is 'LUW', which means Windows, UNIX, Linux. Using a value of 'Z' ensures that the Db2 for z/OS specific SQL statements are used. | LUW | String |
| **decimalHandlingMode** (db2) | Specify how DECIMAL and NUMERIC columns should be represented in change events, including: 'precise' (the default) uses java.math.BigDecimal to represent values, which are encoded in the change events using a binary representation and Kafka Connect’s 'org.apache.kafka.connect.data.Decimal' type; 'string' uses string to represent values; 'double' represents values using Java’s 'double', which may not offer the precision but will be far easier to use in consumers. | precise | String |
| **errorsMaxRetries** (db2) | The maximum number of retries on connection errors before failing (-1 = no limit, 0 = disabled, 0 = num of retries). | \-1 | int |
| **eventProcessingFailureHandlingMode** (db2) | Specify how failures during processing of events (i.e. when encountering a corrupted event) should be handled, including: 'fail' (the default) an exception indicating the problematic event and its position is raised, causing the connector to be stopped; 'warn' the problematic event and its position will be logged and the event will be skipped; 'ignore' the problematic event will be skipped. | fail | String |
| **executorShutdownTimeoutMs** (db2) | The maximum time in milliseconds to wait for task executor to shut down. | 4s | long |
| **extendedHeadersEnabled** (db2) | Enable/Disable Debezium context headers that provides essential metadata for tracking and identifying the source of CDC events in downstream processing systems. | true | boolean |
| **heartbeatIntervalMs** (db2) | Length of an interval in milli-seconds in in which the connector periodically sends heartbeat messages to a heartbeat topic. Use 0 to disable heartbeat messages. Disabled by default. | 0ms | int |
| **heartbeatTopicsPrefix** (db2) | The prefix that is used to name heartbeat topics.Defaults to \_\_debezium-heartbeat. | \_\_debezium-heartbeat | String |
| **includeSchemaChanges** (db2) | Whether the connector should publish changes in the database schema to a Kafka topic with the same name as the database server ID. Each schema change will be recorded using a key that contains the database name and whose value include logical description of the new schema and optionally the DDL statement(s). The default is 'true'. This is independent of how the connector internally records database schema history. | true | boolean |
| **incrementalSnapshotChunkSize** (db2) | The maximum size of chunk (number of documents/rows) for incremental snapshotting. | 1024 | int |
| **incrementalSnapshotWatermarkingStrategy** (db2) | Specify the strategy used for watermarking during an incremental snapshot: 'insert\_insert' both open and close signal is written into signal data collection (default); 'insert\_delete' only open signal is written on signal data collection, the close will delete the relative open signal;. | INSERT\_INSERT | String |
| **maxBatchSize** (db2) | Maximum size of each batch of source records. Defaults to 2048. | 2048 | int |
| **maxQueueSize** (db2) | Maximum size of the queue for change events read from the database log but not yet recorded or forwarded. Defaults to 8192, and should always be larger than the maximum batch size. | 8192 | int |
| **maxQueueSizeInBytes** (db2) | Maximum size of the queue in bytes for change events read from the database log but not yet recorded or forwarded. Defaults to 0. Mean the feature is not enabled. | 0 | long |
| **messageKeyColumns** (db2) | A semicolon-separated list of expressions that match fully-qualified tables and column(s) to be used as message key. Each expression must match the pattern ':', where the table names could be defined as (DB\_NAME.TABLE\_NAME) or (SCHEMA\_NAME.TABLE\_NAME), depending on the specific connector, and the key columns are a comma-separated list of columns representing the custom key. For any table without an explicit key configuration the table’s primary key column(s) will be used as message key. Example: dbserver1.inventory.orderlines:orderId,orderLineId;dbserver1.inventory.orders:id. |  | String |
| **notificationEnabledChannels** (db2) | List of notification channels names that are enabled. |  | String |
| **notificationSinkTopicName** (db2) | The name of the topic for the notifications. This is required in case 'sink' is in the list of enabled channels. |  | String |
| **openlineageIntegrationConfigFilePath** (db2) | Path to OpenLineage file configuration. See [https://openlineage.io/docs/client/java/configuration](https://openlineage.io/docs/client/java/configuration). | ./openlineage.yml | String |
| **openlineageIntegrationEnabled** (db2) | Enable Debezium to emit data lineage metadata through OpenLineage API. | false | boolean |
| **openlineageIntegrationJobDescription** (db2) | The job’s description emitted by Debezium. | Debezium change data capture job | String |
| **openlineageIntegrationJobNamespace** (db2) | The job’s namespace emitted by Debezium. |  | String |
| **openlineageIntegrationJobOwners** (db2) | The job’s owners emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **openlineageIntegrationJobTags** (db2) | The job’s tags emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **pollIntervalMs** (db2) | Time to wait for new change events to appear after receiving no events, given in milliseconds. Defaults to 500 ms. | 500ms | long |
| **postProcessors** (db2) | Optional list of post processors. The processors are defined using '.type' config option and configured using options ''. |  | String |
| **provideTransactionMetadata** (db2) | Enables transaction metadata extraction together with event counting. | false | boolean |
| **queryFetchSize** (db2) | The maximum number of records that should be loaded into memory while streaming. A value of '0' uses the default JDBC fetch size. The default value is '10000'. | 10000 | int |
| **retriableRestartConnectorWaitMs** (db2) | Time to wait before restarting connector after retriable exception occurs. Defaults to 10000ms. | 10s | long |
| **schemaHistoryInternal** (db2) | The name of the SchemaHistory class that should be used to store and recover database schema changes. The configuration properties for the history are prefixed with the 'schema.history.internal.' string. | io.debezium.storage.kafka.history.KafkaSchemaHistory | String |
| **schemaHistoryInternalFileFilename** (db2) | The path to the file that will be used to record the database schema history. |  | String |
| **schemaHistoryInternalSkipUnparseableDdl** (db2) | Controls the action Debezium will take when it meets a DDL statement in binlog, that it cannot parse.By default the connector will stop operating but by changing the setting it can ignore the statements which it cannot parse. If skipping is enabled then Debezium can miss metadata changes. | false | boolean |
| **schemaHistoryInternalStoreOnlyCapturedDatabasesDdl** (db2) | Controls what DDL will Debezium store in database schema history. By default (false) Debezium will store all incoming DDL statements. If set to true, then only DDL that manipulates a table from captured schema/database will be stored. | false | boolean |
| **schemaHistoryInternalStoreOnlyCapturedTablesDdl** (db2) | Controls what DDL will Debezium store in database schema history. By default (false) Debezium will store all incoming DDL statements. If set to true, then only DDL that manipulates a captured table will be stored. | false | boolean |
| **schemaNameAdjustmentMode** (db2) | Specify how schema names should be adjusted for compatibility with the message converter used by the connector, including: 'avro' replaces the characters that cannot be used in the Avro type name with underscore; 'avro\_unicode' replaces the underscore or characters that cannot be used in the Avro type name with corresponding unicode like \_uxxxx. Note: \_ is an escape sequence like backslash in Java;'none' does not apply any adjustment (default). | none | String |
| **signalDataCollection** (db2) | The name of the data collection that is used to send signals/commands to Debezium. Signaling is disabled when not set. |  | String |
| **signalEnabledChannels** (db2) | List of channels names that are enabled. Source channel is enabled by default. | source | String |
| **signalPollIntervalMs** (db2) | Interval for looking for new signals in registered channels, given in milliseconds. Defaults to 5 seconds. | 5s | long |
| **skippedOperations** (db2) | The comma-separated list of operations to skip during streaming, defined as: 'c' for inserts/create; 'u' for updates; 'd' for deletes, 't' for truncates, and 'none' to indicate nothing skipped. By default, only truncate operations will be skipped. | t | String |
| **snapshotDelayMs** (db2) | A delay period before a snapshot will begin, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **snapshotFetchSize** (db2) | The maximum number of records that should be loaded into memory while performing a snapshot. |  | int |
| **snapshotIncludeCollectionList** (db2) | This setting must be set to specify a list of tables/collections whose snapshot must be taken on creating or restarting the connector. |  | String |
| **snapshotLockTimeoutMs** (db2) | The maximum number of millis to wait for table locks at the beginning of a snapshot. If locks cannot be acquired in this time frame, the snapshot will be aborted. Defaults to 10 seconds. | 10s | long |
| **snapshotMode** (db2) | The criteria for running a snapshot upon startup of the connector. Options include: 'initial' (the default) to specify the connector should run a snapshot only when no offsets are available for the logical server name; 'schema\_only' to specify the connector should run a snapshot of the schema when no offsets are available for the logical server name. | initial | String |
| **snapshotModeConfigurationBasedSnapshotData** (db2) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnDataError** (db2) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnSchemaError** (db2) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotSchema** (db2) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedStartStream** (db2) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the stream should start or not after snapshot. | false | boolean |
| **snapshotModeCustomName** (db2) | When 'snapshot.mode' is set as custom, this setting must be set to specify a the name of the custom implementation provided in the 'name()' method. The implementations must implement the 'Snapshotter' interface and is called on each app boot to determine whether to do a snapshot. |  | String |
| **snapshotSelectStatementOverrides** (db2) | This property contains a comma-separated list of fully-qualified tables (DB\_NAME.TABLE\_NAME) or (SCHEMA\_NAME.TABLE\_NAME), depending on the specific connectors. Select statements for the individual tables are specified in further configuration properties, one for each table, identified by the id 'snapshot.select.statement.overrides.DB\_NAME.TABLE\_NAME' or 'snapshot.select.statement.overrides.SCHEMA\_NAME.TABLE\_NAME', respectively. The value of those properties is the select statement to use when retrieving data from the specific table during snapshotting. A possible use case for large append-only tables is setting a specific point where to start (resume) snapshotting, in case a previous snapshotting was interrupted. |  | String |
| **snapshotTablesOrderByRowCount** (db2) | Controls the order in which tables are processed in the initial snapshot. A descending value will order the tables by row count descending. A ascending value will order the tables by row count ascending. A value of disabled (the default) will disable ordering by row count. | disabled | String |
| **sourceinfoStructMaker** (db2) | The name of the SourceInfoStructMaker class that returns SourceInfo schema and struct. | io.debezium.connector.db2.Db2SourceInfoStructMaker | String |
| **streamingDelayMs** (db2) | A delay period after the snapshot is completed and the streaming begins, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **tableExcludeList** (db2) | A comma-separated list of regular expressions that match the fully-qualified names of tables to be excluded from monitoring. |  | String |
| **tableIgnoreBuiltin** (db2) | Flag specifying whether built-in tables should be ignored. | true | boolean |
| **tableIncludeList** (db2) | The tables for which changes are to be captured. |  | String |
| **timePrecisionMode** (db2) | Time, date, and timestamps can be represented with different kinds of precisions, including: 'adaptive' (the default) bases the precision of time, date, and timestamp values on the database column’s precision; 'adaptive\_time\_microseconds' like 'adaptive' mode, but TIME fields always use microseconds precision; 'connect' always represents time, date, and timestamp values using Kafka Connect’s built-in representations for Time, Date, and Timestamp, which uses millisecond precision regardless of the database columns' precision. | adaptive | String |
| **tombstonesOnDelete** (db2) | Whether delete operations should be represented by a delete event and a subsequent tombstone event (true) or only by a delete event (false). Emitting the tombstone event (the default behavior) allows Kafka to completely delete all events pertaining to the given key once the source record got deleted. | false | boolean |
| **topicNamingStrategy** (db2) | The name of the TopicNamingStrategy class that should be used to determine the topic name for data change, schema change, transaction, heartbeat event etc. | io.debezium.schema.SchemaTopicNamingStrategy | String |
| **topicPrefix** (db2) | **Required** Topic prefix that identifies and provides a namespace for the particular database server/cluster is capturing changes. The topic prefix should be unique across all other connectors, since it is used as a prefix for all Kafka topic names that receive events emitted by this connector. Only alphanumeric characters, hyphens, dots and underscores must be accepted. |  | String |
| **transactionMetadataFactory** (db2) | Class to make transaction context & transaction struct/schemas. | io.debezium.pipeline.txmetadata.DefaultTransactionMetadataFactory | String |

## Endpoint Options

The Debezium DB2 Connector endpoint is configured using URI syntax:

debezium-db2:name

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (consumer) | **Required** Unique name for the connector. Attempting to register again with the same name will fail. |  | String |

### Query Parameters (89 parameters)

   
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
| **cdcChangeTablesSchema** (db2) | The name of the schema where CDC change tables are located; defaults to 'ASNCDC'. | ASNCDC | String |
| **cdcControlSchema** (db2) | The name of the schema where CDC control structures are located; defaults to 'ASNCDC'. | ASNCDC | String |
| **columnExcludeList** (db2) | Regular expressions matching columns to exclude from change events. |  | String |
| **columnIncludeList** (db2) | Regular expressions matching columns to include in change events. |  | String |
| **columnPropagateSourceType** (db2) | A comma-separated list of regular expressions matching fully-qualified names of columns that adds the columns original type and original length as parameters to the corresponding field schemas in the emitted change records. |  | String |
| **connectionValidationTimeoutMs** (db2) | The maximum time in milliseconds to wait for connection validation to complete. Defaults to 60 seconds. | 1m | long |
| **converters** (db2) | Optional list of custom converters that would be used instead of default ones. The converters are defined using '.type' config option and configured using options '.'. |  | String |
| **customMetricTags** (db2) | The custom metric tags will accept key-value pairs to customize the MBean object name which should be appended the end of regular name, each key would represent a tag for the MBean object name, and the corresponding value would be the value of that tag the key is. For example: k1=v1,k2=v2. |  | String |
| **databaseDbname** (db2) | The name of the database from which the connector should capture changes. |  | String |
| **databaseHostname** (db2) | Resolvable hostname or IP address of the database server. |  | String |
| **databasePassword** (db2) | **Required** Password of the database user to be used when connecting to the database. |  | String |
| **databasePort** (db2) | Port of the database server. | 50000 | int |
| **databaseUser** (db2) | Name of the database user to be used when connecting to the database. |  | String |
| **datatypePropagateSourceType** (db2) | A comma-separated list of regular expressions matching the database-specific data type names that adds the data type’s original type and original length as parameters to the corresponding field schemas in the emitted change records. |  | String |
| **db2Platform** (db2) | Informs connector which Db2 implementation platform it is connected to. The default is 'LUW', which means Windows, UNIX, Linux. Using a value of 'Z' ensures that the Db2 for z/OS specific SQL statements are used. | LUW | String |
| **decimalHandlingMode** (db2) | Specify how DECIMAL and NUMERIC columns should be represented in change events, including: 'precise' (the default) uses java.math.BigDecimal to represent values, which are encoded in the change events using a binary representation and Kafka Connect’s 'org.apache.kafka.connect.data.Decimal' type; 'string' uses string to represent values; 'double' represents values using Java’s 'double', which may not offer the precision but will be far easier to use in consumers. | precise | String |
| **errorsMaxRetries** (db2) | The maximum number of retries on connection errors before failing (-1 = no limit, 0 = disabled, 0 = num of retries). | \-1 | int |
| **eventProcessingFailureHandlingMode** (db2) | Specify how failures during processing of events (i.e. when encountering a corrupted event) should be handled, including: 'fail' (the default) an exception indicating the problematic event and its position is raised, causing the connector to be stopped; 'warn' the problematic event and its position will be logged and the event will be skipped; 'ignore' the problematic event will be skipped. | fail | String |
| **executorShutdownTimeoutMs** (db2) | The maximum time in milliseconds to wait for task executor to shut down. | 4s | long |
| **extendedHeadersEnabled** (db2) | Enable/Disable Debezium context headers that provides essential metadata for tracking and identifying the source of CDC events in downstream processing systems. | true | boolean |
| **heartbeatIntervalMs** (db2) | Length of an interval in milli-seconds in in which the connector periodically sends heartbeat messages to a heartbeat topic. Use 0 to disable heartbeat messages. Disabled by default. | 0ms | int |
| **heartbeatTopicsPrefix** (db2) | The prefix that is used to name heartbeat topics.Defaults to \_\_debezium-heartbeat. | \_\_debezium-heartbeat | String |
| **includeSchemaChanges** (db2) | Whether the connector should publish changes in the database schema to a Kafka topic with the same name as the database server ID. Each schema change will be recorded using a key that contains the database name and whose value include logical description of the new schema and optionally the DDL statement(s). The default is 'true'. This is independent of how the connector internally records database schema history. | true | boolean |
| **incrementalSnapshotChunkSize** (db2) | The maximum size of chunk (number of documents/rows) for incremental snapshotting. | 1024 | int |
| **incrementalSnapshotWatermarkingStrategy** (db2) | Specify the strategy used for watermarking during an incremental snapshot: 'insert\_insert' both open and close signal is written into signal data collection (default); 'insert\_delete' only open signal is written on signal data collection, the close will delete the relative open signal;. | INSERT\_INSERT | String |
| **maxBatchSize** (db2) | Maximum size of each batch of source records. Defaults to 2048. | 2048 | int |
| **maxQueueSize** (db2) | Maximum size of the queue for change events read from the database log but not yet recorded or forwarded. Defaults to 8192, and should always be larger than the maximum batch size. | 8192 | int |
| **maxQueueSizeInBytes** (db2) | Maximum size of the queue in bytes for change events read from the database log but not yet recorded or forwarded. Defaults to 0. Mean the feature is not enabled. | 0 | long |
| **messageKeyColumns** (db2) | A semicolon-separated list of expressions that match fully-qualified tables and column(s) to be used as message key. Each expression must match the pattern ':', where the table names could be defined as (DB\_NAME.TABLE\_NAME) or (SCHEMA\_NAME.TABLE\_NAME), depending on the specific connector, and the key columns are a comma-separated list of columns representing the custom key. For any table without an explicit key configuration the table’s primary key column(s) will be used as message key. Example: dbserver1.inventory.orderlines:orderId,orderLineId;dbserver1.inventory.orders:id. |  | String |
| **notificationEnabledChannels** (db2) | List of notification channels names that are enabled. |  | String |
| **notificationSinkTopicName** (db2) | The name of the topic for the notifications. This is required in case 'sink' is in the list of enabled channels. |  | String |
| **openlineageIntegrationConfigFilePath** (db2) | Path to OpenLineage file configuration. See [https://openlineage.io/docs/client/java/configuration](https://openlineage.io/docs/client/java/configuration). | ./openlineage.yml | String |
| **openlineageIntegrationEnabled** (db2) | Enable Debezium to emit data lineage metadata through OpenLineage API. | false | boolean |
| **openlineageIntegrationJobDescription** (db2) | The job’s description emitted by Debezium. | Debezium change data capture job | String |
| **openlineageIntegrationJobNamespace** (db2) | The job’s namespace emitted by Debezium. |  | String |
| **openlineageIntegrationJobOwners** (db2) | The job’s owners emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **openlineageIntegrationJobTags** (db2) | The job’s tags emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **pollIntervalMs** (db2) | Time to wait for new change events to appear after receiving no events, given in milliseconds. Defaults to 500 ms. | 500ms | long |
| **postProcessors** (db2) | Optional list of post processors. The processors are defined using '.type' config option and configured using options ''. |  | String |
| **provideTransactionMetadata** (db2) | Enables transaction metadata extraction together with event counting. | false | boolean |
| **queryFetchSize** (db2) | The maximum number of records that should be loaded into memory while streaming. A value of '0' uses the default JDBC fetch size. The default value is '10000'. | 10000 | int |
| **retriableRestartConnectorWaitMs** (db2) | Time to wait before restarting connector after retriable exception occurs. Defaults to 10000ms. | 10s | long |
| **schemaHistoryInternal** (db2) | The name of the SchemaHistory class that should be used to store and recover database schema changes. The configuration properties for the history are prefixed with the 'schema.history.internal.' string. | io.debezium.storage.kafka.history.KafkaSchemaHistory | String |
| **schemaHistoryInternalFileFilename** (db2) | The path to the file that will be used to record the database schema history. |  | String |
| **schemaHistoryInternalSkipUnparseableDdl** (db2) | Controls the action Debezium will take when it meets a DDL statement in binlog, that it cannot parse.By default the connector will stop operating but by changing the setting it can ignore the statements which it cannot parse. If skipping is enabled then Debezium can miss metadata changes. | false | boolean |
| **schemaHistoryInternalStoreOnlyCapturedDatabasesDdl** (db2) | Controls what DDL will Debezium store in database schema history. By default (false) Debezium will store all incoming DDL statements. If set to true, then only DDL that manipulates a table from captured schema/database will be stored. | false | boolean |
| **schemaHistoryInternalStoreOnlyCapturedTablesDdl** (db2) | Controls what DDL will Debezium store in database schema history. By default (false) Debezium will store all incoming DDL statements. If set to true, then only DDL that manipulates a captured table will be stored. | false | boolean |
| **schemaNameAdjustmentMode** (db2) | Specify how schema names should be adjusted for compatibility with the message converter used by the connector, including: 'avro' replaces the characters that cannot be used in the Avro type name with underscore; 'avro\_unicode' replaces the underscore or characters that cannot be used in the Avro type name with corresponding unicode like \_uxxxx. Note: \_ is an escape sequence like backslash in Java;'none' does not apply any adjustment (default). | none | String |
| **signalDataCollection** (db2) | The name of the data collection that is used to send signals/commands to Debezium. Signaling is disabled when not set. |  | String |
| **signalEnabledChannels** (db2) | List of channels names that are enabled. Source channel is enabled by default. | source | String |
| **signalPollIntervalMs** (db2) | Interval for looking for new signals in registered channels, given in milliseconds. Defaults to 5 seconds. | 5s | long |
| **skippedOperations** (db2) | The comma-separated list of operations to skip during streaming, defined as: 'c' for inserts/create; 'u' for updates; 'd' for deletes, 't' for truncates, and 'none' to indicate nothing skipped. By default, only truncate operations will be skipped. | t | String |
| **snapshotDelayMs** (db2) | A delay period before a snapshot will begin, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **snapshotFetchSize** (db2) | The maximum number of records that should be loaded into memory while performing a snapshot. |  | int |
| **snapshotIncludeCollectionList** (db2) | This setting must be set to specify a list of tables/collections whose snapshot must be taken on creating or restarting the connector. |  | String |
| **snapshotLockTimeoutMs** (db2) | The maximum number of millis to wait for table locks at the beginning of a snapshot. If locks cannot be acquired in this time frame, the snapshot will be aborted. Defaults to 10 seconds. | 10s | long |
| **snapshotMode** (db2) | The criteria for running a snapshot upon startup of the connector. Options include: 'initial' (the default) to specify the connector should run a snapshot only when no offsets are available for the logical server name; 'schema\_only' to specify the connector should run a snapshot of the schema when no offsets are available for the logical server name. | initial | String |
| **snapshotModeConfigurationBasedSnapshotData** (db2) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnDataError** (db2) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotOnSchemaError** (db2) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not in case of error. | false | boolean |
| **snapshotModeConfigurationBasedSnapshotSchema** (db2) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not. | false | boolean |
| **snapshotModeConfigurationBasedStartStream** (db2) | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the stream should start or not after snapshot. | false | boolean |
| **snapshotModeCustomName** (db2) | When 'snapshot.mode' is set as custom, this setting must be set to specify a the name of the custom implementation provided in the 'name()' method. The implementations must implement the 'Snapshotter' interface and is called on each app boot to determine whether to do a snapshot. |  | String |
| **snapshotSelectStatementOverrides** (db2) | This property contains a comma-separated list of fully-qualified tables (DB\_NAME.TABLE\_NAME) or (SCHEMA\_NAME.TABLE\_NAME), depending on the specific connectors. Select statements for the individual tables are specified in further configuration properties, one for each table, identified by the id 'snapshot.select.statement.overrides.DB\_NAME.TABLE\_NAME' or 'snapshot.select.statement.overrides.SCHEMA\_NAME.TABLE\_NAME', respectively. The value of those properties is the select statement to use when retrieving data from the specific table during snapshotting. A possible use case for large append-only tables is setting a specific point where to start (resume) snapshotting, in case a previous snapshotting was interrupted. |  | String |
| **snapshotTablesOrderByRowCount** (db2) | Controls the order in which tables are processed in the initial snapshot. A descending value will order the tables by row count descending. A ascending value will order the tables by row count ascending. A value of disabled (the default) will disable ordering by row count. | disabled | String |
| **sourceinfoStructMaker** (db2) | The name of the SourceInfoStructMaker class that returns SourceInfo schema and struct. | io.debezium.connector.db2.Db2SourceInfoStructMaker | String |
| **streamingDelayMs** (db2) | A delay period after the snapshot is completed and the streaming begins, given in milliseconds. Defaults to 0 ms. | 0ms | long |
| **tableExcludeList** (db2) | A comma-separated list of regular expressions that match the fully-qualified names of tables to be excluded from monitoring. |  | String |
| **tableIgnoreBuiltin** (db2) | Flag specifying whether built-in tables should be ignored. | true | boolean |
| **tableIncludeList** (db2) | The tables for which changes are to be captured. |  | String |
| **timePrecisionMode** (db2) | Time, date, and timestamps can be represented with different kinds of precisions, including: 'adaptive' (the default) bases the precision of time, date, and timestamp values on the database column’s precision; 'adaptive\_time\_microseconds' like 'adaptive' mode, but TIME fields always use microseconds precision; 'connect' always represents time, date, and timestamp values using Kafka Connect’s built-in representations for Time, Date, and Timestamp, which uses millisecond precision regardless of the database columns' precision. | adaptive | String |
| **tombstonesOnDelete** (db2) | Whether delete operations should be represented by a delete event and a subsequent tombstone event (true) or only by a delete event (false). Emitting the tombstone event (the default behavior) allows Kafka to completely delete all events pertaining to the given key once the source record got deleted. | false | boolean |
| **topicNamingStrategy** (db2) | The name of the TopicNamingStrategy class that should be used to determine the topic name for data change, schema change, transaction, heartbeat event etc. | io.debezium.schema.SchemaTopicNamingStrategy | String |
| **topicPrefix** (db2) | **Required** Topic prefix that identifies and provides a namespace for the particular database server/cluster is capturing changes. The topic prefix should be unique across all other connectors, since it is used as a prefix for all Kafka topic names that receive events emitted by this connector. Only alphanumeric characters, hyphens, dots and underscores must be accepted. |  | String |
| **transactionMetadataFactory** (db2) | Class to make transaction context & transaction struct/schemas. | io.debezium.pipeline.txmetadata.DefaultTransactionMetadataFactory | String |

For more information about configuration: [https://debezium.io/documentation/reference/1.8/operations/embedded.html#engine-properties](https://debezium.io/documentation/reference/1.18/operations/embedded.html#engine-properties) [https://debezium.io/documentation/reference/1.8/connectors/db2.html#connector-properties](https://debezium.io/documentation/reference/1.18/connectors/db2ql.html#connector-properties)

## Message Headers

The Debezium DB2 Connector component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDebeziumSourceMetadata** (consumer) Constant: [`HEADER_SOURCE_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-debezium-db2/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_SOURCE_METADATA) | The metadata about the source event, for example table name, database name, log position, etc, please refer to the Debezium documentation for more info. |  | Map |
| **CamelDebeziumIdentifier** (consumer) Constant: [`HEADER_IDENTIFIER`](https://javadoc.io/doc/org.apache.camel/camel-debezium-db2/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_IDENTIFIER) | The identifier of the connector, normally is this format {server-name}.{database-name}.{table-name}. |  | String |
| **CamelDebeziumKey** (consumer) Constant: [`HEADER_KEY`](https://javadoc.io/doc/org.apache.camel/camel-debezium-db2/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_KEY) | The key of the event, normally is the table Primary Key. |  | Struct |
| **CamelDebeziumOperation** (consumer) Constant: [`HEADER_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-debezium-db2/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_OPERATION) | If presents, the type of event operation. Values for the connector are c for create (or insert), u for update, d for delete or r for read (in the case of a initial sync) or in case of a snapshot event. |  | String |
| **CamelDebeziumTimestamp** (consumer) Constant: [`HEADER_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-debezium-db2/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_TIMESTAMP) | If presents, the time (using the system clock in the JVM) at which the connector processed the event. |  | Long |
| **CamelDebeziumBefore** (consumer) Constant: [`HEADER_BEFORE`](https://javadoc.io/doc/org.apache.camel/camel-debezium-db2/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_BEFORE) | If presents, contains the state of the row before the event occurred. |  | Struct |
| **CamelDebeziumDdlSQL** (consumer) Constant: [`HEADER_DDL_SQL`](https://javadoc.io/doc/org.apache.camel/camel-debezium-db2/latest/org/apache/camel/component/debezium/DebeziumConstants.html#HEADER_DDL_SQL) | If presents, the ddl sql text of the event. |  | String |

## Message body

The message body if is not `null` (in case of tombstones), it contains the state of the row after the event occurred as `Struct` format or `Map` format if you use the included Type Converter from `Struct` to `Map` (please look below for more explanation).

## Examples

### Consuming events

Here is a basic route that you can use to listen to Debezium events from the db2 connector:

```java
from("debezium-db2:dbz-test-1?offsetStorageFileName=/usr/offset-file-1.dat&databaseHostname=localhost&databaseUser=debezium&databasePassword=dbz&databaseServerName=my-app-connector&databaseHistoryFileFilename=/usr/history-file-1.dat")
    .log("Event received from Debezium : ${body}")
    .log("    with this identifier ${headers.CamelDebeziumIdentifier}")
    .log("    with these source metadata ${headers.CamelDebeziumSourceMetadata}")
    .log("    the event occurred upon this operation '${headers.CamelDebeziumSourceOperation}'")
    .log("    on this database '${headers.CamelDebeziumSourceMetadata[db]}' and this table '${headers.CamelDebeziumSourceMetadata[table]}'")
    .log("    with the key ${headers.CamelDebeziumKey}")
    .log("    the previous value is ${headers.CamelDebeziumBefore}")
```

By default, the component will emit the events in the body and `CamelDebeziumBefore` header as [`Struct`](https://kafka.apache.org/22/javadoc/org/apache/kafka/connect/data/Struct.md) data type, the reasoning behind this, is to perceive the schema information in case is needed. However, the component as well contains a [Type Converter](../../manual/type-converter.md) that converts from default output type of [`Struct`](https://kafka.apache.org/22/javadoc/org/apache/kafka/connect/data/Struct.md) to `Map` in order to leverage Camel’s rich [Data Format](../../manual/data-format.md) types which many of them work out of box with `Map` data type. To use it, you can either add `Map.class` type when you access the message (e.g., `exchange.getIn().getBody(Map.class)`), or you can convert the body always to `Map` from the route builder by adding `.convertBodyTo(Map.class)` to your Camel Route DSL after `from` statement.

We mentioned above the schema, which can be used in case you need to perform advance data transformation and the schema is needed for that. If you choose not to convert your body to `Map`, you can obtain the schema information as [`Schema`](https://kafka.apache.org/22/javadoc/org/apache/kafka/connect/data/Schema.md) type from `Struct` like this:

```java
from("debezium-db2:[name]?[options]])
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
> This component is a thin wrapper around Debezium Engine as mentioned. Therefore, before using this component in production, you need to understand how Debezium works and how configurations can reflect the expected behavior. This is especially true in regard to [handling failures](https://debezium.io/documentation/reference/1.8/operations/embedded.html#_handling_failures).

## Spring Boot Auto-Configuration

When using debezium-db2 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-debezium-db2-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 90 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.debezium-db2.additional-properties** | Additional properties for debezium components in case they can’t be set directly on the camel configurations (e.g: setting Kafka Connect properties needed by Debezium engine, for example setting KafkaOffsetBackingStore), the properties have to be prefixed with additionalProperties.. E.g: additionalProperties.transactional.id=12345&additionalProperties.schema.registry.url=http://localhost:8811/avro. This is a multi-value option with prefix: additionalProperties. |  | Map |
| **camel.component.debezium-db2.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.debezium-db2.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.debezium-db2.cdc-change-tables-schema** | The name of the schema where CDC change tables are located; defaults to 'ASNCDC'. | ASNCDC | String |
| **camel.component.debezium-db2.cdc-control-schema** | The name of the schema where CDC control structures are located; defaults to 'ASNCDC'. | ASNCDC | String |
| **camel.component.debezium-db2.column-exclude-list** | Regular expressions matching columns to exclude from change events. |  | String |
| **camel.component.debezium-db2.column-include-list** | Regular expressions matching columns to include in change events. |  | String |
| **camel.component.debezium-db2.column-propagate-source-type** | A comma-separated list of regular expressions matching fully-qualified names of columns that adds the columns original type and original length as parameters to the corresponding field schemas in the emitted change records. |  | String |
| **camel.component.debezium-db2.configuration** | Allow pre-configured Configurations to be set. The option is a org.apache.camel.component.debezium.db2.configuration.Db2ConnectorEmbeddedDebeziumConfiguration type. |  | Db2ConnectorEmbeddedDebeziumConfiguration |
| **camel.component.debezium-db2.connection-validation-timeout-ms** | The maximum time in milliseconds to wait for connection validation to complete. Defaults to 60 seconds. The option is a long type. | 60000 | Long |
| **camel.component.debezium-db2.converters** | Optional list of custom converters that would be used instead of default ones. The converters are defined using '.type' config option and configured using options '.'. |  | String |
| **camel.component.debezium-db2.custom-metric-tags** | The custom metric tags will accept key-value pairs to customize the MBean object name which should be appended the end of regular name, each key would represent a tag for the MBean object name, and the corresponding value would be the value of that tag the key is. For example: k1=v1,k2=v2. |  | String |
| **camel.component.debezium-db2.database-dbname** | The name of the database from which the connector should capture changes. |  | String |
| **camel.component.debezium-db2.database-hostname** | Resolvable hostname or IP address of the database server. |  | String |
| **camel.component.debezium-db2.database-password** | Password of the database user to be used when connecting to the database. |  | String |
| **camel.component.debezium-db2.database-port** | Port of the database server. | 50000 | Integer |
| **camel.component.debezium-db2.database-user** | Name of the database user to be used when connecting to the database. |  | String |
| **camel.component.debezium-db2.datatype-propagate-source-type** | A comma-separated list of regular expressions matching the database-specific data type names that adds the data type’s original type and original length as parameters to the corresponding field schemas in the emitted change records. |  | String |
| **camel.component.debezium-db2.db2-platform** | Informs connector which Db2 implementation platform it is connected to. The default is 'LUW', which means Windows, UNIX, Linux. Using a value of 'Z' ensures that the Db2 for z/OS specific SQL statements are used. | LUW | String |
| **camel.component.debezium-db2.decimal-handling-mode** | Specify how DECIMAL and NUMERIC columns should be represented in change events, including: 'precise' (the default) uses java.math.BigDecimal to represent values, which are encoded in the change events using a binary representation and Kafka Connect’s 'org.apache.kafka.connect.data.Decimal' type; 'string' uses string to represent values; 'double' represents values using Java’s 'double', which may not offer the precision but will be far easier to use in consumers. | precise | String |
| **camel.component.debezium-db2.enabled** | Whether to enable auto configuration of the debezium-db2 component. This is enabled by default. |  | Boolean |
| **camel.component.debezium-db2.errors-max-retries** | The maximum number of retries on connection errors before failing (-1 = no limit, 0 = disabled, 0 = num of retries). | \-1 | Integer |
| **camel.component.debezium-db2.event-processing-failure-handling-mode** | Specify how failures during processing of events (i.e. when encountering a corrupted event) should be handled, including: 'fail' (the default) an exception indicating the problematic event and its position is raised, causing the connector to be stopped; 'warn' the problematic event and its position will be logged and the event will be skipped; 'ignore' the problematic event will be skipped. | fail | String |
| **camel.component.debezium-db2.executor-shutdown-timeout-ms** | The maximum time in milliseconds to wait for task executor to shut down. The option is a long type. | 4000 | Long |
| **camel.component.debezium-db2.extended-headers-enabled** | Enable/Disable Debezium context headers that provides essential metadata for tracking and identifying the source of CDC events in downstream processing systems. | true | Boolean |
| **camel.component.debezium-db2.heartbeat-interval-ms** | Length of an interval in milli-seconds in in which the connector periodically sends heartbeat messages to a heartbeat topic. Use 0 to disable heartbeat messages. Disabled by default. The option is a int type. | 0 | Integer |
| **camel.component.debezium-db2.heartbeat-topics-prefix** | The prefix that is used to name heartbeat topics.Defaults to \_\_debezium-heartbeat. | \_\_debezium-heartbeat | String |
| **camel.component.debezium-db2.include-schema-changes** | Whether the connector should publish changes in the database schema to a Kafka topic with the same name as the database server ID. Each schema change will be recorded using a key that contains the database name and whose value include logical description of the new schema and optionally the DDL statement(s). The default is 'true'. This is independent of how the connector internally records database schema history. | true | Boolean |
| **camel.component.debezium-db2.incremental-snapshot-chunk-size** | The maximum size of chunk (number of documents/rows) for incremental snapshotting. | 1024 | Integer |
| **camel.component.debezium-db2.incremental-snapshot-watermarking-strategy** | Specify the strategy used for watermarking during an incremental snapshot: 'insert\_insert' both open and close signal is written into signal data collection (default); 'insert\_delete' only open signal is written on signal data collection, the close will delete the relative open signal;. | INSERT\_INSERT | String |
| **camel.component.debezium-db2.internal-key-converter** | The Converter class that should be used to serialize and deserialize key data for offsets. The default is JSON converter. | org.apache.kafka.connect.json.JsonConverter | String |
| **camel.component.debezium-db2.internal-value-converter** | The Converter class that should be used to serialize and deserialize value data for offsets. The default is JSON converter. | org.apache.kafka.connect.json.JsonConverter | String |
| **camel.component.debezium-db2.max-batch-size** | Maximum size of each batch of source records. Defaults to 2048. | 2048 | Integer |
| **camel.component.debezium-db2.max-queue-size** | Maximum size of the queue for change events read from the database log but not yet recorded or forwarded. Defaults to 8192, and should always be larger than the maximum batch size. | 8192 | Integer |
| **camel.component.debezium-db2.max-queue-size-in-bytes** | Maximum size of the queue in bytes for change events read from the database log but not yet recorded or forwarded. Defaults to 0. Mean the feature is not enabled. | 0 | Long |
| **camel.component.debezium-db2.message-key-columns** | A semicolon-separated list of expressions that match fully-qualified tables and column(s) to be used as message key. Each expression must match the pattern ':', where the table names could be defined as (DB\_NAME.TABLE\_NAME) or (SCHEMA\_NAME.TABLE\_NAME), depending on the specific connector, and the key columns are a comma-separated list of columns representing the custom key. For any table without an explicit key configuration the table’s primary key column(s) will be used as message key. Example: dbserver1.inventory.orderlines:orderId,orderLineId;dbserver1.inventory.orders:id. |  | String |
| **camel.component.debezium-db2.notification-enabled-channels** | List of notification channels names that are enabled. |  | String |
| **camel.component.debezium-db2.notification-sink-topic-name** | The name of the topic for the notifications. This is required in case 'sink' is in the list of enabled channels. |  | String |
| **camel.component.debezium-db2.offset-commit-policy** | The name of the Java class of the commit policy. It defines when offsets commit has to be triggered based on the number of events processed and the time elapsed since the last commit. This class must implement the interface 'OffsetCommitPolicy'. The default is a periodic commit policy based upon time intervals. |  | String |
| **camel.component.debezium-db2.offset-commit-timeout-ms** | Maximum number of milliseconds to wait for records to flush and partition offset data to be committed to offset storage before cancelling the process and restoring the offset data to be committed in a future attempt. The default is 5 seconds. The option is a long type. | 5000 | Long |
| **camel.component.debezium-db2.offset-flush-interval-ms** | Interval at which to try committing offsets. The default is 1 minute. The option is a long type. | 60000 | Long |
| **camel.component.debezium-db2.offset-storage** | The name of the Java class that is responsible for persistence of connector offsets. | org.apache.kafka.connect.storage.FileOffsetBackingStore | String |
| **camel.component.debezium-db2.offset-storage-file-name** | Path to file where offsets are to be stored. Required when offset.storage is set to the FileOffsetBackingStore. |  | String |
| **camel.component.debezium-db2.offset-storage-partitions** | The number of partitions used when creating the offset storage topic. Required when offset.storage is set to the 'KafkaOffsetBackingStore'. |  | Integer |
| **camel.component.debezium-db2.offset-storage-replication-factor** | Replication factor used when creating the offset storage topic. Required when offset.storage is set to the KafkaOffsetBackingStore. |  | Integer |
| **camel.component.debezium-db2.offset-storage-topic** | The name of the Kafka topic where offsets are to be stored. Required when offset.storage is set to the KafkaOffsetBackingStore. |  | String |
| **camel.component.debezium-db2.openlineage-integration-config-file-path** | Path to OpenLineage file configuration. See [https://openlineage.io/docs/client/java/configuration](https://openlineage.io/docs/client/java/configuration). | ./openlineage.yml | String |
| **camel.component.debezium-db2.openlineage-integration-enabled** | Enable Debezium to emit data lineage metadata through OpenLineage API. | false | Boolean |
| **camel.component.debezium-db2.openlineage-integration-job-description** | The job’s description emitted by Debezium. | Debezium change data capture job | String |
| **camel.component.debezium-db2.openlineage-integration-job-namespace** | The job’s namespace emitted by Debezium. |  | String |
| **camel.component.debezium-db2.openlineage-integration-job-owners** | The job’s owners emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **camel.component.debezium-db2.openlineage-integration-job-tags** | The job’s tags emitted by Debezium. A comma-separated list of key-value pairs.For example: k1=v1,k2=v2. |  | String |
| **camel.component.debezium-db2.poll-interval-ms** | Time to wait for new change events to appear after receiving no events, given in milliseconds. Defaults to 500 ms. The option is a long type. | 500 | Long |
| **camel.component.debezium-db2.post-processors** | Optional list of post processors. The processors are defined using '.type' config option and configured using options ''. |  | String |
| **camel.component.debezium-db2.provide-transaction-metadata** | Enables transaction metadata extraction together with event counting. | false | Boolean |
| **camel.component.debezium-db2.query-fetch-size** | The maximum number of records that should be loaded into memory while streaming. A value of '0' uses the default JDBC fetch size. The default value is '10000'. | 10000 | Integer |
| **camel.component.debezium-db2.retriable-restart-connector-wait-ms** | Time to wait before restarting connector after retriable exception occurs. Defaults to 10000ms. The option is a long type. | 10000 | Long |
| **camel.component.debezium-db2.schema-history-internal** | The name of the SchemaHistory class that should be used to store and recover database schema changes. The configuration properties for the history are prefixed with the 'schema.history.internal.' string. | io.debezium.storage.kafka.history.KafkaSchemaHistory | String |
| **camel.component.debezium-db2.schema-history-internal-file-filename** | The path to the file that will be used to record the database schema history. |  | String |
| **camel.component.debezium-db2.schema-history-internal-skip-unparseable-ddl** | Controls the action Debezium will take when it meets a DDL statement in binlog, that it cannot parse.By default the connector will stop operating but by changing the setting it can ignore the statements which it cannot parse. If skipping is enabled then Debezium can miss metadata changes. | false | Boolean |
| **camel.component.debezium-db2.schema-history-internal-store-only-captured-databases-ddl** | Controls what DDL will Debezium store in database schema history. By default (false) Debezium will store all incoming DDL statements. If set to true, then only DDL that manipulates a table from captured schema/database will be stored. | false | Boolean |
| **camel.component.debezium-db2.schema-history-internal-store-only-captured-tables-ddl** | Controls what DDL will Debezium store in database schema history. By default (false) Debezium will store all incoming DDL statements. If set to true, then only DDL that manipulates a captured table will be stored. | false | Boolean |
| **camel.component.debezium-db2.schema-name-adjustment-mode** | Specify how schema names should be adjusted for compatibility with the message converter used by the connector, including: 'avro' replaces the characters that cannot be used in the Avro type name with underscore; 'avro\_unicode' replaces the underscore or characters that cannot be used in the Avro type name with corresponding unicode like \_uxxxx. Note: \_ is an escape sequence like backslash in Java;'none' does not apply any adjustment (default). | none | String |
| **camel.component.debezium-db2.signal-data-collection** | The name of the data collection that is used to send signals/commands to Debezium. Signaling is disabled when not set. |  | String |
| **camel.component.debezium-db2.signal-enabled-channels** | List of channels names that are enabled. Source channel is enabled by default. | source | String |
| **camel.component.debezium-db2.signal-poll-interval-ms** | Interval for looking for new signals in registered channels, given in milliseconds. Defaults to 5 seconds. The option is a long type. | 5000 | Long |
| **camel.component.debezium-db2.skipped-operations** | The comma-separated list of operations to skip during streaming, defined as: 'c' for inserts/create; 'u' for updates; 'd' for deletes, 't' for truncates, and 'none' to indicate nothing skipped. By default, only truncate operations will be skipped. | t | String |
| **camel.component.debezium-db2.snapshot-delay-ms** | A delay period before a snapshot will begin, given in milliseconds. Defaults to 0 ms. The option is a long type. | 0 | Long |
| **camel.component.debezium-db2.snapshot-fetch-size** | The maximum number of records that should be loaded into memory while performing a snapshot. |  | Integer |
| **camel.component.debezium-db2.snapshot-include-collection-list** | This setting must be set to specify a list of tables/collections whose snapshot must be taken on creating or restarting the connector. |  | String |
| **camel.component.debezium-db2.snapshot-lock-timeout-ms** | The maximum number of millis to wait for table locks at the beginning of a snapshot. If locks cannot be acquired in this time frame, the snapshot will be aborted. Defaults to 10 seconds. The option is a long type. | 10000 | Long |
| **camel.component.debezium-db2.snapshot-mode** | The criteria for running a snapshot upon startup of the connector. Options include: 'initial' (the default) to specify the connector should run a snapshot only when no offsets are available for the logical server name; 'schema\_only' to specify the connector should run a snapshot of the schema when no offsets are available for the logical server name. | initial | String |
| **camel.component.debezium-db2.snapshot-mode-configuration-based-snapshot-data** | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not. | false | Boolean |
| **camel.component.debezium-db2.snapshot-mode-configuration-based-snapshot-on-data-error** | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the data should be snapshotted or not in case of error. | false | Boolean |
| **camel.component.debezium-db2.snapshot-mode-configuration-based-snapshot-on-schema-error** | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not in case of error. | false | Boolean |
| **camel.component.debezium-db2.snapshot-mode-configuration-based-snapshot-schema** | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the schema should be snapshotted or not. | false | Boolean |
| **camel.component.debezium-db2.snapshot-mode-configuration-based-start-stream** | When 'snapshot.mode' is set as configuration\_based, this setting permits to specify whenever the stream should start or not after snapshot. | false | Boolean |
| **camel.component.debezium-db2.snapshot-mode-custom-name** | When 'snapshot.mode' is set as custom, this setting must be set to specify a the name of the custom implementation provided in the 'name()' method. The implementations must implement the 'Snapshotter' interface and is called on each app boot to determine whether to do a snapshot. |  | String |
| **camel.component.debezium-db2.snapshot-select-statement-overrides** | This property contains a comma-separated list of fully-qualified tables (DB\_NAME.TABLE\_NAME) or (SCHEMA\_NAME.TABLE\_NAME), depending on the specific connectors. Select statements for the individual tables are specified in further configuration properties, one for each table, identified by the id 'snapshot.select.statement.overrides.DB\_NAME.TABLE\_NAME' or 'snapshot.select.statement.overrides.SCHEMA\_NAME.TABLE\_NAME', respectively. The value of those properties is the select statement to use when retrieving data from the specific table during snapshotting. A possible use case for large append-only tables is setting a specific point where to start (resume) snapshotting, in case a previous snapshotting was interrupted. |  | String |
| **camel.component.debezium-db2.snapshot-tables-order-by-row-count** | Controls the order in which tables are processed in the initial snapshot. A descending value will order the tables by row count descending. A ascending value will order the tables by row count ascending. A value of disabled (the default) will disable ordering by row count. | disabled | String |
| **camel.component.debezium-db2.sourceinfo-struct-maker** | The name of the SourceInfoStructMaker class that returns SourceInfo schema and struct. | io.debezium.connector.db2.Db2SourceInfoStructMaker | String |
| **camel.component.debezium-db2.streaming-delay-ms** | A delay period after the snapshot is completed and the streaming begins, given in milliseconds. Defaults to 0 ms. The option is a long type. | 0 | Long |
| **camel.component.debezium-db2.table-exclude-list** | A comma-separated list of regular expressions that match the fully-qualified names of tables to be excluded from monitoring. |  | String |
| **camel.component.debezium-db2.table-ignore-builtin** | Flag specifying whether built-in tables should be ignored. | true | Boolean |
| **camel.component.debezium-db2.table-include-list** | The tables for which changes are to be captured. |  | String |
| **camel.component.debezium-db2.time-precision-mode** | Time, date, and timestamps can be represented with different kinds of precisions, including: 'adaptive' (the default) bases the precision of time, date, and timestamp values on the database column’s precision; 'adaptive\_time\_microseconds' like 'adaptive' mode, but TIME fields always use microseconds precision; 'connect' always represents time, date, and timestamp values using Kafka Connect’s built-in representations for Time, Date, and Timestamp, which uses millisecond precision regardless of the database columns' precision. | adaptive | String |
| **camel.component.debezium-db2.tombstones-on-delete** | Whether delete operations should be represented by a delete event and a subsequent tombstone event (true) or only by a delete event (false). Emitting the tombstone event (the default behavior) allows Kafka to completely delete all events pertaining to the given key once the source record got deleted. | false | Boolean |
| **camel.component.debezium-db2.topic-naming-strategy** | The name of the TopicNamingStrategy class that should be used to determine the topic name for data change, schema change, transaction, heartbeat event etc. | io.debezium.schema.SchemaTopicNamingStrategy | String |
| **camel.component.debezium-db2.topic-prefix** | Topic prefix that identifies and provides a namespace for the particular database server/cluster is capturing changes. The topic prefix should be unique across all other connectors, since it is used as a prefix for all Kafka topic names that receive events emitted by this connector. Only alphanumeric characters, hyphens, dots and underscores must be accepted. |  | String |
| **camel.component.debezium-db2.transaction-metadata-factory** | Class to make transaction context & transaction struct/schemas. | io.debezium.pipeline.txmetadata.DefaultTransactionMetadataFactory | String |