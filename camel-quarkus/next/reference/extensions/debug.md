# Debug

JVM since2.10.0 Native since3.2.0

Enables Camel Route Debugging

## What’s inside

-   [Debug](../../../../components/4.22.x/others/debug.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-debug)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-debug</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

By default, the `debug` extension is automatically enabled in development mode. If you want to leverage debugging capabilities outside of development mode, you must set a configuration property as follows.

```properties
quarkus.camel.debug.enabled=true
```

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.debug.enabled](#quarkus-camel-debug-enabled)`
Set whether to enable Camel debugging support.

 | `boolean` | `false` |
| `[quarkus.camel.debug.suspend](#quarkus-camel-debug-suspend)`

Indicates whether the _suspend mode_ is enabled or not. If `true` the message processing is immediately suspended until the method `attach()` is called.

 | `boolean` | `false` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.