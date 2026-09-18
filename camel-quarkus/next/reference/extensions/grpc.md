# gRPC

JVM since1.0.0 Native since1.0.0

Expose gRPC endpoints and access external gRPC endpoints.

## What’s inside

-   [gRPC component](../../../../components/4.22.x/grpc-component.md), URI syntax: `grpc:host:port/service`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-grpc)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-grpc</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Protobuf generated code

Camel Quarkus gRPC can generate gRPC service stubs for `.proto` files. When using Maven, ensure that you have enabled the `generate-code` goals of the `quarkus-maven-plugin` in your project build.

```xml
<build>
    <plugins>
        <plugin>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-maven-plugin</artifactId>
            <version>${quarkus.platform.version}</version>
            <extensions>true</extensions>
            <executions>
                <execution>
                    <goals>
                        <goal>build</goal>
                        <goal>generate-code</goal>
                        <goal>generate-code-tests</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

With this configuration, you can put your service and message definitions into the `src/main/proto` directory and the `quarkus-maven-plugin` will generate code from your `.proto` files.

#### Scanning `proto` files with imports

The Protocol Buffers specification provides a way to import proto files. You can control the scope of dependencies to scan by adding configuration property `quarkus.camel.grpc.codegen.scan-for-imports` property to `application.properties`. The available options are outlined below.

-   `all` - Scan all dependencies
    
-   `none` - Disable dependency scanning. Use only the proto definitions defined in `src/main/proto` or `src/test/proto`
    
-   `groupId1:artifactId1,groupId2:artifactId2` - Scan only the dependencies matching the `groupId` and `artifactId` list
    

The default value is `com.google.protobuf:protobuf-java`.

#### Scanning `proto` files from dependencies

If you have proto files shared across multiple dependencies, you can generate gRPC service stubs for them by adding configuration property `quarkus.camel.grpc.codegen.scan-for-proto` to `application.properties`.

First add a dependency for the artifact(s) containing proto files to your project. Next, enable proto file dependency scanning.

```properties
quarkus.camel.grpc.codegen.scan-for-proto=org.my.groupId1:my-artifact-id-1,org.my.groupId2:my-artifact-id-2
```

It is possible to include / exclude specific proto files from dependency scanning via configuration properties.

The configuration property name suffix is the Maven `groupId` / `artifactId` for the dependency to configure includes / excludes on. Paths are relative to the classpath location of the proto files within the dependency. Paths can be an explicit path to a proto file, or as glob patterns to include / exclude multiple files.

```properties
quarkus.camel.grpc.codegen.scan-for-proto-includes."<groupId>\:<artifactId>"=foo/**,bar/**,baz/a-proto.proto
quarkus.camel.grpc.codegen.scan-for-proto-excludes."<groupId>\:<artifactId>"=foo/private/**,baz/another-proto.proto
```

> **Note**
> The `:` character within property keys must be escaped with `\`.

### Accessing classpath resources in native mode

The gRPC component has various options where resources are resolved from the classpath:

-   `keyCertChainResource`
    
-   `keyResource`
    
-   `serviceAccountResource`
    
-   `trustCertCollectionResource`
    

When using these options in native mode, you must ensure that any such resources are included in the native image.

This can be accomplished by adding the configuration property `quarkus.native.resources.includes` to `application.properties`. For example, to include SSL / TLS keys and certificates.

```properties
quarkus.native.resources.includes = certs/*.pem,certs.*.key
```

More information about selecting resources for inclusion in the native executable can be found in the [native mode guide](../../user-guide/native-mode.html#embedding-resource-in-native-executable).

## Camel Quarkus limitations

### Integration with Quarkus gRPC is not supported

At present there is no support for integrating Camel Quarkus gRPC with Quarkus gRPC. If you have both the `camel-quarkus-grpc` and `quarkus-grpc` extension dependency on the classpath, you are likely to encounter problems at build time when compiling your application.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.grpc.service-excludes](#quarkus-camel-grpc-service-excludes)`
Excludes classes from the build time scanning of gRPC service classes. This can be useful if there are gRPC services that you want to exclude from participating in Camel gRPC route operations. The value is a comma separated list of class name patterns. You can specify the fully qualified class name of individual classes or use path patterns to match multiple classes. For example to exclude all classes starting with `MyService` use: `**MyService*`. To exclude all services from a specific package use: `com.services.*`. To exclude all services from a specific package and its sub-packages, use double wildcards: `com.services.**`. And to exclude all services from two specific packages use: `com.services.*,com.other.services.*`.

 | List of `string` |  |
| `[quarkus.camel.grpc.codegen.enabled](#quarkus-camel-grpc-codegen-enabled)`

If `true`, Camel Quarkus gRPC code generation is run for .proto files discovered from the `proto` directory, or from dependencies specified in the `scan-for-proto` or `scan-for-imports` options. When `false`, code generation for .proto files is disabled.

 | `boolean` | `true` |
| 

`[quarkus.camel.grpc.codegen.scan-for-proto](#quarkus-camel-grpc-codegen-scan-for-proto)`

Camel Quarkus gRPC code generation can scan application dependencies for .proto files to generate Java stubs from them. This property sets the scope of the dependencies to scan. Applicable values:

-   _none_ - default - don’t scan dependencies
    
-   a comma separated list of _groupId:artifactId_ coordinates to scan
    
-   _all_ - scan all dependencies
    





 | `string` | `none` |
| 

`[quarkus.camel.grpc.codegen.scan-for-imports](#quarkus-camel-grpc-codegen-scan-for-imports)`

Camel Quarkus gRPC code generation can scan dependencies for .proto files that can be imported by protos in this application. Applicable values:

-   _none_ - default - don’t scan dependencies
    
-   a comma separated list of _groupId:artifactId_ coordinates to scan
    
-   _all_ - scan all dependencies The default is _com.google.protobuf:protobuf-java_.
    





 | `string` | `com.google.protobuf:protobuf-java` |
| `[quarkus.camel.grpc.codegen.scan-for-proto-includes."scan-for-proto-includes"](#quarkus-camel-grpc-codegen-scan-for-proto-includes-scan-for-proto-includes)`

Package path or file glob pattern includes per dependency containing .proto files to be considered for inclusion.

 | `Map<String,List<String>>` |  |
| `[quarkus.camel.grpc.codegen.scan-for-proto-excludes."scan-for-proto-excludes"](#quarkus-camel-grpc-codegen-scan-for-proto-excludes-scan-for-proto-excludes)`

Package path or file glob pattern includes per dependency containing .proto files to be considered for exclusion.

 | `Map<String,List<String>>` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.