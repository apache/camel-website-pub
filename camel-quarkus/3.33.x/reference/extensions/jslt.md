# JSLT

JVM since1.1.0 Native since1.4.0

Query or transform JSON payloads using an JSLT.

## What’s inside

-   [JSLT component](../../../../components/4.18.x/jslt-component.md), URI syntax: `jslt:resourceUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jslt)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jslt</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## allowContextMapAll option in native mode

The `allowContextMapAll` option is not supported in native mode as it requires reflective access to security sensitive camel core classes such as `CamelContext` & `Exchange`. This is considered a security risk and thus access to the feature is not provided by default.

## Additional Camel Quarkus configuration

### Loading JSLT templates from classpath in native mode

This component typically loads the templates from classpath. To make it work also in native mode, you need to explicitly embed the templates files in the native executable by using the `quarkus.native.resources.includes` property.

For instance, the route below would load the JSLT schema from a classpath resource named `transformation.json`:

```java
from("direct:start").to("jslt:transformation.json");
```

To include this (and possibly other templates stored in `.json` files) in the native image, you would have to add something like the following to your `application.properties` file:

```properties
quarkus.native.resources.includes = *.json
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resource in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).

### Using JSLT functions in native mode

When using JSLT functions from camel-quarkus in native mode, the classes hosting the functions would need to be [registered for reflection](https://quarkus.io/guides/writing-native-applications-tips#registering-for-reflection). When registering the target function is not possible, one may end up writing a stub as below.

```java
@RegisterForReflection
public class MathFunctionStub {
    public static double pow(double a, double b) {
        return java.lang.Math.pow(a, b);
    }
}
```

The target function `Math.pow(…​)` is now accessible through the `MathFunctionStub` class that could be registered in the component as below:

```java
@Named
JsltComponent jsltWithFunction() throws ClassNotFoundException {
    JsltComponent component = new JsltComponent();
    component.setFunctions(singleton(wrapStaticMethod("power", "org.apache.cq.example.MathFunctionStub", "pow")));
    return component;
}
```