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

Below is an example of using the DFDL Data Format to unmarshal an EDI message into an XML DOM Document:

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

The DFDL dataformat supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **schemaUri** (common) |  | `String` | **Required** The path to the DFDL schema file. |
| **rootElement** (advanced) |  | `String` | The root element name of the schema to use. If not specified, the first root element in the schema will be used. |
| **rootNamespace** (advanced) |  | `String` | The root namespace of the schema to use. |