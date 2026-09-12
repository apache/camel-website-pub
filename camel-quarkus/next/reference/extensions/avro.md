Camel Quarkus

# Avro

JVM since1.0.0 Native since1.0.0

Serialize and deserialize messages using Apache Avro binary data format

## What’s inside

-   [Avro data format](../../../../components/4.22.x/dataformats/avro-dataformat.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-avro)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-avro</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

Beyond standard usages known from vanilla Camel, Camel Quarkus adds the possibility to parse the Avro schema at build time both in JVM and Native mode.

The approach to generate Avro classes from Avro schema files is the one coined by the `quarkus-avro` extension. It requires the following:

1.  Store `*.avsc` files in a folder named `src/main/avro` or `src/test/avro`
    
2.  In addition to the usual `build` goal of `quarkus-maven-plugin`, add the `generate-code` goal:
    
    ```xml
    <plugin>
        <groupId>io.quarkus</groupId>
        <artifactId>quarkus-maven-plugin</artifactId>
        <executions>
            <execution>
                <id>generate-code-and-build</id>
                <goals>
                    <goal>generate-code</goal>
                    <goal>build</goal>
                </goals>
            </execution>
        </executions>
    </plugin>
    ```
    

Please see a working configuration in [Camel Quarkus Avro integration test](https://github.com/apache/camel-quarkus/tree/main/integration-tests/avro) and [Quarkus Avro integration test](https://github.com/quarkusio/quarkus/tree/main/integration-tests/avro-reload/src/test/avro).

### Trusted classes

Since Avro 1.12.2, `SpecificData` refuses to load classes that are not explicitly trusted, failing with:

```text
java.lang.SecurityException: Forbidden com.acme.MyRecord! This class is not trusted to be included in Avro schemas.
```

Classes annotated with `@org.apache.avro.specific.AvroGenerated` are trusted automatically, which covers everything produced by the `generate-code` goal described above. Specific records that predate that annotation, or that were written by hand, have to be trusted explicitly:

```properties
quarkus.avro.trusted-classes=com.acme.MyRecord
quarkus.avro.trusted-packages=com.acme.avro
```