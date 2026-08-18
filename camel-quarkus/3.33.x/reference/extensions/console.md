# Console

JVM since2.16.0 Nativeunsupported

Camel Developer Console

## What’s inside

-   [Console](../../../../manual/camel-console.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-console</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Developer console endpoint

To access the developer console, you must first enable it by adding configuration to `application.properties`.

```properties
quarkus.camel.console.enabled=true
```

Alternatively you can use a `camel-main` configuration option.

```properties
camel.main.dev-console-enabled=true
```

The console is then available at the following URL.

```text
http://localhost:8080/q/camel/dev-console
```

You can then call a console by its id, such as `routes`:

```text
http://localhost:8080/q/camel/dev-console/routes
```

### Exposing the developer console in prod mode

By default, the console is only exposed in dev and test modes. To expose the console in prod mode, add the following configuration to `application.properties`.

```properties
quarkus.camel.console.exposure-mode=ALL
```

See the configuration overview below for further details about `exposure-mode`.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.console.enabled](#quarkus-camel-console-enabled)`
Whether the Camel developer console is enabled.

 | `boolean` | `false` |
| `[quarkus.camel.console.path](#quarkus-camel-console-path)`

The context path under which the Camel developer console is deployed (default `/q/camel/dev-console`).

 | `string` | `camel/dev-console` |
| `[quarkus.camel.console.exposure-mode](#quarkus-camel-console-exposure-mode)`

The modes in which the Camel developer console is available. The default `dev-test` enables the developer console only in dev mode and test modes. A value of `all` enables agent discovery in dev, test and prod modes. Setting the value to `none` will not expose the developer console HTTP endpoint.

 | `all`, `dev-test`, `none` | `dev-test` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.