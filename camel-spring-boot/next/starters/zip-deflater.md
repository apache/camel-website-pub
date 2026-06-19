# GZip Deflater

Compress and decompress messages using java.util.zip.GZIPStream.

## What’s inside

-   [GZip Deflater data format](../../../components/next/dataformats/gzipDeflater-dataformat.md)
    
-   [Zip Deflater data format](../../../components/next/dataformats/zipDeflater-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-zip-deflater-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.gzip-deflater.enabled | Whether to enable auto configuration of the gzipDeflater data format. This is enabled by default. |  | Boolean |
| camel.dataformat.zip-deflater.compression-level | To specify a specific compression between 0-9. -1 is default compression, 0 is no compression, and 9 is the best compression. | \-1 | Integer |
| camel.dataformat.zip-deflater.enabled | Whether to enable auto configuration of the zipDeflater data format. This is enabled by default. |  | Boolean |