# Google Calendar

JVM since1.0.0 Native since1.0.0

Perform various operations on a Google Calendar.

## What’s inside

-   [Google Calendar component](../../../../components/4.22.x/google-calendar-component.md), URI syntax: `google-calendar:apiName/methodName`
    
-   [Google Calendar Stream component](../../../../components/4.22.x/google-calendar-stream-component.md), URI syntax: `google-calendar-stream:index`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-google-calendar)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-google-calendar</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).