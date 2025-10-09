# LevelDB

JVM since1.2.0 Native since1.2.0

Using LevelDB as persistent EIP store

## What’s inside

-   [LevelDB](../../../../components/4.14.x/others/leveldb.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-leveldb)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-leveldb</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

In native mode the extension uses a port of LevelDB written in Java ([documentation](https://github.com/dain/leveldb#leveldb-in-java)), which is within 10% of the performance of the C++ original. Please upvote [this issue](https://github.com/apache/camel-quarkus/issues/1911) if you do not like the present state.

Serialization is [not supported](https://github.com/oracle/graal/issues/460) on GraalVM. Extension has to use serialization based on Jackson. Aggregation repository in native has to be constructed in one of the following ways:

-   Use class `QuarkusLevelDBAggregationRepository` instead of `LevelDBAggregationRepository`.
    
-   Configure jackson serializer on `LevelDBAggregationRepository` by calling `repo.setSerializer(new JacksonLevelDBSerializer());`
    

Jackson serializer has limitation towards binary content. If payload object contains binary data (does not concern payloads which are completely binary), Jackson serialization and deserialization won’t work correctly. To avoid this, define your own jackson serializer/deserializer via `Module` and provide it to the aggregation repository (you can use for example the constructor of `QuarkusLevelDBAggregationRepository`).