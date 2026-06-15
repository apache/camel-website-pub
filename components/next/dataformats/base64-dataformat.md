# Base64

**Since Camel 2.11**

The Base64 data format is used for base64 encoding and decoding.

## Options

The Base64 dataformat supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **lineLength** (common) | `76` | `Integer` | To specific a maximum line length for the encoded data. By default 76 is used. |
| **lineSeparator** (advanced) |  | `String` | The line separators to use. Uses new line characters (CRLF) by default. |
| **urlSafe** (advanced) | `false` | `Boolean` | Instead of emitting '' and '/' we emit '-' and '\_' respectively. urlSafe is only applied to encode operations. Decoding seamlessly handles both modes. Is by default false. |

In Spring DSL, you configure the data format using this tag:

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

```xml
<route>
     <from uri="direct:startEncode" />
     <marshal ref="base64withLineLength64" />
     <to uri="mock:result" />
</route>
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

In this example, we unmarshal the payload from the JMS queue to a byte\[\] object, before its processed by the `newOrder` processor.

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

## Spring Boot Auto-Configuration

When using base64 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-base64-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.base64.enabled** | Whether to enable auto configuration of the base64 data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.base64.line-length** | To specific a maximum line length for the encoded data. By default 76 is used. | 76 | Integer |
| **camel.dataformat.base64.line-separator** | The line separators to use. Uses new line characters (CRLF) by default. |  | String |
| **camel.dataformat.base64.url-safe** | Instead of emitting '' and '/' we emit '-' and '\_' respectively. urlSafe is only applied to encode operations. Decoding seamlessly handles both modes. Is by default false. | false | Boolean |