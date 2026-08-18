# File

JVM since0.4.0 Native since0.4.0

Read and write files.

## What’s inside

-   [File component](../../../../components/4.18.x/file-component.md), URI syntax: `file:directoryName`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-file)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-file</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

### Having only a single consumer in a cluster consuming from a given endpoint

This functionality is provided by the `camel-quarkus-file-cluster-service` extension. Refer to the [extension documentation](file-cluster-service.md) for more information.