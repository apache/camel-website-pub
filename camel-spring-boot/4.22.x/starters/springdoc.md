# Springdoc

Spring Boot auto-configuration for Camel Springdoc integration.

This starter integrates Camel REST DSL routes with [Springdoc OpenAPI](https://springdoc.org), making Camel REST endpoints appear in the Springdoc-generated OpenAPI specification alongside Spring MVC or WebFlux endpoints.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-springdoc-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.springdoc.enabled | Enables Camel Rest DSL to automatic register its OpenAPI (eg swagger doc) in Spring Boot which allows tooling such as SpringDoc to integrate with Camel. | true | Boolean |