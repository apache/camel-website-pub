# Ai Observability

Spring Boot auto-configuration for Camel GenAI observability.

Add this starter to opt in to GenAI observability configuration for Camel AI producers. Camel 4.23+ AI producers emit OpenTelemetry spans and Micrometer metrics when `camel-ai-observability` and a tracing or metrics backend are on the classpath.

Configure the global toggle in `application.properties`:

```properties
# Disable GenAI observability for all AI producers (default is true)
camel.aiobservability.enabled=false
```

Relaxed binding also accepts `camel.aiObservability.enabled` and `camel.ai-observability.enabled`. The property is written to the Camel `PropertiesComponent` local properties as `camel.aiObservability.enabled`, matching Camel Main and JBang.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-ai-observability-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.aiobservability.enabled | Enables GenAI observability for Camel AI producers (OpenTelemetry spans and Micrometer metrics when backends are present). | true | Boolean |