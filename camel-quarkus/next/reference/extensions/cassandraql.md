# Cassandra CQL

JVM since1.0.0 Native since1.7.0

Integrate with Cassandra 2.0 using the CQL3 API (not the Thrift API). Based on Cassandra Java Driver provided by DataStax.

## What’s inside

-   [Cassandra CQL component](../../../../components/next/cql-component.md), URI syntax: `cql:beanRef:hosts:port/keyspace`
    

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

### Cassandra health check

The `cassandra-quarkus-client` dependency, which is used internally by this extension, automatically registers a health check. However, Camel manages its own `CqlSession` independently and does not use the Quarkus-managed Cassandra client, so the health check may fail and cause Kubernetes readiness probes to report the pod as not ready.

To work around this, disable the Cassandra health check in your `application.properties`:

```properties
quarkus.cassandra.health.enabled=false
```

### Cassandra aggregation repository in native mode

In order to use Cassandra aggregation repositories like `CassandraAggregationRepository` in native mode, you must [enable native serialization support](core.html#quarkus-camel-native-reflection-serialization-enabled).

In addition, if your exchange bodies are custom types, then they must be registered for serialization by annotating their class declaration with `@RegisterForReflection(serialization = true)`.