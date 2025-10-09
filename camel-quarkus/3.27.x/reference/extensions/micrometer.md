# Micrometer

JVM since1.5.0 Native since1.5.0

Collect various metrics directly from Camel routes using the Micrometer library.

## What’s inside

-   [Micrometer component](../../../../components/4.14.x/micrometer-component.md), URI syntax: `micrometer:metricsType:metricsName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-micrometer)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-micrometer</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

This extension leverages [Quarkus Micrometer](https://quarkus.io/guides/micrometer). Quarkus supports a variety of Micrometer metric registry implementations.

Your application should declare the following dependency or one of the dependencies listed in the [quarkiverse documentation](https://quarkiverse.github.io/quarkiverse-docs/quarkus-micrometer-registry/dev/index.md), depending on the monitoring solution you want to work with.

```xml
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-micrometer-registry-prometheus</artifactId>
</dependency>
```

If no dependency is declared, the Micrometer extension creates a `SimpleMeterRegistry` instance, suitable mainly for testing.

## Camel Quarkus limitations

### Exposing Micrometer statistics in JMX

Exposing Micrometer statistics in JMX is not available in native mode as `quarkus-micrometer-registry-jmx` does not have native support at present.

### Decrement header for Counter is ignored by Prometheus

Prometheus backend ignores negative values during increment of Counter metrics.

### Exposing statistics in JMX

In Camel Quarkus, registering a `JmxMeterRegistry` is simplified. Add a dependency for `io.quarkiverse.micrometer.registry:quarkus-micrometer-registry-jmx` and a `JmxMeterRegistry` will automatically get created for you.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.metrics.enable-route-policy](#quarkus-camel-metrics-enable-route-policy)`
Set whether to enable the MicrometerRoutePolicyFactory for capturing metrics on route processing times.

 | `boolean` | `true` |
| `[quarkus.camel.metrics.enable-message-history](#quarkus-camel-metrics-enable-message-history)`

Set whether to enable the MicrometerMessageHistoryFactory for capturing metrics on individual route node processing times. Depending on the number of configured route nodes, there is the potential to create a large volume of metrics. Therefore, this option is disabled by default.

 | `boolean` | `false` |
| `[quarkus.camel.metrics.enable-exchange-event-notifier](#quarkus-camel-metrics-enable-exchange-event-notifier)`

Set whether to enable the MicrometerExchangeEventNotifier for capturing metrics on exchange processing times.

 | `boolean` | `true` |
| `[quarkus.camel.metrics.base-endpoint-uri-exchange-event-notifier](#quarkus-camel-metrics-base-endpoint-uri-exchange-event-notifier)`

Whether to use static or dynamic values for Endpoint Name tags in captured metrics. By default, static values are used. When using dynamic tags, then a dynamic to (toD) can compute many different endpoint URIs that, can lead to many tags as the URI is dynamic, so use this with care if setting this option to false.

 | `boolean` | `true` |
| `[quarkus.camel.metrics.enable-route-event-notifier](#quarkus-camel-metrics-enable-route-event-notifier)`

Set whether to enable the MicrometerRouteEventNotifier for capturing metrics on the total number of routes and total number of routes running.

 | `boolean` | `true` |
| `[quarkus.camel.metrics.enable-instrumented-thread-pool-factory](#quarkus-camel-metrics-enable-instrumented-thread-pool-factory)`

Set whether to gather performance information about Camel Thread Pools by injecting an InstrumentedThreadPoolFactory.

 | `boolean` | `false` |
| `[quarkus.camel.metrics.naming-strategy](#quarkus-camel-metrics-naming-strategy)`

Controls the naming style to use for metrics. The available values are `default` and `legacy`. `default` uses the default Micrometer naming convention. `legacy` uses the legacy camel-case naming style.

 | `default`, `legacy` | `default` |
| `[quarkus.camel.metrics.route-policy-level](#quarkus-camel-metrics-route-policy-level)`

Sets the level of metrics to capture. The available values are `all` ,`context` and `route`. `all` captures metrics for both the camel context and routes. `route` captures metrics for routes only. `context` captures metrics for the camel context only.

 | `all`, `context`, `route` | `all` |
| `[quarkus.camel.metrics.route-policy-exclude-pattern](#quarkus-camel-metrics-route-policy-exclude-pattern)`

Comma separated list of route IDs to exclude from metrics collection.

 | `string` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.