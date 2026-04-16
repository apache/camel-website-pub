# ActiveMQ

JVM since1.0.0 Native since1.0.0

Send messages to (or consume from) Apache ActiveMQ 5.x. This component extends the Camel JMS component.

## What’s inside

-   [ActiveMQ 5.x component](../../../../components/next/activemq-component.md), URI syntax: `activemq:destinationType:destinationName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-activemq)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-activemq</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Message mapping with `org.w3c.dom.Node`

The Camel ActiveMQ component supports message mapping between `jakarta.jms.Message` and `org.apache.camel.Message`. When wanting to convert a Camel message body type of `org.w3c.dom.Node`, you must ensure that the `camel-quarkus-xml-jaxp` extension is present on the classpath.

### Native mode support for jakarta.jms.ObjectMessage

When sending JMS message payloads as `jakarta.jms.ObjectMessage`, you must annotate the relevant classes to be registered for serialization with `@RegisterForReflection(serialization = true)`. Note that this extension automatically sets `quarkus.camel.native.reflection.serialization-enabled = true` for you. Refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

## Camel Quarkus limitations

ActiveMQ [XPath selectors](https://activemq.apache.org/selectors.md) are disabled in native mode as the functionality depends on `activemq-broker`. This dependency is excluded from the dependency tree, since none of the ActiveMQ broker functionality is supported in native mode.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).

## transferException option in native mode

To use the `transferException` option in native mode, you must enable support for object serialization. Refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

You will also need to enable serialization for the exception classes that you intend to serialize. For example.

```java
@RegisterForReflection(targets = { IllegalStateException.class, MyCustomException.class }, serialization = true)
```