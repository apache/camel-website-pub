# Flatpack

JVM since1.1.0 Native since1.1.0

Parse fixed width and delimited files using the FlatPack library.

## What’s inside

-   [Flatpack component](../../../../components/4.14.x/flatpack-component.md), URI syntax: `flatpack:type:resourceUri`
    
-   [Flatpack data format](../../../../components/4.14.x/dataformats/flatpack-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-flatpack)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-flatpack</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

This component typically loads Flatpack mappings from classpath. To make it work also in native mode, you need to explicitly embed the mappings in the native executable by using the `quarkus.native.resources.includes` property.

For instance, the route below loads the Flatpack mappings from a classpath resource named `mappings/simple.pzmap.xml`:

```java
from("direct:start").to("flatpack:delim:mappings/simple.pzmap.xml");
```

To include this (an possibly other mappings stored in `.pzmap.xml` files under the `mappings` directory) in the native image, you would have to add something like the following to your `application.properties` file:

```properties
quarkus.native.resources.includes = mappings/*.pzmap.xml
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resource in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).