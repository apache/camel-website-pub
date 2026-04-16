# XPath

JVM since1.0.0 Native since1.0.0

Evaluates an XPath expression against an XML payload

## What’s inside

-   [XPath language](../../../../components/next/languages/xpath-language.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-xpath)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-xpath</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

This component is able to load xpath expressions from classpath resources. To make it work also in native mode, you need to explicitly embed the expression files in the native executable by using the `quarkus.native.resources.includes` property.

For instance, the route below would load an XPath expression from a classpath resource named `myxpath.txt`:

```java
from("direct:start").transform().xpath("resource:classpath:myxpath.txt");
```

To include this (and possibly other expressions stored in `.txt` files) in the native image, you would have to add something like the following to your `application.properties` file:

```properties
quarkus.native.resources.includes = *.txt
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resource in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).