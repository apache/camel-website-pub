# OpenTelemetry

JVM since2.1.0 Native since2.1.0 ⚠️Deprecated

Distributed tracing using OpenTelemetry

## What’s inside

-   [OpenTelemetry](../../../../components/4.22.x/others/opentelemetry.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-opentelemetry)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-opentelemetry</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

The extension automatically creates a Camel `OpenTelemetryTracer` and binds it to the Camel registry.

In order to send the captured traces to a tracing system, you need to configure some properties within `application.properties` like those below.

```properties
# Identifier for the origin of spans created by the application
quarkus.application.name=my-camel-application

# OTLP exporter endpoint
quarkus.otel.exporter.otlp.traces.endpoint=http://localhost:4317
```

Refer to the [Quarkus OpenTelemetry guide](https://quarkus.io/guides/opentelemetry) for a full list of configuration options.

Route endpoints can be excluded from tracing by configuring a property named `quarkus.camel.opentelemetry.exclude-patterns` in `application.properties`. For example:

```properties
# Exclude all direct & netty-http endpoints from tracing
quarkus.camel.opentelemetry.exclude-patterns=direct:*,netty-http:*
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
| `[quarkus.camel.opentelemetry.encoding](#quarkus-camel-opentelemetry-encoding)`
Sets whether header names need to be encoded. Can be useful in situations where OpenTelemetry propagators potentially set header name values in formats that are not compatible with the target system. E.g. for JMS where the specification mandates header names are valid Java identifiers.

 | `boolean` | `false` |
| 

`[quarkus.camel.opentelemetry.exclude-patterns](#quarkus-camel-opentelemetry-exclude-patterns)`

Sets whether to disable tracing for endpoint URIs or Processor ids that match the given comma separated patterns. The pattern can take the following forms:

1.  An exact match on the endpoint URI. E.g. platform-http:/some/path
    
2.  A wildcard match. E.g. platform-http:\*
    
3.  A regular expression matching the endpoint URI. E.g. platform-http:/prefix/.\*
    





 | `string` |  |
| `[quarkus.camel.opentelemetry.trace-processors](#quarkus-camel-opentelemetry-trace-processors)`

Sets whether to create new OpenTelemetry spans for each Camel Processor. Use the excludePatterns property to filter out Processors.

 | `boolean` | `false` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.