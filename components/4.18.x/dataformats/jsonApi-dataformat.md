# JSonApi

**Since Camel 3.0**

The JSonApi dataformat supports 2 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **dataFormatTypes** (common) |  | `String` | The classes to take into account for the marshalling. Multiple classes can be separated by comma. |
| **mainFormatType** (common) |  | `String` | The class to take into account while unmarshalling. |

## Dependencies

To use JsonAPI in your Camel routes, you need to add the dependency on **camel-jsonapi** which implements this data format.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-jsonapi</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using jsonApi with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jsonapi-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.json-api.data-format-types** | The classes to take into account for the marshalling. Multiple classes can be separated by comma. |  | String |
| **camel.dataformat.json-api.enabled** | Whether to enable auto configuration of the jsonApi data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.json-api.main-format-type** | The class to take into account while unmarshalling. |  | String |