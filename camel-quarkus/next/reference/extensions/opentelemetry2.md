# Opentelemetry2

JVM since3.22.0 Native since3.22.0

Implementation of Camel Opentelemetry based on the Camel Telemetry spec

## What’s inside

-   [Opentelemetry2](../../../../components/next/others/opentelemetry2.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-opentelemetry2)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-opentelemetry2</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

The extension automatically creates a Camel `OpenTelemetryTracer` and binds it to the Camel registry.

In order to send the captured traces to a tracing system, you need to configure some properties within `application.properties` like those below.

> **Note**
> This extension addresses inconsistencies found in the original `camel-quarkus-opentelemetry` extensions and offers a more robust implementation.

```properties
# OTLP exporter endpoint
quarkus.otel.exporter.otlp.endpoint=http://localhost:4317
```

Refer to the [Quarkus OpenTelemetry guide](https://quarkus.io/guides/opentelemetry) for a full list of configuration options.

Route endpoints can be excluded from tracing by configuring a property named `quarkus.camel.opentelemetry2.exclude-patterns` in `application.properties`. For example:

```properties
# Exclude all direct & netty-http endpoints from tracing
quarkus.camel.opentelemetry2.exclude-patterns=direct:*,netty-http:*
```

> **Note**
> The use of the [OpenTelemetry Agent](https://opentelemetry.io/docs/zero-code/java/agent/) **is not needed nor recommended**. Quarkus Extensions and the libraries they provide, are directly instrumented. Also, the agent does not work in native mode.

### Exporters

Quarkus OpenTelemetry defaults to the standard OTLP exporter defined in OpenTelemetry. Additional exporters will be available in the Quarkiverse [quarkus-opentelemetry-exporter](https://github.com/quarkiverse/quarkus-opentelemetry-exporter/blob/main/README.md) project.

### Tracing CDI bean method execution

When instrumenting the execution of CDI bean methods from Camel routes, you should annotate such methods with `io.opentelemetry.extension.annotations.WithSpan`. Methods annotated with `@WithSpan` will create a new Span and establish any required relationships with the current Trace context.

For example, to instrument a CDI bean from a Camel route, first ensure the appropriate methods are annotated with `@WithSpan`.

```java
@ApplicationScoped
@Named("myBean")
public class MyBean {
    @WithSpan
    public String greet() {
        return "Hello World!";
    }
}
```

Next, use the bean in your Camel route.

> **Important**
> To ensure that the sequence of recorded spans is correct, you must use the full `to("bean:")` endpoint URI and not the shortened `.bean()` EIP DSL method.

```java
public class MyRoutes extends RouteBuilder {
    @Override
    public void configure() throws Exception {
        from("direct:executeBean")
                .to("bean:myBean?method=greet");
    }
}
```

There is more information about CDI instrumentation in the [Quarkus OpenTelemetry guide](https://quarkus.io/guides/opentelemetry#cdi).

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| 
`[quarkus.camel.opentelemetry2.exclude-patterns](#quarkus-camel-opentelemetry2-exclude-patterns)`

Sets whether to disable tracing for endpoint URIs or Processor ids that match the given comma separated patterns. The pattern can take the following forms:

1.  An exact match on the endpoint URI. E.g. platform-http:/some/path
    
2.  A wildcard match. E.g. platform-http:\*
    
3.  A regular expression matching the endpoint URI. E.g. platform-http:/prefix/.\*
    





 | `string` |  |
| `[quarkus.camel.opentelemetry2.include-patterns](#quarkus-camel-opentelemetry2-include-patterns)`

Sets include pattern(s) that will explicitly enable tracing for Camel processors that matches the pattern. Multiple patterns can be separated by comma. All processors included by default if nothing is specified.

 | `string` |  |
| `[quarkus.camel.opentelemetry2.trace-processors](#quarkus-camel-opentelemetry2-trace-processors)`

Sets whether to create new telemetry spans for each Camel custom Processor. Use the excludePatterns property to filter out Processors.

 | `boolean` | `false` |
| `[quarkus.camel.opentelemetry2.disable-core-processors](#quarkus-camel-opentelemetry2-disable-core-processors)`

Disable any inner core processors (any core DSL processor provided in the route, for example `bean`, `log`, …​).

 | `boolean` | `false` |
| `[quarkus.camel.opentelemetry2.trace-headers-inclusion](#quarkus-camel-opentelemetry2-trace-headers-inclusion)`

If set to `true`, adds the generated telemetry `CAMEL_TRACE_ID` and `CAMEL_SPAN_ID` Exchange headers.

 | `boolean` | `false` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.