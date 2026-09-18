# DFDL

JVM since3.22.0 Nativeunsupported

Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL).

## What’s inside

-   [DFDL component](../../../../components/4.18.x/dfdl-component.md), URI syntax: `dfdl:schemaUri`
    
-   [DFDL data format](../../../../components/4.18.x/dataformats/dfdl-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-dfdl</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Camel Quarkus limitations

While `camel-dfdl` component requires Scala version 2.12, Quarkus BOM enforces Scala version 2.13, which causes `camel-dfdl` to fail. In order to make it work, the application POM needs to override the scala version. You can do that by adding `<dependencyManagement>` in your application POM:

```xml
<properties>
    <scala.version>2.12.20</scala.version>
</properties>
...
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-library</artifactId>
            <version>${scala.version}</version>
        </dependency>
        <dependency>
            <groupId>org.scala-lang</groupId>
            <artifactId>scala-reflect</artifactId>
            <version>${scala.version}</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```