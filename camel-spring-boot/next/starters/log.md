# Log Data

Prints data form the routed message (such as body and headers) to the logger.

## What’s inside

-   [Log Data component](../../../components/next/log-component.md), URI syntax: `log:loggerName`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-log-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.component.log.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.log.enabled | Whether to enable auto configuration of the log component. This is enabled by default. |  | Boolean |
| camel.component.log.exchange-formatter | Sets a custom ExchangeFormatter to convert the Exchange to a String suitable for logging. If not specified, we default to DefaultExchangeFormatter. The option is a org.apache.camel.spi.ExchangeFormatter type. |  | ExchangeFormatter |
| camel.component.log.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.component.log.source-location-logger-name | If enabled then the source location of where the log endpoint is used in Camel routes, would be used as logger name, instead of the given name. However, if the source location is disabled or not possible to resolve then the existing logger name will be used. | false | Boolean |