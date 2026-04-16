# Azure Event Hubs

JVM since1.7.0 Native since1.7.0

The azure-eventhubs component that integrates Azure Event Hubs using AMQP protocol. Azure EventHubs is a highly scalable publish-subscribe service that can ingest millions of events per second and stream them to multiple consumers.

## What’s inside

-   [Azure Event Hubs component](../../../../components/next/azure-eventhubs-component.md), URI syntax: `azure-eventhubs:namespace/eventHubName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-azure-eventhubs)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-azure-eventhubs</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Micrometer metrics support

If you wish to enable the collection of Micrometer metrics for the Reactor Netty transports, then you should declare a dependency on `quarkus-micrometer` to ensure that they are available via the Quarkus metrics HTTP endpoint.

```xml
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-micrometer</artifactId>
</dependency>
```

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).