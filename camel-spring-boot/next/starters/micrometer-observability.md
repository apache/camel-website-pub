# Micrometer Observability

Spring Boot auto-configuration for Camel Micrometer Observability.

This starter integrates Camel with [Micrometer Observation API](https://micrometer.io) to provide distributed tracing and metrics for Camel routes. It auto-configures a `MicrometerObservabilityService` that creates observations (spans and metrics) for each Camel processor.

Use the `@CamelMicrometerObservability` annotation on your Spring Boot main class or configuration to enable.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-micrometer-observability-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.micrometer.observability.disable-core-processors | Disable any inner core processors (any core DSL processor provided in the route, for example `bean`, `log`, …​). | false | Boolean |
| camel.micrometer.observability.exclude-patterns | Sets exclude pattern(s) that will disable tracing for Camel processors that matches the pattern. Multiple patterns can be separated by comma. |  | String |
| camel.micrometer.observability.include-patterns | Sets include pattern(s) that will explicitly enable tracing for Camel processors that matches the pattern. Multiple patterns can be separated by comma. All processors included by default if nothing is specified. |  | String |
| camel.micrometer.observability.trace-processors | Setting this to true will create new telemetry spans for each Camel custom Processors. Use the excludePattern property to filter out Processors. |  | Boolean |