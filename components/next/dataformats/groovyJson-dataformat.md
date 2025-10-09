# Groovy JSon

**Since Camel 4.19**

The Groovy JSon data format is a basic data format to transform JSon to Map objects, and back to JSon; using the Groovy JSon builder and slurper.

This is convenient when working with JSon and using Groovy for data manipulation.

This data format is limited in functionality but intended to be easier to use. There are none or only a few options to configure.

## Groovy XML Options

The Groovy JSon dataformat supports 1 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **prettyPrint** (common) | `true` | `Boolean` | To pretty printing output nicely formatted. Is by default true. |

## Supported Java types

This data format supports marshalling from the following Java type to JSon:

-   Groovy XML Node object (`groovy.util.Node`) (such as message body is from Groovy XML)
    
-   Jackson Node object (`com.fasterxml.jackson.databind.JsonNode`)
    
-   Camel JSonObject (`org.apache.camel.util.json.JsonObject`)
    
-   Java Map object ('java.util.Map')
    
-   Java List object ('java.util.List')
    

And unmarshalling from JSon to (`java.util.Map`) / (`java.util.List`) object.

## Examples

For example to transform from JSon to `java.util.Map`:

```yaml
- route:
    description: From timer to json
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
                    {
                        "library": {
                            "book": [
                                {
                                    "title": "No Title",
                                    "author": "F. Scott Fitzgerald",
                                    "year": "1925",
                                    "genre": "Classic",
                                    "id": "bk101"
                                },
                                {
                                    "title": "1984",
                                    "author": "George Orwell",
                                    "year": "1949",
                                    "genre": "Dystopian",
                                    "id": "bk102"
                                }
                            ]
                        }
                    }
        - unmarshal:
            groovyJson: {}
        - log:
            message: "${body}"
```

This will transform the JSon into a `java.util.Map` object which can be manipulated using Java and Groovy code.

To convert back to JSon you just use the opposite direction with _marshal_.

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

## Spring Boot Auto-Configuration

When using groovyJson with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-groovy-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.groovy-json.enabled** | Whether to enable auto configuration of the groovyJson data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.groovy-json.pretty-print** | To pretty printing output nicely formatted. Is by default true. | true | Boolean |
| **camel.dataformat.groovy-xml.attribute-mapping** | To turn on or off attribute mapping. When enabled then keys that start with \_ or character will be mapped to an XML attribute, and vise versa. This rule is what Jackson and other XML or JSon libraries uses. | true | Boolean |
| **camel.dataformat.groovy-xml.enabled** | Whether to enable auto configuration of the groovyXml data format. This is enabled by default. |  | Boolean |
| **camel.language.groovy.enabled** | Whether to enable auto configuration of the groovy language. This is enabled by default. |  | Boolean |
| **camel.language.groovy.trim** | Whether to trim the source code to remove leading and trailing whitespaces and line breaks. For example when using DSLs where the source will span across multiple lines and there may be additional line breaks at both the beginning and end. | true | Boolean |