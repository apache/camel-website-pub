# Geocoder

Find geocodes (latitude and longitude) for a given address or the other way round.

## What’s inside

-   [Geocoder component](../../../components/next/geocoder-component.md), URI syntax: `geocoder:address:latlng`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-geocoder-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.component.geocoder.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.geocoder.enabled | Whether to enable auto configuration of the geocoder component. This is enabled by default. |  | Boolean |
| camel.component.geocoder.geo-api-context | Configuration for Google maps API. The option is a com.google.maps.GeoApiContext type. |  | GeoApiContext |
| camel.component.geocoder.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |