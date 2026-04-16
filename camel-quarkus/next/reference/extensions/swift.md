# SWIFT

JVM since3.2.0 Native since3.2.0

Encode and decode SWIFT messages.

## What’s inside

-   [SWIFT MT data format](../../../../components/next/dataformats/swiftMt-dataformat.md)
    
-   [SWIFT MX data format](../../../../components/next/dataformats/swiftMx-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-swift)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-swift</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

### MX types

The MX message types are not supported in native mode because it drastically slows down the native image build due to an excessive amount of classes, methods, and fields to access by reflection that need to be registered.