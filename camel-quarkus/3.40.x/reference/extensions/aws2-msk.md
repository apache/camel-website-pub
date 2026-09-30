# AWS 2 Managed Streaming for Apache Kafka (MSK)

JVM since1.0.0 Native since1.0.0

Manage AWS MSK instances.

## What’s inside

-   [AWS Managed Streaming for Apache Kafka (MSK) component](../../../../components/4.22.x/aws2-msk-component.md), URI syntax: `aws2-msk:label`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-aws2-msk)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-aws2-msk</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).