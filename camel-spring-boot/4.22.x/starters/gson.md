# JSON Gson

Marshal POJOs to JSON and back using Gson

## What’s inside

-   [JSON Gson data format](../../../components/4.22.x/dataformats/gson-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-gson-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.gson.content-type-header | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON | true | Boolean |
| camel.dataformat.gson.date-format-pattern | To configure the date format while marshall or unmarshall Date fields in JSON using Gson |  | String |
| camel.dataformat.gson.enabled | Whether to enable auto configuration of the gson data format. This is enabled by default. |  | Boolean |
| camel.dataformat.gson.pretty-print | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| camel.dataformat.gson.unmarshal-type | Class name of the java type to use when unmarshalling. |  | String |