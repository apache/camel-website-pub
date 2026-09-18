# Resilience4j

**Since Camel 3.0**

This component supports the Circuit Breaker EIP with the [Resilience4j](https://resilience4j.readme.io/) library.

For more details, see the [Circuit Breaker EIP](../eips/circuitBreaker-eip.md) documentation.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-resilience4j</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using resilience4j with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-resilience4j-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component has no Spring Boot auto configuration options.