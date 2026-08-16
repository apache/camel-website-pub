# Debezium MySQL Connector

JVM since1.0.0 Native since1.0.0

Capture changes from a MySQL database.

## What’s inside

-   [Debezium MySQL Connector component](../../../../components/4.22.x/debezium-mysql-component.md), URI syntax: `debezium-mysql:name`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-debezium-mysql)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-debezium-mysql</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

We cannot add the MySQL JDBC driver as a compile scope dependency of this extension because it is GPL2 licensed, and it would be against the policy of the Apache Software Foundation.

Therefore, you have to add the dependency to your project yourself, as long as you are able to comply with its license terms.

`quarkus-bom` (transitively included by `camel-quarkus-bom` and `quarkus-camel-bom`) manages a version of `com.mysql:mysql-connector-j` compatible with Camel Quarkus. So you do not need to specify the version of the driver when importing any of the aforementioned BOMs. The following should be sufficient for Maven:

```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
</dependency>
```

## Camel Quarkus limitations

While you can use any of the available Kafka offset stores in JVM mode, only the following offset stores are supported in native mode:

-   `org.apache.kafka.connect.storage.FileOffsetBackingStore`
    
-   `org.apache.kafka.connect.storage.MemoryOffsetBackingStore`
    

Please file an [issue](https://github.com/apache/camel-quarkus/issues/new) if you are missing some specific offset store in native mode.