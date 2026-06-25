# Jackson XML 3

**Since Camel 4.19**

Jackson XML is a Data Format that uses the [Jackson library](https://github.com/FasterXML/jackson/) with the [XMLMapper extension](https://github.com/FasterXML/jackson-dataformat-xml) to unmarshal an XML payload into Java objects or to marshal Java objects into an XML payload.

> **Tip**
> If you are familiar with Jackson, this XML data format behaves in the same way as its JSON counterpart, and thus can be used with classes annotated for JSON serialization/deserialization.

This extension also mimics [JAXB’s "Code first" approach](https://github.com/FasterXML/jackson-dataformat-xml/blob/master/README.md).

This data format relies on [Woodstox](https://github.com/FasterXML/Woodstox) (especially for features like pretty printing), a fast and efficient XML processor.

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .unmarshal().jacksonXml()
    .to("mqseries:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <unmarshal>
    <jacksonXml/>
  </unmarshal>
  <to uri="mqseries:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - unmarshal:
            jacksonXml: {}
        - to:
            uri: mqseries:Another.Queue
```

## JacksonXML Options

The Jackson XML 3 dataformat supports 17 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **xmlMapper** (advanced) |  | `String` | Lookup and use the existing XmlMapper with the given id. |
| **prettyPrint** (common) | `false` | `Boolean` | Whether to enable pretty printing output nicely formatted. Is by default false. |
| **unmarshalType** (common) |  | `String` | Class name of the java type to use when unmarshalling. |
| **allowUnmarshallType** (common) | `false` | `Boolean` | Whether to allow Jackson to use the CamelJacksonUnmarshalType header during unmarshalling. Should only be enabled when desired. |
| **jsonView** (common) |  | `String` | When marshalling a POJO to JSON you might want to exclude certain fields from the JSON output. With Jackson you can use JSON views to accomplish this. This option is to refer to the class which has JsonView annotations. |
| **include** (common) |  | `String` | If you want to marshal a POJO to JSON, and the POJO has some fields with null values. And you want to skip these null values, you can set this option to NON\_NULL. |
| **allowJmsType** (advanced) | `false` | `Boolean` | Whether to allow the JMSType header from the JMS spec to specify a FQN classname to use to unmarshal to. |
| **collectionType** (advanced) |  | `String` | Refers to a custom collection type to lookup in the registry to use. This option should rarely be used, but allows using different collection types than java.util.Collection based as default. |
| **useList** (common) | `false` | `Boolean` | Whether to unmarshal to a List of Map or a List of Pojo. |
| **timezone** (advanced) |  | `String` | If set then Jackson will use the Timezone when marshalling/unmarshalling. |
| **enableJaxbAnnotationModule** (advanced) | `false` | `Boolean` | Whether to enable the JAXB annotations module when using Jackson. When enabled then JAXB annotations can be used by Jackson. |
| **moduleClassNames** (advanced) |  | `String` | To use custom Jackson modules tools.jackson.databind.JacksonModule specified as a String with FQN class names. Multiple classes can be separated by comma. |
| **moduleRefs** (advanced) |  | `String` | To use custom Jackson modules referred from the Camel registry. Multiple modules can be separated by comma. |
| **enableFeatures** (common) |  | `String` | Set of features to enable on the Jackson tools.jackson.databind.ObjectMapper. The features should be a name that matches a enum from tools.jackson.databind.SerializationFeature, tools.jackson.databind.DeserializationFeature, or tools.jackson.databind.MapperFeature Multiple features can be separated by comma. |
| **disableFeatures** (common) |  | `String` | Set of features to disable on the Jackson tools.jackson.databind.ObjectMapper. The features should be a name that matches a enum from tools.jackson.databind.SerializationFeature, tools.jackson.databind.DeserializationFeature, or tools.jackson.databind.MapperFeature Multiple features can be separated by comma. |
| **contentTypeHeader** (common) | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |
| **maxStringLength** (advanced) |  | `Integer` | Maximum allowed string length when deserializing (in chars or bytes, depending on input context). The default is 20,000,000. |

## Usage

### Using Jackson XML in Spring DSL

When using Data Format in Spring DSL, you need to declare the data formats first. This is done in the `dataFormats` XML tag:

_XML-only: declaring a named data format in Spring XML_

```xml
        <dataFormats>
            <!-- here we define an XML data format with the id jack and that it should use the TestPojo as the class type when
                 doing unmarshal. The unmarshalType is optional, if not provided Camel will use a Map as the type -->
            <jacksonXml id="jack" unmarshalType="org.apache.camel.component.jackson3xml.TestPojo"/>
        </dataFormats>
```

And then you can refer to this id in the route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:back")
    .unmarshal("jack")
    .to("mock:reverse");
```

```xml
<route>
    <from uri="direct:back"/>
    <unmarshal><custom ref="jack"/></unmarshal>
    <to uri="mock:reverse"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:back
      steps:
        - unmarshal:
            ref: jack
        - to:
            uri: mock:reverse
```

### Excluding POJO fields from marshalling

When marshalling a POJO to XML, you might want to exclude certain fields from the XML output. With Jackson, you can use [JSON views](https://github.com/FasterXML/jackson-annotations/blob/master/src/main/java/tools/jackson/annotation/JsonView.java) to accomplish this. First, create one or more marker classes.

Use the marker classes with the `@JsonView` annotation to include/exclude certain fields. The annotation also works on getters.

Finally, use the Camel `JacksonXMLDataFormat` to marshall the above POJO to XML.

Note that the weight field is missing in the resulting XML:

```xml
<pojo age="30" weight="70"/>
```

### Include/Exclude fields using the `jsonView` attribute with `JacksonXML`DataFormat

As an example of using this attribute, you can instead of:

_Java-only: Java programmatic data format with class literal_

```java
JacksonXMLDataFormat ageViewFormat = new JacksonXMLDataFormat(TestPojoView.class, Views.Age.class);

from("direct:inPojoAgeView")
  .marshal(ageViewFormat);
```

Directly specify your [JSON view](https://github.com/FasterXML/jackson-annotations/blob/master/src/main/java/tools/jackson/annotation/JsonView.java) inside the Java DSL as:

_Java-only: Java DSL with class literal parameters_

```java
from("direct:inPojoAgeView")
  .marshal().jacksonXml(TestPojoView.class, Views.Age.class);
```

And the same in the route DSL:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:inPojoAgeView")
    .marshal().jacksonXml(TestPojoView.class, Views.Age.class);
```

```xml
<route>
    <from uri="direct:inPojoAgeView"/>
    <marshal>
        <jacksonXml unmarshalType="org.apache.camel.component.jackson3xml.TestPojoView"
                    jsonView="org.apache.camel.component.jackson3xml.Views$Age"/>
    </marshal>
</route>
```

```yaml
- route:
    from:
      uri: direct:inPojoAgeView
      steps:
        - marshal:
            jacksonXml:
              unmarshalType: org.apache.camel.component.jackson3xml.TestPojoView
              jsonView: org.apache.camel.component.jackson3xml.Views$Age
```

### Setting serialization include option

If you want to marshal a POJO to XML, and the POJO has some fields with null values. And you want to skip these null values, then you need to set either an annotation on the POJO:

_Java-only: Java annotation_

```java
@JsonInclude(Include.NON_NULL)
public class MyPojo {
   ...
}
```

But this requires you to include that annotation in your POJO source code. You can also configure the Camel JacksonXMLDataFormat to set the `include` option, as shown below:

_Java-only: Java programmatic data format configuration_

```java
JacksonXMLDataFormat format = new JacksonXMLDataFormat();
format.setInclude("NON_NULL");
```

Or from XML DSL you configure this as

_XML-only: configuring include option in Spring XML_

```xml
<dataFormats>
  <jacksonXml id="jacksonxml" include="NON_NULL"/>
</dataFormats>
```

### Unmarshalling from XML to POJO with dynamic class name

If you use Jackson to unmarshal XML to POJO, then you can now specify a header in the message that indicates which class name to unmarshal to. The header has key `CamelJacksonUnmarshalType` if that header is present in the message, then Jackson will use that as FQN for the POJO class to unmarshal the XML payload as.

For JMS end users, there is the `JMSType` header from the JMS spec that indicates that also. To enable support for `JMSType` you would need to turn that on, on the Jackson data format as shown:

_Java-only: Java programmatic data format configuration_

```java
JacksonDataFormat format = new JacksonDataFormat();
format.setAllowJmsType(true);
```

Or from XML DSL you configure this as:

_XML-only: configuring allowJmsType in Spring XML_

```xml
<dataFormats>
  <jacksonXml id="jacksonxml" allowJmsType="true"/>
</dataFormats>
```

### Unmarshalling from XML to `List<Map>` or `List<POJO>`

If you are using Jackson to unmarshal XML to a list of map/POJO, you can now specify this by setting `useList="true"` or use the `org.apache.camel.component.jackson3xml.ListJacksonXMLDataFormat`. For example, with Java, you can do as shown below:

_Java-only: Java programmatic data format configuration_

```java
JacksonXMLDataFormat format = new ListJacksonXMLDataFormat();
// or
JacksonXMLDataFormat format = new JacksonXMLDataFormat();
format.useList();
// and you can specify the POJO class type also
format.setUnmarshalType(MyPojo.class);
```

And if you use XML DSL then you configure to use a list using `useList` attribute as shown below:

_XML-only: configuring useList in Spring XML_

```xml
<dataFormats>
    <jacksonXml id="jack" useList="true"/>
</dataFormats>
```

And you can specify the POJO type also

_XML-only: configuring useList with unmarshalType in Spring XML_

```xml
<dataFormats>
    <jacksonXml id="jack" useList="true" unmarshalType="com.foo.MyPojo"/>
</dataFormats>
```

### Using custom Jackson modules

You can use custom Jackson modules by specifying the class names of those using the moduleClassNames option as shown below.

_XML-only: configuring moduleClassNames in Spring XML_

```xml
<dataFormats>
    <jacksonXml id="jack" useList="true" unmarshalType="com.foo.MyPojo" moduleClassNames="com.foo.MyModule,com.foo.MyOtherModule"/>
</dataFormats>
```

When using `moduleClassNames` then the custom Jackson modules are not configured, by created using default constructor and used as-is. If a custom module needs any custom configuration, then an instance of the module can be created and configured, and then use modulesRefs to refer to the module as shown below:

_XML-only: configuring moduleRefs with bean declaration in Spring XML_

```xml
<bean id="myJacksonModule" class="com.foo.MyModule">
  ... // configure the module as you want
</bean>

<dataFormats>
    <jacksonXml id="jacksonxml" useList="true" unmarshalType="com.foo.MyPojo" moduleRefs="myJacksonModule"/>
</dataFormats>
```

Multiple modules can be specified separated by comma, such as `moduleRefs="myJacksonModule,myOtherModule"`.

### Enabling or disable features using Jackson

Jackson XML has a number of features you can enable or disable, which its XmlMapper uses. For example, to disable failing on unknown properties when marshalling, you can configure this using the disableFeatures:

_XML-only: configuring disableFeatures in Spring XML_

```xml
<dataFormats>
    <jacksonXml id="jacksonxml" unmarshalType="com.foo.MyPojo" disableFeatures="FAIL_ON_UNKNOWN_PROPERTIES"/>
</dataFormats>
```

You can disable multiple features by separating the values using comma. The values for the features must be the name of the enums from Jackson from the following enum classes:

-   `tools.jackson.databind.SerializationFeature`
    
-   `tools.jackson.databind.DeserializationFeature`
    
-   `tools.jackson.databind.MapperFeature`
    
-   `tools.jackson.dataformat.xml.deser.FromXmlParser.Feature`
    

To enable a feature, use the enableFeatures options instead.

From Java code, you can use the type safe methods from camel-jackson module:

_Java-only: Java programmatic data format configuration_

```java
JacksonDataFormat df = new JacksonDataFormat(MyPojo.class);
df.disableFeature(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES);
df.disableFeature(DeserializationFeature.FAIL_ON_NULL_FOR_PRIMITIVES);
```

### Converting Maps to POJO using Jackson

Jackson `XmlMapper` can be used to convert maps to POJO objects. Jackson component comes with the data converter that can be used to convert `java.util.Map` instance to non-String, non-primitive and non-Number objects.

_Java-only: Java collection API (ProducerTemplate)_

```java
Map<String, Object> invoiceData = new HashMap<String, Object>();
invoiceData.put("netValue", 500);
producerTemplate.sendBody("direct:mapToInvoice", invoiceData);
...
// Later in the processor
Invoice invoice = exchange.getIn().getBody(Invoice.class);
```

If there is a single `XmlMapper` instance available in the Camel registry, it will be used by the converter to perform the conversion. Otherwise, the default mapper will be used.

### Formatted XML marshalling (pretty-printing)

Using the `prettyPrint` option one can output a well-formatted XML while marshalling:

_XML-only: configuring prettyPrint in Spring XML_

```xml
<dataFormats>
    <jacksonXml id="jack" prettyPrint="true"/>
</dataFormats>
```

And in Java DSL:

_Java-only: Java DSL shorthand_

```java
from("direct:inPretty").marshal().jacksonXml(true);
```

Please note that there are 5 different overloaded `jacksonXml()` DSL methods which support the `prettyPrint` option in combination with other settings for `unmarshalType`, `jsonView` etc.

## Dependencies

To use Jackson XML in your Camel routes, you need to add the dependency on **camel-jacksonxml** which implements this data format.

If you use Maven, you could add the following to your `pom.xml`, substituting the version number for the latest & greatest release.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-jackson3xml</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```