# Twitter

JVM since0.2.0 Native since0.1.0

Send tweets and receive tweets, direct messages and access Twitter Search

## What’s inside

-   [Twitter Direct Message component](../../../../components/4.22.x/twitter-directmessage-component.md), URI syntax: `twitter-directmessage:user`
    
-   [Twitter Search component](../../../../components/4.22.x/twitter-search-component.md), URI syntax: `twitter-search:keywords`
    
-   [Twitter Timeline component](../../../../components/4.22.x/twitter-timeline-component.md), URI syntax: `twitter-timeline:timelineType`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-twitter)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-twitter</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).