# Openapi Java

Spring Boot auto-configuration for Camel OpenAPI support.

This starter exposes your Camel REST DSL routes as an OpenAPI (Swagger) specification. The generated spec is available at runtime via an HTTP endpoint, and can be used with Swagger UI or other API documentation tools.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-openapi-java-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.openapi.enabled | Enables Camel Rest DSL to automatic register its OpenAPI (eg swagger doc) in Spring Boot which allows tooling such as SpringDoc to integrate with Camel. | true | Boolean |