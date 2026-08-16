# Splunk HEC

JVM since1.1.0 Native since3.8.0

The splunk component allows publishing events in Splunk using the HTTP Event Collector.

## What’s inside

-   [Splunk HEC component](../../../../components/4.22.x/splunk-hec-component.md), URI syntax: `splunk-hec:splunkURL`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-splunk-hec)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-splunk-hec</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).