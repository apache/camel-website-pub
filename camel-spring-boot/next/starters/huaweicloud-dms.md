# Huawei Distributed Message Service (DMS)

To integrate with a fully managed, high-performance message queuing service on Huawei Cloud

## What’s inside

-   [Huawei Distributed Message Service (DMS) component](../../../components/next/hwcloud-dms-component.md), URI syntax: `hwcloud-dms:operation`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-huaweicloud-dms-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.component.hwcloud-dms.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.hwcloud-dms.enabled | Whether to enable auto configuration of the hwcloud-dms component. This is enabled by default. |  | Boolean |
| camel.component.hwcloud-dms.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |