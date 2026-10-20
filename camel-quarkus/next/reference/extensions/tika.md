# Tika

JVM since1.0.0 Native since1.0.0

Parse documents and extract metadata and text using Apache Tika.

## What’s inside

-   [Tika component](../../../../components/next/tika-component.md), URI syntax: `tika:operation`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-tika)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-tika</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Parser modules

Tika parses only the formats whose parser module is on the classpath. `camel-tika` brings the HTML and plain text modules. For any other format, add its module to your application, e.g. for PDF:

```xml
<dependency>
    <groupId>org.apache.tika</groupId>
    <artifactId>tika-parser-pdf-module</artifactId>
</dependency>
```

The Camel Quarkus BOM manages the version of `tika-parser-pdf-module` only. For other modules, use the version of `org.apache.tika:tika-core` that `camel-tika` brings.

In native mode, the HTML, plain text and PDF modules are supported.