# Kamelet Main

**Since Camel 3.11**

A `main` class that is opinionated to boostrap and run Camel standalone with Kamelets (or plain YAML routes) for development and demo purposes.

## Initial configuration

The `KameletMain` is pre-configured with the following properties:

```properties
camel.component.kamelet.location = classpath:kamelets
camel.component.rest.consumerComponentName = platform-http
camel.component.rest.producerComponentName = vertx-http
camel.main.jmxUpdateRouteEnabled = true
```

These settings can be overridden by configuration in `application.properties`.

You can find an example with this at [kamelet-main](https://github.com/apache/camel-examples/tree/main/kamelet-main).