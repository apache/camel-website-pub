# Freemarker

JVM since1.1.0 Native since1.8.0

Transform messages using FreeMarker templates.

## What’s inside

-   [Freemarker component](../../../../components/4.18.x/freemarker-component.md), URI syntax: `freemarker:resourceUri`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-freemarker)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-freemarker</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## allowContextMapAll option in native mode

The `allowContextMapAll` option is not supported in native mode as it requires reflective access to security sensitive camel core classes such as `CamelContext` & `Exchange`. This is considered a security risk and thus access to the feature is not provided by default.

## Additional Camel Quarkus configuration

## Quarkiverse Freemarker and its configuration

Camel Quarkus Freemarker uses dev/index.html\[Quarkiverse Freemarker\] under the hood. This means in particular, that the `freemarker.template.Configuration` bean produced by Quarkiverse Freemarker is used by Camel Quarkus. The bean can be configured via `quarkus.freemarker.*` properties - check [Freemarker Configuration Reference](https://quarkiverse.github.io/quarkiverse-docs/quarkus-freemarker/dev/index.md) for more details.

If you wish to use your custom `Configuration` bean instead of the default provided by Quarkiverse Freemarker, you can let CDI to do the required wiring:

```java
import jakarta.enterprise.context.ApplicationScoped;
import jakarta.enterprise.inject.Produces;
import jakarta.inject.Named;
import freemarker.template.Configuration;
import io.quarkus.arc.Unremovable;
import org.apache.camel.builder.RouteBuilder;

@ApplicationScoped
public class MyRoutes extends RouteBuilder {

    @Produces
    @ApplicationScoped
    @Unremovable
    @Named("myFreemarkerConfig")
    Configuration produceFreemarkerConfig() {
        Configuration result = new Configuration();
        ...
        return result;
    }

    @Override
    public void configure() {
        from("direct:example")
            .to("freemarker:templates/email.ftl?configuration=myFreemarkerConfig")

    }
}
```