# AWS 2 Simple Queue Service (SQS)

JVM since1.0.0 Native since1.0.0

Send and receive messages to/from AWS SQS.

## What’s inside

-   [AWS Simple Queue Service (SQS) component](../../../../components/next/aws2-sqs-component.md), URI syntax: `aws2-sqs:queueNameOrArn`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-aws2-sqs)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-aws2-sqs</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).