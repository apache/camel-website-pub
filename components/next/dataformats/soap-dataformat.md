# SOAP

**Since Camel 2.3**

SOAP is a Data Format which uses JAXB2 and JAX-WS annotations to marshal and unmarshal SOAP payloads. It provides the basic features of Apache CXF without the need for the CXF Stack.

**Namespace prefix mapping**

See [JAXB](jaxb-dataformat.md) for details how you can control namespace prefix mappings when marshalling using SOAP data format.

## SOAP Options

The SOAP dataformat supports 7 options, which are listed below.

   
| Name | Default | Java Type | Description |
| --- | --- | --- | --- |
| **contextPath** (common) |  | `String` | **Required** Package name where your JAXB classes are located. |
| **encoding** (common) |  | `String` | To overrule and use a specific encoding. |
| **elementNameStrategy** (advanced) |  | `Object` | Refers to an element strategy to lookup from the registry. An element name strategy is used for two purposes. The first is to find a xml element name for a given object and soap action when marshaling the object into a SOAP message. The second is to find an Exception class for a given soap fault name. The following three element strategy class name is provided out of the box. QNameStrategy - Uses a fixed qName that is configured on instantiation. Exception lookup is not supported TypeNameStrategy - Uses the name and namespace from the XMLType annotation of the given type. If no namespace is set then package-info is used. Exception lookup is not supported ServiceInterfaceStrategy - Uses information from a webservice interface to determine the type name and to find the exception class for a SOAP fault All three classes is located in the package name org.apache.camel.dataformat.soap.name If you have generated the web service stub code with cxf-codegen or a similar tool then you probably will want to use the ServiceInterfaceStrategy. In the case you have no annotated service interface you should use QNameStrategy or TypeNameStrategy. |
| **version** (common) | `1.1` | `Enum` | 
SOAP version should either be 1.1 or 1.2. Is by default 1.1.

Enum values:

-   1.1
    
-   1.2
    





 |
| **namespacePrefix** (advanced) |  | `Object` | When marshalling using JAXB or SOAP then the JAXB implementation will automatic assign namespace prefixes, such as ns2, ns3, ns4 etc. To control this mapping, Camel allows you to refer to a map which contains the desired mapping. |
| **schema** (common) |  | `String` | To validate against an existing schema. Your can use the prefix classpath:, file: or http: to specify how the resource should be resolved. You can separate multiple schema files by using the ',' character. |
| **ignoreUnmarshalledHeaders** (advanced) | `false` | `Boolean` | Whether to ignore headers that was not unmarshalled. By default, headers which could not be unmarshalled is recorded in the org.apache.camel.dataformat.soap.UNMARSHALLED\_HEADER\_LIST header which allows to inspect any problematic header. |

## ElementNameStrategy

An element name strategy is used for two purposes. The first is to find an XML element name for a given object and soap action when marshaling the object into a SOAP message. The second is to find an Exception class for a given soap fault name.

 
| Strategy | Usage |
| --- | --- |
| `QNameStrategy` | Uses a fixed qName that is configured on instantiation. Exception lookup is not supported |
| `TypeNameStrategy` | Uses the name and namespace from the `@XMLType` annotation of the given type. If no namespace is set, then package-info is used. Exception lookup is not supported |
| `ServiceInterfaceStrategy` | Uses information from a webservice interface to determine the type name and to find the exception class for a SOAP fault |

If you have generated the web service stub code with cxf-codegen or a similar tool, then you probably will want to use the `ServiceInterfaceStrategy`. In the case you have no annotated service interface you should use `QNameStrategy` or `TypeNameStrategy`.

## Using the Java DSL

