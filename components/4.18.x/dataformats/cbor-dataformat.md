# CBOR

**Since Camel 3.0**

CBOR is a Data Format that uses the [Jackson library](https://github.com/FasterXML/jackson/) with the [CBOR extension](https://github.com/FasterXML/jackson-dataformats-binary/tree/master/cbor) to unmarshal a CBOR payload into Java objects or to marshal Java objects into a CBOR payload.

```java
from("activemq:My.Queue")
    .unmarshal().cbor()
    .to("mqseries:Another.Queue");
```

## Usage

### CBOR Options

The CBOR dataformat supports 10 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **objectMapper** (advanced) |  | `String` | Lookup and use the existing CBOR ObjectMapper with the given id when using Jackson. |
| **useDefaultObjectMapper** (common) | `true` | `Boolean` | Whether to lookup and use default Jackson CBOR ObjectMapper from the registry. |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |
| **collectionType** (advanced) |  | `String` | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows to use different collection types than java.util.Collection based as default. |
| **useList** (common) | `false` | `Boolean` | To unmarshal to a List of Map or a List of Pojo. |
| **allowUnmarshallType** (common) | `false` | `Boolean` | If enabled then Jackson CBOR is allowed to attempt to use the CamelCBORUnmarshalType header during the unmarshalling. This should only be enabled when desired to be used. |
| **prettyPrint** (common) | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **allowJmsType** (advanced) | `false` | `Boolean` | Used for JMS users to allow the JMSType header from the JMS spec to specify a FQN classname to use to unmarshal to. |
| **enableFeatures** (common) |  | `String` | Set of features to enable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |
| **disableFeatures** (common) |  | `String` | Set of features to disable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |

#### Using CBOR in Spring DSL

When using Data Format in Spring DSL, you need to declare the data formats first. This is done in the **DataFormats** XML tag.

```xml
<dataFormats>
    <!-- here we define a CBOR data format with the id test, and that it should use the TestPojo as the class type when
    doing unmarshal. -->
    <cbor id="test" unmarshalType="org.apache.camel.component.cbor.TestPojo"/>
</dataFormats>
```

And then you can refer to this id in the route:

```xml
<route>
    <from uri="direct:back"/>
    <unmarshal><custom ref="test"/></unmarshal>
    <to uri="mock:reverse"/>
</route>
```

## Dependencies

```xml
<dependency>
   <groupId>org.apache.camel</groupId>
   <artifactId>camel-cbor</artifactId>
   <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using cbor with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-cbor-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.cbor.allow-jms-type** | Used for JMS users to allow the JMSType header from the JMS spec to specify a FQN classname to use to unmarshal to. | false | Boolean |
| **camel.dataformat.cbor.allow-unmarshall-type** | If enabled then Jackson CBOR is allowed to attempt to use the CamelCBORUnmarshalType header during the unmarshalling. This should only be enabled when desired to be used. | false | Boolean |
| **camel.dataformat.cbor.collection-type** | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows to use different collection types than java.util.Collection based as default. |  | String |
| **camel.dataformat.cbor.disable-features** | Set of features to disable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |  | String |
| **camel.dataformat.cbor.enable-features** | Set of features to enable on the Jackson com.fasterxml.jackson.databind.ObjectMapper. The features should be a name that matches a enum from com.fasterxml.jackson.databind.SerializationFeature, com.fasterxml.jackson.databind.DeserializationFeature, or com.fasterxml.jackson.databind.MapperFeature Multiple features can be separated by comma. |  | String |
| **camel.dataformat.cbor.enabled** | Whether to enable auto configuration of the cbor data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.cbor.object-mapper** | Lookup and use the existing CBOR ObjectMapper with the given id when using Jackson. |  | String |
| **camel.dataformat.cbor.pretty-print** | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| **camel.dataformat.cbor.unmarshal-type** | Class name of the java type to use when unmarshalling. |  | String |
| **camel.dataformat.cbor.use-default-object-mapper** | Whether to lookup and use default Jackson CBOR ObjectMapper from the registry. | true | Boolean |
| **camel.dataformat.cbor.use-list** | To unmarshal to a List of Map or a List of Pojo. | false | Boolean |