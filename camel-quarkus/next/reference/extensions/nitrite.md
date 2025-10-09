# Nitrite

JVM since1.0.0 Native since1.8.0 ⚠️Deprecated

Access Nitrite databases.

## What’s inside

-   [Nitrite component](../../../../components/4.18.x/nitrite-component.md), URI syntax: `nitrite:database`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-nitrite)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-nitrite</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

If your persistence objects in native mode implement `java.io.Serializable` and are not automatically registered for serialization, you have to register them for serialization. Look into [documentation](core.html#quarkus-camel-native-reflection-serialization-enabled) to see which classes are registered and how to register other ones.

If your persistence objects implement `org.dizitart.no2.mapper.Mappable`. All classes have to implement also `java.io.Serializable` and have to be registered for serialization (see previous option), even though the Java serialization won’t be used.