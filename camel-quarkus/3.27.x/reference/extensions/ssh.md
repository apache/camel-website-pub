# SSH

JVM since1.1.0 Native since1.2.0

Execute commands on remote hosts using SSH.

## What’s inside

-   [SSH component](../../../../components/4.14.x/ssh-component.md), URI syntax: `ssh:host:port`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-ssh)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-ssh</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

### Native mode limitations

#### EdDSA cipher on RHEL8 requires native image based on UBI8

Native image (based on UBI9 by default) requires `GLIBC 2.33`, which is not present on RHEL8. Please use native image based on `ubi8` for the native build for RHEL8 to make EdDSA work in the native mode (for example `ubi-quarkus-mandrel-builder-image:jdk-21`).