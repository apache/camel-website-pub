# Any23

**Since Camel 3.0**

Camel Any23 is a DataFormat that uses the Apache Anything To Triples (Any23) library to extract structured data in RDF from a variety of documents on the web. The main functionality of this DataFormat focuses on its Unmarshal method which extracts RDF triplets from compatible pages, in a wide variety of RDF syntaxes. Any23 is a Data Format that is intended to convert HTML from a site (or file) into rdf.

## Any23 Options

The Any23 dataformat supports 4 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **outputFormat** | `RDF4JMODEL` | `Enum` | 
What RDF syntax to unmarshal as, can be: NTRIPLES, TURTLE, NQUADS, RDFXML, JSONLD, RDFJSON, RDF4JMODEL. It is by default: RDF4JMODEL.

Enum values:

-   NTRIPLES
    
-   TURTLE
    
-   NQUADS
    
-   RDFXML
    
-   JSONLD
    
-   RDFJSON
    
-   RDF4JMODEL
    





 |
| **baseUri** |  | `String` | The URI to use as base for building RDF entities if only relative paths are provided. |
| **configuration** |  | `Array` | Configurations for Apache Any23 as key-value pairs in order to customize the extraction process. The list of supported parameters can be found here. If not provided, a default configuration is used. |
| **extractors** |  | `Array` | List of Any23 extractors to be used in the unmarshal operation. A list of the available extractors can be found here here. If not provided, all the available extractors are used. |

## Java DSL Example

An example where the consumer provides some HTML

```java
from("direct:start").unmarshal().any23("http://mock.foo/bar").to("mock:result");
```

## Spring XML Example

The following example shows how to use Any23 to unmarshal using Spring

```xml
<camelContext id="camel" xmlns="http://camel.apache.org/schema/spring">
    <dataFormats>
      <any23 id="any23" baseUri="http://mock.foo/bar" outputFormat="TURTLE" >
        <configuration key="any23.extraction.metadata.nesting" value="off"/>
        <extractors>html-head-title</extractors>
      </any23>
    </dataFormats>
    <route>
      <from uri="direct:start"/>
      <to uri="http://microformats.org/2009/08"/>
      <unmarshal>
        <custom ref="any23"/>
      </unmarshal>
      <to uri="mock:result"/>
    </route>
  </camelContext>
```

## Dependencies

To use Any23 in your camel routes you need to add the a dependency on **camel-any23** which implements this data format.

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-any23</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using any23 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-any23-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.any23.base-uri** | The URI to use as base for building RDF entities if only relative paths are provided. |  | String |
| **camel.dataformat.any23.configuration** | Configurations for Apache Any23 as key-value pairs in order to customize the extraction process. The list of supported parameters can be found here. If not provided, a default configuration is used. |  | List |
| **camel.dataformat.any23.enabled** | Whether to enable auto configuration of the any23 data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.any23.extractors** | List of Any23 extractors to be used in the unmarshal operation. A list of the available extractors can be found here here. If not provided, all the available extractors are used. |  | List |
| **camel.dataformat.any23.output-format** | What RDF syntax to unmarshal as, can be: NTRIPLES, TURTLE, NQUADS, RDFXML, JSONLD, RDFJSON, RDF4JMODEL. It is by default: RDF4JMODEL. |  | Any23OutputFormat |