# Springdoc

**Since Camel 3.14**

This is available only as a Camel spring boot starter. It supplies support for using the Springdoc Swagger UI with openapi-java.

## Spring Boot Auto-Configuration

When using openapi-java with springdoc with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-springdoc-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.springdoc.enabled** | Enables Camel Rest DSL to automatic register its OpenAPI (eg swagger doc) in Spring Boot which allows tooling such as SpringDoc to integrate with Camel. | true | Boolean |