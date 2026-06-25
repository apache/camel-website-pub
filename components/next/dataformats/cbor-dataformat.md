# CBOR

**Since Camel 3.0**

CBOR is a Data Format that uses the [Jackson library](https://github.com/FasterXML/jackson/) with the [CBOR extension](https://github.com/FasterXML/jackson-dataformats-binary/tree/master/cbor) to unmarshal a CBOR payload into Java objects or to marshal Java objects into a CBOR payload.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .unmarshal().cbor()
    .to("mqseries:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <unmarshal><cbor/></unmarshal>
  <to uri="mqseries:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - unmarshal:
            cbor: {}
        - to:
            uri: mqseries:Another.Queue
```

## Usage

### CBOR Options

The CBOR dataformat supports 10 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **objectMapper** (advanced) |  | `String` | Lookup and use the existing CBOR ObjectMapper with the given id when using Jackson. |
| **useDefaultObjectMapper** (common) | `true` | `Boolean` | Whether to lookup and use default Jackson CBOR ObjectMapper from the registry. |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |
| **collectionType** (advanced) |  | `String` | Refers to a custom collection type to lookup in the registry to use. |
| **useList** (common) | `false` | `Boolean` | To unmarshal to a List of Map or a List of Pojo. |
| **allowUnmarshallType** (common) | `false` | `Boolean` | If enabled then Jackson CBOR is allowed to attempt to use the CamelCBORUnmarshalType header during the unmarshalling. |
| **prettyPrint** (common) | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **allowJmsType** (advanced) | `false` | `Boolean` | Used for JMS users to allow the JMSType header from the JMS spec to specify a FQN classname to use to unmarshal to. |
| **enableFeatures** (advanced) |  | `String` | Set of features to enable on the Jackson ObjectMapper. Multiple features can be separated by comma. |
| **disableFeatures** (advanced) |  | `String` | Set of features to disable on the Jackson ObjectMapper. Multiple features can be separated by comma. |

#### Using CBOR in Spring DSL

When using Data Format in Spring DSL, you need to declare the data formats first. This is done in the **DataFormats** XML tag.

_XML-only: Spring XML data format configuration_

```xml
<dataFormats>
    <!-- here we define a CBOR data format with the id test, and that it should use the TestPojo as the class type when
    doing unmarshal. -->
    <cbor id="test" unmarshalType="org.apache.camel.component.cbor.TestPojo"/>
</dataFormats>
```

And then you can refer to this id in the route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:back")
    .unmarshal("test")
    .to("mock:reverse");
```

```xml
<route>
    <from uri="direct:back"/>
    <unmarshal><custom ref="test"/></unmarshal>
    <to uri="mock:reverse"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:back
      steps:
        - unmarshal:
            ref: test
        - to:
            uri: mock:reverse
```

## Dependencies

```xml
<dependency>
   <groupId>org.apache.camel</groupId>
   <artifactId>camel-cbor</artifactId>
   <version>x.x.x</version>
</dependency>
```