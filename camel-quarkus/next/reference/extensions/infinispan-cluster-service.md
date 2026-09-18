# Infinispan Cluster Service

JVM since3.32.0 Native since3.32.0

Provides an Infinispan implementation of the Camel Cluster Service SPI

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-infinispan-cluster-service)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-infinispan-cluster-service</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

### Having only a single consumer in a cluster consuming from a given endpoint

When the same route is deployed on multiple JVMs, it could be interesting to use this extension in conjunction with the [Master one](master.md). In such a setup, a single consumer will be active at a time across the whole camel master namespace.

For instance, having the route below deployed on multiple JVMs:

```java
from("master:ns:timer:test?period=100")
    .log("Timer invoked on a single JVM at a time");
```

As a result, a single consumer will be active across the `ns` camel master namespace. It means that, at a given time, only a single timer will generate exchanges across all JVMs. In other words, messages will be logged every 100ms on a single JVM at a time.

#### Infinispan Configuration

You can configure the Infinispan client with the various `quarkus.camel.cluster.infinispan` configuration options in `application.properties`.

```properties
quarkus.camel.cluster.infinispan.hosts=localhost:11222
quarkus.camel.cluster.infinispan.username=admin
quarkus.camel.cluster.infinispan.password=2s3cr3t

# Optional additional configuration properties
quarkus.camel.cluster.infinispan.configuration-properties."infinispan.client.hotrod.client_intelligence" = BASIC
quarkus.camel.cluster.infinispan.configuration-properties."infinispan.client.hotrod.connect_timeout" = 5000
```

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.cluster.infinispan.enabled](#quarkus-camel-cluster-infinispan-enabled)`
Whether an Infinispan Cluster Service should be automatically configured according to 'quarkus.camel.cluster.infinispan.\*' configurations.

 | `boolean` | `true` |
| `[quarkus.camel.cluster.infinispan.id](#quarkus-camel-cluster-infinispan-id)`

The cluster service ID.

 | `string` |  |
| `[quarkus.camel.cluster.infinispan.order](#quarkus-camel-cluster-infinispan-order)`

The service lookup order/priority.

 | `int` |  |
| `[quarkus.camel.cluster.infinispan.attributes."attributes"](#quarkus-camel-cluster-infinispan-attributes-attributes)`

The custom attributes associated to the service.

 | `Map<String,String>` |  |
| `[quarkus.camel.cluster.infinispan.configuration-uri](#quarkus-camel-cluster-infinispan-configuration-uri)`

The Infinispan configuration URI. Can be used to specify a custom Infinispan configuration file.

 | `string` |  |
| `[quarkus.camel.cluster.infinispan.hosts](#quarkus-camel-cluster-infinispan-hosts)`

The Infinispan server hosts (e.g., "localhost:11222").

 | `string` |  |
| `[quarkus.camel.cluster.infinispan.secure](#quarkus-camel-cluster-infinispan-secure)`

Enable secure connections to an Infinispan server.

 | `boolean` |  |
| `[quarkus.camel.cluster.infinispan.username](#quarkus-camel-cluster-infinispan-username)`

Username for authentication with the Infinispan server.

 | `string` |  |
| `[quarkus.camel.cluster.infinispan.password](#quarkus-camel-cluster-infinispan-password)`

Password for authentication with the Infinispan server.

 | `string` |  |
| `[quarkus.camel.cluster.infinispan.sasl-mechanism](#quarkus-camel-cluster-infinispan-sasl-mechanism)`

SASL mechanism for authentication (e.g., DIGEST-MD5, PLAIN, SCRAM-SHA-256).

 | `string` |  |
| `[quarkus.camel.cluster.infinispan.security-realm](#quarkus-camel-cluster-infinispan-security-realm)`

Security realm for authentication.

 | `string` |  |
| `[quarkus.camel.cluster.infinispan.security-server-name](#quarkus-camel-cluster-infinispan-security-server-name)`

Security server name for authentication.

 | `string` |  |
| `[quarkus.camel.cluster.infinispan.configuration-properties."configuration-properties"](#quarkus-camel-cluster-infinispan-configuration-properties-configuration-properties)`

Additional configuration properties for the Infinispan client.

 | `Map<String,String>` |  |
| `[quarkus.camel.cluster.infinispan.lifespan](#quarkus-camel-cluster-infinispan-lifespan)`

Lifespan for entries in the cluster view cache.

 | `long` | `30` |
| `[quarkus.camel.cluster.infinispan.lifespan-time-unit](#quarkus-camel-cluster-infinispan-lifespan-time-unit)`

Time unit for lifespan (e.g., SECONDS, MINUTES, HOURS).

 | `nanoseconds`, `microseconds`, `milliseconds`, `seconds`, `minutes`, `hours`, `days` | `seconds` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.