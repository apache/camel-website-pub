# Git

JVM since1.1.0 Native since1.1.0

Perform operations on git repositories.

## What’s inside

-   [Git component](../../../../components/4.22.x/git-component.md), URI syntax: `git:localPath`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-git)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-git</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

If you plan to run your application in native mode and the remote Git repositories it will access require SSL, you will need to set `quarkus.ssl.native=true` in your `application.properties`. See [Quarkus native and SSL guide](https://quarkus.io/guides/native-and-ssl) for more details.