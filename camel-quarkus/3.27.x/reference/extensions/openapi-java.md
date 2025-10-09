# OpenAPI Java

JVM since1.0.0 Native since1.0.0

Expose OpenAPI resources defined in Camel REST DSL

## What’s inside

-   [Openapi Java](../../../../components/4.14.x/others/openapi-java.md)
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-openapi-java)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-openapi-java</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

You can use this extension to expose REST DSL services to Quarkus OpenAPI. With `quarkus-smallrye-openapi`, you can access them by `/q/openapi?format=json`.

Refer to the [Quarkus OpenAPI guide](https://quarkus.io/guides/openapi-swaggerui) for further information.

This is an experimental feature. You can enable it by

```properties
quarkus.camel.openapi.expose.enabled=true
```

> **Warning**
> It’s the user’s responsibility to use `@RegisterForReflection` to register all model classes for reflection.
>
> It doesn’t support the rest services used in `org.apache.camel.builder.LambdaRouteBuilder` right now. Also, it can not use CDI injection in the RouteBuilder `configure()` since we get the rest definitions at build time while CDI is unavailable.

## Additional Camel Quarkus configuration

  
| Configuration property | Type | Default |
| --- | --- | --- |
| `[quarkus.camel.openapi.expose.enabled](#quarkus-camel-openapi-expose-enabled)`
When set to true, Camel REST DSL OpenAPI specifications are exposed under the Quarkus OpenAPI HTTP endpoint (`/q/openapi`). This requires `quarkus-smallrye-openapi` to be added to your application.

 | `boolean` | `false` |

Configuration property fixed at build time. All other configuration properties are overridable at runtime.