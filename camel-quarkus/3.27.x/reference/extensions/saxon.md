# XQuery

JVM since1.1.0 Native since2.0.0

Query and/or transform XML payloads using XQuery and Saxon.

## What’s inside

-   [XQuery component](../../../../components/4.14.x/xquery-component.md), URI syntax: `xquery:resourceUri`
    
-   [XQuery language](../../../../components/4.14.x/languages/xquery-language.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-saxon)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-saxon</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

This component is able to load XQuery definitions from classpath. To make it work also in native mode, you need to explicitly embed the queries in the native executable by using the `quarkus.native.resources.includes` property.

For instance, the two routes below load an XQuery script from two classpath resources named `myxquery.txt` and `another-xquery.txt` respectively:

```java
from("direct:start").transform().xquery("resource:classpath:myxquery.txt", String.class);
from("direct:start").to("xquery:another-xquery.txt");
```

To include these (an possibly other queries stored in `.txt` files) in the native image, you would have to add something like the following to your `application.properties` file:

```properties
quarkus.native.resources.includes = *.txt
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resource in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).