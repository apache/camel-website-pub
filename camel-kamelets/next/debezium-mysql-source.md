# ![debezium mysql source](_images/kamelets/debezium-mysql-source.svg) Debezium MySQL Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Sends a message for each row inserted, updated or deleted in the tables of a MySQL database, as it happens (change data capture with Debezium).

Use it to pass the changes of a database on to another system as they happen, for example to keep a search index or a cache up to date, or to copy new orders to a queue, without polling the tables. To read rows with a query again and again, use `mysql-source`.

Output: the body is JSON text in bytes, an object with the column names as keys, such as `{"id":1,"name":"Tea","price":4.50}`: the row after the change, and for a delete the row before it. The columns are in the order of the table. A `DECIMAL` column is a JSON number with its decimals, such as `4.50`, and a `DATE` column the number of days since 1970-01-01, such as `20454` for 2026-01-01. The `debezium-operation` header says what happened: `c` (insert), `u` (update), `d` (delete) or `r` (a row read by the snapshot, see `snapshotMode`). `debezium-table` is the table, as `database.table` such as `shop.orders`, and `debezium-key` the primary key of the row as JSON text, such as `{"id":1}`. `Content-Type` is `application/json`.

Good to know: the server must write its binary log (binlog) in the `ROW` format with the whole row (`binlog_format=ROW` and `binlog_row_image=FULL`, the defaults of MySQL 8), and the user needs the `SELECT`, `RELOAD`, `SHOW DATABASES`, `REPLICATION SLAVE` and `REPLICATION CLIENT` privileges. The Kamelet reads the binlog as a replica of the server does, under the id `serverId`. On the first start, it by default sends every row of the tables first (`snapshotMode`). It saves how far it got in the file `offsetStorageFileName`, or in a Kafka topic, when it stops and once a minute while it runs, and after a restart it goes on from there, so after a crash the changes of the last minute can be sent again. It also keeps the structure of the tables, as the binlog changed it, in a schema history: the file `schemaHistoryFileName`, or a Kafka topic. Keep both files on a disk that outlives the integration, such as a volume in Kubernetes: when the position is lost, everything is sent again as on the first start, and when only the schema history is lost, the Kamelet fails to start with `The db history topic is missing`, until it is started once with `snapshotMode` set to `recovery`. When the server is not set up as needed, such as with `binlog_format=STATEMENT`, the Kamelet fails to start, and the error says why. The JDBC driver of MySQL (`com.mysql:mysql-connector-j`) is not in the Kamelet, as its license is not the Apache license: Camel JBang downloads it by itself, and `camel export` adds it to the project. Any other option of the Debezium MySQL connector can be set for all the Kamelets of the integration as the `camel.component.debezium-mysql.` property of that option, such as `camel.component.debezium-mysql.columnExcludeList=shop.customers.ssn`.

## Configuration Options

