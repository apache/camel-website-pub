# JSON Gson

**Since Camel 2.10**

Gson is a Data Format that uses the [Gson Library](https://github.com/google/gson)

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .marshal().json(JsonLibrary.Gson)
    .to("mqseries:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <marshal><json library="Gson"/></marshal>
  <to uri="mqseries:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - marshal:
            json:
              library: Gson
        - to:
            uri: mqseries:Another.Queue
```

## Gson Options

The JSON Gson dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **prettyPrint** (common) | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |
| **allowUnmarshallType** (common) | `false` | `Boolean` | If enabled then Jackson, Gson or JSON-B is allowed to attempt to use the CamelJacksonUnmarshalType, CamelGsonUnmarshalType or CamelJsonbUnmarshallType header during the unmarshalling. This should only be enabled when desired to be used. |
| **contentTypeHeader** (common) | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |
| **dateFormatPattern** (common) |  | `String` | To configure the date format while marshall or unmarshall Date fields in JSON using Gson. |

## Message Body

The message body at each side of the JSON Gson data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `any` | A Map, a List or a POJO to write as JSON. Bytes, a stream, a file from a file consumer, or a String with a JSON object or array is written as it is; any other String becomes a JSON string. |
| **Marshal output** | `stream`, as json | The JSON in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file`, as json | 
 |
| **Unmarshal output** | `map` or `list` | A Map (Gson LinkedTreeMap) for a JSON object, a List (ArrayList) for an array, with the numbers as Double.

With `unmarshalType` set: an object of the class it names, or null.

Not known when `allowUnmarshallType` is set.

 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../../manual/body-types.md).

## A body that is already JSON

A body that already is the JSON text is written as it is, not serialized as a Java object: a file from a consumer such as file or ftp, an `InputStream`, a `byte[]`, and a `String` whose text is a JSON object or array (it starts with `{` and ends with `}`, or `[` and `]`). So `marshal: json` after reading a JSON file, or after building the JSON with a template or a Simple expression, sends that JSON unchanged. Any other `String` is written as a JSON string, and POJOs, maps and lists are marshalled as usual. The Jackson, Gson, Jsonb and Fastjson JSON data formats do the same.

## Dependencies

To use Gson in your camel routes, you need to add the dependency on **camel-gson** which implements this data format.

If you use maven, you could add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-gson</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```