# Telemetry Trait

Deprecated since2.9.0

> **Warning**
> The Telemetry trait is **deprecated** as of version 2.9.0 and will be removed in a future release.
>
> The same behavior can be achieved via properties and dependencies configuration. See the [Migration Guide](#migration-guide) section below for details.

The Telemetry trait can be used to automatically publish tracing information to an OTLP compatible collector.

The trait is able to automatically discover the telemetry OTLP endpoint available in the namespace (supports **Jaerger** in version 1.35+).

The Telemetry trait is disabled by default.

> **Warning**
> The Telemetry trait is **deprecated** and will be removed in future release versions. The same behavior can be achieved via properties and dependencies configuration.

Migration example:

Before: --trait telemetry.endpoint=http://jaeger:4317
After:  -p quarkus.otel.exporter.otlp.traces.endpoint=http://jaeger:4317

> **Warning**
> The Telemetry trait can’t be enabled at the same time as the Tracing trait.

This trait is available in the following profiles: **Kubernetes, Knative, OpenShift**.

## Configuration

Trait properties can be specified when running any integration with the CLI:

```console
$ kamel run --trait telemetry.[key]=[value] --trait telemetry.[key2]=[value2] integration.yaml
```

The following configuration options are available:

  
| Property | Type | Description |
| --- | --- | --- |
| `telemetry.enabled` | `bool` | Can be used to enable or disable a trait. All traits share this common property. |
| `telemetry.auto` | `bool` | Enables automatic configuration of the trait, including automatic discovery of the telemetry endpoint. |
| `telemetry.serviceName` | `string` | The name of the service that publishes telemetry data (defaults to the integration name) |
| `telemetry.endpoint` | `string` | The target endpoint of the Telemetry service (automatically discovered by default) |
| `telemetry.sampler` | `string` | The sampler of the telemetry used for tracing (default "on") |
| `telemetry.sampler-ratio` | `string` | The sampler ratio of the telemetry used for tracing |
| `telemetry.sampler-parent-based` | `bool` | The sampler of the telemetry used for tracing is parent based (default "true") |
> **Note**
> the variables names are "snake case" if you’re using in `kamel` CLI, for example `trait.myParam` has to be translated as `-t trait.my-param`

## Examples

-   To activate tracing to a deployed OTLP API Jaeger through discovery:
    
    ```console
    $ kamel run -t telemetry.enable=true ...
    ```
    
-   To define a specific deployed OTLP gRPC reciever:
    
    ```console
    $ kamel run -t telemetry.enable=true -t telemetry.endpoint=http://instance-collector:4317 ...
    ```
    
-   To define another sampler service name:
    
    ```console
    $ kamel run -t telemetry.enable=true -t telemetry.service-name=tracer_myintegration ...
    ```
    
-   To use a ratio sampler with a sampling ratio of 1 to every 1,000 :
    
    ```console
    $ kamel run -t telemetry.enable=true -t telemetry.sampler=ratio -t telemetry.sampler-ratio=0.001 ...
    ```
    

## Migration Guide

The Telemetry trait is deprecated. The same behavior can be achieved via properties and dependencies configuration.

### Property Mapping

The following table shows how to map Telemetry trait properties to application properties:

  
| Telemetry Trait | Application Property | Example |
| --- | --- | --- |
| `telemetry.endpoint=http://jaeger:4317` | `quarkus.otel.exporter.otlp.traces.endpoint=http://jaeger:4317` | `kamel run -p quarkus.otel.exporter.otlp.traces.endpoint=http://jaeger:4317 MyRoute.java` |
| `telemetry.service-name=my-service` | `quarkus.otel.resource.attributes=service.name=my-service` | `kamel run -p quarkus.otel.resource.attributes=service.name=my-service MyRoute.java` |
| `telemetry.sampler=ratio` | `quarkus.otel.traces.sampler=ratio` | `kamel run -p quarkus.otel.traces.sampler=ratio MyRoute.java` |
| `telemetry.sampler-ratio=0.001` | `quarkus.otel.traces.sampler.ratio=0.001` | `kamel run -p quarkus.otel.traces.sampler.ratio=0.001 MyRoute.java` |
| `telemetry.sampler-parent-based=true` | `quarkus.otel.traces.sampler.parent-based=true` | `kamel run -p quarkus.otel.traces.sampler.parent-based=true MyRoute.java` |

### Migration Examples

**Before (deprecated):**

```console
$ kamel run -t telemetry.enabled=true \
  -t telemetry.endpoint=http://jaeger:4317 \
  -t telemetry.service-name=my-integration \
  MyRoute.java
```

**After (recommended):**

```console
$ kamel run \
  --dependency camel:opentelemetry \
  -p quarkus.otel.exporter.otlp.traces.endpoint=http://jaeger:4317 \
  -p quarkus.otel.resource.attributes=service.name=my-integration \
  MyRoute.java
```

> **Note**
> The `--dependency camel:opentelemetry` is required. Previously, the telemetry trait automatically added this dependency via the `camel-k:telemetry` capability. With direct configuration, you must explicitly include the OpenTelemetry dependency.

### Benefits of Direct Configuration

Using properties and dependencies configuration directly provides more flexibility, including:

-   Full access to all Quarkus OpenTelemetry options: [https://quarkus.io/guides/opentelemetry](https://quarkus.io/guides/opentelemetry)
    
-   Custom telemetry dependencies can be added as needed