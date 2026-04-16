# Protobuf

JVM since1.0.0 Native since1.5.0

Serialize and deserialize Java objects using Google’s Protocol buffers.

## What’s inside

-   [Protobuf data format](../../../../components/next/dataformats/protobuf-dataformat.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-protobuf)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-protobuf</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

### Generate classes from protobuf `.proto` files

Use the `generate-code` goal of `quarkus-maven-plugin` to generate Java classes from your `*.proto` service and message definitions stored in the `src/main/proto` directory:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-maven-plugin</artifactId>
            <executions>
                <execution>
                    <goals>
                        <goal>generate-code</goal>
                        <goal>build</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

The [camel-quarkus-protobuf integration test](https://github.com/apache/camel-quarkus/tree/main/integration-tests/protobuf) is a good way to learn more.

### Serialize/Deserialize Java beans using JSON fields representation

Please note that some additional configurations might be needed when using `contentTypeFormat=json`. Indeed, in such a case, the generated `Builder` class needs to be registered for reflection.

For instance, let’s examine the `ProtobufDataFormat` below:

```java
ProtobufDataFormat protobufJsonDataFormat = new ProtobufDataFormat(Person.getDefaultInstance(), ProtobufDataFormat.CONTENT_TYPE_FORMAT_JSON);
```

In such a case, the `Person.Builder` class should be [registered for reflection](../../user-guide/native-mode.html#reflection), for instance as below:

```java
@RegisterForReflection(targets = { org.apache.camel.quarkus.component.protobuf.it.model.AddressBookProtos.Person.Builder.class })
```

A concrete implementation of such a scenario is present in the [camel-quarkus-protobuf integration test](https://github.com/apache/camel-quarkus/tree/main/integration-tests/protobuf).