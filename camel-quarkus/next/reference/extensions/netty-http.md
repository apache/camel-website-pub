# Netty HTTP

JVM since0.2.0 Native since0.2.0

The Netty HTTP extension provides HTTP transport on top of the [Netty extension](netty.md).

## What’s inside

-   [Netty HTTP component](../../../../components/4.22.x/netty-http-component.md), URI syntax: `netty-http:protocol://host:port/path`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-netty-http)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-netty-http</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## transferException option in native mode

To use the `transferException` option in native mode, you must enable support for object serialization. Refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

You will also need to enable serialization for the exception classes that you intend to serialize. For example.

```java
@RegisterForReflection(targets = { IllegalStateException.class, MyCustomException.class }, serialization = true)
```

## Additional Camel Quarkus configuration

-   Check the [Character encodings section](../../user-guide/native-mode.html#charsets) of the Native mode guide if you expect your application to send or receive requests using non-default encodings.