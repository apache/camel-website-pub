# Core

JVM since0.0.1 Native since0.0.1

Camel core functionality and basic Camel languages: Constant, ExchangeProperty, Header, Ref, Simple and Tokenize

## What’s inside

-   [Constant language](../../../../components/4.18.x/languages/constant-language.md)
    
-   [ExchangeProperty language](../../../../components/4.18.x/languages/exchangeProperty-language.md)
    
-   [File language](../../../../components/4.18.x/languages/file-language.md)
    
-   [Header language](../../../../components/4.18.x/languages/header-language.md)
    
-   [Ref language](../../../../components/4.18.x/languages/ref-language.md)
    
-   [Simple language](../../../../components/4.18.x/languages/simple-language.md)
    
-   [Tokenize language](../../../../components/4.18.x/languages/tokenize-language.md)
    
-   [Variable language](../../../../components/4.18.x/languages/variable-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-core)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-core</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

### Simple language

#### Using the OGNL notation

When using the OGNL notation from the simple language, the `camel-quarkus-bean` extension should be used.

For instance, the simple expression below is accessing the `getAddress()` method on the message body of type `Client`.

```java
simple("${body.address}")
```

In such a situation, one should take an additional dependency on the camel-quarkus-bean extension [as described here](../../../../components/4.18.x/bean-component.md). Note that in native mode, some classes may need to be registered for reflection. In the example above, the `Client` class needs to be [registered for reflection](https://quarkus.io/guides/writing-native-applications-tips#registering-for-reflection).

#### Using dynamic type resolution in native mode

When dynamically resolving a type from simple expressions like:

-   `simple("${mandatoryBodyAs(TYPE)}")`
    
-   `simple("${type:package.Enum.CONSTANT}")`
    
-   `from("…​").split(bodyAs(TYPE.class))`
    
-   `simple("${body} is TYPE")`
    

It may be needed to register some classes for reflection manually.

For instance, the simple expression below is dynamically resolving the type `java.nio.ByteBuffer` at runtime:

```java
simple("${body} is 'java.nio.ByteBuffer'")
```

As such, the class `java.nio.ByteBuffer` needs to be [registered for reflection](https://quarkus.io/guides/writing-native-applications-tips#registering-for-reflection).

#### Using the simple language with classpath resources in native mode

If your route is supposed to load a Simple script from classpath, like in the following example

```java
from("direct:start").transform().simple("resource:classpath:mysimple.txt");
```

then you need to use Quarkus `quarkus.native.resources.includes` property to include the resource in the native executable as demonstrated below:

```properties
quarkus.native.resources.includes = mysimple.txt
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resource in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).

#### Configuring a custom bean via properties in native mode

When specifying a custom bean via properties in native mode with configuration like `#class:*` or `#type:*`, it may be needed to register some classes for reflection manually.

For instance, the custom bean definition below involves the use of reflection for bean instantiation and setter invocation:

```properties
---
camel.beans.customBeanWithSetterInjection = #class:org.example.PropertiesCustomBeanWithSetterInjection
camel.beans.customBeanWithSetterInjection.counter = 123
---
```

As such, the class `PropertiesCustomBeanWithSetterInjection` needs to be [registered for reflection](https://quarkus.io/guides/writing-native-applications-tips#registering-for-reflection), note that field access could be omitted in this case.

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.service.discovery.exclude-patterns](#quarkus-camel-service-discovery-exclude-patterns)`
A comma-separated list of Ant-path style patterns to match Camel service definition files in the classpath. The services defined in the matching files will **not** be discoverable via the \*\*`org.apache.camel.spi.FactoryFinder` mechanism.

The excludes have higher precedence than includes. The excludes defined here can also be used to veto the discoverability of services included by Camel Quarkus extensions.

Example values: `META-INF/services/org/apache/camel/foo/*,META-INF/services/org/apache/camel/foo/**/bar`

 | List of `string` |  |
| `[quarkus.camel.service.discovery.include-patterns](#quarkus-camel-service-discovery-include-patterns)`

A comma-separated list of Ant-path style patterns to match Camel service definition files in the classpath. The services defined in the matching files will be discoverable via the `org.apache.camel.spi.FactoryFinder` mechanism unless the given file is excluded via `exclude-patterns`.

Note that Camel Quarkus extensions may include some services by default. The services selected here added to those services and the exclusions defined in `exclude-patterns` are applied to the union set.

Example values: `META-INF/services/org/apache/camel/foo/*,META-INF/services/org/apache/camel/foo/**/bar`

 | List of `string` |  |
| `[quarkus.camel.service.registry.exclude-patterns](#quarkus-camel-service-registry-exclude-patterns)`

A comma-separated list of Ant-path style patterns to match Camel service definition files in the classpath. The services defined in the matching files will **not** be added to Camel registry during application’s static initialization.

The excludes have higher precedence than includes. The excludes defined here can also be used to veto the registration of services included by Camel Quarkus extensions.

Example values: `META-INF/services/org/apache/camel/foo/*,META-INF/services/org/apache/camel/foo/**/bar`\*\*

 | List of `string` |  |
| `[quarkus.camel.service.registry.include-patterns](#quarkus-camel-service-registry-include-patterns)`

A comma-separated list of Ant-path style patterns to match Camel service definition files in the classpath. The services defined in the matching files will be added to Camel registry during application’s static initialization unless the given file is excluded via `exclude-patterns`.

Note that Camel Quarkus extensions may include some services by default. The services selected here added to those services and the exclusions defined in `exclude-patterns` are applied to the union set.

Example values: `META-INF/services/org/apache/camel/foo/*,META-INF/services/org/apache/camel/foo/**/bar`

 | List of `string` |  |
| `[quarkus.camel.runtime-catalog.components](#quarkus-camel-runtime-catalog-components)`

If `true` the Runtime Camel Catalog embedded in the application will contain JSON schemas of Camel components available in the application; otherwise component JSON schemas will not be available in the Runtime Camel Catalog and any attempt to access those will result in a RuntimeException.

Setting this to `false` helps to reduce the size of the native image. In JVM mode, there is no real benefit of setting this flag to `false` except for making the behavior consistent with native mode.

 | `boolean` | `true` |
| `[quarkus.camel.runtime-catalog.languages](#quarkus-camel-runtime-catalog-languages)`

If `true` the Runtime Camel Catalog embedded in the application will contain JSON schemas of Camel languages available in the application; otherwise language JSON schemas will not be available in the Runtime Camel Catalog and any attempt to access those will result in a RuntimeException.

Setting this to `false` helps to reduce the size of the native image. In JVM mode, there is no real benefit of setting this flag to `false` except for making the behavior consistent with native mode.

 | `boolean` | `true` |
| `[quarkus.camel.runtime-catalog.dataformats](#quarkus-camel-runtime-catalog-dataformats)`

If `true` the Runtime Camel Catalog embedded in the application will contain JSON schemas of Camel data formats available in the application; otherwise data format JSON schemas will not be available in the Runtime Camel Catalog and any attempt to access those will result in a RuntimeException.

Setting this to `false` helps to reduce the size of the native image. In JVM mode, there is no real benefit of setting this flag to `false` except for making the behavior consistent with native mode.

 | `boolean` | `true` |
| `[quarkus.camel.runtime-catalog.devconsoles](#quarkus-camel-runtime-catalog-devconsoles)`

If `true` the Runtime Camel Catalog embedded in the application will contain JSON schemas of Camel dev consoles available in the application; otherwise dev console JSON schemas will not be available in the Runtime Camel Catalog and any attempt to access those will result in a RuntimeException.

Setting this to `false` helps to reduce the size of the native image. In JVM mode, there is no real benefit of setting this flag to `false` except for making the behavior consistent with native mode.

 | `boolean` | `true` |
| `[quarkus.camel.runtime-catalog.models](#quarkus-camel-runtime-catalog-models)`

If `true` the Runtime Camel Catalog embedded in the application will contain JSON schemas of Camel EIP models available in the application; otherwise EIP model JSON schemas will not be available in the Runtime Camel Catalog and any attempt to access those will result in a RuntimeException.

Setting this to `false` helps to reduce the size of the native image. In JVM mode, there is no real benefit of setting this flag to `false` except for making the behavior consistent with native mode.

 | `boolean` | `true` |
| `[quarkus.camel.runtime-catalog.transformers](#quarkus-camel-runtime-catalog-transformers)`

If `true` the Runtime Camel Catalog embedded in the application will contain JSON schemas of Camel transformers available in the application; otherwise transformer JSON schemas will not be available in the Runtime Camel Catalog and any attempt to access those will result in a RuntimeException.

Setting this to `false` helps to reduce the size of the native image. In JVM mode, there is no real benefit of setting this flag to `false` except for making the behavior consistent with native mode.

 | `boolean` | `true` |
| `[quarkus.camel.routes-discovery.exclude-patterns](#quarkus-camel-routes-discovery-exclude-patterns)`

Used for exclusive filtering scanning of RouteBuilder classes. The exclusive filtering takes precedence over inclusive filtering. The pattern is using Ant-path style pattern. Multiple patterns can be specified separated by comma. For example to exclude all classes starting with Bar use: \*\*/Bar\* To exclude all routes from a specific package use: com/mycompany/bar/\* To exclude all routes from a specific package and its sub-packages use double wildcards: com/mycompany/bar/\*\* And to exclude all routes from two specific packages use: com/mycompany/bar/\*,com/mycompany/stuff/\*

 | List of `string` |  |
| `[quarkus.camel.routes-discovery.include-patterns](#quarkus-camel-routes-discovery-include-patterns)`

Used for inclusive filtering scanning of RouteBuilder classes. The exclusive filtering takes precedence over inclusive filtering. The pattern is using Ant-path style pattern. Multiple patterns can be specified separated by comma. For example to include all classes starting with Foo use: \*\*/Foo\* To include all routes from a specific package use: com/mycompany/foo/\* To include all routes from a specific package and its sub-packages use double wildcards: com/mycompany/foo/\*\* And to include all routes from two specific packages use: com/mycompany/foo/\*,com/mycompany/stuff/\*

 | List of `string` |  |
| `[quarkus.camel.native.reflection.exclude-patterns](#quarkus-camel-native-reflection-exclude-patterns)`

A comma separated list of Ant-path style patterns to match class names that should be **excluded** from registering for reflection. Use the class name format as returned by the `java.lang.Class.getName()` method: package segments delimited by period `.` and inner classes by dollar sign `$`.

This option narrows down the set selected by `include-patterns`. By default, no classes are excluded.

This option cannot be used to unregister classes which have been registered internally by Quarkus extensions.

 | List of `string` |  |
| `[quarkus.camel.native.reflection.include-patterns](#quarkus-camel-native-reflection-include-patterns)`

A comma separated list of Ant-path style patterns to match class names that should be registered for reflection. Use the class name format as returned by the `java.lang.Class.getName()` method: package segments delimited by period `.` and inner classes by dollar sign `$`.

By default, no classes are included. The set selected by this option can be narrowed down by `exclude-patterns`.

Note that Quarkus extensions typically register the required classes for reflection by themselves. This option is useful in situations when the built in functionality is not sufficient.

Note that this option enables the full reflective access for constructors, fields and methods. If you need a finer grained control, consider using `io.quarkus.runtime.annotations.RegisterForReflection` annotation in your Java code.

For this option to work properly, at least one of the following conditions must be satisfied:

-   There are no wildcards (`*` or `/`) in the patterns
    
-   The artifacts containing the selected classes contain a Jandex index (`META-INF/jandex.idx`)
    
-   The artifacts containing the selected classes are registered for indexing using the `quarkus.index-dependency.*` family of options in `application.properties` - e.g.
    

```properties
quarkus.index-dependency.my-dep.group-id = org.my-group
quarkus.index-dependency.my-dep.artifact-id = my-artifact
```

where `my-dep` is a label of your choice to tell Quarkus that `org.my-group` and with `my-artifact` belong together.

 | List of `string` |  |
| `[quarkus.camel.native.reflection.serialization-enabled](#quarkus-camel-native-reflection-serialization-enabled)`

If `true`, basic classes are registered for serialization; otherwise basic classes won’t be registered automatically for serialization in native mode. The list of classes automatically registered for serialization can be found in [CamelSerializationProcessor.BASE\_SERIALIZATION\_CLASSES](https://github.com/apache/camel-quarkus/blob/main/extensions-core/core/deployment/src/main/java/org/apache/camel/quarkus/core/deployment/CamelSerializationProcessor.java). Setting this to `false` helps to reduce the size of the native image. In JVM mode, there is no real benefit of setting this flag to `true` except for making the behavior consistent with native mode.

 | `boolean` | `false` |
| `[quarkus.camel.expression.on-build-time-analysis-failure](#quarkus-camel-expression-on-build-time-analysis-failure)`

What to do if it is not possible to extract expressions from a route definition at build time.

 | `fail`, `warn`, `ignore` | `warn` |
| `[quarkus.camel.expression.extraction-enabled](#quarkus-camel-expression-extraction-enabled)`

Indicates whether the expression extraction from the route definitions at build time must be done. If disabled, the expressions are compiled at runtime.

 | `boolean` | `true` |
| `[quarkus.camel.event-bridge.enabled](#quarkus-camel-event-bridge-enabled)`

Whether to enable the bridging of Camel events to CDI events.

This allows CDI observers to be configured for Camel events. E.g. those belonging to the `org.apache.camel.quarkus.core.events`, `org.apache.camel.quarkus.main.events` & `org.apache.camel.impl.event` packages.

Note that this configuration item only has any effect when observers configured for Camel events are present in the application.

 | `boolean` | `true` |
| `[quarkus.camel.source-location-enabled](#quarkus-camel-source-location-enabled)`

Build time configuration options for enable/disable camel source location.

 | `boolean` | `false` |
| `[quarkus.camel.trace.enabled](#quarkus-camel-trace-enabled)`

Enables tracer in your Camel application.

 | `boolean` | `false` |
| `[quarkus.camel.trace.standby](#quarkus-camel-trace-standby)`

To set the tracer in standby mode, where the tracer will be installed, but not automatically enabled. The tracer can then be enabled explicitly later from Java, JMX or tooling.

 | `boolean` | `false` |
| `[quarkus.camel.trace.backlog-size](#quarkus-camel-trace-backlog-size)`

Defines how many of the last messages to keep in the tracer.

 | `int` | `1000` |
| `[quarkus.camel.trace.remove-on-dump](#quarkus-camel-trace-remove-on-dump)`

Whether all traced messages should be removed when the tracer is dumping. By default, the messages are removed, which means that dumping will not contain previous dumped messages.

 | `boolean` | `true` |
| `[quarkus.camel.trace.body-max-chars](#quarkus-camel-trace-body-max-chars)`

To limit the message body to a maximum size in the traced message. Use 0 or negative value to use unlimited size.

 | `int` | `131072` |
| `[quarkus.camel.trace.body-include-streams](#quarkus-camel-trace-body-include-streams)`

Whether to include the message body of stream based messages. If enabled then beware the stream may not be re-readable later. See more about Stream Caching.

 | `boolean` | `false` |
| `[quarkus.camel.trace.body-include-files](#quarkus-camel-trace-body-include-files)`

Whether to include the message body of file based messages. The overhead is that the file content has to be read from the file.

 | `boolean` | `true` |
| `[quarkus.camel.trace.include-exchange-properties](#quarkus-camel-trace-include-exchange-properties)`

Whether to include the exchange properties in the traced message.

 | `boolean` | `true` |
| `[quarkus.camel.trace.include-exchange-variables](#quarkus-camel-trace-include-exchange-variables)`

Whether to include the exchange variables in the traced message.

 | `boolean` | `true` |
| `[quarkus.camel.trace.include-exception](#quarkus-camel-trace-include-exception)`

Whether to include the exception in the traced message in case of failed exchange.

 | `boolean` | `true` |
| `[quarkus.camel.trace.trace-rests](#quarkus-camel-trace-trace-rests)`

Whether to trace routes that is created from Rest DSL.

 | `boolean` | `false` |
| `[quarkus.camel.trace.trace-templates](#quarkus-camel-trace-trace-templates)`

Whether to trace routes that is created from route templates or kamelets.

 | `boolean` | `false` |
| `[quarkus.camel.trace.trace-pattern](#quarkus-camel-trace-trace-pattern)`

Filter for tracing by route or node id.

 | `string` |  |
| `[quarkus.camel.trace.trace-filter](#quarkus-camel-trace-trace-filter)`

Filter for tracing messages.

 | `string` |  |
| `[quarkus.camel.type-converter.statistics-enabled](#quarkus-camel-type-converter-statistics-enabled)`

Whether type converter statistics are enabled. By default, type converter utilization statistics are disabled. Note that enabling statistics incurs a minor performance impact under very heavy load.

 | `boolean` | `false` |
| `[quarkus.camel.dev-ui.update-interval](#quarkus-camel-dev-ui-update-interval)`

The interval at which data is updated in Camel Quarkus Dev UI pages.

 | [`Duration`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Duration.md)[](#duration-note-anchor-core) | `5S` |
| `[quarkus.camel.main.shutdown.timeout](#quarkus-camel-main-shutdown-timeout)`

A timeout (with millisecond precision) to wait for `CamelMain#stop()` to finish

 | [`Duration`](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Duration.md)[](#duration-note-anchor-core) | `PT3S` |
| `[quarkus.camel.main.arguments.on-unknown](#quarkus-camel-main-arguments-on-unknown)`

The action to take when `CamelMain` encounters an unknown argument. fail - Prints the `CamelMain` usage statement and throws a `RuntimeException` ignore - Suppresses any warnings and the application startup proceeds as normal warn - Prints the `CamelMain` usage statement but allows the application startup to proceed as normal

 | `fail`, `warn`, `ignore` | `warn` |
| 

`[camel.dataformat."data-format-configs"](#camel-dataformat-data-format-configs)`

Camel data format configuration.

The format of the configuration is as follows.

```properties
camel.dataformat.<name>.<property> = value
```

For example.

```properties
camel.dataformat.beanio.stream-name = test-stream
camel.dataformat.beanio.mapping = test-mapping.xml
```







 | `Map<String,Map<String,String>>` |  |
| `[quarkus.camel.bootstrap.enabled](#quarkus-camel-bootstrap-enabled)`

When set to true, the {@link CamelRuntime} will be started automatically.

 | `boolean` | `true` |
| `[quarkus.camel.routes-discovery.enabled](#quarkus-camel-routes-discovery-enabled)`

Enable automatic discovery of routes during static initialization.

 | `boolean` | `true` |
| `[quarkus.camel.csimple.on-build-time-analysis-failure](#quarkus-camel-csimple-on-build-time-analysis-failure)`

What to do if it is not possible to extract CSimple expressions from a route definition at build time.

 | `fail`, `warn`, `ignore` | `warn` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.

> **Note**
> About the Duration format
>
> To write duration values, use the standard `java.time.Duration` format. See the [Duration#parse() Java API documentation](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/time/Duration.html#parse\(java.lang.CharSequence\)) for more information.
>
> You can also use a simplified format, starting with a number:
>
> -   If the value is only a number, it represents time in seconds.
>     
> -   If the value is a number followed by `ms`, it represents time in milliseconds.
>     
>
> In other cases, the simplified format is translated to the `java.time.Duration` format for parsing:
>
> -   If the value is a number followed by `h`, `m`, or `s`, it is prefixed with `PT`.
>     
> -   If the value is a number followed by `d`, it is prefixed with `P`.