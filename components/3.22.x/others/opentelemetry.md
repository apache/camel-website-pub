# OpenTelemetry

**Since Camel 3.5**

The OpenTelemetry component is used for tracing and timing incoming and outgoing Camel messages using [OpenTelemetry](https://opentelemetry.io/).

Events (spans) are captured for incoming and outgoing messages being sent to/from Camel.

## Configuration

The configuration properties for the OpenTelemetry tracer are:

  
| Option | Default | Description |
| --- | --- | --- |
| excludePatterns |  | Sets exclude pattern(s) that will disable tracing for Camel messages that matches the pattern. The content is a Set<String> where the key is a pattern. The pattern uses the rules from Intercept. |
| encoding | false | Sets whether the header keys need to be encoded (connector specific) or not. The value is a boolean. Dashes need for instances to be encoded for JMS property keys. |

### Configuration

Include the `camel-opentelemetry` component in your POM, along with any specific dependencies associated with the chosen OpenTelemetry compliant Tracer.

To explicitly configure OpenTelemetry support, instantiate the `OpenTelemetryTracer` and initialize the camel context. You can optionally specify a `Tracer`, or alternatively it can be implicitly discovered using the `Registry`

```java
OpenTelemetryTracer otelTracer = new OpenTelemetryTracer();
// By default it uses the DefaultTracer, but you can override it with a specific OpenTelemetry Tracer implementation.
otelTracer.setTracer(...);
// And then initialize the context
otelTracer.init(camelContext);
```

## Spring Boot

If you are using Spring Boot then you can add the `camel-opentelemetry-starter` dependency, and turn on OpenTracing by annotating the main class with `@CamelOpenTelemetry`.

The `OpenTelemetryTracer` will be implicitly obtained from the camel context’s `Registry`, unless a `OpenTelemetryTracer` bean has been defined by the application.

## Java Agent

Download the [latest version](https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/).

This package includes the instrumentation agent as well as instrumentations for all supported libraries and all available data exporters. The package provides a completely automatic, out-of-the-box experience.

Enable the instrumentation agent using the `-javaagent` flag to the JVM.

```none
java -javaagent:path/to/opentelemetry-javaagent.jar \
     -jar myapp.jar
```

By default, the OpenTelemetry Java agent uses [OTLP exporter](https://github.com/open-telemetry/opentelemetry-java/tree/main/exporters/otlp) configured to send data to [OpenTelemetry collector](https://github.com/open-telemetry/opentelemetry-collector/blob/main/receiver/otlpreceiver/README.md) at `[http://localhost:4317](http://localhost:4317)`.

Configuration parameters are passed as Java system properties (`-D` flags) or as environment variables. See [the configuration documentation](https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/agent-config.md) for the full list of configuration items. For example:

```none
java -javaagent:path/to/opentelemetry-javaagent.jar \
     -Dotel.service.name=your-service-name \
     -Dotel.traces.exporter=jaeger \
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

The component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.opentelemetry.encoding** | Activate or deactivate dash encoding in headers (required by JMS) for messaging. |  | Boolean |
| **camel.opentelemetry.exclude-patterns** | Sets exclude pattern(s) that will disable tracing for Camel messages that matches the pattern. |  | Set |

## MDC Logging

When MDC Logging is enabled for the active Camel context the Trace ID and Span ID will be added and removed from the MDC for each route, the keys are `trace_id` and `span_id`, respectively.