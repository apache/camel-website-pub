# LZF Deflate Compression

**Since Camel 2.17**

The LZF [Data Format](../../../manual/data-format.md) is a message compression and decompression format. It uses the LZF deflate algorithm. Messages marshalled using LZF compression can be unmarshalled using LZF decompression just prior to being consumed at the endpoint. The compression capability is quite useful when you deal with large XML and text-based payloads or when you read messages previously compressed using LZF algorithm.

## Options

The LZF Deflate Compression dataformat supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **usingParallelCompression** (common) | `false` | `Boolean` | Enable encoding (compress) using multiple processing cores. |

## Marshal

In this example, we marshal a regular text/XML payload to a compressed payload employing LZF compression format and send it an ActiveMQ queue called MY\_QUEUE.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start").marshal().lzf().to("activemq:queue:MY_QUEUE");
```

```xml
<route>
  <from uri="direct:start"/>
  <marshal><lzf/></marshal>
  <to uri="activemq:queue:MY_QUEUE"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            lzf: {}
        - to:
            uri: activemq:queue:MY_QUEUE
```

## Unmarshal

In this example we unmarshal a LZF payload from an ActiveMQ queue called MY\_QUEUE to its original format, and forward it for processing to the `UnGZippedMessageProcessor`.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:queue:MY_QUEUE").unmarshal().lzf().process(new UnCompressedMessageProcessor());
```

```xml
<route>
  <from uri="activemq:queue:MY_QUEUE"/>
  <unmarshal><lzf/></unmarshal>
  <process ref="unCompressedMessageProcessor"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:queue:MY_QUEUE
      steps:
        - unmarshal:
            lzf: {}
        - process:
            ref: unCompressedMessageProcessor
```

## Dependencies

To use LZF compression in your Camel routes, you need to add a dependency on **camel-lzf** which implements this data format.

If you use Maven you can add the following to your `pom.xml`, substituting the version number for the latest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-lzf</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```