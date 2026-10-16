# BeanIO

JVM since3.8.0 Native since3.16.0

Marshal and unmarshal Java beans to and from flat files (such as CSV, delimited, or fixed length formats)

## What’s inside

-   [BeanIO data format](../../../../components/next/dataformats/beanio-dataformat.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-beanio)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-beanio</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### BeanIO in native mode

#### XML mapping files

When BeanIO configuration is defined in XML files that are read from the classpath. You must ensure each file is added to the native application image. To do this, add the `quarkus.native.resources.includes` configuration property to `application.properties`. For example.

```properties
quarkus.native.resources.includes=mapping.xml,model/other-mapping.xml
```

More information about selecting resources for inclusion in the native executable can be found at [Embedding resources in native executable](../../user-guide/native-mode.html#embedding-resource-in-native-executable).

#### BeanIO Record classes

All classes that participate in BeanIO marshal / unmarshal operations must be registered for reflection.

This can be achieved with the `@RegisterForReflection` annotation or with configuration property `quarkus.camel.native.reflection.include-patterns`. For example:

```java
@RegisterForReflection
public class Employee {
    ...
}
```

Refer to the [Native mode](../../user-guide/native-mode.html#reflection) user guide for more information.