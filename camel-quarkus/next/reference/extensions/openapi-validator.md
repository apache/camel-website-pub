# OpenAPI Validator

JVM since3.38.0 Native since3.38.0

OpenAPI validator for Camel Rest DSL

## What’s inside

-   [Openapi Validator](../../../../components/next/others/openapi-validator.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-openapi-validator)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-openapi-validator</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Native Mode

When using a classpath-based OpenAPI specification in native mode, the file must be explicitly included in the native image. Add the following to your `application.properties`:

```properties
quarkus.native.resources.includes=openapi.json
```