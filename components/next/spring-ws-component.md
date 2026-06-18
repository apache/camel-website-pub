# Spring WebService

**Since Camel 2.6**

**Both producer and consumer are supported**

The Spring WS component allows you to integrate with [Spring Web Services](https://docs.spring.io/spring-ws/docs/4.0.x/reference/html/). It offers both _client_\-side support, for accessing web services, and _server_\-side support for creating your own contract-first web services.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spring-ws</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

**Be aware** Spring WS version 4.x does not support Axiom anymore (because Axiom does not support Jakarta JEE 9)

## URI format

The URI scheme for this component is as follows

spring-ws:\[mapping-type:\]address\[?options\]

To expose a web service **mapping-type** needs to be set to any of the following:

 
| Mapping type | Description |
| --- | --- |
| `rootqname` | Offers the option to map web service requests based on the qualified name of the root element contained in the message. |
| `soapaction` | Used to map web service requests based on the SOAP action specified in the header of the message. |
| `uri` | To map web service requests that target a specific URI. |
| `uripath` | To map web service requests that target a specific path in URI. |
| `xpathresult` | Used to map web service requests based on the evaluation of an XPath `expression` against the incoming message. The result of the evaluation should match the XPath result specified in the endpoint URI. |
| `beanname` | Allows you to reference an `org.apache.camel.component.spring.ws.bean.CamelEndpointDispatcher` object to integrate with existing (legacy) [endpoint mappings](https://docs.spring.io/spring-ws/docs/4.0.x/reference/html/#server-endpoint-mapping) like `PayloadRootQNameEndpointMapping`, `SoapActionEndpointMapping`, etc. |

As a consumer, the **address** should contain a value relevant to the specified mapping-type (e.g. a SOAP action, XPath expression). As a producer, the address should be set to the URI of the web service your calling upon.

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The Spring WebService component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |

## Endpoint Options

The Spring WebService endpoint is configured using URI syntax:

spring-ws:type:lookupKey:webServiceEndpointUri

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **type** (consumer) | 
Endpoint mapping type if endpoint mapping is used. rootqname - Offers the option to map web service requests based on the qualified name of the root element contained in the message. soapaction - Used to map web service requests based on the SOAP action specified in the header of the message. uri - In order to map web service requests that target a specific URI. xpathresult - Used to map web service requests based on the evaluation of an XPath expression against the incoming message. The result of the evaluation should match the XPath result specified in the endpoint URI. beanname - Allows you to reference an org.apache.camel.component.spring.ws.bean.CamelEndpointDispatcher object in order to integrate with existing (legacy) endpoint mappings like PayloadRootQNameEndpointMapping, SoapActionEndpointMapping, etc.

Enum values:

-   ROOT\_QNAME
    
-   ACTION
    
-   TO
    
-   SOAP\_ACTION
    
-   XPATHRESULT
    
-   URI
    
-   URI\_PATH
    
-   BEANNAME
    





 |  | EndpointMappingType |
| **lookupKey** (consumer) | Endpoint mapping key if endpoint mapping is used. |  | String |
| **webServiceEndpointUri** (producer) | The default Web Service endpoint uri to use for the producer. |  | String |

### Query Parameters (23 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **headerFilterStrategy** (common) | To use a custom HeaderFilterStrategy to filter headers mapped to and from the Camel message. By default the internal Camel and camel header namespace (case-insensitive) is filtered out from inbound SOAP headers. |  | HeaderFilterStrategy |
| **messageFilter** (common) | Option to provide a custom MessageFilter. For example when you want to process your headers or attachments by your own. |  | MessageFilter |
| **messageIdStrategy** (common) | Option to provide a custom MessageIdStrategy to control generation of WS-Addressing unique message ids. |  | MessageIdStrategy |
| **endpointDispatcher** (consumer) | Spring org.springframework.ws.server.endpoint.MessageEndpoint for dispatching messages received by Spring-WS to a Camel endpoint, to integrate with existing (legacy) endpoint mappings like PayloadRootQNameEndpointMapping, SoapActionEndpointMapping, etc. |  | CamelEndpointDispatcher |
| **endpointMapping** (consumer) | Reference to an instance of org.apache.camel.component.spring.ws.bean.CamelEndpointMapping in the Registry/ApplicationContext. Only one bean is required in the registry to serve all Camel/Spring-WS endpoints. This bean is auto-discovered by the MessageDispatcher and used to map requests to Camel endpoints based on characteristics specified on the endpoint (like root QName, SOAP action, etc). |  | CamelSpringWSEndpointMapping |
| **expression** (consumer) | The XPath expression to use when option type=xpathresult. Then this option is required to be configured. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **allowResponseAttachmentOverride** (producer) | Option to override soap response attachments in in/out exchange with attachments from the actual service layer. If the invoked service appends or rewrites the soap attachments this option when set to true, allows the modified soap attachments to be overwritten in in/out message attachments. | false | boolean |
| **allowResponseHeaderOverride** (producer) | Option to override soap response header in in/out exchange with header info from the actual service layer. If the invoked service appends or rewrites the soap header this option when set to true, allows the modified soap header to be overwritten in in/out message headers. | false | boolean |
| **faultAction** (producer) | Signifies the value for the faultAction response WS-Addressing Fault Action header that is provided by the method. See org.springframework.ws.soap.addressing.server.annotation.Action annotation for more details. |  | URI |
| **faultTo** (producer) | Signifies the value for the faultAction response WS-Addressing FaultTo header that is provided by the method. See org.springframework.ws.soap.addressing.server.annotation.Action annotation for more details. |  | URI |
| **messageFactory** (producer) | Option to provide a custom WebServiceMessageFactory. |  | WebServiceMessageFactory |
| **messageSender** (producer) | Option to provide a custom WebServiceMessageSender. For example to perform authentication or use alternative transports. |  | WebServiceMessageSender |
| **outputAction** (producer) | Signifies the value for the response WS-Addressing Action header that is provided by the method. See org.springframework.ws.soap.addressing.server.annotation.Action annotation for more details. |  | URI |
| **replyTo** (producer) | Signifies the value for the replyTo response WS-Addressing ReplyTo header that is provided by the method. See org.springframework.ws.soap.addressing.server.annotation.Action annotation for more details. |  | URI |
| **soapAction** (producer) | SOAP action to include inside a SOAP request when accessing remote web services. |  | String |
| **timeout** (producer) | Sets the socket read timeout (in milliseconds) while invoking a webservice using the producer, see URLConnection.setReadTimeout() and CommonsHttpMessageSender.setReadTimeout(). This option works when using the built-in message sender implementations: CommonsHttpMessageSender and HttpUrlConnectionMessageSender. One of these implementations will be used by default for HTTP based services unless you customize the Spring WS configuration options supplied to the component. If you are using a non-standard sender, it is assumed that you will handle your own timeout configuration. The built-in message sender HttpComponentsMessageSender is considered instead of CommonsHttpMessageSender which has been deprecated, see HttpComponentsMessageSender.setReadTimeout(). |  | int |
| **webServiceTemplate** (producer) | Option to provide a custom WebServiceTemplate. This allows for full control over client-side web services handling; like adding a custom interceptor or specifying a fault resolver, message sender or message factory. |  | WebServiceTemplate |
| **wsAddressingAction** (producer) | WS-Addressing 1.0 action header to include when accessing web services. The To header is set to the address of the web service as specified in the endpoint URI (default Spring-WS behavior). |  | URI |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **sslContextParameters** (security) | To configure security using SSLContextParameters. |  | SSLContextParameters |

## Message Headers

The Spring WebService component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSpringWebserviceEndpointUri** (producer) Constant: [`SPRING_WS_ENDPOINT_URI`](https://javadoc.io/doc/org.apache.camel/camel-spring-ws/latest/org/apache/camel/component/spring/ws/SpringWebserviceConstants.html#SPRING_WS_ENDPOINT_URI) | The endpoint URI. |  | String |
| **CamelSpringWebserviceSoapAction** (producer) Constant: [`SPRING_WS_SOAP_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-spring-ws/latest/org/apache/camel/component/spring/ws/SpringWebserviceConstants.html#SPRING_WS_SOAP_ACTION) | SOAP action to include inside a SOAP request when accessing remote web services. |  | String |
| **CamelSpringWebserviceSoapHeader** (producer) Constant: [`SPRING_WS_SOAP_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-spring-ws/latest/org/apache/camel/component/spring/ws/SpringWebserviceConstants.html#SPRING_WS_SOAP_HEADER) | The soap header source. |  | Source |
| **CamelSpringWebserviceAddressingAction** (producer) Constant: [`SPRING_WS_ADDRESSING_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-spring-ws/latest/org/apache/camel/component/spring/ws/SpringWebserviceConstants.html#SPRING_WS_ADDRESSING_ACTION) | WS-Addressing 1.0 action header to include when accessing web services. The To header is set to the address of the web service as specified in the endpoint URI (default Spring-WS behavior). |  | URI |
| **CamelSpringWebserviceAddressingFaultTo** (producer) Constant: [`SPRING_WS_ADDRESSING_PRODUCER_FAULT_TO`](https://javadoc.io/doc/org.apache.camel/camel-spring-ws/latest/org/apache/camel/component/spring/ws/SpringWebserviceConstants.html#SPRING_WS_ADDRESSING_PRODUCER_FAULT_TO) | Signifies the value for the faultAction response WS-Addressing FaultTo header that is provided by the method. See org.springframework.ws.soap.addressing.server.annotation.Action annotation for more details. |  | URI |
| **CamelSpringWebserviceAddressingReplyTo** (producer) Constant: [`SPRING_WS_ADDRESSING_PRODUCER_REPLY_TO`](https://javadoc.io/doc/org.apache.camel/camel-spring-ws/latest/org/apache/camel/component/spring/ws/SpringWebserviceConstants.html#SPRING_WS_ADDRESSING_PRODUCER_REPLY_TO) | Signifies the value for the replyTo response WS-Addressing ReplyTo header that is provided by the method. See org.springframework.ws.soap.addressing.server.annotation.Action annotation for more details. |  | URI |
| **breadcrumbId** (consumer) Constant: [`BREADCRUMB_ID`](https://javadoc.io/doc/org.apache.camel/camel-spring-ws/latest/org/apache/camel/component/spring/ws/SpringWebserviceConstants.html#BREADCRUMB_ID) | The breadcrumb id. |  | String |

## Usage

### Accessing web services

To call a web service at `http://foo.com/bar` simply define a route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:example").to("spring-ws:http://foo.com/bar");
```

```xml
<route>
  <from uri="direct:example"/>
  <to uri="spring-ws:http://foo.com/bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:example
      steps:
        - to:
            uri: spring-ws:http://foo.com/bar
```

And sent a message:

_Java-only: ProducerTemplate test API_

```java
template.requestBody("direct:example", "<foobar xmlns=\"http://foo.com\"><msg>test message</msg></foobar>");
```

Remember if it’s a SOAP service you’re calling, you don’t have to include SOAP tags. Spring-WS will perform the XML-to-SOAP marshaling.

### Sending SOAP and WS-Addressing action headers

When a remote web service requires a SOAP action or use of the WS-Addressing standard, you define your route as:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:example")
  .to("spring-ws:http://foo.com/bar?soapAction=http://foo.com&wsAddressingAction=http://bar.com");
```

```xml
<route>
  <from uri="direct:example"/>
  <to uri="spring-ws:http://foo.com/bar?soapAction=http://foo.com&amp;wsAddressingAction=http://bar.com"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:example
      steps:
        - to:
            uri: spring-ws:http://foo.com/bar
            parameters:
              soapAction: "http://foo.com"
              wsAddressingAction: "http://bar.com"
```

Optionally, you can override the endpoint options with header values:

_Java-only: ProducerTemplate setting SOAP action header_

```java
template.requestBodyAndHeader("direct:example",
    "<foobar xmlns=\"http://foo.com\"><msg>test message</msg></foobar>",
    "CamelSpringWebserviceSoapAction", "http://baz.com");
```

### Using SOAP headers

You can provide the SOAP header(s) as a Camel Message header when sending a message to a spring-ws endpoint, for example, given the following SOAP header in a String

_Java-only: constructing SOAP header and setting it on the Exchange_

```java
String body = ...
String soapHeader = "<h:Header xmlns:h=\"http://www.webserviceX.NET/\">"
        + "<h:MessageID>1234567890</h:MessageID>"
        + "<h:Nested><h:NestedID>1111</h:NestedID></h:Nested></h:Header>";

exchange.getIn().setBody(body);
exchange.getIn().setHeader("CamelSpringWebserviceSoapHeader", soapHeader);
```

And then send the Exchange to a `spring-ws` endpoint to call the Web Service.

Likewise, the spring-ws consumer will also enrich the Camel Message with the SOAP header.

For example, see this [unit test](https://github.com/apache/camel/blob/main/components/camel-spring-ws/src/test/java/org/apache/camel/component/spring/ws/SoapHeaderTest.java).

### The header and attachment propagation

Spring WS Camel supports propagation of the headers and attachments into Spring-WS `WebServiceMessage` response. The endpoint will use so-called "hook" the `MessageFilter` (default implementation is provided by `BasicMessageFilter`) to propagate the exchange headers and attachments into `WebServiceMessage` response. Now you can use

_Java-only: programmatic header and attachment manipulation_

```java
exchange.getOut().getHeaders().put("myCustom", "myHeaderValue");
exchange.getIn().addAttachment("myAttachment", new DataHandler(...));
```

> **Note**
> If the exchange header in the pipeline contains text, it generates Qname(key)=value attribute in the soap header. Recommended is to create a QName class directly and put any key into header.

### How to transform the soap header using a stylesheet

The header transformation filter (`HeaderTransformationMessageFilter`) can be used to transform the soap header for a soap request. If you want to use the header transformation filter, see the below example:

_XML-only: Spring bean definition for HeaderTransformationMessageFilter_

```xml
<bean id="headerTransformationFilter" class="org.apache.camel.component.spring.ws.filter.impl.HeaderTransformationMessageFilter">
    <constructor-arg index="0" value="org/apache/camel/component/spring/ws/soap-header-transform.xslt"/>
</bean>
```

Use the bean defined above in the camel endpoint

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:stockQuoteWebserviceHeaderTransformation")
    .to("spring-ws:http://localhost?webServiceTemplate=#webServiceTemplate&soapAction=http://www.stockquotes.edu/GetQuote&messageFilter=#headerTransformationFilter");
```

```xml
<route>
    <from uri="direct:stockQuoteWebserviceHeaderTransformation"/>
    <to uri="spring-ws:http://localhost?webServiceTemplate=#webServiceTemplate&amp;soapAction=http://www.stockquotes.edu/GetQuote&amp;messageFilter=#headerTransformationFilter"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:stockQuoteWebserviceHeaderTransformation
      steps:
        - to:
            uri: spring-ws:http://localhost
            parameters:
              webServiceTemplate: "#webServiceTemplate"
              soapAction: "http://www.stockquotes.edu/GetQuote"
              messageFilter: "#headerTransformationFilter"
```

### The custom header and attachment filtering

If you need to provide your custom processing of either headers or attachments, extend existing `BasicMessageFilter` and override the appropriate methods or write a brand-new implementation of the `MessageFilter` interface. To use your custom filter, add this into your spring context:

You can specify either a global a or a local message filter as follows:

-   the global custom filter that provides the global configuration for all Spring-WS endpoints
    

```xml
<bean id="messageFilter" class="your.domain.myMessageFiler" scope="singleton" />
```

-   the local messageFilter directly on the endpoint as follows:
    

_Java-only: endpoint URI fragment with bean reference_

```java
to("spring-ws:http://yourdomain.com?messageFilter=#myEndpointSpecificMessageFilter");
```

For more information, see [CAMEL-5724](https://issues.apache.org/jira/browse/CAMEL-5724)

If you want to create your own `MessageFilter`, consider overriding the following methods in the default implementation of `MessageFilter` in class `BasicMessageFilter`:

_Java-only: custom `MessageFilter` method overrides_

```java
protected void doProcessSoapHeader(Message inOrOut, SoapMessage soapMessage) {
    // your code, no need to call super
}

protected void doProcessSoapAttachements(Message inOrOut, SoapMessage response) {
    // your code, no need to call super
}
```

### Using a custom MessageSender and MessageFactory

A custom message sender or factory in the registry can be referenced like this:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:example")
    .to("spring-ws:http://foo.com/bar?messageFactory=#messageFactory&messageSender=#messageSender");
```

```xml
<route>
  <from uri="direct:example"/>
  <to uri="spring-ws:http://foo.com/bar?messageFactory=#messageFactory&amp;messageSender=#messageSender"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:example
      steps:
        - to:
            uri: spring-ws:http://foo.com/bar
            parameters:
              messageFactory: "#messageFactory"
              messageSender: "#messageSender"
```

Spring configuration:

```xml
<!-- authenticate using HTTP Basic Authentication -->
<bean id="messageSender" class="org.springframework.ws.transport.http.HttpComponentsMessageSender">
    <property name="credentials">
        <bean class="org.apache.commons.httpclient.UsernamePasswordCredentials">
            <constructor-arg index="0" value="admin"/>
            <constructor-arg index="1" value="secret"/>
        </bean>
    </property>
</bean>
```

### Exposing web services

To expose a web service using this component, you first need to set up a [MessageDispatcher](https://docs.spring.io/spring-ws/docs/4.0.x/reference/html/#_the_messagedispatcher) to look for endpoint mappings in a Spring XML file. If you plan on running inside a servlet container, you probably want to use a `MessageDispatcherServlet` configured in `web.xml`.

By default, the `MessageDispatcherServlet` will look for a Spring XML named `/WEB-INF/spring-ws-servlet.xml`. To use Camel with Spring-WS the only mandatory bean in that XML file is `CamelEndpointMapping`. This bean allows the `MessageDispatcher` to dispatch web service requests to your routes.

_web.xml_

```xml
<web-app>
    <servlet>
        <servlet-name>spring-ws</servlet-name>
        <servlet-class>org.springframework.ws.transport.http.MessageDispatcherServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>spring-ws</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>
</web-app>
```

_spring-ws-servlet.xml_

```xml
<bean id="endpointMapping" class="org.apache.camel.component.spring.ws.bean.CamelEndpointMapping" />

<bean id="wsdl" class="org.springframework.ws.wsdl.wsdl11.DefaultWsdl11Definition">
    <property name="schema">
        <bean class="org.springframework.xml.xsd.SimpleXsdSchema">
            <property name="xsd" value="/WEB-INF/foobar.xsd"/>
        </bean>
    </property>
    <property name="portTypeName" value="FooBar"/>
    <property name="locationUri" value="/"/>
    <property name="targetNamespace" value="http://example.com/"/>
</bean>
```

More information on setting up Spring-WS can be found in [Writing Contract-First Web Services](https://docs.spring.io/spring-ws/docs/4.0.x/reference/html/#tutorial). Basically paragraph 3.6 "Implementing the Endpoint" is handled by this component (specifically paragraph 3.6.2 "Routing the Message to the Endpoint" is where `CamelEndpointMapping` comes in). Also remember to check out the Spring Web Services Example included in the Camel distribution.

### Endpoint mapping in routes

With the XML configuration in place, you can now use Camel’s DSL to define what web service requests are handled by your endpoint:

The following route will receive all web service requests that have a root element named "GetFoo" within the `http://example.com/` namespace.

-   Java
    
-   XML
    
-   YAML
    

```java
from("spring-ws:rootqname:{http://example.com/}GetFoo?endpointMapping=#endpointMapping")
    .convertBodyTo(String.class).to("mock:example");
```

```xml
<route>
  <from uri="spring-ws:rootqname:{http://example.com/}GetFoo?endpointMapping=#endpointMapping"/>
  <convertBodyTo type="String"/>
  <to uri="mock:example"/>
</route>
```

```yaml
- route:
    from:
      uri: "spring-ws:rootqname:{http://example.com/}GetFoo"
      parameters:
        endpointMapping: "#endpointMapping"
      steps:
        - convertBodyTo:
            type: String
        - to:
            uri: mock:example
```

The following route will receive web service requests containing the `http://example.com/GetFoo` SOAP action.

-   Java
    
-   XML
    
-   YAML
    

```java
from("spring-ws:soapaction:http://example.com/GetFoo?endpointMapping=#endpointMapping")
    .convertBodyTo(String.class).to("mock:example");
```

```xml
<route>
  <from uri="spring-ws:soapaction:http://example.com/GetFoo?endpointMapping=#endpointMapping"/>
  <convertBodyTo type="String"/>
  <to uri="mock:example"/>
</route>
```

```yaml
- route:
    from:
      uri: "spring-ws:soapaction:http://example.com/GetFoo"
      parameters:
        endpointMapping: "#endpointMapping"
      steps:
        - convertBodyTo:
            type: String
        - to:
            uri: mock:example
```

The following route will receive all requests sent to `http://example.com/foobar`.

-   Java
    
-   XML
    
-   YAML
    

```java
from("spring-ws:uri:http://example.com/foobar?endpointMapping=#endpointMapping")
    .convertBodyTo(String.class).to("mock:example");
```

```xml
<route>
  <from uri="spring-ws:uri:http://example.com/foobar?endpointMapping=#endpointMapping"/>
  <convertBodyTo type="String"/>
  <to uri="mock:example"/>
</route>
```

```yaml
- route:
    from:
      uri: "spring-ws:uri:http://example.com/foobar"
      parameters:
        endpointMapping: "#endpointMapping"
      steps:
        - convertBodyTo:
            type: String
        - to:
            uri: mock:example
```

The route below will receive requests that contain the element `<foobar>abc</foobar>` anywhere inside the message (and the default namespace).

-   Java
    
-   XML
    
-   YAML
    

```java
from("spring-ws:xpathresult:abc?expression=//foobar&endpointMapping=#endpointMapping")
    .convertBodyTo(String.class).to("mock:example");
```

```xml
<route>
  <from uri="spring-ws:xpathresult:abc?expression=//foobar&amp;endpointMapping=#endpointMapping"/>
  <convertBodyTo type="String"/>
  <to uri="mock:example"/>
</route>
```

```yaml
- route:
    from:
      uri: "spring-ws:xpathresult:abc"
      parameters:
        expression: "//foobar"
        endpointMapping: "#endpointMapping"
      steps:
        - convertBodyTo:
            type: String
        - to:
            uri: mock:example
```

### Alternative configuration, using existing endpoint mappings

For every endpoint with mapping-type `beanname` one bean of type `CamelEndpointDispatcher` with a corresponding name is required in the `Registry`/`ApplicationContext`. This bean acts as a bridge between the Camel endpoint and an existing [endpoint mapping](https://docs.spring.io/spring-ws/docs/4.0.x/reference/html/#server-endpoint-mapping) like `PayloadRootQNameEndpointMapping`.

> **Note**
> The use of the `beanname` mapping-type is primarily meant for (legacy) situations where you’re already using Spring-WS and have endpoint mappings defined in a Spring XML file. The `beanname` mapping-type allows you to wire your Camel route into an existing endpoint mapping. When you’re starting from scratch, it’s recommended to define your endpoint mappings as Camel URI’s (as illustrated above with `endpointMapping`) since it requires less configuration and is more expressive. Alternatively, you could use vanilla Spring-WS with the help of annotations.

An example of a route using `beanname`:

_XML-only: Spring XML with legacy endpoint mapping and CamelEndpointDispatcher beans_

```xml
<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route>
        <from uri="spring-ws:beanname:QuoteEndpointDispatcher" />
        <to uri="mock:example" />
    </route>
</camelContext>

<bean id="legacyEndpointMapping" class="org.springframework.ws.server.endpoint.mapping.PayloadRootQNameEndpointMapping">
    <property name="mappings">
        <props>
            <prop key="{http://example.com/}GetFuture">FutureEndpointDispatcher</prop>
            <prop key="{http://example.com/}GetQuote">QuoteEndpointDispatcher</prop>
        </props>
    </property>
</bean>

<bean id="QuoteEndpointDispatcher" class="org.apache.camel.component.spring.ws.bean.CamelEndpointDispatcher" />
<bean id="FutureEndpointDispatcher" class="org.apache.camel.component.spring.ws.bean.CamelEndpointDispatcher" />
```

### POJO (un)marshalling

Camel’s pluggable data formats offer support for pojo/xml marshalling using libraries such as JAXB. You can use these data formats in your route to send and receive pojo’s, to and from web services.

When _accessing_ web services, you can marshal the request and unmarshal the response message:

_Java-only: programmatic JAXB data format configuration with marshal/unmarshal_

```java
JaxbDataFormat jaxb = new JaxbDataFormat(false);
jaxb.setContextPath("com.example.model");

from("direct:example").marshal(jaxb).to("spring-ws:http://foo.com/bar").unmarshal(jaxb);
```

Similarly, when _providing_ web services, you can unmarshal XML requests to POJO’s and marshal the response message back to XML:

_Java-only: unmarshal incoming SOAP requests and marshal responses with JAXB_

```java
from("spring-ws:rootqname:{http://example.com/}GetFoo?endpointMapping=#endpointMapping")
    .unmarshal(jaxb)
    .to("mock:example")
    .marshal(jaxb);
```

## Spring Boot Auto-Configuration

When using spring-ws with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-spring-ws-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.spring-ws.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.spring-ws.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.spring-ws.enabled** | Whether to enable auto configuration of the spring-ws component. This is enabled by default. |  | Boolean |
| **camel.component.spring-ws.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.spring-ws.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |