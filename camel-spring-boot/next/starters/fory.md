# Fory

Serialize and deserialize messages using Apache Fory

## What’s inside

-   [Fory data format](../../../components/next/dataformats/fory-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-fory-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.fory.allow-auto-wired-fory | Whether to auto-discover Fory from the registry | true | Boolean |
| camel.dataformat.fory.enabled | Whether to enable auto configuration of the fory data format. This is enabled by default. |  | Boolean |
| camel.dataformat.fory.require-class-registration | Whether to require register classes | true | Boolean |
| camel.dataformat.fory.thread-safe | Whether to use the threadsafe Fory | true | Boolean |
| camel.dataformat.fory.unmarshal-type | Class of the java type to use when unmarshalling |  | String |