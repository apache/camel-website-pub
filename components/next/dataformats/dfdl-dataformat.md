# DFDL

**Since Camel 4.11**

The DFDL Data Format allows you to transform the fixed format data such as EDI message from/to XML using [Data Format Description Language](https://ogf.org/ogf/doku.php/standards/dfdl/dfdl.md), also known as DFDL. DFDL schema is an XML schema annotated with DFDL elements and attributes.

While DFDL schema defines the XML representation of the data structure, it also defines how the conversion between the fixed format and XML is processed using DFDL annotations.

This component uses [Apache Daffodil](https://daffodil.apache.org/) as an underlying DFDL implementation.

Maven users will need to add the following dependency to their `pom.xml` for this data format:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-dfdl</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Usage

### Unmarshal (Fixed format to XML)

Below is an example of using the DFDL Data Format to unmarshal an EDI message into an XML DOM Document:

-   Java
    
-   YAML
    

```java
from("direct:unmarshal")
    .unmarshal().dfdl("X12-837P.dfdl.xsd")
    .log("Unmarshalled X12 837P message: ${body}");
```

```yaml
- route:
    from:
      uri: direct:unmarshal
      steps:
        - unmarshal:
            dfdl:
              schemaUri: X12-837P.dfdl.xsd
        - log:
            message: "Unmarshalled X12 837P message: ${body}"
```

### Marshal (XML to fixed format)

Below is an example of using the DFDL Data Format to marshal XML (a DOM Document, or XML text) into an EDI message:

-   Java
    
-   YAML
    

```java
from("direct:marshal")
    .marshal().dfdl("X12-837P.dfdl.xsd")
    .log("Marshalled X12 837P message: ${body}");
```

```yaml
- route:
    from:
      uri: direct:marshal
      steps:
        - marshal:
            dfdl:
              schemaUri: X12-837P.dfdl.xsd
        - log:
            message: "Marshalled X12 837P message: ${body}"
```

## DFDL Data Format Options

The DFDL dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **schemaUri** (common) |  | `String` | **Required** The path to the DFDL schema file. |
| **rootElement** (advanced) |  | `String` | The root element name of the schema to use. If not specified, the first root element in the schema will be used. |
| **rootNamespace** (advanced) |  | `String` | The root namespace of the schema to use. |

## Message Body

The message body at each side of the DFDL data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `text`, `bytes`, `stream`, `file` or `pojo`, as xml | The XML infoset of the DFDL schema, as text or as a DOM Document (or another DOM Node or Source), which is converted to a DOM Document. |
| **Marshal output** | `stream` | The data in the format the DFDL schema describes, in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file` | Data in the format the DFDL schema describes, such as an EDI message. |
| **Unmarshal output** | `pojo` (`org.w3c.dom.Document`) | The XML infoset as a DOM Document. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).