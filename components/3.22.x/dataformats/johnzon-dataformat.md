# JSON Johnzon

**Since Camel 2.18**

Johnzon is a Data Format which uses the [Johnzon Library](http://johnzon.apache.org/)

```java
from("activemq:My.Queue").
  marshal().json(JsonLibrary.Johnzon).
  to("mqseries:Another.Queue");
```

## Johnzon Options

The JSON Johnzon dataformat supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **objectMapper** |  | `String` | Lookup and use the existing Mapper with the given id. |
| **prettyPrint** | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **unmarshalType** |  | `String` | Class name of the java type to use when unmarshalling. |

## Dependencies

To use Johnzon in your camel routes you need to add the dependency on **camel-johnzon** which implements this data format.

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-johnzon</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using johnzon with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-johnzon-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.johnzon.enabled** | Whether to enable auto configuration of the johnzon data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.johnzon.object-mapper** | Lookup and use the existing Mapper with the given id. |  | String |
| **camel.dataformat.johnzon.pretty-print** | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| **camel.dataformat.johnzon.unmarshal-type** | Class name of the java type to use when unmarshalling. |  | String |