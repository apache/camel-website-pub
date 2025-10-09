# GZip Deflater

**Since Camel 2.0**

The GZip Deflater Data Format is a message compression and de-compression format. It uses the same deflate algorithm that is used in the Zip data format, although some additional headers are provided. This format is produced by popular `gzip`/`gunzip` tool. Messages marshalled using GZip compression can be unmarshalled using GZip decompression just prior to being consumed at the endpoint. The compression capability is quite useful when you deal with large XML and Text based payloads or when you read messages previously comressed using `gzip` tool.

> **Note**
> This dataformat is not for working with gzip files such as uncompressing and building gzip files. Instead use the zipfile dataformat.

## Options

The GZip Deflater dataformat has no options.

## Marshal

In this example we marshal a regular text/XML payload to a compressed payload employing gzip compression format and send it an ActiveMQ queue called MY\_QUEUE.

```java
from("direct:start").marshal().gzipDeflater().to("activemq:queue:MY_QUEUE");
```

## Unmarshal

In this example we unmarshal a gzipped payload from an ActiveMQ queue called MY\_QUEUE to its original format, and forward it for processing to the `UnGZippedMessageProcessor`.

```java
from("activemq:queue:MY_QUEUE").unmarshal().gzipDeflater().process(new UnGZippedMessageProcessor());
```

## Dependencies

This data format is provided in **camel-core** so no additional dependencies is needed.

## Spring Boot Auto-Configuration

When using gzipDeflater with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-zip-deflater-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.gzip-deflater.enabled** | Whether to enable auto configuration of the gzipDeflater data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.zip-deflater.compression-level** | To specify a specific compression between 0-9. -1 is default compression, 0 is no compression, and 9 is the best compression. | \-1 | Integer |
| **camel.dataformat.zip-deflater.enabled** | Whether to enable auto configuration of the zipDeflater data format. This is enabled by default. |  | Boolean |