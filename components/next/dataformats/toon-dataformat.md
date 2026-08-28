# TOON

**Since Camel 4.23**

The TOON data format marshals JSON-compatible Java values to [TOON (Token-Oriented Object Notation)](https://github.com/toon-format/spec) and unmarshals TOON text back to a Java object graph.

TOON is a compact, human-readable encoding of the JSON data model. It is designed as an alternative textual representation of JSON values rather than as a general-purpose serialization format. This Camel data format is a **Preview** component for Camel 4.23.x.

The implementation uses the official Java library [JToon](https://github.com/toon-format/toon-java). Camel does not implement a TOON parser or encoder of its own.

## TOON Options

The TOON dataformat supports the following options which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **indent** (common) | `2` | `Integer` | Number of spaces per indentation level. |
| **delimiter** (common) | `COMMA` | `Enum` | 
Delimiter used for tabular array rows and inline primitive arrays.

Enum values:

-   COMMA
    
-   TAB
    
-   PIPE
    





 |
| **lengthMarker** (common) | `false` | `Boolean` | Whether to prefix array lengths with a hash marker so arrays render as hash-prefixed lengths instead of plain lengths. |
| **strict** (common) | `true` | `Boolean` | Whether to enable strict validation when unmarshalling TOON. When false, JToon uses best-effort parsing. |
| **contentTypeHeader** (common) | `true` | `Boolean` | Whether the data format should set the Content-Type header to text/toon when marshalling. |

## Marshal behavior

Marshalling converts a JSON-compatible message body to TOON text:

-   `Map`, `List`, POJOs, numbers, booleans, and `null` are encoded with JToon `encode`.
    
-   A Java `String` body is always treated as a JSON document and encoded with JToon `encodeJson`. This is the path to use when transforming existing JSON text to TOON.
    

> **Important**
> A plain (non-JSON) `String` such as `hello world` is **not** encoded as a TOON string scalar. JToon rejects it with `IllegalArgumentException`. To marshal a Java string as a TOON scalar, wrap it in a `List` or `Map`, or use a typed Java value rather than a raw `String` body.

The output charset follows Camel’s exchange charset (`ExchangeHelper.getCharsetName(exchange)`). When `contentTypeHeader` is enabled (the default), marshalling sets the `Content-Type` header to `text/toon`. That media type is provisional in the TOON specification.

## Unmarshal behavior

Unmarshalling decodes TOON text with JToon `decode` and returns a Java JSON-compatible object graph. Typical results are:

-   `Map` for objects
    
-   `List` for arrays
    
-   `String`, `Long`, `Double`, `Boolean`, or `null` for scalars
    

JToon may decode whole numbers as `Long` rather than `Integer`. Malformed TOON fails with the exception thrown by JToon; Camel does not swallow parse errors.

## Usage

### Marshalling (Java object to TOON)

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:marshal")
    .marshal().toon()
    .to("mock:toon");
```

```xml
<route>
  <from uri="direct:marshal"/>
  <marshal>
    <toon/>
  </marshal>
  <to uri="mock:toon"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:marshal
    steps:
      - marshal:
          toon: {}
      - to:
          uri: mock:toon
```

### Unmarshalling (TOON to Java object)

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:unmarshal")
    .unmarshal().toon()
    .to("mock:json");
```

```xml
<route>
  <from uri="direct:unmarshal"/>
  <unmarshal>
    <toon/>
  </unmarshal>
  <to uri="mock:json"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:unmarshal
    steps:
      - unmarshal:
          toon: {}
      - to:
          uri: mock:json
```

### JSON document to TOON

A `String` body that contains JSON is parsed as JSON and encoded as TOON:

```java
from("direct:jsonToToon")
    .marshal().toon();
```

For example, the JSON document `{"id":1,"name":"Ada"}` is marshalled to TOON object syntax rather than being encoded as a quoted TOON string scalar. A `String` body that is not valid JSON fails rather than becoming a TOON scalar.

### TOON to Java object

```java
from("direct:toonToObject")
    .unmarshal().toon()
    .process(exchange -> {
        Object graph = exchange.getMessage().getBody();
        // typically a Map, List, or JSON scalar
    });
```

## Dependencies

Maven users need to add the following dependency:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-toon</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```