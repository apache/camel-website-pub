# JAXB

**Since Camel 1.0**

JAXB is a Data Format which uses the JAXB XML marshalling standard to unmarshal an XML payload into Java objects or to marshal Java objects into an XML payload.

## Options

The JAXB dataformat supports 20 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **contextPath** |  | `String` | **Required** Package name where your JAXB classes are located. |
| **contextPathIsClassName** | `false` | `Boolean` | This can be set to true to mark that the contextPath is referring to a classname and not a package name. |
| **schema** |  | `String` | To validate against an existing schema. Your can use the prefix classpath:, file: or http: to specify how the resource should be resolved. You can separate multiple schema files by using the ',' character. |
| **schemaSeverityLevel** | `0` | `Enum` | 
Sets the schema severity level to use when validating against a schema. This level determines the minimum severity error that triggers JAXB to stop continue parsing. The default value of 0 (warning) means that any error (warning, error or fatal error) will trigger JAXB to stop. There are the following three levels: 0=warning, 1=error, 2=fatal error.

Enum values:

-   0
    
-   1
    
-   2
    





 |
| **prettyPrint** | `false` | `Boolean` | To enable pretty printing output nicely formatted. Is by default false. |
| **objectFactory** | `false` | `Boolean` | Whether to allow using ObjectFactory classes to create the POJO classes during marshalling. This only applies to POJO classes that has not been annotated with JAXB and providing jaxb.index descriptor files. |
| **ignoreJAXBElement** | `false` | `Boolean` | Whether to ignore JAXBElement elements - only needed to be set to false in very special use-cases. |
| **mustBeJAXBElement** | `false` | `Boolean` | Whether marhsalling must be java objects with JAXB annotations. And if not then it fails. This option can be set to false to relax that, such as when the data is already in XML format. |
| **filterNonXmlChars** | `false` | `Boolean` | To ignore non xml characheters and replace them with an empty space. |
| **encoding** |  | `String` | To overrule and use a specific encoding. |
| **fragment** | `false` | `Boolean` | To turn on marshalling XML fragment trees. By default JAXB looks for XmlRootElement annotation on given class to operate on whole XML tree. This is useful but not always - sometimes generated code does not have XmlRootElement annotation, sometimes you need unmarshall only part of tree. In that case you can use partial unmarshalling. To enable this behaviours you need set property partClass. Camel will pass this class to JAXB’s unmarshaler. |
| **partClass** |  | `String` | Name of class used for fragment parsing. See more details at the fragment option. |
| **partNamespace** |  | `String` | XML namespace to use for fragment parsing. See more details at the fragment option. |
| **namespacePrefixRef** |  | `String` | When marshalling using JAXB or SOAP then the JAXB implementation will automatic assign namespace prefixes, such as ns2, ns3, ns4 etc. To control this mapping, Camel allows you to refer to a map which contains the desired mapping. |
| **xmlStreamWriterWrapper** |  | `String` | To use a custom xml stream writer. |
| **schemaLocation** |  | `String` | To define the location of the schema. |
| **noNamespaceSchemaLocation** |  | `String` | To define the location of the namespaceless schema. |
| **jaxbProviderProperties** |  | `String` | Refers to a custom java.util.Map to lookup in the registry containing custom JAXB provider properties to be used with the JAXB marshaller. |
| **contentTypeHeader** | `true` | `Boolean` | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. |
| **accessExternalSchemaProtocols** | `false` | `String` | Only in use if schema validation has been enabled. Restrict access to the protocols specified for external reference set by the schemaLocation attribute, Import and Include element. Examples of protocols are file, http, jar:file. false or none to deny all access to external references; a specific protocol, such as file, to give permission to only the protocol; the keyword all to grant permission to all protocols. |

## Using the Java DSL

