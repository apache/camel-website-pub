# Context Reload

The context reload functionality in Camel is capable of reloading all existing routes and property placeholders upon an external triggered event.

For example, if you are using [AWS Secrets](../components/4.22.x/aws-secrets-manager-component.md), then enabling context-reload would then reload Camel routes upon a secret is updated in AWS.

The context reload refreshes the following on reload:

-   [property placeholders](using-propertyplaceholder.md)
    
-   component options whose configured value is a property placeholder (requires Camel Main, Camel Spring Boot or Camel Quarkus)
    
-   all beans implementing `SecretRotationAware`, so they can re-authenticate in place (see below)
    
-   all existing [routes](routes.md) (no changes to structure of routes; see [Route Reload](route-reload.md)\])
    

Other general services in [CamelContext](camelcontext.md) and java beans or Camel [Processor](processor.md) are not updated.

Re-applying the component options is what allows a rotated secret to reach a component, as an option such as the following has its placeholder resolved once, when the component is configured:

```properties
camel.component.kafka.saslJaasConfig = {{aws:broker-credentials}}
```

Only options whose value is a placeholder are re-applied, as they are the only ones whose resolved value can change while the configuration itself stays the same.

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

The method `onReload` will then reload all the [property placeholders](using-propertyplaceholder.md), re-apply the component options that were configured with a placeholder, notify all `SecretRotationAware` beans, and then afterward reload all existing [routes](routes.md).

## Re-authenticating on rotated secrets

Reloading the routes rebuilds the routes and their endpoints, but it does not rebuild the components themselves, nor any bean in the [Registry](registry.md). A component that holds a live authenticated resource, such as a pooled JMS connection factory, a JDBC connection pool or a shared HTTP client, therefore keeps using the credentials it captured when it was created, even though the secret has been rotated.

Such a component or bean can implement `org.apache.camel.spi.SecretRotationAware` to be told when this happens:

```java
public class MyComponent extends DefaultComponent implements SecretRotationAware {

    @Override
    public void onSecretRotation(Object source) throws Exception {
        // re-read the configured credentials and re-authenticate the connection
        // that was created with the secret that has just been rotated
    }
}
```

The callback is invoked after the property placeholders have been reloaded and the component options re-applied, but before the routes are restarted, so that by the time the routes come back up the underlying resource is already authenticated with the new secret.

The callback is advisory: it says that a reload was triggered, not which secrets changed. Implementations should be quick, as the callback runs inline on the reload. A callback that throws is logged and ignored, so that one component cannot prevent the others from being refreshed, nor fail the reload as a whole.

## See Also

See related [Route Reload](route-reload.md).