# Cassandra CQL

JVM since1.0.0 Native since1.7.0

Integrate with Cassandra 2.0 using the CQL3 API (not the Thrift API). Based on Cassandra Java Driver provided by DataStax.

## What’s inside

-   [Cassandra CQL component](../../../../components/4.14.x/cql-component.md), URI syntax: `cql:beanRef:hosts:port/keyspace`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-cassandraql)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-cassandraql</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

### Cassandra aggregation repository in native mode

In order to use Cassandra aggregation repositories like `CassandraAggregationRepository` in native mode, you must [enable native serialization support](core.html#quarkus-camel-native-reflection-serialization-enabled).

In addition, if your exchange bodies are custom types, then they must be registered for serialization by annotating their class declaration with `@RegisterForReflection(serialization = true)`.