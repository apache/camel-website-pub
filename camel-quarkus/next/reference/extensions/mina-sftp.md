# MINA SFTP

JVM since3.33.0 Native since3.33.0

Upload and download files to/from SFTP servers using Apache MINA SSHD.

## What’s inside

-   [MINA SFTP component](../../../../components/4.22.x/mina-sftp-component.md), URI syntax: `mina-sftp:host:port/directoryName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-mina-sftp)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-mina-sftp</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

### Incompatibility with camel-quarkus-ftp extension

The `camel-quarkus-mina-sftp` and `camel-quarkus-ftp` extensions cannot be used together in the same application. If you have both extension dependencies on the classpath, you are likely to encounter problems at build time when compiling your application.