The following example uses a named `DataFormat` of _soap_ which is configured with the package `com.example.customerservice` to initialize the [JAXBContext](http://java.sun.com/javase/6/docs/api/javax/xml/bind/JAXBContext.md). The second parameter is the `ElementNameStrategy`. The route is able to marshal normal objects as well as exceptions.

> **Note**
> The below just sends a SOAP Envelope to a queue. A web service provider would actually need to be listening to the queue for a SOAP call to actually occur, in which case it would be a one way SOAP request. If you need to request a reply, then you should look at the next example.

_Java-only: Java programmatic data format instantiation_

```java
SoapDataFormat soap = new SoapDataFormat("com.example.customerservice", new ServiceInterfaceStrategy(CustomerService.class));
from("direct:start")
  .marshal(soap)
  .to("jms:myQueue");
```

> **Tip**
> **See also**
>
> As the SOAP dataformat inherits from the [JAXB](jaxb-dataformat.md) dataformat, most settings apply here as well

### Using SOAP 1.2

**Since Camel 2.11**

_Java-only: Java programmatic data format configuration_

```java
SoapDataFormat soap = new SoapDataFormat("com.example.customerservice", new ServiceInterfaceStrategy(CustomerService.class));
soap.setVersion("1.2");
from("direct:start")
  .marshal(soap)
  .to("jms:myQueue");
```

When using XML DSL, there is a version attribute you can set on the <soap> element.

_XML-only: Spring bean definition for ServiceInterfaceStrategy_

```xml
    <!-- Defining a ServiceInterfaceStrategy for retrieving the element name when marshalling -->
    <bean id="myNameStrategy" class="org.apache.camel.dataformat.soap.name.ServiceInterfaceStrategy">
        <constructor-arg value="com.example.customerservice.CustomerService"/>
    <constructor-arg value="true"/>
    </bean>
```

And in the Camel route

-   Java
    
-   XML
    
-   YAML
    

```java
SoapDataFormat soap = new SoapDataFormat("com.example.customerservice", new ServiceInterfaceStrategy(CustomerService.class));
soap.setVersion("1.2");
from("direct:start")
    .marshal(soap)
    .to("jms:myQueue");
```

```xml
<route>
  <from uri="direct:start"/>
  <marshal>
    <soap contentPath="com.example.customerservice" version="1.2" elementNameStrategyRef="myNameStrategy"/>
  </marshal>
  <to uri="jms:myQueue"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - marshal:
            soap:
              contextPath: com.example.customerservice
              version: "1.2"
              elementNameStrategyRef: myNameStrategy
        - to:
            uri: jms:myQueue
```

## Multi-part Messages

**Since Camel 2.8.1**

Multipart SOAP messages are supported by the `ServiceInterfaceStrategy`. The `ServiceInterfaceStrategy` must be initialized with a service interface definition that is annotated in accordance with JAX-WS 2.2 and meets the requirements of the Document Bare style. The target method must meet the following criteria, as per the JAX-WS specification: 1. it must have at most one `in` or `in/out` non-header parameter, 2. if it has a return type other than `void` it must have no `in/out` or `out` non-header parameters, 3. if it has a return type of `void` it must have at most one `in/out` or `out` non-header parameter.

The `ServiceInterfaceStrategy` should be initialized with a boolean parameter that indicates whether the mapping strategy applies to the request parameters or response parameters.

_Java-only: Java class instantiation_

```java
ServiceInterfaceStrategy strat =  new ServiceInterfaceStrategy(com.example.customerservice.multipart.MultiPartCustomerService.class, true);
SoapDataFormat soapDataFormat = new SoapDataFormat("com.example.customerservice.multipart", strat);
```

### Holder Object mapping

JAX-WS specifies the use of a type-parameterized `javax.xml.ws.Holder` object for `In/Out` and `Out` parameters. You may use an instance of the parameterized-type directly. The camel-soap DataFormat marshals Holder values in accordance with the JAXB mapping for the class of the `Holder`'s value. No mapping is provided for `Holder` objects in an unmarshalled response.

## Examples

### Webservice client

The following route supports marshalling the request and unmarshalling a response or fault.

_Java-only: Java programmatic data format with exception handling_

```java
String WS_URI = "cxf://http://myserver/customerservice?serviceClass=com.example.customerservice&dataFormat=RAW";
SoapDataFormat soapDF = new SoapDataFormat("com.example.customerservice", new ServiceInterfaceStrategy(CustomerService.class));
from("direct:customerServiceClient")
  .onException(Exception.class)
    .handled(true)
    .unmarshal(soapDF)
  .end()
  .marshal(soapDF)
  .to(WS_URI)
  .unmarshal(soapDF);
```

The below snippet creates a proxy for the service interface and makes a SOAP call to the above route.

_Java-only: Java proxy API_

```java
import org.apache.camel.Endpoint;
import org.apache.camel.component.bean.ProxyHelper;
...

Endpoint startEndpoint = context.getEndpoint("direct:customerServiceClient");
ClassLoader classLoader = Thread.currentThread().getContextClassLoader();
// CustomerService below is the service endpoint interface, *not* the javax.xml.ws.Service subclass
CustomerService proxy = ProxyHelper.createProxy(startEndpoint, classLoader, CustomerService.class);
GetCustomersByNameResponse response = proxy.getCustomersByName(new GetCustomersByName());
```

### Webservice Server

Using the following route sets up a webservice server that consumes from the jms queue `customerServiceQueue` and processes requests using the class `CustomerServiceImpl`. The `customerServiceImpl` should implement the interface `CustomerService`. Instead of directly instantiating the server class it could be defined in a spring context as a regular bean.

_Java-only: Java programmatic data format with bean processing_

```java
SoapDataFormat soapDF = new SoapDataFormat("com.example.customerservice", new ServiceInterfaceStrategy(CustomerService.class));
CustomerService serverBean = new CustomerServiceImpl();
from("jms://queue:customerServiceQueue")
  .onException(Exception.class)
    .handled(true)
    .marshal(soapDF)
  .end()
  .unmarshal(soapDF)
  .bean(serverBean)
  .marshal(soapDF);
```

## Dependencies

To use the SOAP dataformat in your Camel routes, you need to add the following dependency to your `pom.xml`.

```xml
<dependency>
  <groupId>org.apache.camel</groupId>
  <artifactId>camel-soap</artifactId>
  <version>x.y.z</version>
</dependency>
```