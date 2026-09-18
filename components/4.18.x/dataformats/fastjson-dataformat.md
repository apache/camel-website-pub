# JSON Fastjson

**Since Camel 2.20**

Fastjson is a Data Format that uses the [Fastjson Library](https://github.com/alibaba/fastjson)

```java
from("activemq:My.Queue").
  marshal().json(JsonLibrary.Fastjson).
  to("mqseries:Another.Queue");
```

## Fastjson Options

The JSON Fastjson dataformat supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |
| **contentTypeHeader** (common) | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |

## Dependencies

To use Fastjson in your camel routes, you need to add the dependency on **camel-fastjson** which implements this data format.

If you use maven, you could add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-fastjson</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using fastjson with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-fastjson-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.fastjson.content-type-header** | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. | true | Boolean |
| **camel.dataformat.fastjson.enabled** | Whether to enable auto configuration of the fastjson data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.fastjson.unmarshal-type** | Class name of the java type to use when unmarshalling. |  | String |