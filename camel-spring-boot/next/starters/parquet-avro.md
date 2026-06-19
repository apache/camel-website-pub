# Parquet File

Parquet Avro serialization and de-serialization.

## What’s inside

-   [Parquet File data format](../../../components/next/dataformats/parquetAvro-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-parquet-avro-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.parquet-avro.compression-codec-name | Compression codec to use when marshalling. | GZIP | String |
| camel.dataformat.parquet-avro.enabled | Whether to enable auto configuration of the parquetAvro data format. This is enabled by default. |  | Boolean |
| camel.dataformat.parquet-avro.lazy-load | Whether the unmarshalling should produce an iterator of records or read all the records at once. | false | Boolean |
| camel.dataformat.parquet-avro.unmarshal-type | Class to use when (un)marshalling. If omitted, parquet files are converted into Avro’s GenericRecords for unmarshalling and input objects are assumed as GenericRecords for marshalling. |  | String |