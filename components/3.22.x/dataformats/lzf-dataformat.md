# LZF Deflate Compression

**Since Camel 2.17**

The LZF [Data Format](../../../manual/data-format.md) is a message compression and de-compression format. It uses the LZF deflate algorithm. Messages marshalled using LZF compression can be unmarshalled using LZF decompression just prior to being consumed at the endpoint. The compression capability is quite useful when you deal with large XML and Text based payloads or when you read messages previously comressed using LZF algotithm.

## Options

The LZF Deflate Compression dataformat supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **usingParallelCompression** | `false` | `Boolean` | Enable encoding (compress) using multiple processing cores. |

## Marshal

In this example we marshal a regular text/XML payload to a compressed payload employing LZF compression format and send it an ActiveMQ queue called MY\_QUEUE.

```java
from("direct:start").marshal().lzf().to("activemq:queue:MY_QUEUE");
```

## Unmarshal

In this example we unmarshal a LZF payload from an ActiveMQ queue called MY\_QUEUE to its original format, and forward it for processing to the `UnGZippedMessageProcessor`.

```java
from("activemq:queue:MY_QUEUE").unmarshal().lzf().process(new UnCompressedMessageProcessor());
```

## Dependencies

To useLZF compression in your camel routes you need to add a dependency on **camel-lzf** which implements this data format.

If you use Maven you can just add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-lzf</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using lzf with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-lzf-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.lzf.enabled** | Whether to enable auto configuration of the lzf data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.lzf.using-parallel-compression** | Enable encoding (compress) using multiple processing cores. | false | Boolean |