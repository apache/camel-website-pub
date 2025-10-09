# Zip Deflater

**Since Camel 2.12**

The Zip Deflater Data Format is a message compression and decompression format. Messages marshaled using Zip compression can be unmarshalled using Zip decompression just prior to being consumed at the endpoint. The compression capability is quite useful when you deal with large XML and Text based payloads. It facilitates more optimal use of network bandwidth while incurring a small cost to compress and decompress payloads at the endpoint.

> **Note**
> This dataformat is not for working with zip files such as uncompressing and building zip files. Instead, use the [zipfile](zipFile-dataformat.md) dataformat.

## Options

The Zip Deflater dataformat supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **compressionLevel** (common) | `-1` | `Enum` | 
To specify a specific compression between 0-9. -1 is default compression, 0 is no compression, and 9 is the best compression.

Enum values:

-   \-1
    
-   0
    
-   1
    
-   2
    
-   3
    
-   4
    
-   5
    
-   6
    
-   7
    
-   8
    
-   9
    





 |

## Marshal

In this example we marshal a regular text/XML payload to a compressed payload employing zip compression `Deflater.BEST_COMPRESSION` and send it an ActiveMQ queue called MY\_QUEUE.

```java
from("direct:start").marshal().zipDeflater(Deflater.BEST_COMPRESSION).to("activemq:queue:MY_QUEUE");
```

Alternatively, if you would like to use the default setting, you could send it as

```java
from("direct:start").marshal().zipDeflater().to("activemq:queue:MY_QUEUE");
```

## Unmarshal

In this example, we unmarshal a zipped payload from an ActiveMQ queue called MY\_QUEUE to its original format, and forward it for processing to the UnZippedMessageProcessor. Note that the compression Level employed during marshaling should be identical to the one employed during unmarshalling to avoid errors.

```java
from("activemq:queue:MY_QUEUE").unmarshal().zipDeflater().process(new UnZippedMessageProcessor());
```

## Dependencies

If you use Maven you could add the following to your `pom.xml`, substituting the version number for the latest and greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-zip-deflater</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using zipDeflater with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

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