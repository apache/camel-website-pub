# Olingo4

JVM since1.0.0 Native since1.0.0 ⚠️Deprecated

Communicate with OData 4.0 services using Apache Olingo OData API.

## What’s inside

-   [Olingo4 component](../../../../components/4.22.x/olingo4-component.md), URI syntax: `olingo4:apiName/methodName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-olingo4)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-olingo4</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).