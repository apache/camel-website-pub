# Kamelet Main

**Since Camel 3.11**

A `main` class that is opinionated to boostrap and run Camel standalone with Kamelets (or plain YAML routes) for development and demo purposes.

## Initial configuration

The `KameletMain` is pre-configured with the following properties:

```properties
camel.component.kamelet.location = classpath:kamelets,github:apache:camel-kamelets/kamelets
camel.component.rest.consumerComponentName = platform-http
camel.component.rest.producerComponentName = vertx-http
camel.main.jmxUpdateRouteEnabled = true
```

These settings can be overridden by configuration in `application.properties`.

## Automatic dependencies downloading

The Kamelet Main can automatically download Kamelet YAML files from a remote location over http/https, and from github as well.

The official Kamelets from the Apache Camel Kamelet Catalog is stored on github and they can be used out of the box as-is.

For example a Camel route can be _coded_ in YAML which uses the Earthquake Kamelet from the catalog, as shown below:

```yaml
- route:
    from: "kamelet:earthquake-source"
    steps:
      - unmarshal:
          json: {}
      - log: "Earthquake with magnitude ${body[properties][mag]} at ${body[properties][place]}"
```

In this use-case the earthquake kamelet will be downloaded from github, and as well its required dependencies.

You can find an example with this at [kamelet-main](https://github.com/apache/camel-examples/tree/main/kamelet-main).