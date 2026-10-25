# Groovy JSon

**Since Camel 4.19**

The Groovy JSon data format is a basic data format to transform JSon to Map objects, and back to JSon; using the Groovy JSon builder and slurper.

This is convenient when working with JSon and using Groovy for data manipulation.

This data format is limited in functionality but intended to be easier to use. There are none or only a few options to configure.

## Groovy XML Options

The Groovy JSon dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **prettyPrint** (common) | `true` | `Boolean` | Whether to pretty print output nicely formatted. |

## Message Body

The message body at each side of the Groovy JSon data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `text`, `bytes`, `stream`, `file`, `map`, `list` or `pojo` | A Map, a List, a Groovy Node or a Jackson JsonNode to write as JSON. Text, bytes, a stream or a file is written as it is. |
| **Marshal output** | `stream`, as json | The JSON in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file`, as json | 
 |
| **Unmarshal output** | `map` or `list` | A Map (Groovy LazyMap) for a JSON object, a List (ArrayList) for an array. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## Supported Java types

This data format supports marshalling from the following Java type to JSon:

-   Groovy XML Node object (`groovy.util.Node`) (such as message body is from Groovy XML)
    
-   Jackson Node object (`com.fasterxml.jackson.databind.JsonNode` or `tools.jackson.databind.JsonNode`)
    
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