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

The Syslog dataformat has no options.

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

## Spring Boot Auto-Configuration

When using syslog with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-syslog-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 1 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.syslog.enabled** | Whether to enable auto configuration of the syslog data format. This is enabled by default. |  | Boolean |