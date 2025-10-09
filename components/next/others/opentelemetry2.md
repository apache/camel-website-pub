# Opentelemetry2

**Since Camel 4.11**

This module is an implementation of the common `camel-telemetry` interface based on [OpenTelemetry](https://opentelemetry.io/) technology.

It is named `camel-opentelemetry2` to differentiate it from the existing `camel-opentelemetry` component, which is based on an older Camel tracing specification. We recommend using this new component for future projects and migrating existing applications from `camel-opentelemetry`, as this component will likely become the default in a future version of Camel.

> **Note**
> This component addresses inconsistencies found in the original `camel-opentelemetry` component and offers a more robust implementation.

## Configuration

The configuration properties for the OpenTelemetry2 tracer are:

  
| Option | Default | Description |
| --- | --- | --- |
| `excludePatterns` |  | A comma-separated list of patterns (e.g., `log*,direct*,setBody*`) to exclude from tracing. Spans matching these patterns will be disabled. |
| `traceProcessors` | `false` | If set to `true`, Camel creates OpenTelemetry Spans for each processor in your routes. You can use `excludePatterns` to filter which processors are traced. |
| `traceHeadersInclusion` | `false` | If set to `true`, adds the generated telemetry `CAMEL_TRACE_ID` and `CAMEL_SPAN_ID` Exchange headers. |

### Using with Standalone Camel

When using `camel-main`, you can enable and configure OpenTelemetry declaratively in your `application.properties` file without writing any Java code.

First, add the `camel-opentelemetry2` dependency to your project `pom.xml`. Then, add configuration options to `application.properties`:

```properties
camel.opentelemetry2.enabled = true
# Other options can also be configured
# camel.opentelemetry2.traceProcessors = true
```

When starting your application, you may also need to configure OpenTelemetry SDK system properties. For example:

```bash
java -Dotel.metrics.exporter=none -Dotel.logs.exporter=none -jar my-app.jar
```

### Using the OpenTelemetry Java Agent

To capture and export traces, your application typically needs the OpenTelemetry Java agent. The agent automatically instruments your application to collect telemetry data.

> **Note**
> Some runtimes, such as Quarkus, provide built-in OpenTelemetry integration and may not require a separate agent. Consult the documentation for your specific runtime for guidance.

To use the agent:

1.  Download the latest `opentelemetry-javaagent.jar` from the [official releases page](https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/).
    
2.  Attach the agent to your application’s JVM using the `-javaagent` flag.
    

```bash
java -javaagent:path/to/opentelemetry-javaagent.jar \
     -Dotel. ... \
     -jar myapp.jar
```

By default, the agent uses the OTLP exporter and sends data to an [OpenTelemetry Collector](https://github.com/open-telemetry/opentelemetry-collector/blob/main/receiver/otlpreceiver/README.md) at `[http://localhost:4318](http://localhost:4318)`.

You can configure the agent using Java system properties (`-D` flags) or environment variables. For a complete list of options, see the official [agent configuration documentation](https://opentelemetry.io/docs/zero-code/java/agent/configuration/).

For example, to set the service name and exporter type:

```bash
java -javaagent:path/to/opentelemetry-javaagent.jar \
     -Dotel.service.name=your-service-name \
     -Dotel.traces.exporter=otlp \
     -jar myapp.jar
```

### Collect OpenTelemetry Traces

A popular open-source choice is [Jaeger](https://www.jaegertracing.io/), an end-to-end distributed tracing system. For setup instructions, see the [Jaeger Getting Started guide](https://www.jaegertracing.io/docs/latest/getting-started/).

### MDC Logging

To correlate logs with traces, you can include trace and span IDs in your application’s Mapped Diagnostic Context (MDC). This allows you to filter logs for a specific trace, which is invaluable for debugging.

There are two primary ways to achieve this:

Camel MDC Integration (Recommended)

This is the idiomatic approach for Camel applications.

1.  Set the `traceHeadersInclusion` option to `true`. This adds `CAMEL_TRACE_ID` and `CAMEL_SPAN_ID` to the Camel Exchange headers.
    
2.  Use the `camel-mdc` component to automatically copy these headers into the MDC. Configure it in `application.properties`:
    
    ```properties
    camel.mdc.customHeaders=CAMEL_TRACE_ID,CAMEL_SPAN_ID
    ```
    

OpenTelemetry Agent MDC Instrumentation

As an alternative, you can use the agent’s built-in MDC integration.

1.  Enable the [Logger MDC auto-instrumentation](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/logger-mdc-instrumentation.md). This automatically adds `trace_id` and `span_id` to the MDC.
    
2.  Configure your logging framework to include these MDC keys in your log format. The exact configuration depends on the logging library you use.