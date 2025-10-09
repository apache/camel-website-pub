# Resilience4j Micrometer

**Since Camel 4.15**

This component adds Micrometer statistics for Circuit Breaker EIP with the [Resilience4j](https://resilience4j.readme.io/) library.

For more details, see the [Circuit Breaker EIP](../eips/circuitBreaker-eip.md) documentation.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-resilience4j-micrometer</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Configuring Resilience4j Micrometer

When adding `camel-resilience4j-micrometer` JAR to the classpath, then CircuitBreakers will automatically enable gathering statistics using Micrometer.

However, this can explicit be configured via: `application.properties` such as:

```properties
camel.resilience4j.micrometerEnabled = true
```

Or to turn it off:

```properties
camel.resilience4j.micrometerEnabled = false
```