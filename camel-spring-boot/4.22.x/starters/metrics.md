# Metrics

Collect various metrics directly from Camel routes using the DropWizard metrics library.

## What’s inside

-   [Metrics component](../../../components/4.22.x/metrics-component.md), URI syntax: `metrics:metricsType:metricsName`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-metrics-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.component.metrics.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.metrics.enabled | Whether to enable auto configuration of the metrics component. This is enabled by default. |  | Boolean |
| camel.component.metrics.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.metrics.metric-registry | To use a custom configured MetricRegistry. The option is a com.codahale.metrics.MetricRegistry type. |  | MetricRegistry |