# SmallRye Reactive Messaging

JVM since1.0.0 Native since1.0.0

Camel integration with SmallRye Reactive Messaging

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-smallrye-reactive-messaging)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-smallrye-reactive-messaging</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

This extension leverages [SmallRye Reactive Messaging](https://www.smallrye.io/smallrye-reactive-messaging/). Examples for how to use the Camel connector are outlined within the [documentation](https://www.smallrye.io/smallrye-reactive-messaging/).

> **Note**
> Where the SmallRye Reactive Messaging documentation makes references to Camel component maven dependencies, you should ensure that the corresponding camel-quarkus extension is used. E.g. `<artifactId>camel-file</artifactId>` should be `<artifactId>camel-quarkus-file</artifactId>`.
>
> When using this extension, there is no need to explicitly add `io.smallrye.reactive:smallrye-reactive-messaging-camel` or `io.quarkus:quarkus-quarkus-smallrye-reactive-messaging` to your project.

## Additional Camel Quarkus configuration

This extension leverages the Camel [Reactive Streams](reactive-streams.md) extension. Various aspects of the reactive streams component can be configured via the configuration options outlined within the [documentation](reactive-streams.md).

This extension also leverages the Quarkus SmallRye Reactive Messaging extension. Its configuration options are documented [here](https://quarkus.io/guides/all-config#quarkus-smallrye-reactive-messaging_quarkus-smallrye-reactive-messaging).