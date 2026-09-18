# JSonApi

Marshal and unmarshal JSON:API resources using JSONAPI-Converter library

## What’s inside

-   [JSonApi data format](../../../components/next/dataformats/jsonApi-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-jsonapi-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.json-api.data-format-types | The classes to take into account for the marshalling. Multiple classes can be separated by comma. |  | String |
| camel.dataformat.json-api.enabled | Whether to enable auto configuration of the jsonApi data format. This is enabled by default. |  | Boolean |
| camel.dataformat.json-api.main-format-type | The class to take into account while unmarshalling. |  | String |