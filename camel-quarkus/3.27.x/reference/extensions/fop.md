# FOP

JVM since1.1.0 Native since1.2.0

Render messages into PDF and other output formats supported by Apache FOP.

## What’s inside

-   [FOP component](../../../../components/4.14.x/fop-component.md), URI syntax: `fop:outputType`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-fop)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-fop</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

While you can use any of the available output types in JVM mode, only PDF output type is supported in native mode.

Please file an [issue](https://github.com/apache/camel-quarkus/issues/new) if you are missing some specific output format in native mode.