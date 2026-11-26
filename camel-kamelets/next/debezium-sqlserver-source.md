# ![debezium sqlserver source](_images/kamelets/debezium-sqlserver-source.svg) Debezium SQL Server Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Sends a message for each row inserted, updated or deleted in the tables of a SQL Server database, as it happens (change data capture with Debezium).

Use it to pass the changes of a database on to another system as they happen, for example to keep a search index or a cache up to date, or to copy new orders to a queue, without polling the tables. To read rows with a query again and again, use `sqlserver-source`.

Output: the body is JSON text in bytes, an object with the column names as keys, such as `{"id":1,"name":"Tea","price":4.50}`: the row after the change, and for a delete the row before it. The columns are in the order of the table. A `DECIMAL` column is a JSON number with its decimals, such as `4.50`, and a `DATE` column the number of days since 1970-01-01, such as `20454` for 2026-01-01. The `debezium-operation` header says what happened: `c` (insert), `u` (update), `d` (delete) or `r` (a row read by the snapshot, see `snapshotMode`). `debezium-table` is the table, as `schema.table` such as `dbo.orders`, and `debezium-key` the primary key of the row as JSON text, such as `{"id":1}`. `Content-Type` is `application/json`.

Good to know: the Kamelet reads the changes that the change data capture (CDC) of SQL Server records, so CDC must be enabled on the database, with `EXEC sys.sp_cdc_enable_db`, and on each table, such as with `EXEC sys.sp_cdc_enable_table @source_schema = 'dbo', @source_name = 'orders', @role_name = NULL`, which needs a member of `sysadmin`. SQL Server Agent must run, as its jobs copy the changes into the change tables of CDC. The changes of a table without CDC are not sent. The user needs to read the tables and the change tables, as a member of the `db_owner` role of the database does. On the first start, the Kamelet by default sends every row of the tables first (`snapshotMode`). It saves how far it got in the file `offsetStorageFileName`, or in a Kafka topic, when it stops and once a minute while it runs, and after a restart it goes on from there, so after a crash the changes of the last minute can be sent again. It also keeps the structure of the tables in a schema history: the file `schemaHistoryFileName`, or a Kafka topic. Keep both files on a disk that outlives the integration, such as a volume in Kubernetes: when the position is lost, everything is sent again as on the first start, and when only the schema history is lost, the Kamelet fails to start with `The db history topic is missing`, until it is started once with `snapshotMode` set to `recovery`. The cleanup job of CDC deletes the changes after 3 days by default, so start a stopped Kamelet again before that. Any other option of the Debezium SQL Server connector can be set for all the Kamelets of the integration as the `camel.component.debezium-sqlserver.` property of that option, such as `camel.component.debezium-sqlserver.columnExcludeList=dbo.customers.ssn`.

## Configuration Options