The following table summarizes the configuration options available for the `debezium-mysql-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **serverId** | Server Id | **Required** The number the Kamelet uses as a replica of the MySQL server to read the binlog, such as `5400`. It must differ from the `server_id` of every MySQL server and of every other client that reads the binlog of the same servers, the other Kamelets included. | integer |  | 5400 |
| **serverName** | Server Name | **Required** The host name or IP address of the MySQL server, without the port. | string |  | db.example.com |
| **topicPrefix** | Logical Name | **Required** A name for this source of changes, made of letters, digits, `.`, `_` and `-`. The saved position is stored under this name, so keep it the same across restarts, and give each Kamelet that reads another server its own name. | string |  | shop |
| **username** | Username | **Required** The database user to log in as. It needs the `SELECT`, `RELOAD`, `SHOW DATABASES`, `REPLICATION SLAVE` and `REPLICATION CLIENT` privileges. | string |  |  |
| **offsetStorage** | Position Store | Where the Kamelet saves how far it got. `org.apache.kafka.connect.storage.FileOffsetBackingStore` (the default): in the file `offsetStorageFileName`. `org.apache.kafka.connect.storage.KafkaOffsetBackingStore`: in the Kafka topic `offsetStorageTopic`, on the Kafka of `offsetStorageBootstrapServers`, for an integration that has no lasting disk. Use the same kind of store for `schemaHistory`. Enum values: \* org.apache.kafka.connect.storage.FileOffsetBackingStore \* org.apache.kafka.connect.storage.KafkaOffsetBackingStore | string | org.apache.kafka.connect.storage.FileOffsetBackingStore |  |
| **offsetStorageBootstrapServers** | Kafka Brokers | The Kafka brokers of the Kafka stores of `offsetStorage` and `schemaHistory`, as `host:port` separated by commas. Needed with a Kafka store. The connection is made without TLS and without a login. | string |  | my-cluster-kafka-bootstrap:9092 |
| **offsetStorageFileName** | Position File | The file where the Kamelet saves how far it got, such as `/data/offsets.dat`, read again after a restart. It is created when it does not exist, but its folder must exist and be writable, or the Kamelet fails to start. A relative name is in the folder the integration runs in. When it is lost, the changes are sent again as on the first start. Not used when `offsetStorage` is the Kafka store. | string | debezium-mysql-offsets.dat | /data/offsets.dat |
| **offsetStoragePartitions** | Position Topic Partitions | The number of partitions of the topic `offsetStorageTopic` when the Kamelet creates it. Needed with the Kafka store. | integer |  | 1 |
| **offsetStorageReplicationFactor** | Position Topic Replicas | The number of copies of the topic `offsetStorageTopic` on the Kafka brokers when the Kamelet creates it. Needed with the Kafka store. | integer |  | 3 |
| **offsetStorageTopic** | Position Topic | The Kafka topic where the Kafka store saves how far the Kamelet got. It is created when it does not exist. Needed with the Kafka store. | string |  | shop-offsets |
| **schemaHistory** | Schema History Store | Where the Kamelet keeps the structure of the tables. `io.debezium.storage.file.history.FileSchemaHistory` (the default): in the file `schemaHistoryFileName`. `io.debezium.storage.kafka.history.KafkaSchemaHistory`: in the Kafka topic `schemaHistoryTopic`, on the Kafka of `offsetStorageBootstrapServers`, for an integration that has no lasting disk. Enum values: \* io.debezium.storage.file.history.FileSchemaHistory \* io.debezium.storage.kafka.history.KafkaSchemaHistory | string | io.debezium.storage.file.history.FileSchemaHistory |  |
| **schemaHistoryFileName** | Schema History File | The file where the Kamelet keeps the structure of the tables, such as `/data/schema-history.dat`, read again after a restart. It is created when it does not exist, with its folders. A relative name is in the folder the integration runs in. Not used when `schemaHistory` is the Kafka store. | string | debezium-mysql-schema-history.dat | /data/schema-history.dat |
| **schemaHistoryTopic** | Schema History Topic | The Kafka topic where the Kafka store keeps the structure of the tables. It is created with one partition when it does not exist. Use a topic of its own, not `offsetStorageTopic`. Needed with the Kafka store. | string |  | shop-schema-history |
| **serverPort** | Server Port | The port the MySQL server listens on. MySQL uses 3306 unless it was set up otherwise. | integer | 3306 |  |
| **snapshotMode** | Snapshot Mode | Whether to send the rows that are already in the tables before the changes. `initial` (the default): on the first start, every row of the tables is sent with the operation `r`, then the changes; after a restart with a saved position, only the changes since. `no_data`: only the changes made from the first start on. `always`: every row on each start, then the changes. `initial_only`: every row on the first start, and no changes. `when_needed`: as `initial`, and every row again when the saved position can no longer be found in the binlog. `recovery`: for one start after the schema history is lost, to write it again from the tables as they are now, then go on from the saved position; only when the structure of the tables has not changed since the Kamelet stopped. Enum values: \* initial \* no\_data \* always \* initial\_only \* when\_needed \* recovery | string | initial |  |
| **sslMode** | TLS Mode | Whether the connection to MySQL uses TLS. `preferred` (the default): TLS when the server offers it, without checking its certificate. `required`: always TLS, without checking the certificate of the server. `disabled`: no TLS. Enum values: \* disabled \* preferred \* required | string | preferred |  |
| **tableIncludeList** | Tables | The tables whose changes to send, as regular expressions that match `database.table`, separated by commas, such as `shop.orders,shop.customers`. When it is not set, the changes of all tables of all databases are sent, except those of the system databases. | string |  | shop.orders,shop.customers |

## Dependencies

At runtime, the `debezium-mysql-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
-   camel:debezium-mysql
    

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
      uri: "kamelet:debezium-mysql-source"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/debezium-mysql-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/debezium-mysql-source.kamelet.yaml)