# OpenTelemetry

> **Warning**
> **Deprecated:** This opentelemetry is deprecated and may be removed in a future release.

**Since Camel 3.5**

The OpenTelemetry component is used for tracing and timing incoming and outgoing Camel messages using [OpenTelemetry](https://opentelemetry.io/).

Events (spans) are captured for incoming and outgoing messages being sent to/from Camel.

> **Note**
> this component is deprecated since version 4.19.0. Please, use [`camel-opentelemetry2`](opentelemetry2.md) component instead.

## Configuration

The configuration properties for the OpenTelemetry tracer are:

  
| Option | Default | Description |
| --- | --- | --- |
| `instrumentationName` | camel | A name uniquely identifying the instrumentation scope, such as the instrumentation library, package, or fully qualified class name. Must not be null. |
| `excludePatterns` |  | Sets exclude pattern(s) that will disable tracing for Camel messages that matches the pattern. The content is a Set<String> where the key is a pattern. The pattern uses the rules from Intercept. |
| `encoding` | `false` | Sets whether the header keys need to be encoded (connector specific) or not. The value is a boolean. Dashes are required for instances to be encoded for JMS property keys. |
| `traceProcessors` | `false` | Setting this to true will create new OpenTelemetry Spans for each Camel Processors. Use the excludePattern property to filter out Processors |

## Using Camel OpenTelemetry

Include the `camel-opentelemetry` component in your POM, along with any specific dependencies associated with the chosen OpenTelemetry compliant Tracer.

To explicitly configure OpenTelemetry support, instantiate the `OpenTelemetryTracer` and initialize the camel context. You can optionally specify a `Tracer`, or alternatively it can be implicitly discovered using the `Registry`

```java
OpenTelemetryTracer otelTracer = new OpenTelemetryTracer();
// By default, it uses the DefaultTracer, but you can override it with a specific OpenTelemetry Tracer implementation.
otelTracer.setTracer(...);
// And then initialize the context
otelTracer.init(camelContext);
```

> **Note**
> You would still need OpenTelemetry to instrument your code, which can be done via a [Java agent](#OpenTelemetry-JavaAgent).

### Using with standalone Camel

If you use `camel-main` as standalone Camel, then you can enable and use OpenTelemetry without Java code.

Add `camel-opentelemetry` component in your POM, and configure in `application.properties`:

```properties
camel.opentelemetry.enabled = true
# you can configure the other options
# camel.opentelemetry.instrumentationName = myApp
```

The configuration alone provide a NOOP default implementation, which is only useful for testing purposes as it will always create the same trace and span. In order to leverage an easy configuration you can also use the [OpenTelemetry zero code SDK autoconfiguration](https://opentelemetry.io/docs/languages/java/configuration/#zero-code-sdk-autoconfigure). With this approach you will need to add the `io.opentelemetry:opentelemetry-sdk-extension-autoconfigure` to your Camel main application, and start the application with the following system properties:

```bash
$ java -Dotel.java.global-autoconfigure.enabled=true -Dotel.metrics.exporter=none -Dotel.traces.exporter=none -Dotel.logs.exporter=none -jar my-app.jar
```

> **Note**
> you will need to check the SDK manual to configure according to your specific needs.

## Spring Boot

When running on Spring Boot, add the `camel-opentelemetry-starter` dependency to get started.

There are several ways to configure instrumentation of your Camel application running on Spring Boot with OpenTelemetry. The first and easiest one is by using the [OpenTelemetry Java agent](https://opentelemetry.io/docs/zero-code/java/agent/). The other one is through Spring Boot’s Actuator. We’ll cover both.

### Java Agent

Download the [latest version](https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/).

This package includes the instrumentation agent as well as instrumentation for all supported libraries and all available data exporters. The package provides a completely automatic, out-of-the-box experience.

Enable the instrumentation agent using the `-javaagent` flag to the JVM.

```bash
java -javaagent:path/to/opentelemetry-javaagent.jar \
     -jar myapp.jar
```

By default, the OpenTelemetry Java agent uses [OTLP exporter](https://github.com/open-telemetry/opentelemetry-java/tree/main/exporters/otlp) configured to send data to [OpenTelemetry collector](https://github.com/open-telemetry/opentelemetry-collector/blob/main/receiver/otlpreceiver/README.md) at `[http://localhost:4318](http://localhost:4318)`.

Configuration parameters are passed as Java system properties (`-D` flags) or as environment variables. See [the configuration documentation](https://opentelemetry.io/docs/zero-code/java/agent/configuration/) for the full list of configuration items. For example:

```bash
java -javaagent:path/to/opentelemetry-javaagent.jar \
     -Dotel.service.name=your-service-name \
     -Dotel.traces.exporter=otlp \
     -jar myapp.jar
```

## Spring Boot Auto-Configuration

When using opentelemetry with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-opentelemetry-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.opentelemetry.enabled** | **Deprecated** Global option to enable/disable OpenTelemetry integration, default is true. | true | Boolean |
| **camel.opentelemetry.encoding** | **Deprecated** Activate or deactivate dash encoding in headers (required by JMS) for messaging. |  | Boolean |
| **camel.opentelemetry.exclude-patterns** | **Deprecated** Sets exclude pattern(s) that will disable tracing for Camel messages that matches the pattern. Multiple patterns can be separated by comma. |  | String |
| **camel.opentelemetry.trace-processors** | **Deprecated** Setting this to true will create new OpenTelemetry Spans for each Camel Processors. Use the excludePattern property to filter out Processors. |  | Boolean |

### Spring Boot’s Actuator

To have Spring Boot’s Actuator configure OpenTelemetry, you need to add `org.springframework.boot:spring-boot-starter-actuator` and `io.micrometer:micrometer-tracing-bridge-otel` to your project. OpenTelemetry’s `Tracer` will then be [configured](https://docs.spring.io/spring-boot/reference/actuator/tracing.md) through `spring-boot-starter-actuator` unless a `Tracer` is already defined.

**Noteworthy**: by default, this will sample only 10% of requests to prevent overwhelming the trace backend. Set the property `management.tracing.sampling.probability` to `1.0` if you want to see all traces.

### SpanExporters

You’ll probably want to configure at least one [SpanExporter](https://opentelemetry.io/docs/languages/java/sdk/#spanexporter) as they allow you to export your traces to various backends (e.g., Zipkin and Jaeger), or log them. For example, to export your traces to Jaeger using OTLP via gRPC, add `io.opentelemetry:opentelemetry-exporter-otlp` as a dependency to your project. To configure it, you can use the `management.otlp.tracing` properties or register a new `SpanExporter` bean yourself:

```java
@Bean
public SpanExporter OtlpGrpcSpanExporter(@Value("${tracing.url}") String url) {
    return OtlpGrpcSpanExporter.builder().setEndpoint(url).build();
}
```

Spring Boot’s Actuator will take care of the wiring for you.

Alternatively if you just want to log your traces in OTLP JSON format, add `io.opentelemetry:opentelemetry-exporter-logging-otlp` as a dependency to your project and also register a new `SpanExporter` bean:

```java
@Bean
public SpanExporter logTraces() {
    return OtlpJsonLoggingSpanExporter.create();
}
```

Multiple `SpanExporters` can be used at the same time.

## MDC Logging

You can add Mapped Diagnostic Context tracing information (ie, `trace_id` and `span_id`) adding the specific [Opentelemetry Logger MDC auto instrumentation](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/logger-mdc-instrumentation.md). The configuration depends on the logging framework you’re using.

## Customizing OpenTelemetry spans

In _rare_ circumstances, it may be desirable to apply advanced customizations to the OpenTelemetry Span generated by the Camel `OpenTelemetryTracer`.

To do this, you can provide a custom implementation of `SpanCustomizer` and either set it explicitly on the `OpenTelemetryTracer`, or bind it to the Camel registry, where it will be automatically resolved by the tracer upon initialization.

Note that care should be taken when configuring parents & links to avoid breaking the relationship between spans & traces.

```java
public class MySpanCustomizer implements SpanCustomizer {
    @Override
    public void customize(SpanBuilder spanBuilder, String operationName, Exchange exchange) {
        spanBuilder.setAttribute("foo", "bar");
        spanBuilder.setParent(myCustomParentContext);
        spanBuilder.addLink(linkedSpanContext);
        // other customizations...
    }

    // By default, all spans will have customizations applied. You can restrict this by overriding isEnabled
    @Override
    public boolean isEnabled(String operationName, Exchange exchange) {
        String header = exchange.getMessage().getHeader("foo", String.class);
        return operationName.equals("my-message-queue") && header.equals("bar");
    }
}
```