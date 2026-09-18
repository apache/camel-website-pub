# SAP NetWeaver

JVM since1.0.0 Native since1.0.0

Send requests to SAP NetWeaver Gateway using HTTP.

## What’s inside

-   [SAP NetWeaver component](../../../../components/4.22.x/sap-netweaver-component.md), URI syntax: `sap-netweaver:url`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-sap-netweaver)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-sap-netweaver</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).