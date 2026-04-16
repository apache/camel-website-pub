# Disruptor

JVM since1.1.0 Native since1.2.0

Provides asynchronous SEDA behavior using LMAX Disruptor.

## What’s inside

-   [Disruptor component](../../../../components/next/disruptor-component.md), URI syntax: `disruptor:name`
    
-   [Disruptor VM component](../../../../components/next/disruptor-component.md), URI syntax: `disruptor-vm:name`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-disruptor)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-disruptor</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

The `disruptor-vm` component is not available on Camel Quarkus. This is because it is supposed to provide support for communication across multiple CamelContext instances within a single JVM, but by design, there is always just a single `CamelContext` on Camel Quarkus. Therefore `disruptor-vm` would make no sense.