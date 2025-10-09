# Groovy XML

**Since Camel 4.15**

The Groovy XML data format is a basic data format to transform XML to Groovy Node objects, and back to XML. This is convenient when working with XML and using Groovy for data manipulation.

This data format is limited in functionality but intended to be easier to use. There are none or only a few options to configure.

## Groovy XML Options

The Groovy XML dataformat supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **attributeMapping** (common) | `true` | `Boolean` | To turn on or off attribute mapping. When enabled then keys that start with \_ or character will be mapped to an XML attribute, and vise versa. This rule is what Jackson and other XML or JSon libraries uses. |

## Supported Java types

This data format supports marshalling from the following Java type to XML:

-   Groovy Node object (`groovy.util.Node`)
    
-   Jackson Node object (`com.fasterxml.jackson.databind.JsonNode`)
    
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
            groovyXml:
              {}
        - log:
            message: "${body}"
```

This will transform the XML into a Groovy Node object which can be manipulated using Java and Groovy code.

To convert back to XML you just use the opposite direction with _marshal_.

## Dependencies

To use the data format in your camel routes, you need to add a dependency on **camel-groovy-xml** which implements this data format.

If you use maven, you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-groovy-xml</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using groovyXml with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-groovy-xml-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.groovy-xml.attribute-mapping** | To turn on or off attribute mapping. When enabled then keys that start with \_ or character will be mapped to an XML attribute, and vise versa. This rule is what Jackson and other XML or JSon libraries uses. | true | Boolean |
| **camel.dataformat.groovy-xml.enabled** | Whether to enable auto configuration of the groovyXml data format. This is enabled by default. |  | Boolean |