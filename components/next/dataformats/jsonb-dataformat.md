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

The JSON JSON-B dataformat supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **objectMapper** (common) |  | `String` | Lookup and use the existing Jsonb instance with the given id. |
| **prettyPrint** (common) | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |

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