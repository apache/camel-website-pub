# Observability Services

Spring Boot auto-configuration bundling the Camel observability services: metrics, tracing and health.

The starter pulls in `camel-micrometer`, `micrometer-registry-prometheus`, `camel-opentelemetry2` and `camel-management`, and contributes a set of defaults so that a Camel application exposes a Prometheus scrape endpoint and Kubernetes-shaped liveness and readiness probes without any configuration.

The defaults are registered as the lowest precedence property source, so anything you set in `application.properties`, in an environment variable or on the command line overrides them.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-observability-services-starter</artifactId>
</dependency>
```

## Usage

Add the starter to the classpath and the endpoints below are available on a separate management listener, bound to loopback on port `9876`:

 
| Endpoint | Purpose |
| --- | --- |
| `[http://127.0.0.1:9876/observe/health](http://127.0.0.1:9876/observe/health)` | Aggregate health |
| `[http://127.0.0.1:9876/observe/health/live](http://127.0.0.1:9876/observe/health/live)` | Kubernetes liveness probe |
| `[http://127.0.0.1:9876/observe/health/ready](http://127.0.0.1:9876/observe/health/ready)` | Kubernetes readiness probe |
| `[http://127.0.0.1:9876/observe/metrics](http://127.0.0.1:9876/observe/metrics)` | Prometheus scrape endpoint |

### Injected defaults

This is the full set of properties the starter contributes. Every one of them can be overridden by your own configuration:

  
| Property | Value | Notes |
| --- | --- | --- |
| `management.server.port` | `9876` | Management endpoints run on their own listener, separate from the application port. |
| `management.server.address` | `127.0.0.1` | The listener binds to loopback. See [Exposing the management listener](#_exposing_the_management_listener). |
| `management.endpoints.web.exposure.include` | `health,prometheus` | Only these two endpoints are exposed. |
| `management.endpoints.web.base-path` | `/observe` | Replaces the `/actuator` base path. |
| `management.endpoints.web.path-mapping.prometheus` | `metrics` | Serves the Prometheus endpoint at `/observe/metrics`. |
| `camel.metrics.log-metrics-on-shutdown` | `true` | Dumps a metrics summary to the log when the application stops. |
| `camel.metrics.log-metrics-on-shutdown-filters` | `app.info,camel.exchanges.*,process.cpu.usage,jvm.memory.max,jvm.memory.used` | Which metrics that summary contains. |
| `camel.metrics.log-metrics-on-shutdown-format` | `prometheus` | Format of that summary. |
| `camel.opentelemetry2.enabled` | `true` | Enables the OpenTelemetry tracing instrumentation. |
| `management.endpoint.health.probes.enabled` | `true` | Enables the liveness and readiness health groups. |
| `management.health.livenessState.enabled` | `true` | Registers the `livenessState` indicator. |
| `management.health.readinessState.enabled` | `true` | Registers the `readinessState` indicator. |
| `management.endpoint.health.show-details` | `when-authorized` | See [Health detail exposure](#_health_detail_exposure). |
| `management.endpoint.health.group.live.include` | `livenessState,camelLivenessState` | Contents of `/observe/health/live`. |
| `management.endpoint.health.group.live.show-details` | `always` | See [Health detail exposure](#_health_detail_exposure). |
| `management.endpoint.health.group.ready.include` | `readinessState,camelReadinessState` | Contents of `/observe/health/ready`. |
| `management.endpoint.health.group.ready.show-details` | `always` | See [Health detail exposure](#_health_detail_exposure). |

### Exposing the management listener

The management listener binds to `127.0.0.1`, so out of the box the health and metrics endpoints are reachable from the same host only. This matches the Spring Boot baseline, which ships no separate management listener at all: opening one on every interface should be a decision you make, not one the starter makes for you.

A Kubernetes deployment whose kubelet probes or Prometheus scrapers reach the pod over the network has to widen the bind address:

```properties
management.server.address = 0.0.0.0
```

Pair that with a `NetworkPolicy`, or with authentication in front of the management port, so the endpoints are only reachable from your probes and your scrapers.

### Health detail exposure

`/observe/health` uses `when-authorized`, the setting that shows the individual health indicators to an authenticated caller and the overall status alone to everybody else. Camel health checks report on the resources a route talks to — broker connections, data sources, remote endpoints — and their detail can identify those resources, so it is not something to hand to an unauthenticated caller. With no Spring Security on the classpath there is no authenticated caller, and the endpoint behaves as `never`.

To restore the previous behaviour of showing the details to anyone who asks:

```properties
management.endpoint.health.show-details = always
```

The `live` and `ready` groups keep `always`. The kubelet reaches them unauthenticated, and it puts the response body into the probe-failure event, so `kubectl describe pod` names the indicator that took the pod down. Both groups contain availability-state indicators only — `livenessState`, `readinessState` and their Camel counterparts report a status and carry no data — so there is nothing in those responses beyond the indicator names and their state.

### Camel health exposure level

`camel.health.exposure-level` is left at its Camel default of `default`, which filters health check metadata — endpoint URIs, route and consumer identifiers — out of the health response while keeping the check names, error messages and stack traces that tell you what failed.

If you want the metadata as well, opt in:

```properties
camel.health.exposure-level = full
```