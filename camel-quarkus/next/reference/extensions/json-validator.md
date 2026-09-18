# JSON Schema Validator

JVM since1.0.0 Native since1.0.0

Validate JSON payloads using NetworkNT JSON Schema.

## What’s inside

-   [JSON Schema Validator component](../../../../components/4.22.x/json-validator-component.md), URI syntax: `json-validator:resourceUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-json-validator)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-json-validator</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## allowContextMapAll option in native mode

The `allowContextMapAll` option is not supported in native mode as it requires reflective access to security sensitive camel core classes such as `CamelContext` & `Exchange`. This is considered a security risk and thus access to the feature is not provided by default.

## Additional Camel Quarkus configuration

This component typically loads JSON schemas from classpath. To make it work also in native mode, you need to explicitly embed the schema files in the native executable by using the `quarkus.native.resources.includes` property.

For instance, the route below would load the schema from a classpath resource named `schema.json`:

```java
from("direct:start").to("json-validator:schema.json");
```

To include this (and possibly other schemas stored in `.json` files) in the native image, you would have to add something like the following to your `application.properties` file:

```properties
quarkus.native.resources.includes = schema.json
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resource in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).