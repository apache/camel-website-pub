# JOLT

JVM since1.0.0 Native since1.0.0

JSON to JSON transformation using JOLT.

## What’s inside

-   [JOLT component](../../../../components/4.14.x/jolt-component.md), URI syntax: `jolt:resourceUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jolt)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jolt</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

This component typically loads its specs from classpath resources. To make it work also in native mode, you need to explicitly embed the spec files in the native executable by using the `quarkus.native.resources.includes` property.

For instance, the route below would load the Jolt spec from a classpath resource named `defaultr.json`:

```java
from("direct:start").to("jolt:defaultr.json");
```

To include this (an possibly other specs stored in `.json` files) in the native image, you would have to add something like the following to your `application.properties` file:

```properties
quarkus.native.resources.includes = *.json
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resource in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).