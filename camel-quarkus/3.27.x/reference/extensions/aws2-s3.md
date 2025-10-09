# AWS 2 S3 Storage Service

JVM since1.0.0 Native since1.0.0

Store and retrieve objects from AWS S3 Storage Service.

## What’s inside

-   [AWS S3 Storage Service component](../../../../components/4.14.x/aws2-s3-component.md), URI syntax: `aws2-s3://bucketNameOrArn`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-aws2-s3)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-aws2-s3</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).