# AWS 2 Simple Notification System (SNS)

JVM since1.0.0 Native since1.0.0

Send messages to AWS Simple Notification Topic.

## What’s inside

-   [AWS Simple Notification System (SNS) component](../../../../components/4.18.x/aws2-sns-component.md), URI syntax: `aws2-sns:topicNameOrArn`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-aws2-sns)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-aws2-sns</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).