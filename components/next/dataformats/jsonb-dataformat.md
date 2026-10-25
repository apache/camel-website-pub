# JSON JSON-B

**Since Camel 3.7**

JSON-B is a Data Format that uses the standard (javax) JSON-B library.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .marshal().json(JsonLibrary.Jsonb)
    .to("mqseries:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <marshal><json library="Jsonb"/></marshal>
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
              library: Jsonb
        - to:
            uri: mqseries:Another.Queue
```

## JSON-B Options

The JSON JSON-B dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **objectMapper** (common) |  | `String` | Lookup and use the existing Jsonb instance with the given id. |
| **prettyPrint** (common) | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |
| **allowUnmarshallType** (common) | `false` | `Boolean` | If enabled then Jackson, Gson or JSON-B is allowed to attempt to use the CamelJacksonUnmarshalType, CamelGsonUnmarshalType or CamelJsonbUnmarshallType header during the unmarshalling. This should only be enabled when desired to be used. |

## Message Body

The message body at each side of the JSON JSON-B data format: _Marshal input_ and _Unmarshal input_ are the bodies marshal and unmarshal can take, and _Marshal output_ and _Unmarshal output_ the body after them.

  
| Side | Body | Description |
| --- | --- | --- |
| **Marshal input** | `any` | A Map, a List or a POJO to write as JSON. Bytes, a stream, a file from a file consumer, or a String with a JSON object or array is written as it is; any other String becomes a JSON string. |
| **Marshal output** | `stream`, as json | The JSON in the stream cache, or a byte array when stream caching is off. |
| **Unmarshal input** | `text`, `bytes`, `stream` or `file`, as json | 
 |
| **Unmarshal output** | `map` or `list` | A Map (HashMap with Yasson) for a JSON object, a List (ArrayList) for an array, with the numbers as BigDecimal.

With `unmarshalType` set: an object of the class it names, or null.

Not known when `allowUnmarshallType` is set.

 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../../manual/camel-catalog.md).

## A body that is already JSON

A body that already is the JSON text is written as it is, not serialized as a Java object: a file from a consumer such as file or ftp, an `InputStream`, a `byte[]`, and a `String` whose text is a JSON object or array (it starts with `{` and ends with `}`, or `[` and `]`). So `marshal: json` after reading a JSON file, or after building the JSON with a template or a Simple expression, sends that JSON unchanged. Any other `String` is written as a JSON string, and POJOs, maps and lists are marshalled as usual. The Jackson, Gson, Jsonb and Fastjson JSON data formats do the same.

## Dependencies

To use JSON-B in your Camel routes, you need to add the dependency on **camel-jsonb** that implements this data format.

If you use Maven, you could add the following to your pom.xml, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-jsonb</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

You have to add a dependency on the **implementation** of a jsonb specification.

If you want to add the Johnzon implementation, and you are using maven, add following to your `pom.xml`:

```xml
<dependency>
  <groupId>org.apache.johnzon</groupId>
  <artifactId>johnzon-jsonb</artifactId>
  <version>x.x.x</version>
</dependency>
```