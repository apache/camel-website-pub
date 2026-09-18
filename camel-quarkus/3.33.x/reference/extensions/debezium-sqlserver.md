# Debezium SQL Server Connector

JVM since1.0.0 Native since1.0.0

Capture changes from an SQL Server database.

## What’s inside

-   [Debezium SQL Server Connector component](../../../../components/4.18.x/debezium-sqlserver-component.md), URI syntax: `debezium-sqlserver:name`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-debezium-sqlserver)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-debezium-sqlserver</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

Depending on its configuration, SQL server may require SSL encryption on JDBC connections. In such a case, you will need to add `quarkus.ssl.native=true` to your `application.properties`. See also [Quarkus native SSL guide](https://quarkus.io/guides/native-and-ssl) and [Native mode](../../user-guide/native-mode.md) section of Camel Quarkus user guide.

## Camel Quarkus limitations

While you can use any of the available Kafka offset stores in JVM mode, only the following offset stores are supported in native mode:

-   `org.apache.kafka.connect.storage.FileOffsetBackingStore`
    
-   `org.apache.kafka.connect.storage.MemoryOffsetBackingStore`
    

Please file an [issue](https://github.com/apache/camel-quarkus/issues/new) if you are missing some specific offset store in native mode.