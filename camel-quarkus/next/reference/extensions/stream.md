# Stream

JVM since1.0.0 Native since1.0.0

Read from system-in and write to system-out and system-err streams.

## What’s inside

-   [Stream component](../../../../components/4.18.x/stream-component.md), URI syntax: `stream:kind`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-stream)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-stream</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

-   Check the [Character encodings section](../../user-guide/native-mode.html#charsets) of the Native mode guide if you want to use non-default encodings for the stream endpoint `encoding` URI parameter.