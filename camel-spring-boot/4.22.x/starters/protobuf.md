# Protobuf

Serialize and deserialize Java objects using Google’s Protocol buffers

## What’s inside

-   [Protobuf data format](../../../components/4.22.x/dataformats/protobuf-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-protobuf-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.protobuf.content-type-format | Defines a content type format in which protobuf message will be serialized/deserialized from(to) the Java been. The format can either be native or json for either native protobuf or json fields representation. | native | String |
| camel.dataformat.protobuf.content-type-header | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON | true | Boolean |
| camel.dataformat.protobuf.enabled | Whether to enable auto configuration of the protobuf data format. This is enabled by default. |  | Boolean |
| camel.dataformat.protobuf.instance-class | Name of class to use when unmarshalling. |  | String |