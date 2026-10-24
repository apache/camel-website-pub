# Base64

**Since Camel 2.11**

The Base64 data format is used for base64 encoding and decoding.

## Options

The Base64 dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **lineLength** (common) | `76` | `Integer` | To specific a maximum line length for the encoded data. By default 76 is used. |
| **lineSeparator** (advanced) |  | `String` | The line separators to use. By default \\r\\n is used. |
| **urlSafe** (advanced) | `false` | `Boolean` | Instead of emitting and / we emit - and \_ respectively. urlSafe is only applied to encode operations. Decoding seamlessly handles both modes. |

## Message Body

The message body at each side of the Base64 data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `text`, `bytes`, `stream` or `file` | The bytes to encode: text in the charset of the exchange, bytes, a stream or a file. |
| **Marshal output** | `stream`, as text | The Base64 text in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file`, as text | 
 |
| **Unmarshal output** | `stream` | The decoded bytes, as a stream. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

In Spring DSL, you configure the data format using this tag:

_XML-only: Spring XML data format configuration_

```xml
<camelContext>
    <dataFormats>
        <!-- for a newline character (\n), use the HTML entity notation coupled with the ASCII code. -->
        <base64 lineSeparator="&#10;" id="base64withNewLine" />
        <base64 lineLength="64" id="base64withLineLength64" />
    </dataFormats>
    ...
</camelContext>
```

Then you can use it later by its reference:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:startEncode")
    .marshal("base64withLineLength64")
    .to("mock:result");
```

```xml
<route>
     <from uri="direct:startEncode" />
     <marshal>
       <custom ref="base64withLineLength64" />
     </marshal>
     <to uri="mock:result" />
</route>
```

```yaml
- route:
    from:
      uri: direct:startEncode
      steps:
        - marshal:
            custom:
              ref: base64withLineLength64
        - to:
            uri: mock:result
```

Most of the time, you won’t need to declare the data format if you use the default options. In that case, you can declare the data format inline as shown below.

## Marshal

In this example, we marshal the file content to a base64 object.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://data.bin")
    .marshal().base64()
    .to("jms://myqueue");
```

```xml
<route>
  <from uri="file://data.bin"/>
  <marshal>
    <base64/>
  </marshal>
  <to uri="jms://myqueue"/>
</route>
```

```yaml
- route:
    from:
      uri: file://data.bin
      steps:
        - marshal:
            base64: {}
        - to:
            uri: jms://myqueue
```

## Unmarshal

In this example, we unmarshal the payload from the JMS queue to a stream of the decoded bytes, before its processed by the `newOrder` processor.

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms://queue/order")
    .unmarshal().base64()
    .process("newOrder");
```

```xml
<route>
  <from uri="jms://queue/order"/>
  <unmarshal>
    <base64/>
  </unmarshal>
  <to uri="bean:newOrder"/>
</route>
```

```yaml
- route:
    from:
      uri: jms://queue/order
      steps:
        - unmarshal:
            base64: {}
        - to:
            uri: bean:newOrder
```

## Dependencies

To use Base64 in your Camel routes, you need to add a dependency on **camel-base64** which implements this data format.

If you use Maven, you can add the following to your pom.xml:

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-base64</artifactId>
  <version>x.x.x</version>  <!-- use the same version as your Camel core version -->
</dependency>
```