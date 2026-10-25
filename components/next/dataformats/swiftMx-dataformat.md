# SWIFT MX

**Since Camel 3.20**

The SWIFT MX data format is used to encode and decode SWIFT MX messages. The data format leverages the library [Prowide ISO 20022](https://github.com/prowide/prowide-iso20022) to encode and decode SWIFT MX messages.

## Options

The SWIFT MX dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **writeInJson** (common) | `false` | `Boolean` | Whether to marshal messages in JSON format. |
| **readMessageId** (advanced) |  | `Object` | The type of MX message to produce when unmarshalling an input stream. If not set, it will be automatically detected from the namespace used. |
| **readConfig** (advanced) |  | `Object` | Refers to a specific configuration to use when unmarshalling an input stream to lookup from the registry. |
| **writeConfig** (advanced) |  | `Object` | Refers to a specific configuration to use when marshalling a message to lookup from the registry. |

## Message Body

The message body at each side of the SWIFT MX data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `pojo` (`com.prowidesoftware.swift.model.mx.AbstractMX`) | 
A Prowide MX message, such as an MxPacs00800108, as unmarshal gives. The body is not converted: MX XML text fails.

-   With `writeInJson=true`: `pojo` (`com.prowidesoftware.JsonSerializable`)
    





 |
| **Marshal output** | `stream` | The MX XML, or JSON with writeInJson, in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file`, as xml | An MX message, read as UTF-8. |
| **Unmarshal output** | `pojo` or `null` (`com.prowidesoftware.swift.model.mx.AbstractMX`) | The Prowide class of the message by its namespace (or readMessageId), such as MxPacs00800108; null when the type is not detected. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../../manual/body-types.md).

In Spring DSL, you configure the data format using this tag:

_XML-only: Spring XML data format configuration_

```xml
<camelContext>
    <dataFormats>
        <swiftMx id="swiftInJson" writeInJson="true"/>
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
    .marshal("swiftInJson")
    .to("mock:result");
```

```xml
<route>
     <from uri="direct:startEncode" />
     <marshal>
       <custom ref="swiftInJson" />
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
              ref: swiftInJson
        - to:
            uri: mock:result
```

Most of the time, you won’t need to declare the data format if you use the default options. In that case, you can declare the data format inline as shown below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:startEncode")
    .marshal().swiftMx()
    .to("mock:result");
```

```xml
<route>
    <from uri="direct:startEncode" />
    <marshal>
        <swiftMx />
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
            swiftMx: {}
        - to:
            uri: mock:result
```

## Marshal

In this example, we marshal the messages read from a JMS queue in SWIFT format before storing the result into a file. The body must be a Prowide MX object, such as an `MxPacs00800108`, as unmarshal gives: it is not converted, so an MX message as text fails.

-   Java
    
-   XML
    
-   YAML
    

```java
from("jms://myqueue")
    .marshal().swiftMx()
    .to("file://data.bin");
```

```xml
<route>
  <from uri="jms://myqueue"/>
  <marshal>
    <swiftMx/>
  </marshal>
  <to uri="file://data.bin"/>
</route>
```

```yaml
- route:
    from:
      uri: jms://myqueue
      steps:
        - marshal:
            swiftMx: {}
        - to:
            uri: file://data.bin
```

## Unmarshal

The unmarshaller converts the input data into the concrete class of type `com.prowidesoftware.swift.model.mx.AbstractMX` that best matches with the content of the message.

In this example, we unmarshal the content of a file to get SWIFT MX objects before processing them with the `newOrder` processor.

-   Java
    
-   XML
    
-   YAML
    

```java
from("file://data.bin")
    .unmarshal().swiftMx()
    .process("newOrder");
```

```xml
<route>
  <from uri="file://data.bin"/>
  <unmarshal>
    <swiftMx/>
  </unmarshal>
  <to uri="bean:newOrder"/>
</route>
```

```yaml
- route:
    from:
      uri: file://data.bin
      steps:
        - unmarshal:
            swiftMx: {}
        - to:
            uri: bean:newOrder
```

## Translating between MT and MX

The SWIFT MX and [SWIFT MT](swiftMt-dataformat.md) data formats read and write messages, but they do not translate one format into the other. They also do not validate messages against SWIFT network rules or usage guidelines such as CBPR+ or SEPA.

To convert a message, such as an MT103 into a pacs.008, unmarshal it with SWIFT MT, map the fields to an ISO 20022 model class such as `MxPacs00800108` in your own bean or processor, and marshal the result with SWIFT MX. The other direction works the same way, starting with SWIFT MX.

Translation that follows the official SWIFT mapping rules is outside the scope of Camel. Use a dedicated translation product or service for that.

## Dependencies

To use SWIFT MX in your Camel routes, you need to add a dependency on **camel-swift** which implements this data format.

If you use Maven, you can add the following to your pom.xml:

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-swift</artifactId>
  <version>x.x.x</version>  <!-- use the same version as your Camel core version -->
</dependency>
```