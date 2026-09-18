# Mdc

JVM since3.29.0 Native since3.29.0

Logging MDC (Mapped Diagnostic Context) Service

## What’s inside

-   [MDC Logging](../../../../components/4.18.x/others/mdc.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-mdc)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-mdc</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.mdc.enabled](#quarkus-camel-mdc-enabled)`
Sets whether to enable the MDC tracing.

 | `boolean` | `false` |
| `[quarkus.camel.mdc.custom-exchange-headers](#quarkus-camel-mdc-custom-exchange-headers)`

Provide the headers you would like to use in the logging. Use \* value to include all available headers.

 | `string` |  |
| `[quarkus.camel.mdc.custom-exchange-properties](#quarkus-camel-mdc-custom-exchange-properties)`

Provide the properties you would like to use in the logging. Use \* value to include all available properties.

 | `string` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.