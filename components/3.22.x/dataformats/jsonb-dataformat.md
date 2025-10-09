# JSON JSON-B

**Since Camel 3.7**

JSON-B is a Data Format which uses the standard (javax) JSON-B library.

```java
from("activemq:My.Queue").
  marshal().json(JsonLibrary.Jsonb).
  to("mqseries:Another.Queue");
```

## JSON-B Options

The JSON JSON-B dataformat supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **objectMapper** |  | `String` | Lookup and use the existing Jsonb instance with the given id. |
| **prettyPrint** | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **unmarshalType** |  | `String` | Class name of the java type to use when unmarshalling. |

## Dependencies

To use JSON-B in your camel routes you need to add the dependency on **camel-jsonb** which implements this data format.

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-jsonb</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

You have to add a dependency on the **implementation** of a jsonb specification.

If you want to add the Johnzon implementation and you are using maven, just add following to your pom.xml

```xml
<dependency>
  <groupId>org.apache.johnzon</groupId>
  <artifactId>johnzon-jsonb</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using jsonb with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jsonb-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.jsonb.enabled** | Whether to enable auto configuration of the jsonb data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.jsonb.object-mapper** | Lookup and use the existing Jsonb instance with the given id. |  | String |
| **camel.dataformat.jsonb.pretty-print** | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| **camel.dataformat.jsonb.unmarshal-type** | Class name of the java type to use when unmarshalling. |  | String |