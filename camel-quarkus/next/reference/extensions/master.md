# Master

JVM since1.0.0 Native since1.0.0

Have only a single consumer in a cluster consuming from a given endpoint; with automatic failover if the JVM dies.

## What’s inside

-   [Master component](../../../../components/next/master-component.md), URI syntax: `master:namespace:delegateUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-master)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-master</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

This extension can be used in conjunction with extensions below:

-   [Camel Quarkus File](file.md)
    
-   [Camel Quarkus Kubernetes](kubernetes.md)