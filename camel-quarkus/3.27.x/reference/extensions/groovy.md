# Groovy

JVM since1.0.0 Native since3.2.0

Evaluate a Groovy script

## What’s inside

-   [Groovy language](../../../../components/4.14.x/languages/groovy-language.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-groovy)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-groovy</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

### Native mode limitations

> **Important**
> Due to an issue in GraalVM / Mandrel 23.1.x, you **must** build your native application with the [`--report-unsupported-elements-at-runtime`](https://quarkus.io/guides/all-config#quarkus-core_quarkus-native-report-errors-at-runtime) option. You can do this by adding the following configuration to `application.properties`.
>
> ```properties
> quarkus.native.report-errors-at-runtime=true
> ```

Compilation of Groovy expressions is made with static compilation enabled. Which means that the types used in your expressions must be known at compile time. Please refer to the [Groovy documentation for more details](https://docs.groovy-lang.org/latest/html/documentation/core-semantics.html#static-type-checking).

This primarily impacts the customization of the Groovy Shell and the handling of exchange information. In native mode, customizing the Groovy Shell and accessing the following exchange variables will not function as expected.

-   `attachment`
    
-   `exchangeProperty`
    
-   `exchangeProperties`
    
-   `header`
    
-   `log`
    
-   `variable`
    
-   `variables`
    

If you use property placeholders within your expressions like.

```java
from("direct:start")
    .transform().groovy("println '{{greeting.message}}'");
```

`greeting.message` will be evaluated once at build time and its value will be permanently stored in the native image. It is not possible to override the value of the property at runtime. Attempting to do so will result in an exception being thrown.