The following table summarizes the configuration options available for the `debezium-sqlserver-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database whose changes to send. CDC must be enabled on it. | string |  | shop |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **serverName** | Server Name | **Required** The host name or IP address of the SQL Server server, without the port. | string |  | db.example.com |
| **topicPrefix** | Logical Name | **Required** A name for this source of changes, made of letters, digits, `.`, `_` and `-`. The saved position is stored under this name, so keep it the same across restarts, and give each Kamelet that reads another database its own name. | string |  | shop |
| **username** | Username | **Required** The database user to log in as. It needs to read the tables and the change tables of CDC, as a member of the `db_owner` role of the database does. | string |  |  |
| **encrypt** | Encrypt Connection | Whether the connection to SQL Server is encrypted with TLS. When true, the certificate of the server must be trusted by Java, or `trustServerCertificate` must be true. | boolean | true |  |
| **offsetStorage** | Position Store | Where the Kamelet saves how far it got. `org.apache.kafka.connect.storage.FileOffsetBackingStore` (the default): in the file `offsetStorageFileName`. `org.apache.kafka.connect.storage.KafkaOffsetBackingStore`: in the Kafka topic `offsetStorageTopic`, on the Kafka of `offsetStorageBootstrapServers`, for an integration that has no lasting disk. Use the same kind of store for `schemaHistory`. Enum values: \* org.apache.kafka.connect.storage.FileOffsetBackingStore \* org.apache.kafka.connect.storage.KafkaOffsetBackingStore | string | org.apache.kafka.connect.storage.FileOffsetBackingStore |  |
| **offsetStorageBootstrapServers** | Kafka Brokers | The Kafka brokers of the Kafka stores of `offsetStorage` and `schemaHistory`, as `host:port` separated by commas. Needed with a Kafka store. The connection is made without TLS and without a login. | string |  | my-cluster-kafka-bootstrap:9092 |
| **offsetStorageFileName** | Position File | The file where the Kamelet saves how far it got, such as `/data/offsets.dat`, read again after a restart. It is created when it does not exist, but its folder must exist and be writable, or the Kamelet fails to start. A relative name is in the folder the integration runs in. When it is lost, the changes are sent again as on the first start. Not used when `offsetStorage` is the Kafka store. | string | debezium-sqlserver-offsets.dat | /data/offsets.dat |
| **offsetStoragePartitions** | Position Topic Partitions | The number of partitions of the topic `offsetStorageTopic` when the Kamelet creates it. Needed with the Kafka store. | integer |  | 1 |
| **offsetStorageReplicationFactor** | Position Topic Replicas | The number of copies of the topic `offsetStorageTopic` on the Kafka brokers when the Kamelet creates it. Needed with the Kafka store. | integer |  | 3 |
| **offsetStorageTopic** | Position Topic | The Kafka topic where the Kafka store saves how far the Kamelet got. It is created when it does not exist. Needed with the Kafka store. | string |  | shop-offsets |
| **schemaHistory** | Schema History Store | Where the Kamelet keeps the structure of the tables. `io.debezium.storage.file.history.FileSchemaHistory` (the default): in the file `schemaHistoryFileName`. `io.debezium.storage.kafka.history.KafkaSchemaHistory`: in the Kafka topic `schemaHistoryTopic`, on the Kafka of `offsetStorageBootstrapServers`, for an integration that has no lasting disk. Enum values: \* io.debezium.storage.file.history.FileSchemaHistory \* io.debezium.storage.kafka.history.KafkaSchemaHistory | string | io.debezium.storage.file.history.FileSchemaHistory |  |
| **schemaHistoryFileName** | Schema History File | The file where the Kamelet keeps the structure of the tables, such as `/data/schema-history.dat`, read again after a restart. It is created when it does not exist, with its folders. A relative name is in the folder the integration runs in. Not used when `schemaHistory` is the Kafka store. | string | debezium-sqlserver-schema-history.dat | /data/schema-history.dat |
| **schemaHistoryTopic** | Schema History Topic | The Kafka topic where the Kafka store keeps the structure of the tables. It is created with one partition when it does not exist. Use a topic of its own, not `offsetStorageTopic`. Needed with the Kafka store. | string |  | shop-schema-history |
| **serverPort** | Server Port | The port the SQL Server server listens on. SQL Server uses 1433 unless it was set up otherwise. | integer | 1433 |  |
| **snapshotMode** | Snapshot Mode | Whether to send the rows that are already in the tables before the changes. `initial` (the default): on the first start, every row of the tables is sent with the operation `r`, then the changes; after a restart with a saved position, only the changes since. `no_data`: only the changes made from the first start on. `always`: every row on each start, then the changes. `initial_only`: every row on the first start, and no changes. `when_needed`: as `initial`, and every row again when the saved position can no longer be found in the change tables. `recovery`: for one start after the schema history is lost, to write it again from the tables as they are now, then go on from the saved position; only when the structure of the tables has not changed since the Kamelet stopped. Enum values: \* initial \* no\_data \* always \* initial\_only \* when\_needed \* recovery | string | initial |  |
| **tableIncludeList** | Tables | The tables whose changes to send, as regular expressions that match `schema.table`, separated by commas, such as `dbo.orders,dbo.customers`. When it is not set, the changes of all tables with CDC are sent. | string |  | dbo.orders,dbo.customers |
| **trustServerCertificate** | Trust Server Certificate | Whether to accept the certificate of the server without checking it, as needed for a server with a self-signed certificate. Only for development and tests: the connection can then be intercepted. | boolean | false |  |

## Dependencies

At runtime, the `debezium-sqlserver-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
-   camel:debezium-sqlserver
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:debezium-sqlserver-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/debezium-sqlserver-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/debezium-sqlserver-source.kamelet.yaml)