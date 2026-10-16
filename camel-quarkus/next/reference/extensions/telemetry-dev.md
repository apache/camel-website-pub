# Telemetry Dev

JVM since3.22.0 Native since3.22.0

Basic implementation of Camel Telemetry useful for development purposes

## What’s inside

-   [Telemetry Dev](../../../../components/next/others/telemetry-dev.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-telemetry-dev)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-telemetry-dev</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| 
`[quarkus.camel.telemetryDev.exclude-patterns](#quarkus-camel-telemetrydev-exclude-patterns)`

Sets whether to disable tracing for endpoint URIs or Processor ids that match the given comma separated patterns. The pattern can take the following forms:

1.  An exact match on the endpoint URI. E.g. platform-http:/some/path
    
2.  A wildcard match. E.g. platform-http:\*
    
3.  A regular expression matching the endpoint URI. E.g. platform-http:/prefix/.\*
    





 | `string` |  |
| `[quarkus.camel.telemetryDev.include-patterns](#quarkus-camel-telemetrydev-include-patterns)`

Sets include pattern(s) that will explicitly enable tracing for Camel processors that matches the pattern. Multiple patterns can be separated by comma. All processors included by default if nothing is specified.

 | `string` |  |
| `[quarkus.camel.telemetryDev.trace-processors](#quarkus-camel-telemetrydev-trace-processors)`

Sets whether to create new telemetry spans for each Camel custom Processor. Use the excludePatterns property to filter out Processors.

 | `boolean` | `false` |
| `[quarkus.camel.telemetryDev.disable-core-processors](#quarkus-camel-telemetrydev-disable-core-processors)`

Disable any inner core processors (any core DSL processor provided in the route, for example `bean`, `log`, …​).

 | `boolean` | `false` |
| `[quarkus.camel.telemetryDev.trace-format](#quarkus-camel-telemetrydev-trace-format)`

The output format for traces

 | `string` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.