# Rest

JVM since0.0.1 Native since0.0.1

Expose REST services and their OpenAPI Specification or call external REST services.

## What’s inside

-   [REST component](../../../../components/4.14.x/rest-component.md), URI syntax: `rest:method:path:uriTemplate`
    
-   [REST API component](../../../../components/4.14.x/rest-api-component.md), URI syntax: `rest-api:path`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-rest)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-rest</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Additional Camel Quarkus configuration

This extension depends on the [Platform HTTP](platform-http.md) extension and configures it as the component that provides the REST transport.

### Path parameters containing special characters with platform-http

When using the `platform-http` REST transport, some characters are not allowed within path parameter names. This includes the '-' and '$' characters.

In order to make the below example REST `/dashed/param` route work correctly, a system property is required `io.vertx.web.route.param.extended-pattern=true`.

```java
import org.apache.camel.builder.RouteBuilder;

public class CamelRoute extends RouteBuilder {

    @Override
    public void configure() {
        rest("/api")
            // Dash '-' is not allowed by default
            .get("/dashed/param/{my-param}")
            .to("direct:greet")

            // The non-dashed path parameter works by default
            .get("/undashed/param/{myParam}")
            .to("direct:greet");

            from("direct:greet")
                .setBody(constant("Hello World"));
    }
}
```

There is some more background to this in the [Vert.x Web documentation](https://vertx.io/docs/vertx-web/java/#_capturing_path_parameters).

### Configuring alternate REST transport providers

To use another REST transport provider, such as `netty-http` or `servlet`, you need to add the respective extension as a dependency to your project and set the provider in your `RouteBuilder`. E.g. for `servlet`, you’d have to add the `org.apache.camel.quarkus:camel-quarkus-servlet` dependency and the set the provider as follows:

```java
import org.apache.camel.builder.RouteBuilder;

public class CamelRoute extends RouteBuilder {

    @Override
    public void configure() {
        restConfiguration()
                .component("servlet");
        ...
    }
}
```