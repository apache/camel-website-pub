# DFDL

Transforms fixed format data such as EDI message from/to XML using a Data Format Description Language (DFDL).

## What’s inside

-   [DFDL component](../../../components/next/dfdl-component.md), URI syntax: `dfdl:schemaUri`
    
-   [DFDL data format](../../../components/next/dataformats/dfdl-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-dfdl-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.component.dfdl.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.dfdl.enabled | Whether to enable auto configuration of the dfdl component. This is enabled by default. |  | Boolean |
| camel.component.dfdl.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| camel.dataformat.dfdl.enabled | Whether to enable auto configuration of the dfdl data format. This is enabled by default. |  | Boolean |
| camel.dataformat.dfdl.root-element | The root element name of the schema to use. If not specified, the first root element in the schema will be used. |  | String |
| camel.dataformat.dfdl.root-namespace | The root namespace of the schema to use. |  | String |
| camel.dataformat.dfdl.schema-uri | The path to the DFDL schema file. |  | String |