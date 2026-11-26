# ![debezium postgresql source](_images/kamelets/debezium-postgresql-source.svg) Debezium PostgreSQL Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Sends a message for each row inserted, updated or deleted in the tables of a PostgreSQL database, as it happens (change data capture with Debezium).

Use it to pass the changes of a database on to another system as they happen, for example to keep a search index or a cache up to date, or to copy new orders to a queue, without polling the tables. To read rows with a query again and again, use `postgresql-source`.

Output: the body is JSON text in bytes, an object with the column names as keys, such as `{"id":1,"name":"Tea","price":4.50}`: the row after the change, and for a delete the row before it. The columns are in the order of the table. A `NUMERIC` column is a JSON number with its decimals, such as `4.50`, and a `DATE` column the number of days since 1970-01-01, such as `20454` for 2026-01-01. The `debezium-operation` header says what happened: `c` (insert), `u` (update), `d` (delete) or `r` (a row read by the snapshot, see `snapshotMode`). `debezium-table` is the table, as `schema.table` such as `public.orders`, and `debezium-key` the primary key of the row as JSON text, such as `{"id":1}`. `Content-Type` is `application/json`.

Good to know: the server must run with `wal_level=logical`, and the user needs the `REPLICATION` attribute and the right to read the tables. When the server is not set up as needed, such as with `wal_level=replica`, the Kamelet fails to start, and the error says why. On the first start, the Kamelet creates a replication slot named `slotName` and a publication named `publicationName` in the database, and by default sends every row of the tables first (`snapshotMode`). It saves how far it got in the file `offsetStorageFileName`, or in a Kafka topic, when it stops and once a minute while it runs, and after a restart it goes on from there, so after a crash the changes of the last minute can be sent again. Keep the file on a disk that outlives the integration, such as a volume in Kubernetes: when it is lost, everything is sent again as on the first start. The slot keeps the changes in the database until the Kamelet has read them, so a slot that is no longer read lets the disk of the server fill up: drop it with `SELECT pg_drop_replication_slot('debezium')`. For a delete, PostgreSQL logs only the primary key of the row unless the table has `REPLICA IDENTITY FULL`, so by default a deleted row has only its key columns set, and the others are `null`. Any other option of the Debezium PostgreSQL connector can be set for all the Kamelets of the integration as the `camel.component.debezium-postgres.` property of that option, such as `camel.component.debezium-postgres.columnExcludeList=public.customers.ssn`.

## Configuration Options

The following table summarizes the configuration options available for the `debezium-postgresql-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **databaseName** | Database Name | **Required** The name of the database whose changes to send. | string |  | shop |
| **password** | Password | **Required** The password of the database user `username`. | string |  |  |
| **serverName** | Server Name | **Required** The host name or IP address of the PostgreSQL server, without the port. It must be the primary server, not a read replica. | string |  | db.example.com |
| **topicPrefix** | Logical Name | **Required** A name for this source of changes, made of letters, digits, `.`, `_` and `-`. The saved position is stored under this name, so keep it the same across restarts, and give each Kamelet that reads another database its own name. | string |  | shop |
| **username** | Username | **Required** The database user to log in as. It needs the `REPLICATION` attribute, the right to read the tables and, unless the publication already exists, the right to create it (to create a publication for all tables, the user must be a superuser). | string |  |  |
| **offsetStorage** | Position Store | Where the Kamelet saves how far it got. `org.apache.kafka.connect.storage.FileOffsetBackingStore` (the default): in the file `offsetStorageFileName`. `org.apache.kafka.connect.storage.KafkaOffsetBackingStore`: in the Kafka topic `offsetStorageTopic`, on the Kafka of `offsetStorageBootstrapServers`, for an integration that has no lasting disk. Enum values: \* org.apache.kafka.connect.storage.FileOffsetBackingStore \* org.apache.kafka.connect.storage.KafkaOffsetBackingStore | string | org.apache.kafka.connect.storage.FileOffsetBackingStore |  |
| **offsetStorageBootstrapServers** | Position Kafka Brokers | The Kafka brokers of the Kafka store, as `host:port` separated by commas. Needed with the Kafka store. The connection is made without TLS and without a login. | string |  | my-cluster-kafka-bootstrap:9092 |
| **offsetStorageFileName** | Position File | The file where the Kamelet saves how far it got, such as `/data/offsets.dat`, read again after a restart. It is created when it does not exist, but its folder must exist and be writable, or the Kamelet fails to start. A relative name is in the folder the integration runs in. When it is lost, the changes are sent again as on the first start. Not used when `offsetStorage` is the Kafka store. | string | debezium-postgresql-offsets.dat | /data/offsets.dat |
| **offsetStoragePartitions** | Position Topic Partitions | The number of partitions of the topic `offsetStorageTopic` when the Kamelet creates it. Needed with the Kafka store. | integer |  | 1 |
| **offsetStorageReplicationFactor** | Position Topic Replicas | The number of copies of the topic `offsetStorageTopic` on the Kafka brokers when the Kamelet creates it. Needed with the Kafka store. | integer |  | 3 |
| **offsetStorageTopic** | Position Topic | The Kafka topic where the Kafka store saves how far the Kamelet got. It is created when it does not exist. Needed with the Kafka store. | string |  | shop-offsets |
| **pluginName** | Decoding Plugin | The PostgreSQL plugin that decodes the changes. `pgoutput` is built into PostgreSQL 10 and newer. `decoderbufs` must be installed on the server. Enum values: \* pgoutput \* decoderbufs | string | pgoutput |  |
| **publicationAutocreateMode** | Create Publication | Whether the Kamelet creates the publication when it does not exist. `all_tables` (the default): for all tables, which needs a superuser. `filtered`: for the tables of `tableIncludeList` only, which needs only to own them. `disabled`: never; the Kamelet fails to start when the publication does not exist. `no_tables`: for no table, so that the tables can be added to it later. An existing publication is used as it is. Enum values: \* all\_tables \* filtered \* disabled \* no\_tables | string | all\_tables |  |
| **publicationName** | Publication | The name of the PostgreSQL publication that says which tables are logged for the Kamelet, made of letters, digits and `_`. See `publicationAutocreateMode` for whether it is created. | string | dbz\_publication |  |
| **serverPort** | Server Port | The port the PostgreSQL server listens on. PostgreSQL uses 5432 unless it was set up otherwise. | integer | 5432 |  |
| **slotName** | Replication Slot | The name of the PostgreSQL replication slot that keeps the changes until the Kamelet has read them, made of lowercase letters, digits and `_`. It is created when it does not exist. Each Kamelet that reads the same database needs its own slot. | string | debezium |  |
| **snapshotMode** | Snapshot Mode | Whether to send the rows that are already in the tables before the changes. `initial` (the default): on the first start, every row of the tables is sent with the operation `r`, then the changes; after a restart with a saved position, only the changes since. `no_data`: only the changes made from the first start on. `always`: every row on each start, then the changes. `initial_only`: every row on the first start, and no changes. `when_needed`: as `initial`, and every row again when the saved position can no longer be found in the database. Enum values: \* initial \* no\_data \* always \* initial\_only \* when\_needed | string | initial |  |
| **tableIncludeList** | Tables | The tables whose changes to send, as regular expressions that match `schema.table`, separated by commas, such as `public.orders,public.customers`. When it is not set, the changes of all tables are sent. | string |  | public.orders,public.customers |

## Dependencies

At runtime, the `debezium-postgresql-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:kamelet
    
-   camel:debezium-postgres
    

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
      uri: "kamelet:debezium-postgresql-source"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/debezium-postgresql-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/debezium-postgresql-source.kamelet.yaml)