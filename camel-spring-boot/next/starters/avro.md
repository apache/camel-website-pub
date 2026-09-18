# Avro

Serialize and deserialize messages using Apache Avro binary data format

## What’s inside

-   [Avro data format](../../../components/next/dataformats/avro-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-avro-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.avro.enabled | Whether to enable auto configuration of the avro data format. This is enabled by default. |  | Boolean |
| camel.dataformat.avro.instance-class-name | Class name to use for marshal and unmarshalling. |  | String |
| camel.dataformat.avro.serializable-packages | Comma-separated list of additional packages that contain trusted Avro model classes. Avro 1.12 validates classes resolved from schemas; Camel automatically trusts packages derived from the configured schema or instance class. |  | String |