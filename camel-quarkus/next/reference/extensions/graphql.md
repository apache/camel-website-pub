# GraphQL

JVM since1.0.0 Native since1.0.0

Send GraphQL queries and mutations to external systems.

## What’s inside

-   [GraphQL component](../../../../components/next/graphql-component.md), URI syntax: `graphql:httpUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-graphql)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-graphql</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.graphql.query-files](#quarkus-camel-graphql-query-files)`
A comma separated list of paths to files containing GraphQL queries for use by GraphQL endpoints. Query files that only need to be accessible from the classpath should be specified on this property. Paths can either be schemeless (E.g. graphql/my-query.graphql) or be prefixed with the classpath: URI scheme (E.g. classpath:graphql/my-query.graphql). Other URI schemes are not supported.

 | List of `string` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.