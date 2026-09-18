# Spring Cloud Config

Spring Boot auto-configuration for Camel Spring Cloud Config integration.

This starter allows Camel to resolve property placeholders from a [Spring Cloud Config Server](https://spring.io/projects/spring-cloud-config). It hooks into Spring Boot’s `Environment` early in the startup lifecycle to fetch remote configuration before Camel routes are initialized.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-spring-cloud-config-starter</artifactId>
</dependency>
```