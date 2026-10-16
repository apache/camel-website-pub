# MongoDB GridFS

JVM since1.0.0 Native since1.0.0

Interact with MongoDB GridFS.

## What’s inside

-   [MongoDB GridFS component](../../../../components/next/mongodb-gridfs-component.md), URI syntax: `mongodb-gridfs:connectionBean`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-mongodb-gridfs)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-mongodb-gridfs</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

The extension leverages the [Quarkus MongoDB Client](https://quarkus.io/guides/mongodb) extension. The Mongo client can be configured via the Quarkus MongoDB Client [configuration options](https://quarkus.io/guides/mongodb#configuration-reference).

The Camel Quarkus MongoDB extension automatically registers a MongoDB client bean named `camelMongoClient`. This can be referenced in the mongodb endpoint URI `connectionBean` path parameter. For example:

```java
from("direct:start")
    .to("mongodb-gridfs:camelMongoClient?database=test&operation=listAll");
```