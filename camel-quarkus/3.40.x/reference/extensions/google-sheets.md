# Google Sheets

JVM since1.0.0 Native since1.0.0

Manage spreadsheets in Google Sheets.

## What’s inside

-   [Google Sheets component](../../../../components/4.22.x/google-sheets-component.md), URI syntax: `google-sheets:apiName/methodName`
    
-   [Google Sheets Stream component](../../../../components/4.22.x/google-sheets-stream-component.md), URI syntax: `google-sheets-stream:spreadsheetId`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-google-sheets)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-google-sheets</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).