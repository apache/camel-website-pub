# Groovy XML

**Since Camel 4.15**

The Groovy XML data format is a basic data format to transform XML to Groovy Node objects, and back to XML. This is convenient when working with XML and using Groovy for data manipulation.

This data format is limited in functionality but intended to be easier to use. There are none or only a few options to configure.

## Groovy XML Options

The Groovy XML dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **attributeMapping** (common) | `true` | `Boolean` | Whether to enable attribute mapping. When enabled, keys that start with \_ or character will be mapped to an XML attribute, and vice versa. |

## Message Body

The message body at each side of the Groovy XML data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `text`, `bytes`, `stream`, `file`, `map` or `pojo` | A Groovy Node or GPathResult, a Map or a Jackson JsonNode to write as XML. Text, bytes, a stream or a file is written as it is. |
| **Marshal output** | `stream`, as xml | The XML in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file`, as xml | 
 |
| **Unmarshal output** | `pojo` (`groovy.util.Node`) | The XML parsed into a Groovy Node. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Supported Java types

This data format supports marshalling from the following Java type to XML:

-   Groovy XML Node object (`groovy.util.Node`)
    
-   Jackson Node object (`com.fasterxml.jackson.databind.JsonNode` or `tools.jackson.databind.JsonNode`)
    
-   Camel JSonObject (`org.apache.camel.util.json.JsonObject`)
    
-   Java Map object ('java.util.Map')
    

And unmarshalling from XML to Groovy Node (`groovy.util.Node`) object.

## Examples

For example to transform from XML to Groovy Node:

```yaml
- route:
    description: From timer to xml
    from:
      uri: timer
      parameters:
        repeatCount: "1"
        timerName: tick
      steps:
        - setBody:
            expression:
              constant:
                expression: |-
                  <library>
                    <book id="bk101">
                      <title>No Title</title>
                      <author>F. Scott Fitzgerald</author>
                      <year>1925</year>
                      <genre>Classic</genre>
                    </book>
                    <book id="bk102">
                      <title>1984</title>
                      <author>George Orwell</author>
                      <year>1949</year>
                      <genre>Dystopian</genre>
                    </book>
                  </library>
        - unmarshal:
            groovyXml: {}
        - log:
            message: "${body}"
```

This will transform the XML into a Groovy Node object which can be manipulated using Java and Groovy code.

To convert back to XML you just use the opposite direction with _marshal_.

## Dependencies

To use the data format in your camel routes, you need to add a dependency on **camel-groovy** which implements this data format.

If you use maven, you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-groovy</artifactId>
  <version>x.x.x</version>
</dependency>
```