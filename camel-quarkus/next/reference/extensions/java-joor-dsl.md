# Java jOOR DSL

JVM since1.8.0 Native since2.16.0

Support for parsing Java route definitions at runtime

## What’s inside

-   [Java DSL (runtime compiled)](../../../../components/next/others/java-joor-dsl.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-java-joor-dsl)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-java-joor-dsl</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

The annotations added to the classes to be compiled by the component are ignored by Quarkus. The only annotation that is partially supported by the extension is the annotation `RegisterForReflection` to ease the configuration of the reflection for the native mode however please note that the element `registerFullHierarchy` is not supported.