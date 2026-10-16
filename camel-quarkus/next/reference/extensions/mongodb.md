# MongoDB

JVM since1.0.0 Native since1.0.0

Perform operations on MongoDB documents and collections.

## What’s inside

-   [MongoDB component](../../../../components/next/mongodb-component.md), URI syntax: `mongodb:connectionBean`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-mongodb)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-mongodb</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

The extension leverages the [Quarkus MongoDB Client](https://quarkus.io/guides/mongodb) extension. The Mongo client can be configured via the Quarkus MongoDB Client [configuration options](https://quarkus.io/guides/mongodb#configuration-reference).

The Camel Quarkus MongoDB extension automatically registers a MongoDB client bean named `camelMongoClient`. This can be referenced in the mongodb endpoint URI `connectionBean` path parameter. For example:

```java
from("direct:start")
    .to("mongodb:camelMongoClient?database=myDb&collection=myCollection&operation=findAll")
```

If your application needs to work with multiple MongoDB servers, you can create a "named" client and reference in your route by injecting a client and the related configuration as explained in the [Quarkus MongoDB extension client injection](https://quarkus.io/guides/mongodb#named-mongo-client-injection). For example:

```properties
quarkus.mongodb.mongoClient1.connection-string = mongodb://root:example@localhost:27017/
```

```java
@ApplicationScoped
public class Routes extends RouteBuilder {
    @Inject
    @MongoClientName("mongoClient1")
    MongoClient mongoClient1;

    @Override
    public void configure() throws Exception {
        from("direct:defaultServer")
            .to("mongodb:camelMongoClient?database=myDb&collection=myCollection&operation=findAll");

        from("direct:otherServer")
            .to("mongodb:mongoClient1?database=myOtherDb&collection=myOtherCollection&operation=findAll");
    }
}
```

Note that when using named clients, the "default" `camelMongoClient` bean will still be produced. Refer to the Quarkus documentation on [Multiple MongoDB Clients](https://quarkus.io/guides/mongodb#multiple-mongodb-clients) for more information.