# GZip Deflater

**Since Camel 2.0**

The GZip Deflater Data Format is a message compression and decompression format. It uses the same deflating algorithm used in the Zip data format, although some additional headers are provided. This format is produced by popular `gzip`/`gunzip` tool. Messages marshalled using GZip compression can be unmarshalled using GZip decompression just prior to being consumed at the endpoint. The compression capability is quite useful when you deal with large XML and text-based payloads or when you read messages previously comressed using `gzip` tool.

> **Note**
> Marshal writes the gzip format of a `.gz` file, and unmarshal reads it, so this data format builds and uncompresses gzip files. A `.tar.gz` file is a tar archive in gzip: unmarshal it with gzipDeflater, then with the [tarFile](tarFile-dataformat.md) data format. For zip files, use the [zipFile](zipFile-dataformat.md) data format.

## Options

The GZip Deflater dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |

## Message Body

The message body at each side of the GZip Deflater data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `text`, `bytes`, `stream` or `file` | The data to compress: text in the charset of the exchange, bytes, a stream or a file. |
| **Marshal output** | `stream`, as binary | The gzip data, as in a .gz file, in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `bytes`, `stream` or `file`, as binary | Gzip data, such as a .gz file; gzip members one after the other are read as one. |
| **Unmarshal output** | `stream` | The decompressed data in the stream cache, or a byte array when stream caching is off. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Marshal

In this example, we marshal a regular text/XML payload to a compressed payload employing gzip compression format and send it an ActiveMQ queue called MY\_QUEUE.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start").marshal().gzipDeflater().to("activemq:queue:MY_QUEUE");
```

```xml
<route>
  <from uri="direct:start"/>
  <marshal><gzipDeflater/></marshal>
  <to uri="activemq:queue:MY_QUEUE"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            gzipDeflater: {}
        - to:
            uri: activemq:queue:MY_QUEUE
```

## Unmarshal

In this example we unmarshal a gzipped payload from an ActiveMQ queue called MY\_QUEUE to its original format, and forward it for processing to the `UnGZippedMessageProcessor`.

_Java-only: unmarshalling a gzipped payload and forwarding to a custom processor_

```java
from("activemq:queue:MY_QUEUE").unmarshal().gzipDeflater().process(new UnGZippedMessageProcessor());
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