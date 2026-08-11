# AMQP

JVM since1.0.0 Native since1.0.0

Messaging with AMQP protocol using Apache Qpid Client.

## What’s inside

-   [AMQP component](../../../../components/next/amqp-component.md), URI syntax: `amqp:destinationType:destinationName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-amqp)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-amqp</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

This extension leverages [Quarkus Qpid JMS](https://github.com/amqphub/quarkus-qpid-jms/). A `ConnectionFactory` bean is created automatically and wired into the AMQP component for you. The connection factory can be configured via the Quarkus Qpid JMS [configuration options](https://github.com/amqphub/quarkus-qpid-jms#configuration).

### Message mapping with `org.w3c.dom.Node`

The Camel AMQP component supports message mapping between `jakarta.jms.Message` and `org.apache.camel.Message`. When wanting to convert a Camel message body type of `org.w3c.dom.Node`, you must ensure that the `camel-quarkus-xml-jaxp` extension is present on the classpath.

### Native mode support for jakarta.jms.ObjectMessage

When sending JMS message payloads as `jakarta.jms.ObjectMessage`, you must annotate the relevant classes to be registered for serialization with `@RegisterForReflection(serialization = true)`. Note that this extension automatically sets `quarkus.camel.native.reflection.serialization-enabled = true` for you. Refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

### Connection Pooling

You can use the `quarkus-pooled-jms` extension to get pooling support for the connections. Refer to the [quarkus-pooled-jms](https://quarkiverse.github.io/quarkiverse-docs/quarkus-pooled-jms/dev/index.md) extension documentation for more information.

Just add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>io.quarkiverse.messaginghub</groupId>
    <artifactId>quarkus-pooled-jms</artifactId>
</dependency>
```

To enable the pooling support, you need to add the following configuration to your `application.properties`:

```properties
quarkus.qpid-jms.wrap=true
```

## transferException option in native mode

To use the `transferException` option in native mode, you must enable support for object serialization. Refer to the [native mode user guide](../../user-guide/native-mode.html#serialization) for more information.

You will also need to enable serialization for the exception classes that you intend to serialize. For example.

```java
@RegisterForReflection(targets = { IllegalStateException.class, MyCustomException.class }, serialization = true)
```