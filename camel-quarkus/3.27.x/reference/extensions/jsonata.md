# JSONATA

JVM since1.6.0 Native since1.6.0

JSON to JSON transformation using JSONATA.

## What’s inside

-   [JSONata component](../../../../components/4.14.x/jsonata-component.md), URI syntax: `jsonata:resourceUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jsonata)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jsonata</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## allowContextMapAll option in native mode

The `allowContextMapAll` option is not supported in native mode as it requires reflective access to security sensitive camel core classes such as `CamelContext` & `Exchange`. This is considered a security risk and thus access to the feature is not provided by default.

## Additional Camel Quarkus configuration

This component typically loads JSONata specifications from classpath. To make it work also in native mode, you need to explicitly embed the specification files in the native executable by using the `quarkus.native.resources.includes` property.

```java
from("direct:start").to("jsonata:spec/expressions.spec");
```

To include this (an possibly other specifications stored in `.spec` files) in the native image, you would have to add something like the following to your `application.properties` file:

```properties
quarkus.native.resources.includes = spec/*.spec
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resource in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).