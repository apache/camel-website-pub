# REST OpenApi

JVM since1.0.0 Native since1.0.0

To call REST services using OpenAPI specification as contract.

## What’s inside

-   [REST OpenApi component](../../../../components/4.18.x/rest-openapi-component.md), URI syntax: `rest-openapi:specificationUri#operationId`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-rest-openapi)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-rest-openapi</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Required Dependencies

A `RestProducerFactory` implementation must be available when using the rest-openapi extension. The currently known extensions are:

-   camel-quarkus-http
    
-   camel-quarkus-netty-http
    

Maven users will need to add one of these dependencies to their `pom.xml`, for example:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-http</artifactId>
</dependency>
```

Depending on which mechanism is used to load the OpenApi specification, additional dependencies may be required. When using the `file` resource locator, the `org.apache.camel.quarkus:camel-quarkus-file` extension must be added as a project dependency. When using `ref` or `bean` to load the specification, not only must the `org.apache.camel.quarkus:camel-quarkus-bean` dependency be added, but the bean itself must be annotated with `@RegisterForReflection`.

When using the `classpath` resource locator with native code, the path to the OpenAPI specification must be specified in the `quarkus.native.resources.includes` property of the `application.properties` file. For example:

```none
quarkus.native.resources.includes=openapi.json
```

### Contract First Development

Model class generation has been integrated into the `quarkus-maven-plugin`. So there’s no need to use the `swagger-codegen-maven-plugin`. Instead, put your contract files in `src/main/openapi` with a `.json` or `.yaml` suffix then ensure the `generate-code` goal is configured on the `quarkus-maven-plugin`:

```xml
<plugin>
    <groupId>io.quarkus</groupId>
    <artifactId>quarkus-maven-plugin</artifactId>
    <executions>
        <execution>
            <goals>
                <goal>generate-code</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

You can customize the package name of the generated classes by adding configuration property `quarkus.camel.openapi.codegen.model-package` to `application.properties` file.

```properties
quarkus.camel.openapi.codegen.model-package=org.acme
```

In addition, you should also add this package to configuration property `camel.rest.bindingPackageScan`.

The contract files in `src/main/openapi` need to be added in the classpath, since they could be used in the Camel Rest DSL. For example, to do this with Maven:

```xml
<build>
    <resources>
        <resource>
            <directory>src/main/openapi</directory>
        </resource>
        <resource>
            <directory>src/main/resources</directory>
        </resource>
    </resources>
</build>
```

When running in the native mode, the contract files must be added to the native image via the `quarkus.native.resources.include` configuration property.

```properties
quarkus.native.resources.includes=contract.json
```

> **Important**
> It’s recommended to configure a base path under which your REST service endpoints will be accessible.
>
> Using the default path `/` can result in other HTTP endpoints already hosted under that path being inaccessible.
>
> To set a base path, do any one of the following.
>
> -   Add [servers configuration](https://swagger.io/docs/specification/v3_0/api-host-and-base-path/) into your OpenAPI spec file.
>     
> -   Add configuration to `application.properties` like `camel.component.rest-openapi.basePath=/api/v1`.
>     
> -   Set a context path on the REST DSL configuration like `restConfiguration().contextPath("/api/v1")`.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.openapi.codegen.enabled](#quarkus-camel-openapi-codegen-enabled)`
If `true`, Camel Quarkus OpenAPI code generation is run for .json and .yaml files discovered from the `openapi` directory. When `false`, code generation for .json and .yaml files is disabled.

 | `boolean` | `true` |
| `[quarkus.camel.openapi.codegen.model-package](#quarkus-camel-openapi-codegen-model-package)`

The package to use for generated model classes.

 | `string` | `org.apache.camel.quarkus` |
| `[quarkus.camel.openapi.codegen.models](#quarkus-camel-openapi-codegen-models)`

A comma separated list of models to generate. The default is empty list for all models.

 | `string` |  |
| `[quarkus.camel.openapi.codegen.use-bean-validation](#quarkus-camel-openapi-codegen-use-bean-validation)`

If `true`, use bean validation annotations in the generated model classes.

 | `boolean` | `false` |
| `[quarkus.camel.openapi.codegen.not-null-jackson](#quarkus-camel-openapi-codegen-not-null-jackson)`

If `true`, use NON\_NULL Jackson annotation in the generated model classes.

 | `boolean` | `false` |
| `[quarkus.camel.openapi.codegen.ignore-unknown-properties](#quarkus-camel-openapi-codegen-ignore-unknown-properties)`

If `true`, use JsonIgnoreProperties(ignoreUnknown = true) annotation in the generated model classes.

 | `boolean` | `false` |
| `[quarkus.camel.openapi.codegen.additional-properties."additional-properties"](#quarkus-camel-openapi-codegen-additional-properties-additional-properties)`

Additional properties to be used in the mustache templates.

 | `Map<String,String>` |  |
| `[quarkus.camel.openapi.codegen.locations](#quarkus-camel-openapi-codegen-locations)`

A comma separated list of OpenAPI spec locations.

 | `string` |  |
| 

`[quarkus.camel.openapi.codegen.type-mappings."type-mappings"](#quarkus-camel-openapi-codegen-type-mappings-type-mappings)`

Mappings between swagger spec types and generated code types.

Multiple type mappings can be specified like the following.

```properties
quarkus.camel.openapi.codegen.type-mappings.Double=java.math.BigDecimal
quarkus.camel.openapi.codegen.type-mappings.Date=java.time.LocalDate
```







 | `Map<String,String>` |  |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.