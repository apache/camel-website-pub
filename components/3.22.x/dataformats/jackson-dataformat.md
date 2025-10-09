# JSON Jackson

**Since Camel 2.0**

Jackson is a Data Format which uses the [Jackson Library](https://github.com/FasterXML/jackson-core)

```java
from("activemq:My.Queue").
  marshal().json(JsonLibrary.Jackson).
  to("mqseries:Another.Queue");
```

## Jackson Options

The JSON Jackson dataformat supports 20 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **objectMapper** |  | `String` | Lookup and use the existing ObjectMapper with the given id when using Jackson. |
| **useDefaultObjectMapper** | `true` | `Boolean` | Whether to lookup and use default Jackson ObjectMapper from the registry. |
| **autoDiscoverObjectMapper** | `false` | `Boolean` | If set to true then Jackson will look for an objectMapper to use from the registry. |
| **prettyPrint** | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **unmarshalType** |  | `String` | Class name of the java type to use when unmarshalling. |
| **jsonView** |  | `String` | When marshalling a POJO to JSON you might want to exclude certain fields from the JSON output. With Jackson you can use JSON views to accomplish this. This option is to refer to the class which has JsonView annotations. |
| **include** |  | `String` | If you want to marshal a pojo to JSON, and the pojo has some fields with null values. And you want to skip these null values, you can set this option to NON\_NULL. |
| **allowJmsType** | `false` | `Boolean` | Used for JMS users to allow the JMSType header from the JMS spec to specify a FQN classname to use to unmarshal to. |
| **collectionType** |  | `String` | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows using different collection types than java.util.Collection based as default. |
| **useList** | `false` | `Boolean` | To unmarshal to a List of Map or a List of Pojo. |
| **moduleClassNames** |  | `String` | To use custom Jackson modules com.fasterxml.jackson.databind.Module specified as a String with FQN class names. Multiple classes can be separated by comma. |
| **moduleRefs** |  | `String` | To use custom Jackson modules referred from the Camel registry. Multiple modules can be separated by comma. |
| **enableFeatures** |  | `String` | Set of features to enable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |
| **disableFeatures** |  | `String` | Set of features to disable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |
| **allowUnmarshallType** | `false` | `Boolean` | If enabled then Jackson is allowed to attempt to use the CamelJacksonUnmarshalType header during the unmarshalling. This should only be enabled when desired to be used. |
| **timezone** |  | `String` | If set then Jackson will use the Timezone when marshalling/unmarshalling. This option will have no effect on the others Json DataFormat, like gson, fastjson and xstream. |
| **schemaResolver** |  | `String` | Optional schema resolver used to lookup schemas for the data in transit. |
| **autoDiscoverSchemaResolver** | `true` | `Boolean` | When not disabled, the SchemaResolver will be looked up into the registry. |
| **namingStrategy** |  | `String` | If set then Jackson will use the the defined Property Naming Strategy.Possible values are: LOWER\_CAMEL\_CASE, LOWER\_DOT\_CASE, LOWER\_CASE, KEBAB\_CASE, SNAKE\_CASE and UPPER\_CAMEL\_CASE. |
| **contentTypeHeader** | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |

## Using custom ObjectMapper

You can configure `JacksonDataFormat` to use a custom `ObjectMapper` in case you need more control of the mapping configuration.

If you setup a single `ObjectMapper` in the registry, then Camel will automatic lookup and use this `ObjectMapper`. For example if you use Spring Boot, then Spring Boot can provide a default `ObjectMapper` for you if you have Spring MVC enabled. And this would allow Camel to detect that there is one bean of `ObjectMapper` class type in the Spring Boot bean registry and then use it. When this happens you should set a `INFO` logging from Camel.

## Using Jackson for automatic type conversion

The `camel-jackson` module allows integrating Jackson as a [Type Converter](../../../manual/type-converter.md).

This gives a set of out of the box converters to/from the Jackson type `JSonNode`, such as converting from `JSonNode` to `String` or vice-versa.

### Enabling more type converters and support for POJOs

To enable POJO conversion support for `camel-jackson` then this must be enabled, which is done by setting the following options on the `CamelContext` global options, as shown:

```java
// Enable Jackson JSON type converter for more types.
camelContext.getGlobalOptions().put("CamelJacksonEnableTypeConverter", "true");
// Allow Jackson JSON to convert to pojo types also
// (by default Jackson only converts to String and other simple types)
getContext().getGlobalOptions().put("CamelJacksonTypeConverterToPojo", "true");
```

The `camel-jackson` type converter integrates with [JAXB](jaxb-dataformat.md) which means you can annotate POJO class with `JAXB` annotations that Jackson can use. You can also use Jacksons own annotations on your POJO classes.

## Dependencies

To use Jackson in your camel routes you need to add the dependency on **camel-jackson** which implements this data format.

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-jackson</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using jackson with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jackson-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 21 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.jackson.allow-jms-type** | Used for JMS users to allow the JMSType header from the JMS spec to specify a FQN classname to use to unmarshal to. | false | Boolean |
| **camel.dataformat.jackson.allow-unmarshall-type** | If enabled then Jackson is allowed to attempt to use the CamelJacksonUnmarshalType header during the unmarshalling. This should only be enabled when desired to be used. | false | Boolean |
| **camel.dataformat.jackson.auto-discover-object-mapper** | If set to true then Jackson will look for an objectMapper to use from the registry. | false | Boolean |
| **camel.dataformat.jackson.auto-discover-schema-resolver** | When not disabled, the SchemaResolver will be looked up into the registry. | true | Boolean |
| **camel.dataformat.jackson.collection-type** | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows using different collection types than java.util.Collection based as default. |  | String |
| **camel.dataformat.jackson.content-type-header** | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. | true | Boolean |
| **camel.dataformat.jackson.disable-features** | Set of features to disable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |  | String |
| **camel.dataformat.jackson.enable-features** | Set of features to enable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |  | String |
| **camel.dataformat.jackson.enabled** | Whether to enable auto configuration of the jackson data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.jackson.include** | If you want to marshal a pojo to JSON, and the pojo has some fields with null values. And you want to skip these null values, you can set this option to NON\_NULL. |  | String |
| **camel.dataformat.jackson.json-view** | When marshalling a POJO to JSON you might want to exclude certain fields from the JSON output. With Jackson you can use JSON views to accomplish this. This option is to refer to the class which has JsonView annotations. |  | String |
| **camel.dataformat.jackson.module-class-names** | To use custom Jackson modules com.fasterxml.jackson.databind.Module specified as a String with FQN class names. Multiple classes can be separated by comma. |  | String |
| **camel.dataformat.jackson.module-refs** | To use custom Jackson modules referred from the Camel registry. Multiple modules can be separated by comma. |  | String |
| **camel.dataformat.jackson.naming-strategy** | If set then Jackson will use the the defined Property Naming Strategy.Possible values are: LOWER\_CAMEL\_CASE, LOWER\_DOT\_CASE, LOWER\_CASE, KEBAB\_CASE, SNAKE\_CASE and UPPER\_CAMEL\_CASE. |  | String |
| **camel.dataformat.jackson.object-mapper** | Lookup and use the existing ObjectMapper with the given id when using Jackson. |  | String |
| **camel.dataformat.jackson.pretty-print** | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| **camel.dataformat.jackson.schema-resolver** | Optional schema resolver used to lookup schemas for the data in transit. |  | String |
| **camel.dataformat.jackson.timezone** | If set then Jackson will use the Timezone when marshalling/unmarshalling. This option will have no effect on the others Json DataFormat, like gson, fastjson and xstream. |  | String |
| **camel.dataformat.jackson.unmarshal-type** | Class name of the java type to use when unmarshalling. |  | String |
| **camel.dataformat.jackson.use-default-object-mapper** | Whether to lookup and use default Jackson ObjectMapper from the registry. | true | Boolean |
| **camel.dataformat.jackson.use-list** | To unmarshal to a List of Map or a List of Pojo. | false | Boolean |