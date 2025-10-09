# Telegram

JVM since1.0.0 Native since1.0.0

Send and receive messages using the Telegram Bot API.

## What’s inside

-   [Telegram component](../../../../components/4.14.x/telegram-component.md), URI syntax: `telegram:type`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-telegram)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-telegram</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

## Webhook Mode

The Telegram extension supports usage in the webhook mode.

In order to enable webhook mode, users need first to add a REST implementation to their application. Maven users, for example, can add **camel-quarkus-rest** extension to their `pom.xml` file:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-rest</artifactId>
</dependency>
```

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).