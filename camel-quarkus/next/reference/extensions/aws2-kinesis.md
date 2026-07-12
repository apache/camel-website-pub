# AWS 2 Kinesis

JVM since1.1.0 Native since1.7.0

Consume and produce records from and to AWS Kinesis Streams. Produce data to AWS Kinesis Firehose streams.

## What’s inside

-   [AWS Kinesis component](../../../../components/next/aws2-kinesis-component.md), URI syntax: `aws2-kinesis:streamName`
    
-   [AWS Kinesis Firehose component](../../../../components/next/aws2-kinesis-firehose-component.md), URI syntax: `aws2-kinesis-firehose:streamName`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-aws2-kinesis)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-aws2-kinesis</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).