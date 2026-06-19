# Opentelemetry

Spring Boot auto-configuration for Camel OpenTelemetry (legacy).

This starter integrates Camel with [OpenTelemetry](https://opentelemetry.io) to provide distributed tracing for Camel routes. It auto-configures an `OpenTelemetryTracer` that creates spans for each Camel processor and propagates trace context across routes and components.

> **Note**
> This is the legacy OpenTelemetry integration. Consider using `camel-opentelemetry2-starter` instead, which is the newer implementation.

Use the `@CamelOpenTelemetry` annotation on your Spring Boot main class or configuration to enable.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-opentelemetry-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.opentelemetry.enabled | Global option to enable/disable OpenTelemetry integration, default is true. | true | Boolean |
| camel.opentelemetry.encoding | Activate or deactivate dash encoding in headers (required by JMS) for messaging |  | Boolean |
| camel.opentelemetry.exclude-patterns | Sets exclude pattern(s) that will disable tracing for Camel messages that matches the pattern. Multiple patterns can be separated by comma. |  | String |
| camel.opentelemetry.trace-processors | Setting this to true will create new OpenTelemetry Spans for each Camel Processors. Use the excludePattern property to filter out Processors. |  | Boolean |