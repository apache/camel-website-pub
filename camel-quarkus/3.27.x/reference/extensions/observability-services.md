# Observability Services

JVM since3.19.0 Native since3.19.0

Camel Observability Services

## What’s inside

-   [Observability Services](../../../../components/4.14.x/others/observability-services.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-observability-services)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-observability-services</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

This extension provides a set of opinionated components and configuration to simplify operations such as observability on cloud environments. Although the extension is mainly targeted for cloud, it can be used in any other environment.

By adding the `camel-quarkus-observability-services` extension to your application, each observability component (described below) will be configured with their individual default settings. No additional configuration is required.

HTTP endpoints will be exposed under the context path `/observe/<service>` by default. Further details about this are described below.

If you need to customize any component provided by this extension, then you can specify any of their related configuration options in `application.properties`, as it would be done normally when you work with the individual component extension(s).

## Components

This extension automatically provides the following Camel Quarkus component extensions:

-   [Camel Quarkus MicroProfile Health](microprofile-health.md) - for health checks
    
-   [Camel Quarkus Management](management.md) - for JMX
    
-   [Camel Quarkus Micrometer](micrometer.md) - for Camel Micrometer metrics
    
-   [Camel Quarkus OpenTelemetry2](opentelemetry2.md) - for tracing Camel messages (events/spans)
    
-   [Quarkus Micrometer Registry Prometheus](https://quarkus.io/guides/telemetry-micrometer#micrometer-and-monitoring-system-extensions) - for exporting metrics in Prometheus format
    

### List of known endpoints

The presence of this extension will expose the following endpoints:

 
| Endpoint | Description |
| --- | --- |
| `/observe/health` | Accumulation of all health check procedures in the application |
| `/observe/health/live` | Liveness probe endpoint |
| `/observe/health/ready` | Readiness probe endpoint |
| `/observe/health/started` | Application started probe endpoint |
| `/observe/metrics` | Metrics exposed from the Micrometer Prometheus registry |

By default, these endpoints are exposed on the management port (`9876`). This value can be changed as any other configuration (in this case, via `quarkus.management.port` application property). You can also disable it (`quarkus.management.enabled=false`) if you want to expose those endpoints in the regular service port (default, `8080`).

> **Note**
> You can configure the endpoints as you’d do normally within each extension configuration.

## OpenTelemetry configuration

The presence of this extension will provide the required instrumentation to enable the collection of OpenTelemetry metrics. The Camel Quarkus OpenTelemetry extension instruments your application and periodically attempts to export traces to the configured collector. This is disabled by default in order to prevent the application exporting traces when no telemetry server is available.

In order to enable instrumentation, you need to add the following configuration to `application.properties`.

```properties
quarkus.otel.sdk.disabled=false
```

To configure any aspect of OpenTelemetry, you can add the following configuration to `application.properties`. For example to customize the server endpoint where traces should be exported (default, `[http://localhost:4317](http://localhost:4317)`).

```properties
quarkus.otel.exporter.otlp.traces.endpoint=http://my-otel-collector.svc:4317
```

The full set of configuration options are documented in the [Camel Quarkus OpenTelemetry](opentelemetry.md) and [Quarkus OpenTelemetry](https://quarkus.io/guides/opentelemetry) documentation.

> **Note**
> Quarkus trace exporting defaults to the gRPC protocol on port 4317.

## JMX configuration

The presence of this extension implies the presence of the `camel-quarkus-management` extension. This exposes Camel JMX MBeans to provide insights and management of the running application.

If you prefer to disable Camel JMX instrumentation, you can add the following configuration to `application.properties`.

```properties
camel.main.jmxEnabled=false
```

The full set of configuration options are documented in the [Camel Quarkus Management](management.md) documentation.