# JQ

JVM since2.11.0 Native since2.11.0

Evaluates a JQ expression against a JSON message body

## What’s inside

-   [JQ language](../../../../components/next/languages/jq-language.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jq)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jq</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### JQ transformations to custom result types in native mode

If you choose to perform JQ transformations that specify the result class as some custom type in native mode, then you must register that type for reflection.

E.g. via the `@RegisterForReflection` annotation or configuration property `quarkus.camel.native.reflection.include-patterns`. For example:

```java
@RegisterForReflection
public class Book {
    ...
}
```

```java
public class MyJQRoutes extends RouteBuilder {
    @Override
    public void configure() {
        from("direct:jq")
            .transform().jq(".book", Book.class);
    }
}
```

Refer to the [Native mode](../../user-guide/native-mode.html#reflection) user guide for more information.