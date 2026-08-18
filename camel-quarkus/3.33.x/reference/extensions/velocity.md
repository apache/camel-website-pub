# Velocity

JVM since1.1.0 Native since1.2.0

Transform messages using a Velocity template.

## What’s inside

-   [Velocity component](../../../../components/4.18.x/velocity-component.md), URI syntax: `velocity:resourceUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-velocity)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-velocity</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Custom body as domain object in the native mode

When using a custom object as message body and referencing its properties in the template in the native mode, all the classes need to be registered for reflection (see the [documentation](https://quarkus.io/guides/writing-native-applications-tips#register-reflection)).

Example:

```java
@RegisterForReflection
public interface CustomBody {
}
```

## allowContextMapAll option in native mode

The `allowContextMapAll` option is not supported in native mode as it requires reflective access to security sensitive camel core classes such as `CamelContext` & `Exchange`. This is considered a security risk and thus access to the feature is not provided by default.

## Additional Camel Quarkus configuration

This component typically loads Velocity templates from classpath. To make it work also in native mode, you need to explicitly embed the templates in the native executable by using the `quarkus.native.resources.includes` property.

For instance, the route below would load the Velocity template from a classpath resource named `template/simple.vm`:

```java
from("direct:start").to("velocity://template/simple.vm");
```

To include this (and possibly other templates stored in `.vm` files in the `template` directory) in the native image, you would have to add something like the following to your `application.properties` file:

```properties
quarkus.native.resources.includes = template/*.vm
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resource in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).