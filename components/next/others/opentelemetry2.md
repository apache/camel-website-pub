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
| `enabled` | false | Turn the tracing on/off. |
| `traceProcessors` | false | Trace inner custom processors (i.e., any `process` configured in the route). When disabled, custom processors are not visible from the OpenTelemetry perspective and have no active span or context. |
| `disableCoreProcessors` | false | Disable any inner core processors (any core DSL processor provided in the route, for example `bean`, `log`, …​). |
| `excludePatterns` |  | A comma-separated list of patterns (e.g., `log*,direct*,setBody*`) to exclude from tracing. Spans matching these patterns will be disabled. If nothing is specified, no processors are excluded by default. |
| `includePatterns` |  | A comma-separated list of patterns (e.g., `log*,direct*,setBody*`) to explicitly include in a trace. Spans matching these patterns will be enabled. If nothing is specified, all processors are included by default. |
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

### Dev Profile (In-Memory Span Exporter)

When the Camel profile is set to `dev` (the default for Camel JBang), the component automatically configures an in-memory span exporter. This captures OTel spans locally without requiring an external collector such as Jaeger or an OpenTelemetry Collector.

This is useful during development when you want to inspect traces via the dev console or local tooling without setting up external infrastructure.

With Camel JBang, enable it with the `--observe` flag:

```bash
camel run my-route.yaml --observe
```

The captured spans are available through the dev console at `/q/dev/opentelemetry`:

```bash
# Summary (span count, capacity)
curl http://localhost:8080/q/dev/opentelemetry

# Full span data as JSON
curl http://localhost:8080/q/dev/opentelemetry?dump=true

# Limit the number of returned spans
curl http://localhost:8080/q/dev/opentelemetry?dump=true&limit=50
```

The in-memory exporter holds up to 500 spans with oldest-first eviction. When the buffer is full, the oldest spans are discarded to make room for new ones.

> **Note**
> The in-memory exporter is only activated when the Camel profile is `dev` and no user-provided OTel `Tracer` bean is registered. For production deployments, configure a proper span exporter (OTLP, Jaeger, Zipkin, etc.).

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
    

### Using the OpenTelemetry Spring Boot starter

An alternative to the OpenTelemetry agent is to use [OpenTelemetry Spring Boot starter](https://opentelemetry.io/docs/zero-code/java/spring-boot-starter/).

To ensure version alignment across all OpenTelemetry dependencies, you should import the opentelemetry-instrumentation-bom BOM.

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>io.opentelemetry.instrumentation</groupId>
            <artifactId>opentelemetry-instrumentation-bom</artifactId>
            <version>2.26.1</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Note: Import the OpenTelemetry BOMs before any other BOMs in your project. For example, if you import the spring-boot-dependencies BOM, you have to declare it after the OpenTelemetry BOMs. Also make sure that the version you choose is compatible with the Opentelemetry version used by the Camel version you’re using.

Then add the following dependency for the OpenTelemetry Spring Boot starter:

```xml
<dependency>
    <groupId>io.opentelemetry.instrumentation</groupId>
    <artifactId>opentelemetry-spring-boot-starter</artifactId>
</dependency>
```

The starter auto-configures most aspects of the OpenTelemetry instrumentation, with two exceptions: No `Tracer` or `ContextPropagators` beans are autoconfigured, they need to be configured manually:

```java
import io.opentelemetry.api.OpenTelemetry;
import io.opentelemetry.api.trace.Tracer;
import io.opentelemetry.context.propagation.ContextPropagators;

@Configuration
public class OpenTelemetryConfiguration {

  @Bean
  public Tracer tracer(@Value("${spring.application.name}") String serviceName, OpenTelemetry openTelemetry) {
    return openTelemetry.getTracer(serviceName);
  }

  @Bean
  public ContextPropagators contextPropagators(OpenTelemetry openTelemetry) {
    return openTelemetry.getPropagators();
  }

}
```

The instrumentation can be configured using the standard Spring Boot configuration mechanisms (e.g. using application.yml). For a complete list of options, see the official [agent configuration documentation](https://opentelemetry.io/docs/zero-code/java/agent/configuration/).

For example, to set the service name and exporter type:

```yaml
otel:
  service:
    name: your-service-name
  traces:
    exporter: otlp
```

### Span customization

When you’re working at a very low level, you may need to tweak your metrics and add some in-process custom `span` in order to trace some specific measure of your application. If you need this advanced use case, you can create it during your process by configuring an Opentelemetry Tracer object and share it to your route. For example, in Java DSL:

```java
private Tracer otelTracer = otelExtension.getOpenTelemetry().getTracer("traceTest");
...
public void process(Exchange exchange) throws Exception {
     exchange.getIn().setHeader("operation", "fake");
     // We add a span during the processing. We need to verify this span is correctly
     // created and belong to the proper hierarchy. Important: the user has to know which is the
     // tracer, likely, setting it on the camel-telemetry Tracer component explicitly.
     Span mySpan = otelTracer.spanBuilder("mySpan").startSpan();
     // Do the work here
     mySpan.end();
}
```

#### Custom spans or third party spans hierarchy

In complex integrations it is advisable to have third party dependencies or add custom spans at a Processor level in order to get advanced telemetry information. When these spans are added at Processor level, then, you can expect the span to be nested under the specific core Processor. For example:

```java
    from("direct:start")
            .bean(MyBean.class)
...
    class MyBean {
        @WithSpan
        public void myLogic() {
            // custom logic
        }
    }
```

You should expect your custom span "myLogic" to be nested under the Bean processor span.

If you instead call it with an endpoint producer, the process is converted to an event, and as we cannot capture the scope, then it would nest the custom span under the endpoint instead. For example:

```java
    from("direct:start")
            .to("bean:myBean")
...
```

The spans produced are slightly different because now they include an additional span for the endpoint ("to" node). And, more important, as highlighted above, the custom span is going to be nested directly under the endpoint span "to" instead of the processor span ("bean").

For this reason, whenever you need to provide custom telemetry information, it is highly advisable to call directly the processors instead of the endpoints DSL. Otherwise you just have to expect the custom span to be nested under the endpoint.

### Baggage customization

`Baggage` is a way to attach key-value metadata to a request and carry it across service boundaries. In the context of OpenTelemetry, baggage travels along with the context (like trace/span), but it’s meant for custom data you define, not telemetry internals. Camel allows you to programmatically provide any `Baggage` information via Exchange property settings. Whenever the component finds a property defined as `CamelBaggage_xyz` it will consider it as a baggage variable named `xyz`. For example, in Java DSL:

```java
                from("direct:start")
                        .setProperty("CamelBaggage_myValue", constant("1234"))
                        .routeId("start")
                        .log("A message")
                        .process(new Processor() {
                            @Override
                            public void process(Exchange exchange) throws Exception {
                                // Baggage is available via the OpenTelemetry API
                                String val = Baggage.current().getEntryValue("myValue");
                            }
                        })
                        .to("log:info");
```

Any span executed after the `setProperty` will include a baggage variable named `myValue` with value `1234` which will be reflected in your telemetry result.

> **Note**
> any baggage setting defined externally (i.e., calling the Camel process with a context propagation) is normally going to be propagated in Camel logic.