# HTTP

JVM since1.0.0 Native since1.0.0

Send requests to external HTTP servers using Apache HTTP Client 5.x.

## What’s inside

-   [HTTP component](../../../../components/4.14.x/http-component.md), URI syntax: `[http://httpUri](http://httpUri)`
    
-   [HTTPS (Secure) component](../../../../components/4.14.x/http-component.md), URI syntax: `[https://httpUri](https://httpUri)`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-http)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-http</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).

## Additional Camel Quarkus configuration

-   Check the [Character encodings section](../../user-guide/native-mode.html#charsets) of the Native mode guide if you expect your application to send or receive requests using non-default encodings.