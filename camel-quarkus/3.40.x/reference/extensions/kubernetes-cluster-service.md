# Kubernetes Cluster Service

JVM since3.10.0 Native since3.10.0

Provides a Kubernetes implementation of the Camel Cluster Service SPI

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-kubernetes-cluster-service)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-kubernetes-cluster-service</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

### Having only a single consumer in a cluster consuming from a given endpoint

When the same route is deployed on multiple pods, it could be interesting to use this extension in conjunction with the [Master one](master.md). In such a setup, a single consumer will be active at a time across the whole camel master namespace.

For instance, having the route below deployed on multiple pods:

```java
from("master:ns:timer:test?period=100")
    .log("Timer invoked on a single pod at a time");
```

As a result, a single consumer will be active across the `ns` camel master namespace. It means that, at a given time, only a single timer will generate exchanges across the whole cluster. In other words, messages will be logged every 100ms on a single pod at a time.

The kubernetes cluster service could further be tuned by tweaking `quarkus.camel.cluster.kubernetes.*` properties.

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.cluster.kubernetes.enabled](#quarkus-camel-cluster-kubernetes-enabled)`
Whether a Kubernetes Cluster Service should be automatically configured according to 'quarkus.camel.cluster.kubernetes.\*' configurations.

 | `boolean` | `true` |
| `[quarkus.camel.cluster.kubernetes.rebalancing](#quarkus-camel-cluster-kubernetes-rebalancing)`

Whether the camel master namespace leaders should be distributed evenly across all the camel contexts in the cluster.

 | `boolean` | `true` |
| `[quarkus.camel.cluster.kubernetes.id](#quarkus-camel-cluster-kubernetes-id)`

The cluster service ID (defaults to null).

 | `string` |  |
| `[quarkus.camel.cluster.kubernetes.master-url](#quarkus-camel-cluster-kubernetes-master-url)`

The URL of the Kubernetes master (read from Kubernetes client properties by default).

 | `string` |  |
| `[quarkus.camel.cluster.kubernetes.connection-timeout-millis](#quarkus-camel-cluster-kubernetes-connection-timeout-millis)`

The connection timeout in milliseconds to use when making requests to the Kubernetes API server.

 | `int` |  |
| `[quarkus.camel.cluster.kubernetes.namespace](#quarkus-camel-cluster-kubernetes-namespace)`

The name of the Kubernetes namespace containing the pods and the configmap (autodetected by default).

 | `string` |  |
| `[quarkus.camel.cluster.kubernetes.pod-name](#quarkus-camel-cluster-kubernetes-pod-name)`

The name of the current pod (autodetected from container host name by default).

 | `string` |  |
| `[quarkus.camel.cluster.kubernetes.jitter-factor](#quarkus-camel-cluster-kubernetes-jitter-factor)`

The jitter factor to apply in order to prevent all pods to call Kubernetes APIs in the same instant (defaults to 1.2).

 | `double` |  |
| `[quarkus.camel.cluster.kubernetes.lease-duration-millis](#quarkus-camel-cluster-kubernetes-lease-duration-millis)`

The default duration of the lease for the current leader (defaults to 15000).

 | `long` |  |
| `[quarkus.camel.cluster.kubernetes.renew-deadline-millis](#quarkus-camel-cluster-kubernetes-renew-deadline-millis)`

The deadline after which the leader must stop its services because it may have lost the leadership (defaults to 10000).

 | `long` |  |
| `[quarkus.camel.cluster.kubernetes.retry-period-millis](#quarkus-camel-cluster-kubernetes-retry-period-millis)`

The time between two subsequent attempts to check and acquire the leadership. It is randomized using the jitter factor (defaults to 2000).

 | `long` |  |
| `[quarkus.camel.cluster.kubernetes.order](#quarkus-camel-cluster-kubernetes-order)`

Service lookup order/priority (defaults to 2147482647).

 | `int` |  |
| `[quarkus.camel.cluster.kubernetes.resource-name](#quarkus-camel-cluster-kubernetes-resource-name)`

The name of the lease resource used to do optimistic locking (defaults to 'leaders'). The resource name is used as prefix when the underlying Kubernetes resource can manage a single lock.

 | `string` |  |
| `[quarkus.camel.cluster.kubernetes.lease-resource-type](#quarkus-camel-cluster-kubernetes-lease-resource-type)`

The lease resource type used in Kubernetes, either 'config-map' or 'lease' (defaults to 'lease').

 | `config-map`, `lease` |  |
| `[quarkus.camel.cluster.kubernetes.labels."labels"](#quarkus-camel-cluster-kubernetes-labels-labels)`

The labels key/value used to identify the pods composing the cluster, defaults to empty map.

 | `Map<String,String>` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.