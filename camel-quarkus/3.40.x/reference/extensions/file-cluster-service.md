# File Cluster Service

JVM since3.10.0 Native since3.10.0

Provides a FileLock implementation of the Camel Cluster Service SPI

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-file-cluster-service)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-file-cluster-service</artifactId>
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

It’s possible to configure the file cluster service with a property like below in `application.properties`:

```properties
quarkus.camel.cluster.file.root = target/cluster-folder-where-lock-file-will-be-held
```

As a result, a single consumer will be active across the `ns` camel master namespace. It means that, at a given time, only a single timer will generate exchanges across all JVMs. In other words, messages will be logged every 100ms on a single JVM at a time.

The file cluster service could further be tuned by tweaking `quarkus.camel.cluster.file.*` properties.

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.cluster.file.id](#quarkus-camel-cluster-file-id)`
The cluster service ID (defaults to null).

 | `string` |  |
| `[quarkus.camel.cluster.file.root](#quarkus-camel-cluster-file-root)`

The root path (defaults to null).

 | `string` |  |
| `[quarkus.camel.cluster.file.order](#quarkus-camel-cluster-file-order)`

The service lookup order/priority (defaults to 2147482647).

 | `int` |  |
| `[quarkus.camel.cluster.file.attributes."attributes"](#quarkus-camel-cluster-file-attributes-attributes)`

The custom attributes associated to the service (defaults to empty map).

 | `Map<String,String>` |  |
| `[quarkus.camel.cluster.file.acquire-lock-delay](#quarkus-camel-cluster-file-acquire-lock-delay)`

The time to wait before starting to try to acquire the cluster lock. Note that if FileLockClusterService determines no cluster members are running or cannot reliably determine the cluster state, the initial delay is computed from the acquireLockInterval (defaults to 1000ms).

 | `string` |  |
| `[quarkus.camel.cluster.file.acquire-lock-interval](#quarkus-camel-cluster-file-acquire-lock-interval)`

The time to wait between attempts to try to acquire the cluster lock evaluated using wall-clock time. All cluster members must use the same value so leadership checks and leader liveness detection remain consistent (defaults to 10000ms).

 | `string` |  |
| `[quarkus.camel.cluster.file.heartbeat-timeout-multiplier](#quarkus-camel-cluster-file-heartbeat-timeout-multiplier)`

Multiplier applied to the cluster leader `acquireLockInterval` to determine how long followers should wait before considering the leader "stale".

For example, if the leader updates its heartbeat every 2 seconds and the `heartbeatTimeoutMultiplier` is `3`, followers will tolerate up to `2s * 3 = 6s` of silence before declaring the leader unavailable.

 | `int` |  |
| `[quarkus.camel.cluster.file.cluster-data-task-max-attempts](#quarkus-camel-cluster-file-cluster-data-task-max-attempts)`

Sets how many times a cluster data task will run, counting both the first execution and subsequent retries in case of failure or timeout. The default is 5 attempts.

This can be useful when the cluster data root is on network based file storage, where I/O operations may occasionally block for long or unpredictable periods.

 | `int` |  |
| `[quarkus.camel.cluster.file.cluster-data-task-timeout](#quarkus-camel-cluster-file-cluster-data-task-timeout)`

Sets the timeout for a cluster data task (reading or writing cluster data). The default is 10 seconds.

Timeouts are useful when the cluster data root is on network storage, where I/O operations may occasionally block for long or unpredictable periods.

 | `string` |  |
| `[quarkus.camel.cluster.file.enabled](#quarkus-camel-cluster-file-enabled)`

Whether a File Lock Cluster Service should be automatically configured according to 'quarkus.camel.cluster.file.\*' configurations.

 | `boolean` | `true` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.