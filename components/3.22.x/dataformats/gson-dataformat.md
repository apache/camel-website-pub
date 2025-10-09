# JSON Gson

**Since Camel 2.10**

Gson is a Data Format which uses the [Gson Library](https://github.com/google/gson)

```java
from("activemq:My.Queue").
  marshal().json(JsonLibrary.Gson).
  to("mqseries:Another.Queue");
```

## Gson Options

The JSON Gson dataformat supports 4 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **prettyPrint** | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **unmarshalType** |  | `String` | Class name of the java type to use when unmarshalling. |
| **contentTypeHeader** | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |
| **dateFormatPattern** |  | `String` | To configure the date format while marshall or unmarshall Date fields in JSON using Gson. |

## Dependencies

To use Gson in your camel routes you need to add the dependency on **camel-gson** which implements this data format.

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-gson</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using gson with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-gson-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.gson.content-type-header** | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. | true | Boolean |
| **camel.dataformat.gson.date-format-pattern** | To configure the date format while marshall or unmarshall Date fields in JSON using Gson. |  | String |
| **camel.dataformat.gson.enabled** | Whether to enable auto configuration of the gson data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.gson.pretty-print** | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| **camel.dataformat.gson.unmarshal-type** | Class name of the java type to use when unmarshalling. |  | String |