# AWS 2 Eventbridge

JVM since1.4.0 Native since1.7.0

Manage AWS EventBridge cluster instances and consume events via SQS-backed polling.

## What’s inside

-   [AWS Eventbridge component](../../../../components/next/aws2-eventbridge-component.md), URI syntax: `aws2-eventbridge://eventbusNameOrArn`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-aws2-eventbridge)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-aws2-eventbridge</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).