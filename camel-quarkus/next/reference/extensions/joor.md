# jOOR

JVM since2.0.0 Native since3.2.0 ⚠️Deprecated

Evaluate a jOOR (Java compiled once at runtime) expression language.

## What’s inside

-   [Java language](../../../../components/4.22.x/languages/java-language.md)
    
-   [jOOR language](../../../../components/4.22.x/languages/joor-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-joor)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-joor</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

The expressions and scripts written using the jOOR language are extracted and compiled at build time, to do so the language needs to be instantiated and configured at build time in order to be able to generate the exact same source code as the one generated at runtime. For this purpose, the next configuration properties have been added:

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.joor.single-quotes](#quarkus-camel-joor-single-quotes)`
Indicates whether a jOOR expression can use single quotes instead of double quotes.

 | `boolean` | `true` |
| `[quarkus.camel.joor.config-resource](#quarkus-camel-joor-config-resource)`

The specific location of the configuration of the jOOR language.

 | `string` |  |
| `[quarkus.camel.joor.compile-at-build-time](#quarkus-camel-joor-compile-at-build-time)`

In JVM mode, indicates whether the expressions must be compiled at build time.

 | `boolean` | `false` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.