# Protobuf Jackson 3

**Since Camel 4.19**

Jackson Protobuf is a Data Format which uses the [Jackson library](https://github.com/FasterXML/jackson/) version 3 with the [Protobuf extension](https://github.com/FasterXML/jackson-dataformats-binary) to unmarshal a Protobuf payload into Java objects or to marshal Java objects into a Protobuf payload.

> **Tip**
> If you are familiar with Jackson, this Protobuf data format behaves in the same way as its JSON counterpart, and thus can be used with classes annotated for JSON serialization/deserialization.

-   Java
    
-   XML
    
-   YAML
    

```java
from("kafka:topic")
    .unmarshal().protobuf(ProtobufLibrary.Jackson, JsonNode.class)
    .to("log:info");
```

```xml
<route>
  <from uri="kafka:topic"/>
  <unmarshal><protobuf library="Jackson"/></unmarshal>
  <to uri="log:info"/>
</route>
```

```yaml
- route:
    from:
      uri: kafka:topic
      steps:
        - unmarshal:
            protobuf:
              library: Jackson
        - to:
            uri: log:info
```

## Protobuf Jackson Options

The Protobuf Jackson 3 dataformat supports 18 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **objectMapper** (advanced) |  | `String` | Lookup and use the existing ObjectMapper with the given id when using Jackson. |
| **useDefaultObjectMapper** (common) | `true` | `Boolean` | Whether to lookup and use default Jackson ObjectMapper from the registry. |
| **autoDiscoverObjectMapper** (common) | `false` | `Boolean` | If set to true then Jackson will lookup for an objectMapper into the registry. |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |
| **jsonView** (common) |  | `String` | When marshalling a POJO to JSON you might want to exclude certain fields from the JSON output. With Jackson you can use JSON views to accomplish this. This option is to refer to the class which has JsonView annotations. |
| **include** (common) |  | `String` | If you want to marshal a pojo to JSON, and the pojo has some fields with null values. And you want to skip these null values, you can set this option to NON\_NULL. |
| **allowJmsType** (advanced) | `false` | `Boolean` | Used for JMS users to allow the JMSType header from the JMS spec to specify a FQN classname to use to unmarshal to. |
| **collectionType** (advanced) |  | `String` | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows using different collection types than java.util.Collection based as default. |
| **useList** (common) | `false` | `Boolean` | To unmarshal to a List of Map or a List of Pojo. |
| **moduleClassNames** (advanced) |  | `String` | To use custom Jackson modules tools.jackson.databind.JacksonModule specified as a String with FQN class names. Multiple classes can be separated by comma. |
| **moduleRefs** (advanced) |  | `String` | To use custom Jackson modules referred from the Camel registry. Multiple modules can be separated by comma. |
| **enableFeatures** (common) |  | `String` | Set of features to enable on the Jackson tools.jackson.databind.ObjectMapper. The features should be a name that matches a enum from tools.jackson.databind.SerializationFeature, tools.jackson.databind.DeserializationFeature, or tools.jackson.databind.MapperFeature Multiple features can be separated by comma. |
| **disableFeatures** (common) |  | `String` | Set of features to disable on the Jackson tools.jackson.databind.ObjectMapper. The features should be a name that matches a enum from tools.jackson.databind.SerializationFeature, tools.jackson.databind.DeserializationFeature, or tools.jackson.databind.MapperFeature Multiple features can be separated by comma. |
| **allowUnmarshallType** (common) | `false` | `Boolean` | If enabled then Jackson is allowed to attempt to use the CamelJacksonUnmarshalType header during the unmarshalling. |
| **timezone** (advanced) |  | `String` | If set then Jackson will use the Timezone when marshalling/unmarshalling. |
| **schemaResolver** (advanced) |  | `String` | Optional schema resolver used to lookup schemas for the data in transit. |
| **autoDiscoverSchemaResolver** (advanced) | `true` | `Boolean` | When not disabled, the SchemaResolver will be looked up into the registry. |
| **contentTypeHeader** (common) | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |

## Usage

### Configuring the `SchemaResolver`

Since Protobuf serialization is schema-based, this data format requires that you provide a SchemaResolver object that is able to look up the schema for each exchange that is going to be marshalled/unmarshalled.

You can add a single SchemaResolver to the registry, and it will be looked up automatically. Or you can explicitly specify the reference to a custom SchemaResolver.

### Using custom ProtobufMapper

You can configure `JacksonProtobufDataFormat` to use a custom `ProtobufMapper` in case you need more control of the mapping configuration.

If you set up a single `ProtobufMapper` in the registry, then Camel will automatic lookup and use this `ProtobufMapper`.

## Dependencies

To use Protobuf Jackson in your Camel routes, you need to add the dependency on **camel-jackson3-protobuf**, which implements this data format.

If you use Maven, you could add the following to your pom.xml, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-jackson3-protobuf</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```