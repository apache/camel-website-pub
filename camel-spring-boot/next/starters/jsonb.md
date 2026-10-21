# JSON JSON-B

Marshal POJOs to JSON and back using JSON-B.

## What’s inside

-   [JSON JSON-B data format](../../../components/next/dataformats/jsonb-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-jsonb-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.jsonb.allow-unmarshall-type | If enabled then Jackson, Gson or JSON-B is allowed to attempt to use the CamelJacksonUnmarshalType, CamelGsonUnmarshalType or CamelJsonbUnmarshallType header during the unmarshalling. This should only be enabled when desired to be used. | false | Boolean |
| camel.dataformat.jsonb.enabled | Whether to enable auto configuration of the jsonb data format. This is enabled by default. |  | Boolean |
| camel.dataformat.jsonb.object-mapper | Lookup and use the existing Jsonb instance with the given id. |  | String |
| camel.dataformat.jsonb.pretty-print | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| camel.dataformat.jsonb.unmarshal-type | Class name of the java type to use when unmarshalling. |  | String |