# LZF Deflate Compression

Compress and decompress streams using LZF deflate algorithm

## What’s inside

-   [LZF Deflate Compression data format](../../../components/4.22.x/dataformats/lzf-dataformat.md)
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-lzf-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

The starter supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.dataformat.lzf.enabled | Whether to enable auto configuration of the lzf data format. This is enabled by default. |  | Boolean |
| camel.dataformat.lzf.using-parallel-compression | Whether to enable encoding (compress) using multiple processing cores. | false | Boolean |