The following example uses a named DataFormat of `jaxb` which is configured with a Java package name to initialize the [JAXBContext](https://jakarta.ee/specifications/xml-binding/2.3/apidocs/javax/xml/bind/jaxbcontext).

```java
DataFormat jaxb = new JaxbDataFormat("com.acme.model");

from("activemq:My.Queue").
  unmarshal(jaxb).
  to("mqseries:Another.Queue");
```

You can if you prefer use a named reference to a data format which can then be defined in your Registry such as via your Spring XML file. e.g.

```java
from("activemq:My.Queue").
  unmarshal("myJaxbDataType").
  to("mqseries:Another.Queue");
```

## Using Spring XML

The following example shows how to configure the `JaxbDataFormat` and use it in multiple routes.

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
    http://camel.apache.org/schema/spring http://camel.apache.org/schema/spring/camel-spring.xsd">

  <bean id="myJaxb" class="org.apache.camel.converter.jaxb.JaxbDataFormat">
    <property name="contextPath" value="org.apache.camel.example"/>
  </bean>

  <camelContext xmlns="http://camel.apache.org/schema/spring">
    <route>
      <from uri="direct:start"/>
      <marshal><custom ref="myJaxb"/></marshal>
      <to uri="direct:marshalled"/>
    </route>
    <route>
      <from uri="direct:marshalled"/>
      <unmarshal><custom ref="myJaxb"/></unmarshal>
      <to uri="mock:result"/>
    </route>
  </camelContext>

</beans>
```

## Multiple context paths

It is possible to use this data format with more than one context path. You can specify multiple context paths using `:` as a separator, for example `com.mycompany:com.mycompany2`.

## Partial marshalling / unmarshalling

JAXB 2 supports marshalling and unmarshalling XML tree fragments. By default JAXB looks for the `@XmlRootElement` annotation on a given class to operate on whole XML tree. This is useful, but not always. Sometimes the generated code does not have the `@XmlRootElement` annotation and sometimes you need to unmarshall only part of the tree.

In that case you can use partial unmarshalling. To enable this behaviour you need set property `partClass` on the `JaxbDataFormat`. Camel will pass this class to the JAXB unmarshaller. If `JaxbConstants.JAXB_PART_CLASS` is set as one of the exchange headers, its value is used to override the `partClass` property on the `JaxbDataFormat`.

For marshalling you have to add the `partNamespace` attribute with the `QName` of the destination namespace.

If `JaxbConstants.JAXB_PART_NAMESPACE` is set as one of the exchange headers, its value is used to override the `partNamespace` property on the `JaxbDataFormat`.

While setting `partNamespace` through `JaxbConstants.JAXB_PART_NAMESPACE`, please note that you need to specify its value in the format `{namespaceUri}localPart`, as per the example below.

```java
.setHeader(JaxbConstants.JAXB_PART_NAMESPACE, constant("{http://www.camel.apache.org/jaxb/example/address/1}address"));
```

## Fragment

`JaxbDataFormat` has a property named `fragment` which can set the `Marshaller.JAXB_FRAGMENT` property on the JAXB Marshaller. If you don’t want the JAXB Marshaller to generate the XML declaration, you can set this option to be `true`. The default value of this property is `false`.

## Ignoring Non-XML Characters

`JaxbDataFormat` supports ignoring [Non-XML Characters](https://www.w3.org/TR/xml/#NT-Char), you just need to set the `filterNonXmlChars` property to `true`. The `JaxbDataFormat` will replace any non-XML character with a space character (`" "`) during message marshalling or unmarshalling. You can also set the Exchange property `Exchange.FILTER_NON_XML_CHARS`.

  
|  | JDK 1.5 | JDK 1.6+ |
| --- | --- | --- |
| Filtering in use | StAX API and implementation | No |
| Filtering not in use | StAX API only | No |

This feature has been tested with Woodstox 3.2.9 and Sun JDK 1.6 StAX implementation.

`JaxbDataFormat` now allows you to customize the `XMLStreamWriter` used to marshal the stream to XML. Using this configuration, you can add your own stream writer to completely remove, escape, or replace non-XML characters.

```java
JaxbDataFormat customWriterFormat = new JaxbDataFormat("org.apache.camel.foo.bar");
customWriterFormat.setXmlStreamWriterWrapper(new TestXmlStreamWriter());
```

The following example shows using the Spring DSL and also enabling Camel’s non-XML filtering:

```xml
<bean id="testXmlStreamWriterWrapper" class="org.apache.camel.jaxb.TestXmlStreamWriter"/>
<jaxb filterNonXmlChars="true" contextPath="org.apache.camel.foo.bar" xmlStreamWriterWrapper="#testXmlStreamWriterWrapper" />
```

## Working with the `ObjectFactory`

If you use XJC to create the java class from the schema, you will get an `ObjectFactory` for your JAXB context. Since the `ObjectFactory` uses [JAXBElement](https://jakarta.ee/specifications/xml-binding/2.3/apidocs/javax/xml/bind/jaxbelement) to hold the reference of the schema and element instance value, `JaxbDataformat` will ignore the `JAXBElement` by default and you will get the element instance value instead of the `JAXBElement` object from the unmarshaled message body.

If you want to get the `JAXBElement` object form the unmarshaled message body, you need to set the `JaxbDataFormat` `ignoreJAXBElement` property to be `false`.

## Setting the encoding

You can set the `encoding` option on the `JaxbDataFormat` to configure the `Marshaller.JAXB_ENCODING` encoding property on the JAXB Marshaller.

You can setup which encoding to use when you declare the `JaxbDataFormat`. You can also provide the encoding in the Exchange property `Exchange.CHARSET_NAME`. This property will override the encoding set on the `JaxbDataFormat`.

## Controlling namespace prefix mapping

When marshalling using [JAXB](#) or [SOAP](#) then the JAXB implementation will automatically assign namespace prefixes, such as `ns2`, `ns3`, `ns4` etc. To control this mapping, Camel allows you to refer to a map which contains the desired mapping.

For example, in Spring XML we can define a `Map` with the mapping. In the mapping file below, we map SOAP to use soap as as a prefix. While our custom namespace `[http://www.mycompany.com/foo/2](http://www.mycompany.com/foo/2)` is not using any prefix.

```xml
 <util:map id="myMap">
    <entry key="http://www.w3.org/2003/05/soap-envelope" value="soap"/>
    <!-- we don't want any prefix for our namespace -->
    <entry key="http://www.mycompany.com/foo/2" value=""/>
 </util:map>
```

To use this in JAXB or SOAP data formats you refer to this map, using the `namespacePrefixRef` attribute as shown below. Then Camel will lookup in the Registry a `java.util.Map` with the id `myMap`, which was what we defined above.

```xml
 <marshal>
    <soap version="1.2" contextPath="com.mycompany.foo" namespacePrefixRef="myMap"/>
 </marshal>
```

## Schema validation

The `JaxbDataFormat` supports validation by marshalling and unmarshalling from / to XML. You can use the prefix `classpath:`, `file:` or `http:` to specify how the resource should be resolved. You can separate multiple schema files by using the `,` character.

> **Note**
> if the XSD schema files import/access other files, then you need to enable file protocol (or others to allow access)

Using the Java DSL, you can configure it in the following way:

```java
JaxbDataFormat jaxbDataFormat = new JaxbDataFormat();
jaxbDataFormat.setContextPath(Person.class.getPackage().getName());
jaxbDataFormat.setSchema("classpath:person.xsd,classpath:address.xsd");
jaxbDataFormat.setAccessExternalSchemaProtocols("file");
```

You can do the same using the XML DSL:

```xml
<marshal>
    <jaxb id="jaxb" schema="classpath:person.xsd,classpath:address.xsd"
          accessExternalSchemaProtocols="file"/>
</marshal>
```

## Schema Location

The `JaxbDataFormat` supports to specify the `SchemaLocation` when marshalling the XML.

Using the Java DSL, you can configure it in the following way:

```java
JaxbDataFormat jaxbDataFormat = new JaxbDataFormat();
jaxbDataFormat.setContextPath(Person.class.getPackage().getName());
jaxbDataFormat.setSchemaLocation("schema/person.xsd");
```

You can do the same using the XML DSL:

```xml
<marshal>
    <jaxb id="jaxb" schemaLocation="schema/person.xsd"/>
</marshal>
```

## Marshal data that is already XML

The JAXB marshaller requires that the message body is JAXB compatible, e.g it is a `JAXBElement`, a java instance that has JAXB annotations, or extends `JAXBElement`. There can be situations where the message body is already in XML, e.g from a `String` type.

`JaxbDataFormat` has an option named `mustBeJAXBElement` which you can set to `false` to relax this check and have the JAXB marshaller only attempt marshalling on `JAXBElement` (`javax.xml.bind.JAXBIntrospector#isElement` returns `true`). In those situations the marshaller will fallback to marshal the message body as-is.

## Dependencies

To use JAXB in your camel routes you need to add dependency on **camel-jaxb** which implements this data format.

If you use maven you could just add the following to your pom.xml, substituting the version number for the latest & greatest release (see the download page for the latest versions).

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-jaxb</artifactId>
  <version>x.x.x</version>
</dependency>
```

## Spring Boot Auto-Configuration

When using jaxb with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jaxb-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 21 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.dataformat.jaxb.access-external-schema-protocols** | Only in use if schema validation has been enabled. Restrict access to the protocols specified for external reference set by the schemaLocation attribute, Import and Include element. Examples of protocols are file, http, jar:file. false or none to deny all access to external references; a specific protocol, such as file, to give permission to only the protocol; the keyword all to grant permission to all protocols. | false | String |
| **camel.dataformat.jaxb.content-type-header** | Whether the data format should set the Content-Type header with the type from the data format. For example application/xml for data formats marshalling to XML, or application/json for data formats marshalling to JSON. | true | Boolean |
| **camel.dataformat.jaxb.context-path** | Package name where your JAXB classes are located. |  | String |
| **camel.dataformat.jaxb.context-path-is-class-name** | This can be set to true to mark that the contextPath is referring to a classname and not a package name. | false | Boolean |
| **camel.dataformat.jaxb.enabled** | Whether to enable auto configuration of the jaxb data format. This is enabled by default. |  | Boolean |
| **camel.dataformat.jaxb.encoding** | To overrule and use a specific encoding. |  | String |
| **camel.dataformat.jaxb.filter-non-xml-chars** | To ignore non xml characheters and replace them with an empty space. | false | Boolean |
| **camel.dataformat.jaxb.fragment** | To turn on marshalling XML fragment trees. By default JAXB looks for XmlRootElement annotation on given class to operate on whole XML tree. This is useful but not always - sometimes generated code does not have XmlRootElement annotation, sometimes you need unmarshall only part of tree. In that case you can use partial unmarshalling. To enable this behaviours you need set property partClass. Camel will pass this class to JAXB’s unmarshaler. | false | Boolean |
| **camel.dataformat.jaxb.ignore-j-a-x-b-element** | Whether to ignore JAXBElement elements - only needed to be set to false in very special use-cases. | false | Boolean |
| **camel.dataformat.jaxb.jaxb-provider-properties** | Refers to a custom java.util.Map to lookup in the registry containing custom JAXB provider properties to be used with the JAXB marshaller. |  | String |
| **camel.dataformat.jaxb.must-be-j-a-x-b-element** | Whether marhsalling must be java objects with JAXB annotations. And if not then it fails. This option can be set to false to relax that, such as when the data is already in XML format. | false | Boolean |
| **camel.dataformat.jaxb.namespace-prefix-ref** | When marshalling using JAXB or SOAP then the JAXB implementation will automatic assign namespace prefixes, such as ns2, ns3, ns4 etc. To control this mapping, Camel allows you to refer to a map which contains the desired mapping. |  | String |
| **camel.dataformat.jaxb.no-namespace-schema-location** | To define the location of the namespaceless schema. |  | String |
| **camel.dataformat.jaxb.object-factory** | Whether to allow using ObjectFactory classes to create the POJO classes during marshalling. This only applies to POJO classes that has not been annotated with JAXB and providing jaxb.index descriptor files. | false | Boolean |
| **camel.dataformat.jaxb.part-class** | Name of class used for fragment parsing. See more details at the fragment option. |  | String |
| **camel.dataformat.jaxb.part-namespace** | XML namespace to use for fragment parsing. See more details at the fragment option. |  | String |
| **camel.dataformat.jaxb.pretty-print** | To enable pretty printing output nicely formatted. Is by default false. | false | Boolean |
| **camel.dataformat.jaxb.schema** | To validate against an existing schema. Your can use the prefix classpath:, file: or http: to specify how the resource should be resolved. You can separate multiple schema files by using the ',' character. |  | String |
| **camel.dataformat.jaxb.schema-location** | To define the location of the schema. |  | String |
| **camel.dataformat.jaxb.schema-severity-level** | Sets the schema severity level to use when validating against a schema. This level determines the minimum severity error that triggers JAXB to stop continue parsing. The default value of 0 (warning) means that any error (warning, error or fatal error) will trigger JAXB to stop. There are the following three levels: 0=warning, 1=error, 2=fatal error. | 0 | Integer |
| **camel.dataformat.jaxb.xml-stream-writer-wrapper** | To use a custom xml stream writer. |  | String |