# FTP

JVM since1.0.0 Native since1.0.0

Upload and download files to/from SFTP, FTP or SFTP servers

## What’s inside

-   [FTP component](../../../../components/4.22.x/ftp-component.md), URI syntax: `ftp:host:port/directoryName`
    
-   [FTPS component](../../../../components/4.22.x/ftps-component.md), URI syntax: `ftps:host:port/directoryName`
    
-   [SFTP component](../../../../components/4.22.x/sftp-component.md), URI syntax: `sftp:host:port/directoryName`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-ftp)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-ftp</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

### Incompatibility with camel-quarkus-mina-sftp extension

The `camel-quarkus-mina-sftp` and `camel-quarkus-ftp` extensions cannot be used together in the same application. If you have both extension dependencies on the classpath, you are likely to encounter problems at build time when compiling your application.