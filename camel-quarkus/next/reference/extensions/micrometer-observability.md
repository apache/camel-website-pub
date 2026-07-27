# Micrometer Observability 2

JVM since3.39.0 Native since3.39.0

Micrometer Observability implementation of Camel Telemetry

## What’s inside

-   [Micrometer Observability 2](../../../../components/next/others/micrometer-observability.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-micrometer-observability)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-micrometer-observability</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

The extension automatically creates a `MicrometerObservabilityTracer` and binds it to the Camel registry. It bridges Camel’s telemetry SPI to Micrometer Tracing via the OTel bridge, using the `OpenTelemetry` CDI bean provided by `quarkus-opentelemetry` (pulled in transitively).

Refer to the [Micrometer Observability 2](../../../../components/next/others/micrometer-observability.md) documentation for full details on tracing configuration. The following Quarkus config properties map directly to the tracer options described there:

```properties
quarkus.camel.micrometer-observability.exclude-patterns=direct:*,timer:*
quarkus.camel.micrometer-observability.include-patterns=platform-http:*
quarkus.camel.micrometer-observability.trace-processors=true
quarkus.camel.micrometer-observability.disable-core-processors=true
quarkus.camel.micrometer-observability.trace-headers-inclusion=true
```

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| 
`[quarkus.camel.micrometer-observability.exclude-patterns](#quarkus-camel-micrometer-observability-exclude-patterns)`

Sets whether to disable tracing for endpoint URIs or Processor ids that match the given comma separated patterns. The pattern can take the following forms:

1.  An exact match on the endpoint URI, e.g., {@code platform-http:/some/path}
    
2.  A wildcard match, e.g., {@code platform-http:\*}
    
3.  A regular expression matching the endpoint URI, e.g., {@code platform-http:/prefix/.\*}
    





 | `string` |  |
| `[quarkus.camel.micrometer-observability.include-patterns](#quarkus-camel-micrometer-observability-include-patterns)`

Sets include pattern(s) that will explicitly enable tracing for Camel processors that match the pattern. Multiple patterns can be separated by comma. All processors are included by default if nothing is specified.

 | `string` |  |
| `[quarkus.camel.micrometer-observability.trace-processors](#quarkus-camel-micrometer-observability-trace-processors)`

Sets whether to create new spans for each Camel Processor. Use the {@code excludePatterns} property to filter out specific processors.

When enabled, this generates much more detailed traces but also increases overhead.

 | `boolean` | `false` |
| `[quarkus.camel.micrometer-observability.disable-core-processors](#quarkus-camel-micrometer-observability-disable-core-processors)`

Disable tracing of inner core processors (any core DSL processor provided in the route, for example {@code bean}, {@code log}, …​).

 | `boolean` | `false` |
| `[quarkus.camel.micrometer-observability.trace-headers-inclusion](#quarkus-camel-micrometer-observability-trace-headers-inclusion)`

If set to {@code true}, adds the generated telemetry {@code CAMEL\_TRACE\_ID} and {@code CAMEL\_SPAN\_ID} Exchange headers.

 | `boolean` | `false` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.