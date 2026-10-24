# Syslog

**Since Camel 2.6**

The Syslog dataformat is used for working with [RFC3164](http://www.ietf.org/rfc/rfc3164.txt) and RFC5424 messages.

This component supports the following:

-   UDP consumption of syslog messages
    
-   Agnostic data format using either plain String objects or SyslogMessage model objects.
    
-   Type Converter from/to SyslogMessage and String
    
-   Integration with the [camel-mina](../mina-component.md) component.
    
-   Integration with the [camel-netty](../netty-component.md) component.
    
-   Encoder and decoder for the [Netty component](../netty-component.md).
    
-   Support for RFC5424 also.
    

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-syslog</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## RFC3164 Syslog protocol

Syslog uses the user datagram protocol (UDP) as its underlying transport layer mechanism. The UDP port that has been assigned to syslog is 514.

To expose a Syslog listener service, we reuse the existing [Mina Component](../mina-component.md) or [Netty Component](../netty-component.md) where we just use the `Rfc3164SyslogDataFormat` to marshal and unmarshal messages. Notice that from **Camel 2.14** onwards the syslog dataformat is renamed to `SyslogDataFormat`.

## Options

The Syslog dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |

## Message Body

The message body at each side of the Syslog data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `text` or `pojo` | A SyslogMessage, or the text of a syslog message, which is parsed first. A missing facility, severity, hostname or timestamp gets a default. |
| **Marshal output** | `stream`, as text | The syslog message in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file`, as text | An RFC 3164 or RFC 5424 message, decoded with the charset of the exchange. |
| **Unmarshal output** | `pojo` (`org.apache.camel.component.syslog.SyslogMessage`) | A SyslogMessage, an Rfc5424SyslogMessage for an RFC 5424 message. The facility, severity, hostname and timestamp are headers as well. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## RFC5424 Syslog protocol

**Since Camel 2.14**

To expose a Syslog listener service, we reuse the existing [Mina Component](../mina-component.md) or [Netty Component](../netty-component.md) where we just use the `SyslogDataFormat` to marshal and unmarshal messages

### Exposing a Syslog listener

In our Spring XML file, we configure an endpoint to listen for udp messages on port 10514, note that in netty we disable the defaultCodec, this  
will allow a fallback to a NettyTypeConverter and delivers the message as an InputStream:

-   Java
    
-   XML
    
-   YAML
    

```java
from("netty:udp://localhost:10514?sync=false&allowDefaultCodec=false")
    .unmarshal(new SyslogDataFormat())
    .to("mock:stop1");
```

```xml
<camelContext id="myCamel" xmlns="http://camel.apache.org/schema/spring">

    <dataFormats>
          <syslog id="mySyslog"/>
    </dataFormats>

    <route>
          <from uri="netty:udp://localhost:10514?sync=false&amp;allowDefaultCodec=false"/>
          <unmarshal><custom ref="mySyslog"/></unmarshal>
          <to uri="mock:stop1"/>
    </route>

</camelContext>
```

```yaml
- route:
    from:
      uri: netty:udp://localhost:10514
      parameters:
        sync: false
        allowDefaultCodec: false
      steps:
        - unmarshal:
            syslog: {}
        - to:
            uri: mock:stop1
```

The same route using [Mina Component](../mina-component.md)

-   Java
    
-   XML
    
-   YAML
    

```java
from("mina:udp://localhost:10514")
    .unmarshal(new SyslogDataFormat())
    .to("mock:stop1");
```

```xml
<camelContext id="myCamel" xmlns="http://camel.apache.org/schema/spring">

    <dataFormats>
          <syslog id="mySyslog"/>
    </dataFormats>

    <route>
          <from uri="mina:udp://localhost:10514"/>
          <unmarshal><custom ref="mySyslog"/></unmarshal>
          <to uri="mock:stop1"/>
    </route>

</camelContext>
```

```yaml
- route:
    from:
      uri: mina:udp://localhost:10514
      steps:
        - unmarshal:
            syslog: {}
        - to:
            uri: mock:stop1
```

### Sending syslog messages to a remote destination

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:syslogMessages")
    .marshal(new SyslogDataFormat())
    .to("mina:udp://remotehost:10514");
```

```xml
<camelContext id="myCamel" xmlns="http://camel.apache.org/schema/spring">

    <dataFormats>
        <syslog id="mySyslog"/>
    </dataFormats>

    <route>
        <from uri="direct:syslogMessages"/>
        <marshal><custom ref="mySyslog"/></marshal>
        <to uri="mina:udp://remotehost:10514"/>
    </route>

</camelContext>
```

```yaml
- route:
    from:
      uri: direct:syslogMessages
      steps:
        - marshal:
            syslog: {}
        - to:
            uri: mina:udp://remotehost:10514
```