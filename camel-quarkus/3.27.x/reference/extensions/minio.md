# Minio

JVM since1.5.0 Native since1.6.0

Store and retrieve objects from Minio Storage Service using Minio SDK.

## What’s inside

-   [Minio component](../../../../components/4.14.x/minio-component.md), URI syntax: `minio:bucketName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-minio)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-minio</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

Depending on Minio configuration, this extension may require SSL encryption on its connections. In such cases, you will need to add `quarkus.ssl.native=true` to your `application.properties`. See also [Quarkus native SSL guide](https://quarkus.io/guides/native-and-ssl) and [Native mode](../../user-guide/native-mode.md) section of Camel Quarkus user guide.

There are two different configuration approaches:

-   Minio client can be defined via quarkus properties leveraging the Quarkiverse Minio (see [documentation](http://github.com/quarkiverse/quarkiverse-minio#configuration-reference)). Camel will autowire client into the Minio component. This configuration allows definition of only one minio client, therefore it isn’t possible to define several different minio endpoints, which run together.
    
-   Provide client/clients for camel registry (e.g. CDI producer/bean) and reference them from endpoint.
    

minio:foo?minioClient=#minioClient