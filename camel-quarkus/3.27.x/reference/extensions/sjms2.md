# Simple JMS2

JVM since1.0.0 Native since1.0.0

Send and receive messages to/from a JMS Queue or Topic using plain JMS 2.x API.

## What’s inside

-   [Simple JMS2 component](../../../../components/4.14.x/sjms2-component.md), URI syntax: `sjms2:destinationType:destinationName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-sjms2)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-sjms2</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Message mapping with `org.w3c.dom.Node`

The Camel SJMS2 component supports message mapping between `jakarta.jms.Message` and `org.apache.camel.Message`. When wanting to convert a Camel message body type of `org.w3c.dom.Node`, you must ensure that the `camel-quarkus-xml-jaxp` extension is present on the classpath.

### Native mode support for jakarta.jms.ObjectMessage

When sending JMS message payloads as `jakarta.jms.ObjectMessage`, you must annotate the relevant classes to be registered for serialization with `@RegisterForReflection(serialization = true)`. Note that this extension automatically sets `quarkus.camel.native.reflection.serialization-enabled = true` for you. Refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

## transferException option in native mode

To use the `transferException` option in native mode, you must enable support for object serialization. Refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

You will also need to enable serialization for the exception classes that you intend to serialize. For example.

```java
@RegisterForReflection(targets = { IllegalStateException.class, MyCustomException.class }, serialization = true)
```