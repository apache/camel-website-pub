# Ref

JVM since1.0.0 Native since1.0.0

Route messages to an endpoint looked up dynamically by name in the Camel Registry.

## What’s inside

-   [Ref component](../../../../components/4.18.x/ref-component.md), URI syntax: `ref:name`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-ref)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-ref</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

CDI producer methods can be harnessed to bind endpoints to the Camel registry, so that they can be resolved using the `ref` URI scheme in Camel routes.

For example, to produce endpoint beans:

```java
@ApplicationScoped
public class MyEndpointProducers {
    @Inject
    CamelContext context;

    @Singleton
    @Produces
    @Named("endpoint1")
    public Endpoint directStart() {
        return context.getEndpoint("direct:start");
    }

    @Singleton
    @Produces
    @Named("endpoint2")
    public Endpoint logEnd() {
        return context.getEndpoint("log:end");
    }
}
```

Use `ref:` to refer to the names of the CDI beans that were bound to the Camel registry:

```java
public class MyRefRoutes extends RouteBuilder {
    @Override
    public void configure() {
        // direct:start -> log:end
        from("ref:endpoint1")
            .to("ref:endpoint2");
    }
}
```