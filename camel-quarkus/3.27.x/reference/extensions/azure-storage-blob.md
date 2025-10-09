# Azure Storage Blob Service

JVM since1.1.0 Native since1.6.0

Store and retrieve blobs from Azure Storage Blob Service using SDK v12.

## What’s inside

-   [Azure Storage Blob Service component](../../../../components/4.14.x/azure-storage-blob-component.md), URI syntax: `azure-storage-blob:accountName/containerName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-azure-storage-blob)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-azure-storage-blob</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Micrometer metrics support

If you wish to enable the collection of Micrometer metrics for the Reactor Netty transports, then you should declare a dependency on `quarkus-micrometer` to ensure that they are available via the Quarkus metrics HTTP endpoint.

```xml
<dependency>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-micrometer</artifactId>
</dependency>
```

## SSL in native mode

This extension auto-enables SSL support in native mode. Hence you do not need to add `quarkus.ssl.native=true` to your `application.properties` yourself. See also [Quarkus SSL guide](https://quarkus.io/guides/native-and-ssl).