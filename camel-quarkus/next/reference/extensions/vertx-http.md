# Vert.x HTTP Client

JVM since1.1.0 Native since1.1.0

Camel HTTP client support with Vert.x

## What’s inside

-   [Vert.x HTTP Client component](../../../../components/next/vertx-http-component.md), URI syntax: `vertx-http:httpUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-vertx-http)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-vertx-http</artifactId>
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

## allowJavaSerializedObject option in native mode

When using the `allowJavaSerializedObject` option in native mode, the support of serialization might need to be enabled. Please, refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

### Character encodings

Check the [Character encodings section](../../user-guide/native-mode.html#charsets) of the Native mode guide if the application is expected to send and receive requests using non-default encodings.