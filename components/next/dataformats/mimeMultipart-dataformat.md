# MIME Multipart

**Since Camel 2.17**

This data format that can convert a Camel message with attachments into a Camel message that has a MIME-Multipart message as message body (and no attachments).

The use case for this is to enable the user to send attachments over endpoints that do not directly support attachments, either as special protocol implementation (e.g. send a MIME-multipart over an HTTP endpoint) or as a kind of tunneling solution (e.g. because camel-jms does not support attachments but by marshalling the message with attachments into a MIME-Multipart, sending that to a JMS queue, receiving the message from the JMS queue and unmarshalling it again (into a message body with attachments).

The marshal option of the mimeMultipart data format will convert a message with attachments into a MIME-Multipart message. If the parameter `multipartWithoutAttachment` is set to true, it will also marshal messages without attachments into a multipart message with a single part, if the parameter is set to false it will leave the message alone.

MIME headers of the multipart as "MIME-Version" and "Content-Type" are set as camel headers to the message. If the parameter "headersInline" is set to true, it will also create a MIME multipart message in any case.  
Furthermore, the MIME headers of the multipart are written as part of the message body, not as camel headers.

The unmarshal option of the mimeMultipart data format will convert a MIME-Multipart message into a camel message with attachments and leave other messages alone. MIME-Headers of the MIME-Multipart message have to be set as Camel headers. The unmarshalling will only take place if the "Content-Type" header is set to a "multipart" type. If the option "headersInline" is set to true, the body is always parsed as a MIME message. As a consequence, if the message body is a stream and stream caching is not enabled, a message body that is actually not a MIME message with MIME headers in the message body will be replaced by an empty message.

## Options

The MIME Multipart dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **multipartSubType** (common) | `mixed` | `String` | Specify the subtype of the MIME Multipart. |
| **multipartWithoutAttachment** (common) | `false` | `Boolean` | Whether a message without attachment is also marshaled into a MIME Multipart (with only one body part). |
| **headersInline** (common) | `false` | `Boolean` | Whether the MIME-Multipart headers are part of the message body (true) or are set as Camel headers (false). |
| **includeHeaders** (common) |  | `String` | A regex that defines which Camel headers are also included as MIME headers into the MIME multipart. This only works if headersInline is set to true. |
| **binaryContent** (common) | `false` | `Boolean` | Whether the content of binary parts in the MIME multipart is binary (true) or Base-64 encoded (false). |

## Message Body

The message body at each side of the MIME Multipart data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `text`, `bytes`, `stream` or `file` | The body of the first part, of the content type in the Content-Type header (application/octet-stream when not set); the attachments of the message are the other parts. |
| **Marshal output** | `stream` | The MIME multipart in the stream cache, or a byte array when stream caching is off, with its MIME headers as Camel headers unless headersInline is true. Without attachments the body is written as it is, unless multipartWithoutAttachment or headersInline is true. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file` | A MIME multipart, with its Content-Type (multipart/\*) and MIME-Version as Camel headers, as marshal leaves them; with headersInline, the MIME headers are at the start of the body. |
| **Unmarshal output** | `stream` | 
The first part, decoded, as a stream, with the other parts as attachments and its Content-Type as a header. Without a multipart Content-Type header the body is given back as a stream; with headersInline, a body that is not a multipart stays as it was.

-   With `headersInline=true`: `stream` or `unchanged`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Message Headers (marshal)

  
| Name | Type | Description |
| --- | --- | --- |
| Message-Id | String | The marshal operation will set this parameter to the generated MIME message id if the "headersInline" parameter is set to false. |
| MIME-Version | String | The marshal operation will set this parameter to the applied MIME version (1.0) if the "headersInline" parameter is set to false. |
| Content-Type | String | The content of this header will be used as a content type for the message body part. If no content type is set, "application/octet-stream" is assumed. After the marshal operation, the content type is set to "multipart/" with the "multipartSubType" ("multipart/mixed" by default), or empty if the "headersInline" parameter is set to true. |
| Content-Encoding | String | If the incoming content type is "text/\*" the content encoding will be set to the encoding parameter of the Content-Type MIME header of the body part. Furthermore, the given charset is applied for text to binary conversions. |

## Message Headers (unmarshal)

  
| Name | Type | Description |
| --- | --- | --- |
| Content-Type | String | If this header is not set to `multipart/*` the unmarshal operation will not do anything. In other cases, the multipart will be parsed into a camel message with attachments and the header is set to the Content-Type header of the body part, except if this is application/octet-stream. In the latter case, the header is removed. |
| Content-Encoding | String | If the content-type of the body part contains an encoding parameter, this header will be set to the value of this encoding parameter (converted from MIME encoding descriptor to Java encoding descriptor) |
| MIME-Version | String | The unmarshal operation will read this header and use it for parsing the MIME multipart. The header is removed afterward |

## Examples

-   Java
    
-   YAML
    

```java
from(...).marshal().mimeMultipart()
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            mimeMultipart: {}
        - to:
            uri: mock:result
```

With a message where no Content-Type header is set, will create a Message with the following message Camel headers:

**Camel Message Headers**

Content-Type=multipart/mixed; \\n boundary="----=\_Part\_0\_14180567.1447658227051"
Message-Id=<...>
MIME-Version=1.0

The message body will be:

**Camel Message Body**

\------=\_Part\_0\_14180567.1447658227051
Content-Type: application/octet-stream
Content-Transfer-Encoding: base64
Qm9keSB0ZXh0
------=\_Part\_0\_14180567.1447658227051
Content-Type: application/binary
Content-Transfer-Encoding: base64
Content-Disposition: attachment; filename="Attachment File Name"
AAECAwQFBgc=
------=\_Part\_0\_14180567.1447658227051--

A message with the header Content-Type set to "text/plain" sent to the route

-   Java
    
-   YAML
    

```java
from("...").marshal().mimeMultipart("related", true, true, "(included|x-.*)", true);
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            mimeMultipart:
              multipartSubType: related
              multipartWithoutAttachment: true
              headersInline: true
              includeHeaders: "(included|x-.*)"
              binaryContent: true
        - to:
            uri: mock:result
```

will create a message without any specific MIME headers set as Camel headers (the Content-Type header is removed from the Camel message) and the following message body that includes also all headers of the original message starting with "x-" and the header with name "included":

**Camel Message Body**

Message-ID: <...>
MIME-Version: 1.0
Content-Type: multipart/related;
    boundary="----=\_Part\_0\_1134128170.1447659361365"
x-bar: also there
included: must be included
x-foo: any value

------=\_Part\_0\_1134128170.1447659361365
Content-Type: text/plain
Content-Transfer-Encoding: 8bit

Body text
------=\_Part\_0\_1134128170.1447659361365
Content-Type: application/binary
Content-Transfer-Encoding: binary
Content-Disposition: attachment; filename="Attachment File Name"

\[binary content\]
------=\_Part\_0\_1134128170.1447659361365

## Dependencies

To use MIME-Multipart in your Camel routes, you need to add a dependency on **camel-mail**, which implements this data format.

If you use Maven, you can add the following to your pom.xml:

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-mail</artifactId>
  <version>x.x.x</version> <!-- use the same version as your Camel core version -->
</dependency>
```