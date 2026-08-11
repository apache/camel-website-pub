# Context Reload

The context reload functionality in Camel is capable of reloading all existing routes and property placeholders upon an external triggered event.

For example, if you are using [AWS Secrets](../components/4.22.x/aws-secrets-manager-component.md), then enabling context-reload would then reload Camel routes upon a secret is updated in AWS.

The context reload is limited to refresh the following on reload:

-   [property placeholders](using-propertyplaceholder.md)
    
-   all existing [routes](routes.md) (no changes to structure of routes; see [Route Reload](route-reload.md)\])
    

General services in [CamelContext](camelcontext.md) and java beans or Camel [Processor](processor.md) is not updated.

## Using context reloading

The context reloading can be configured in Java or with Spring Boot, Quarkus in the following way:

```java
CamelContext context = ...

ContextReloadStrategy reload = new DefaultContextReloadStrategy();
context.addService(reload);
```

And with Camel Quarkus / Camel Main / Camel Spring Boot you can configure this in `application.properties:`

```properties
# turn on context reloading
camel.main.context-reload-enabled = true
```

## Triggering context reloading

Any custom code can trigger context reloading. This is done by ensuring the context reload is enabled (see the note above), and then from Java you can get hold of `ContextReloadStrategy` as follows:

```java
ContextReloadStrategy reload = context.hasService(ContextReloadStrategy.class);
if (reload != null) {
    // trigger reload
    reload.onReload(this);
}
```

The method `onReload` will then reload all the [property placeholders](using-propertyplaceholder.md) and then afterward reload all existing [routes](routes.md).

## See Also

See related [Route Reload](route-reload.md).