# YAML IO

JVM since3.2.0 Native since3.2.0

Camel YAML IO

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-yaml-io)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-yaml-io</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

This an auxiliary extension that provides support for Camel route dumping in YAML.

For example, when the application is configured to dump routes on startup with the following configuration in `application.properties`.

```properties
camel.main.dump-routes = yaml
```