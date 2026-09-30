# AWS 2 DynamoDB

JVM since1.0.0 Native since1.0.0

Store and retrieve data from AWS DynamoDB. Receive messages from AWS DynamoDB Stream.

## What’s inside

-   [AWS DynamoDB component](../../../../components/4.22.x/aws2-ddb-component.md), URI syntax: `aws2-ddb:tableName`
    
-   [AWS DynamoDB Streams component](../../../../components/4.22.x/aws2-ddbstream-component.md), URI syntax: `aws2-ddbstream:tableName`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-aws2-ddb)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-aws2-ddb</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).