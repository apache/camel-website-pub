# Debezium PostgresSQL Connector

JVM since1.0.0 Native since1.0.0

Capture changes from a PostgresSQL database.

## What’s inside

-   [Debezium PostgresSQL Connector component](../../../../components/4.18.x/debezium-postgres-component.md), URI syntax: `debezium-postgres:name`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-debezium-postgres)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-debezium-postgres</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

While you can use any of the available Kafka offset stores in JVM mode, only the following offset stores are supported in native mode:

-   `org.apache.kafka.connect.storage.FileOffsetBackingStore`
    
-   `org.apache.kafka.connect.storage.MemoryOffsetBackingStore`
    

Please file an [issue](https://github.com/apache/camel-quarkus/issues/new) if you are missing some specific offset store in native mode.