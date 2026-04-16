# MapStruct

JVM since3.2.0 Native since3.2.0

Type Conversion using Mapstruct

## What’s inside

-   [MapStruct component](../../../../components/next/mapstruct-component.md), URI syntax: `mapstruct:className`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-mapstruct)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-mapstruct</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Annotation Processor

To use MapStruct, you must configure your build to use an annotation processor.

#### Maven

```xml
<plugins>
    <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
            <annotationProcessorPaths>
                <path>
                    <groupId>org.mapstruct</groupId>
                    <artifactId>mapstruct-processor</artifactId>
                    <version>1.6.3</version>
                </path>
            </annotationProcessorPaths>
        </configuration>
    </plugin>
</plugins>
```

#### Gradle

```gradle
dependencies {
    annotationProcessor 'org.mapstruct:mapstruct-processor:1.6.3'
    testAnnotationProcessor 'org.mapstruct:mapstruct-processor:1.6.3'
}
```

### Mapper definition discovery

By default, Camel Quarkus will automatically discover the package paths of your `@Mapper` annotated interfaces or abstract classes and pass them to the Camel MapStruct component.

If you want finer control over the specific packages that are scanned, then you can set a configuration property in `application.properties`.

```properties
camel.component.mapstruct.mapper-package-name = com.first.package,org.second.package
```