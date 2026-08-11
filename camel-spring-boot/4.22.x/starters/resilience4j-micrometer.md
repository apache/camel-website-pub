# Resilience4j Micrometer

Spring Boot auto-configuration for Resilience4j Micrometer metrics in Camel.

This starter adds [Micrometer](https://micrometer.io) metrics instrumentation to Camel’s Resilience4j Circuit Breaker EIP, exposing circuit breaker state, call counts, and latency metrics.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-resilience4j-micrometer-starter</artifactId>
</dependency>
```