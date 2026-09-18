# Mustache

JVM since1.0.0 Native since1.0.0

Transform messages using a Mustache template.

## What’s inside

-   [Mustache component](../../../../components/4.18.x/mustache-component.md), URI syntax: `mustache:resourceUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-mustache)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-mustache</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## allowContextMapAll option in native mode

The `allowContextMapAll` option is not supported in native mode as it requires reflective access to security sensitive camel core classes such as `CamelContext` & `Exchange`. This is considered a security risk and thus access to the feature is not provided by default.

## Additional Camel Quarkus configuration

This component typically loads Mustache templates from classpath. To make it work also in native mode, you need to explicitly embed the templates in the native executable by using the `quarkus.native.resources.includes` property.

For instance, the route below would load the Mustache template from a classpath resource named `template/simple.mustache`:

```java
from("direct:start").to("mustache://template/simple.mustache");
```

To include this (and possibly other templates stored in `.mustache` files) in the native image, you would have to add something like the following to your `application.properties` file:

```properties
quarkus.native.resources.includes = template/*.mustache
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resource in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).