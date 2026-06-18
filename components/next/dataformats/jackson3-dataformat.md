# JSON Jackson 3

**Since Camel 4.19**

Jackson 3 is a Data Format that uses the [Jackson 3 Library](https://github.com/FasterXML/jackson)

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .marshal().jackson()
    .to("mqseries:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <marshal><jackson/></marshal>
  <to uri="mqseries:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - marshal:
            jackson: {}
        - to:
            uri: mqseries:Another.Queue
```

## Jackson 3 Options

The JSON Jackson 3 dataformat supports 22 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **objectMapper** (common) |  | `String` | Lookup and use the existing ObjectMapper with the given id when using Jackson. |
| **useDefaultObjectMapper** (common) | `true` | `Boolean` | Whether to lookup and use default Jackson ObjectMapper from the registry. |
| **autoDiscoverObjectMapper** (common) | `false` | `Boolean` | If set to true then Jackson will look for an objectMapper to use from the registry. |
| **prettyPrint** (common) | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **combineUnicodeSurrogates** (common) | `false` | `Boolean` | Force generator that outputs JSON content to combine surrogate pairs (if any) into 4-byte characters. This should be preferred when using 4-byte characters such as Japanese. |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |
| **jsonView** (advanced) |  | `String` | When marshalling a POJO to JSON you might want to exclude certain fields from the JSON output. With Jackson you can use JSON views to accomplish this. This option is to refer to the class which has JsonView annotations. |
| **include** (advanced) |  | `String` | If you want to marshal a pojo to JSON, and the pojo has some fields with null values. And you want to skip these null values, you can set this option to NON\_NULL. |
| **allowJmsType** (advanced) | `false` | `Boolean` | Used for JMS users to allow the JMSType header from the JMS spec to specify a FQN classname to use to unmarshal to. |
| **collectionType** (advanced) |  | `String` | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows using different collection types than java.util.Collection based as default. |
| **useList** (common) | `false` | `Boolean` | To unmarshal to a List of Map or a List of Pojo. |
| **moduleClassNames** (advanced) |  | `String` | To use custom Jackson modules com.fasterxml.jackson.databind.Module specified as a String with FQN class names. Multiple classes can be separated by comma. |
| **moduleRefs** (advanced) |  | `String` | To use custom Jackson modules referred from the Camel registry. Multiple modules can be separated by comma. |
| **enableFeatures** (advanced) |  | `String` | Set of features to enable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |
| **disableFeatures** (advanced) |  | `String` | Set of features to disable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |
| **allowUnmarshallType** (common) | `false` | `Boolean` | If enabled then Jackson is allowed to attempt to use the CamelJacksonUnmarshalType header during the unmarshalling. This should only be enabled when desired to be used. |
| **timezone** (advanced) |  | `String` | If set then Jackson will use the Timezone when marshalling/unmarshalling. This option will have no effect on the others Json DataFormat, like gson and fastjson. |
| **schemaResolver** (advanced) |  | `Object` | Optional schema resolver used to lookup schemas for the data in transit. |
| **autoDiscoverSchemaResolver** (advanced) | `true` | `Boolean` | When not disabled, the SchemaResolver will be looked up into the registry. |
| **namingStrategy** (common) |  | `String` | If set then Jackson will use the the defined Property Naming Strategy.Possible values are: LOWER\_CAMEL\_CASE, LOWER\_DOT\_CASE, LOWER\_CASE, KEBAB\_CASE, SNAKE\_CASE and UPPER\_CAMEL\_CASE. |
| **contentTypeHeader** (common) | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |
| **maxStringLength** (advanced) |  | `Integer` | Jackson. Sets the maximum string length (in chars or bytes, depending on input context). The default is 20,000,000. This limit is not exact, the limit is applied when we increase internal buffer sizes and an exception will happen at sizes greater than this limit. Some text values that are a little bigger than the limit may be treated as valid but no text values with sizes less than or equal to this limit will be treated as invalid. |

## Usage

### Using Jackson with the json() DSL

Jackson can also be used via the generic `json()` DSL method by specifying `JsonLibrary.Jackson`:

_Java-only: using the json() DSL method with JsonLibrary.Jackson_

```java
from("activemq:My.Queue")
  .marshal().json(JsonLibrary.Jackson)
  .to("mqseries:Another.Queue");
```

This is equivalent to using `.jackson()` directly. The `json()` method also supports additional parameters:

_Java-only: json() DSL with pretty print and unmarshal type_

```java
// Pretty print
from("activemq:My.Queue")
  .marshal().json(JsonLibrary.Jackson, true)
  .to("mqseries:Another.Queue");

// Specify unmarshal type
from("activemq:My.Queue")
  .unmarshal().json(JsonLibrary.Jackson, MyPojo.class)
  .to("mqseries:Another.Queue");
```

### 2 and 4 bytes characters

Jackson 3 by default outputs 4-byte characters (in languages such as Japanese) as surrogate pair, escaped. This is compliant with Json specification. This can however frustrate users, because it garbles regular output, such as names and texts with Unicode escapes. To avoid this, users commonly use 4-bytes would need to turn on `combineUnicodeSurrogates=true` in the Camel dataformat.

### Using custom ObjectMapper

You can configure `JacksonDataFormat` to use a custom `ObjectMapper` in case you need more control of the mapping configuration.

If you set up a single `ObjectMapper` in the registry, then Camel will automatic lookup and use this `ObjectMapper`. For example, if you use Spring Boot, then Spring Boot can provide a default `ObjectMapper` for you if you have Spring MVC enabled. And this would allow Camel to detect that there is one bean of `ObjectMapper` class type in the Spring Boot bean registry and then use it. When this happens you should set a `INFO` logging from Camel.

### Using Jackson 3 for automatic type conversion

The `camel-jackson3` module allows integrating Jackson 3 as a [Type Converter](../../../manual/type-converter.md).

This gives a set of out-of-the-box converters to/from the Jackson type `JsonNode`, such as converting from `JsonNode` to `String` or vice versa.

#### Enabling more type converters and support for POJOs

To enable POJO conversion support for `camel-jackson3` then this must be enabled, which is done by setting the following options on the `CamelContext` global options, as shown:

_Java-only: enabling Jackson 3 POJO type converter via CamelContext options_

```java
// Enable Jackson 3 JSON type converter for more types.
camelContext.getGlobalOptions().put("CamelJacksonEnableTypeConverter", "true");
// Allow Jackson 3 JSON to convert to pojo types also
// (by default, Jackson only converts to String and other simple types)
getContext().getGlobalOptions().put("CamelJacksonTypeConverterToPojo", "true");
```

The `camel-jackson3` type converter integrates with [JAXB](jaxb-dataformat.md) which means you can annotate POJO class with `JAXB` annotations that Jackson can use. You can also use Jackson’s own annotations in your POJO classes.

## Dependencies

To use Jackson 3 in your Camel routes, you need to add the dependency on **camel-jackson3**, which implements this data format.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest & greatest release:

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-jackson3</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Spring Boot Auto-Configuration

When using jackson3 with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jackson3-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.jackson.allow-jms-type** | Used for JMS users to allow the JMSType header from the JMS spec to specify a FQN classname to use to unmarshal to. | false | Boolean |
| **camel.dataformat.jackson.allow-unmarshall-type** | If enabled then Jackson is allowed to attempt to use the CamelJacksonUnmarshalType header during the unmarshalling. This should only be enabled when desired to be used. | false | Boolean |
| **camel.dataformat.jackson.auto-discover-object-mapper** | If set to true then Jackson will look for an objectMapper to use from the registry. | false | Boolean |
| **camel.dataformat.jackson.auto-discover-schema-resolver** | When not disabled, the SchemaResolver will be looked up into the registry. | true | Boolean |
| **camel.dataformat.jackson.collection-type** | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows using different collection types than java.util.Collection based as default. |  | String |
| **camel.dataformat.jackson.combine-unicode-surrogates** | Force generator that outputs JSON content to combine surrogate pairs (if any) into 4-byte characters. This should be preferred when using 4-byte characters such as Japanese. | false | Boolean |
| **camel.dataformat.jackson.content-type-header** | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. | true | Boolean |
| **camel.dataformat.jackson.disable-features** | Set of features to disable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |  | String |
| **camel.dataformat.jackson.enable-features** | Set of features to enable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |  | String |
| **camel.dataformat.jackson.enabled** | Whether to enable auto configuration of the jackson data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.jackson.include** | If you want to marshal a pojo to JSON, and the pojo has some fields with null values. And you want to skip these null values, you can set this option to NON\_NULL. |  | String |
| **camel.dataformat.jackson.json-view** | When marshalling a POJO to JSON you might want to exclude certain fields from the JSON output. With Jackson you can use JSON views to accomplish this. This option is to refer to the class which has JsonView annotations. |  | String |
| **camel.dataformat.jackson.max-string-length** | Jackson. Sets the maximum string length (in chars or bytes, depending on input context). The default is 20,000,000. This limit is not exact, the limit is applied when we increase internal buffer sizes and an exception will happen at sizes greater than this limit. Some text values that are a little bigger than the limit may be treated as valid but no text values with sizes less than or equal to this limit will be treated as invalid. |  | Integer |
| **camel.dataformat.jackson.module-class-names** | To use custom Jackson modules com.fasterxml.jackson.databind.Module specified as a String with FQN class names. Multiple classes can be separated by comma. |  | String |
| **camel.dataformat.jackson.module-refs** | To use custom Jackson modules referred from the Camel registry. Multiple modules can be separated by comma. |  | String |
| **camel.dataformat.jackson.naming-strategy** | If set then Jackson will use the the defined Property Naming Strategy.Possible values are: LOWER\_CAMEL\_CASE, LOWER\_DOT\_CASE, LOWER\_CASE, KEBAB\_CASE, SNAKE\_CASE and UPPER\_CAMEL\_CASE. |  | String |
| **camel.dataformat.jackson.object-mapper** | Lookup and use the existing ObjectMapper with the given id when using Jackson. |  | String |
| **camel.dataformat.jackson.pretty-print** | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| **camel.dataformat.jackson.schema-resolver** | Optional schema resolver used to lookup schemas for the data in transit. The option is a org.apache.camel.component.jackson.SchemaResolver type. |  | String |
| **camel.dataformat.jackson.timezone** | If set then Jackson will use the Timezone when marshalling/unmarshalling. This option will have no effect on the others Json DataFormat, like gson and fastjson. |  | String |
| **camel.dataformat.jackson.unmarshal-type** | Class name of the java type to use when unmarshalling. |  | String |
| **camel.dataformat.jackson.use-default-object-mapper** | Whether to lookup and use default Jackson ObjectMapper from the registry. | true | Boolean |
| **camel.dataformat.jackson.use-list** | To unmarshal to a List of Map or a List of Pojo. | false | Boolean |