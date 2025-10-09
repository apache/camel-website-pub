# JSON XStream

**Since Camel 2.0**

XStream is a Data Format which uses the [XStream library](http://xstream.codehaus.org/) to marshal and unmarshal Java objects to and from JSon. However XStream was created primary for working with XML and therefore using JSon with XStream is not as popular as for example Jackson is for JSon.

To use XStream in your camel routes you need to add the a dependency on **camel-xstream** which implements this data format.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-xstream</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Options

The JSON XStream dataformat supports 3 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **prettyPrint** | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **dropRootNode** | `false` | `Boolean` | Whether XStream will drop the root node in the generated JSon. You may want to enable this when using POJOs; as then the written object will include the class name as root node, which is often not intended to be written in the JSON output. |
| **contentTypeHeader** | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |

## Using the Java DSL

```java
// lets turn Object messages into XML then send to MQSeries
from("activemq:My.Queue").
  marshal().json(JsonLibrary.XStream).
  to("mqseries:Another.Queue");
```

## Spring Boot Auto-Configuration

When using xstreamJson with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-xstream-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.xstream-json.content-type-header** | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. | true | Boolean |
| **camel.dataformat.xstream-json.drop-root-node** | Whether XStream will drop the root node in the generated JSon. You may want to enable this when using POJOs; as then the written object will include the class name as root node, which is often not intended to be written in the JSON output. | false | Boolean |
| **camel.dataformat.xstream-json.enabled** | Whether to enable auto configuration of the xstreamJson data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.xstream-json.pretty-print** | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| **camel.dataformat.xstream.aliases** | Alias a Class to a shorter name to be used in XML elements. |  | List |
| **camel.dataformat.xstream.content-type-header** | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. | true | Boolean |
| **camel.dataformat.xstream.converters** | List of class names for using custom XStream converters. The classes must be of type com.thoughtworks.xstream.converters.Converter. |  | List |
| **camel.dataformat.xstream.enabled** | Whether to enable auto configuration of the xstream data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.xstream.encoding** | Sets the encoding to use. |  | String |
| **camel.dataformat.xstream.implicit-collections** | Adds a default implicit collection which is used for any unmapped XML tag. Multiple values can be separated by comma. |  | List |
| **camel.dataformat.xstream.mode** | Mode for dealing with duplicate references The possible values are: NO\_REFERENCES ID\_REFERENCES XPATH\_RELATIVE\_REFERENCES XPATH\_ABSOLUTE\_REFERENCES SINGLE\_NODE\_XPATH\_RELATIVE\_REFERENCES SINGLE\_NODE\_XPATH\_ABSOLUTE\_REFERENCES. |  | String |
| **camel.dataformat.xstream.omit-fields** | Prevents a field from being serialized. To omit a field you must always provide the declaring type and not necessarily the type that is converted. Multiple values can be separated by comma. |  | List |
| **camel.dataformat.xstream.permissions** | Adds permissions that controls which Java packages and classes XStream is allowed to use during unmarshal from xml/json to Java beans. A permission must be configured either here or globally using a JVM system property. The permission can be specified in a syntax where a plus sign is allow, and minus sign is deny. Wildcards is supported by using . as prefix. For example to allow com.foo and all subpackages then specify com.foo.. Multiple permissions can be configured separated by comma, such as com.foo.,-com.foo.bar.MySecretBean. The following default permission is always included: -,java.lang.,java.util. unless its overridden by specifying a JVM system property with they key org.apache.camel.xstream.permissions. |  | String |