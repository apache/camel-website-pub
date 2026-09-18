# JAXB

JVM since1.0.0 Native since1.0.0

Unmarshal XML payloads to POJOs and back using JAXB2 XML marshalling standard.

## What’s inside

-   [JAXB data format](../../../../components/4.18.x/dataformats/jaxb-dataformat.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-jaxb)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-jaxb</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Native mode `ObjectFactory` instantiation of non-JAXB annotated classes

When performing JAXB marshal operations with a custom `ObjectFactory` to instantiate POJO classes that do not have JAXB annotations, you must register those POJO classes for reflection in order for them to be instantiated in native mode. E.g. via the `@RegisterForReflection` annotation or configuration property `quarkus.camel.native.reflection.include-patterns`.

Refer to the [Native mode](../../user-guide/native-mode.html#reflection) user guide for more information.