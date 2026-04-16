# FOP

JVM since1.1.0 Native since1.2.0

Render messages into PDF and other output formats supported by Apache FOP.

## What’s inside

-   [FOP component](../../../../components/next/fop-component.md), URI syntax: `fop:outputType`
    

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

### JDK 25+

Due to an [issue](https://issues.apache.org/jira/browse/FOP-3275) with Apache FOP encountered with JDK 25+, [`Saxon-HE`](https://www.saxonica.com/documentation12/documentation.xml) is required to avoid reentrant XML parsing problems.

`Saxon-HE` can be added to your application as follows.

```xml
<dependency>
    <groupId>net.sf.saxon</groupId>
    <artifactId>Saxon-HE</artifactId>
</dependency>
```

### Supported Output Types

While you can use any of the available output types in JVM mode, only PDF output type is supported in native mode.

Please file an [issue](https://github.com/apache/camel-quarkus/issues/new) if you are missing some specific output format in native mode.