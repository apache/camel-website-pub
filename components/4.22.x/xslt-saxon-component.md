# XSLT Saxon

**Since Camel 3.0**

**Only producer is supported**

The XSLT Saxon component allows you to process a message using an [XSLT](http://www.w3.org/TR/xslt) template using Saxon. This can be ideal when using Templating to generate responses for requests.

## URI format

xslt-saxon:templateName\[?options\]

The URI format contains **templateName**, which can be one of the following:

-   the classpath-local URI of the template to invoke
    
-   the complete URL of the remote template.
    

You can append query options to the URI in the following format:

**?option=value&option=value&…​**

Table 1. Example URIs  
| URI | Description |
| --- | --- |
| `xslt-saxon:com/acme/mytransform.xsl` | Refers to the file `com/acme/mytransform.xsl` on the classpath |
| `xslt-saxon:file:///foo/bar.xsl` | Refers to the file `/foo/bar.xsl` |
| `xslt-saxon:http://acme.com/cheese/foo.xsl` | Refers to the remote http resource |

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

The XSLT Saxon component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Cache for the resource content (the stylesheet file) when it is loaded. If set to false Camel will reload the stylesheet file on each message processing. This is good for development. A cached stylesheet can be forced to reload at runtime via JMX using the clearCachedStylesheet operation. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **saxonConfiguration** (advanced) | To use a custom Saxon configuration. |  | Configuration |
| **saxonConfigurationProperties** (advanced) | To set custom Saxon configuration properties. |  | Map |
| **saxonExtensionFunctions** (advanced) | Allows you to use a custom net.sf.saxon.lib.ExtensionFunctionDefinition. You would need to add camel-saxon to the classpath. The function is looked up in the registry, where you can use commas to separate multiple values to lookup. |  | String |
| **secureProcessing** (advanced) | Feature for XML secure processing (see javax.xml.XMLConstants). This is enabled by default. However, when using Saxon Professional you may need to turn this off to allow Saxon to be able to use Java extension functions. | true | boolean |
| **transformerFactoryClass** (advanced) | To use a custom XSLT transformer factory, specified as a FQN class name. |  | String |
| **transformerFactoryConfigurationStrategy** (advanced) | A configuration strategy to apply on freshly created instances of TransformerFactory. |  | TransformerFactoryConfigurationStrategy |
| **uriResolver** (advanced) | To use a custom UriResolver. Should not be used together with the option 'uriResolverFactory'. |  | URIResolver |
| **uriResolverFactory** (advanced) | To use a custom UriResolver which depends on a dynamic endpoint resource URI. Should not be used together with the option 'uriResolver'. |  | XsltUriResolverFactory |
| **xpathTotalOpLimit** (advanced) | Limits the total number of XPath operators in an XSL Stylesheet. The default (from JDK) is 10000. The limit is set per TransformerFactory instance used by each endpoint, not as a JVM-global system property. | 10000 | int |

## Endpoint Options

The XSLT Saxon endpoint is configured using URI syntax:

xslt-saxon:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** Path to the template. The following is supported by the default URIResolver. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the resource using these protocols (classpath is default). ref will lookup the resource in the registry. bean will call a method on a bean to be used as the resource. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowStAX** (producer) | Whether to allow using StAX as the javax.xml.transform.Source. You can enable this if the XSLT library supports StAX such as the Saxon library (camel-saxon). The Xalan library (default in JVM) does not support StAXSource. | true | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Cache for the resource content (the stylesheet file) when it is loaded on startup. If set to false Camel will reload the stylesheet file on each message processing. This is good for development. A cached stylesheet can be forced to reload at runtime via JMX using the clearCachedStylesheet operation. | true | boolean |
| **deleteOutputFile** (producer) | If you have output=file then this option dictates whether or not the output file should be deleted when the Exchange is done processing. For example suppose the output file is a temporary file, then it can be a good idea to delete it after use. | false | boolean |
| **failOnNullBody** (producer) | Whether or not to throw an exception if the input body is null. | true | boolean |
| **output** (producer) | 
Option to specify which output type to use. Possible values are: string, bytes, DOM, file. The first three options are all in memory based, where as file is streamed directly to a java.io.File. For file you must specify the filename in the IN header with the key XsltConstants.XSLT\_FILE\_NAME which is also CamelXsltFileName. Also any paths leading to the filename must be created beforehand, otherwise an exception is thrown at runtime.

Enum values:

-   string
    
-   bytes
    
-   DOM
    
-   file
    





 | string | XsltOutput |
| **source** (producer) | Source to use, instead of message body. You can prefix with variable:, header:, or property: to specify kind of source. Otherwise, the source is assumed to be a variable. Use empty or null to use default source, which is the message body. |  | String |
| **transformerCacheSize** (producer) | The number of javax.xml.transform.Transformer object that are cached for reuse to avoid calls to Template.newTransformer(). | 0 | int |
| **useJsonBody** (producer) | Whether to use JSON body as input. When enabled, the message body is expected to be JSON and will be converted to XML representation of JSON using XSLT3 json-to-xml() function before XSLT processing. This allows XSLT stylesheets to process JSON input directly using standard XPath expressions. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **entityResolver** (advanced) | To use a custom org.xml.sax.EntityResolver with javax.xml.transform.sax.SAXSource. |  | EntityResolver |
| **errorListener** (advanced) | Allows to configure to use a custom javax.xml.transform.ErrorListener. Beware when doing this then the default error listener which captures any errors or fatal errors and store information on the Exchange as properties is not in use. So only use this option for special use-cases. |  | ErrorListener |
| **resultHandlerFactory** (advanced) | Allows you to use a custom org.apache.camel.builder.xml.ResultHandlerFactory which is capable of using custom org.apache.camel.builder.xml.ResultHandler types. |  | ResultHandlerFactory |
| **saxonConfiguration** (advanced) | To use a custom Saxon configuration. |  | Configuration |
| **saxonExtensionFunctions** (advanced) | Allows you to use a custom net.sf.saxon.lib.ExtensionFunctionDefinition. You would need to add camel-saxon to the classpath. The function is looked up in the registry, where you can comma to separate multiple values to lookup. |  | String |
| **secureProcessing** (advanced) | Feature for XML secure processing (see javax.xml.XMLConstants). This is enabled by default. However, when using Saxon Professional you may need to turn this off to allow Saxon to be able to use Java extension functions. | true | boolean |
| **transformerFactory** (advanced) | To use a custom XSLT transformer factory. |  | TransformerFactory |
| **transformerFactoryClass** (advanced) | To use a custom XSLT transformer factory, specified as a FQN class name. |  | String |
| **transformerFactoryConfigurationStrategy** (advanced) | A configuration strategy to apply on freshly created instances of TransformerFactory. |  | TransformerFactoryConfigurationStrategy |
| **uriResolver** (advanced) | To use a custom javax.xml.transform.URIResolver. |  | URIResolver |
| **xpathTotalOpLimit** (advanced) | Limits the total number of XPath operators in an XSL Stylesheet. The default (from JDK) is 10000. The limit is set per TransformerFactory instance used by this endpoint. | 10000 | int |
| **xsltMessageLogger** (advanced) | A consumer to messages generated during XSLT transformations. |  | XsltMessageLogger |

## Message Headers

The XSLT Saxon component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelXsltResourceUri** (producer) Constant: [`XSLT_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-xslt-saxon/latest/org/apache/camel/component/xslt/XsltConstants.html#XSLT_RESOURCE_URI) | A URI for the template resource to load and use instead of the endpoint configured. |  | String |
| **CamelXsltStylesheet** (producer) Constant: [`XSLT_STYLESHEET`](https://javadoc.io/doc/org.apache.camel/camel-xslt-saxon/latest/org/apache/camel/component/xslt/XsltConstants.html#XSLT_STYLESHEET) | The template to use instead of the endpoint configured. |  | String |
| **CamelXsltFileName** (producer) Constant: [`XSLT_FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-xslt-saxon/latest/org/apache/camel/component/xslt/XsltConstants.html#XSLT_FILE_NAME) | The XSLT file name. |  | String |

## Usage

### Using XSLT endpoints

The following format is an example of using an XSLT template to formulate a response for a message for InOut message exchanges (where there is a `JMSReplyTo` header)

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("xslt-saxon:com/acme/mytransform.xsl");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="xslt-saxon:com/acme/mytransform.xsl"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: xslt-saxon:com/acme/mytransform.xsl
```

If you want to use InOnly and consume the message and send it to another destination, you could use the following route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("xslt-saxon:com/acme/mytransform.xsl")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="xslt-saxon:com/acme/mytransform.xsl"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: xslt-saxon:com/acme/mytransform.xsl
        - to:
            uri: activemq:Another.Queue
```

### Getting Usable Parameters into the XSLT

By default, all headers and variables are added as parameters which are then available in the XSLT.  
To make the parameters usable, you will need to declare them.

-   Header
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("myParam", constant("42"))
    .to("xslt-saxon:MyTransform.xsl");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="myParam"><constant>42</constant></setHeader>
  <to uri="xslt-saxon:MyTransform.xsl"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: myParam
            constant: "42"
        - to:
            uri: xslt-saxon:MyTransform.xsl
```

-   Variable
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setVariable("myParam", constant("42"))
    .to("xslt-saxon:MyTransform.xsl");
```

```xml
<route>
  <from uri="direct:start"/>
  <setVariable name="myParam"><constant>42</constant></setVariable>
  <to uri="xslt-saxon:MyTransform.xsl"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setVariable:
            name: myParam
            constant: "42"
        - to:
            uri: xslt-saxon:MyTransform.xsl
```

The parameter also needs to be declared in the top level of the XSLT for it to be available:

```xml
<xsl: ...... >

   <xsl:param name="myParam"/>

    <xsl:template ...>
```

### Spring XML versions

To use the above examples in Spring XML, you would use something like the following code:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("xslt-saxon:org/apache/camel/spring/processor/example.xsl")
    .to("activemq:Another.Queue");
```

```xml
<camelContext xmlns="http://activemq.apache.org/camel/schema/spring">
  <route>
    <from uri="activemq:My.Queue"/>
    <to uri="xslt-saxon:org/apache/camel/spring/processor/example.xsl"/>
    <to uri="activemq:Another.Queue"/>
  </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: xslt-saxon:org/apache/camel/spring/processor/example.xsl
        - to:
            uri: activemq:Another.Queue
```

### Using `xsl:include`

Camel provides its own implementation of `URIResolver`. This allows Camel to load included files from the classpath.

For example, the included file in the following code will be located relative to the starting endpoint.

```xml
<xsl:include href="staff_template.xsl"/>
```

This means that Camel will locate the file in the **classpath** as **org/apache/camel/component/xslt/staff\_template.xsl**  

You can use `classpath:` or `file:` to instruct Camel to look either in the classpath or file system. If you omit the prefix, then Camel uses the prefix from the endpoint configuration. If no prefix is specified in the endpoint configuration, the default is `classpath:`.

You can also refer backwards in the included paths. In the following example, the XSL file will be resolved under `org/apache/camel/component`.

```xml
    <xsl:include href="../staff_other_template.xsl"/>
```

### Using `xsl:include` and default prefix

Camel will use the prefix from the endpoint configuration as the default prefix.

You can explicitly specify `file:` or `classpath:` loading. The two loading types can be mixed in an XSLT script, if necessary.

### Using Saxon extension functions

Since Saxon 9.2, writing extension functions has been supplemented by a new mechanism, referred to as [extension functions](https://www.saxonica.com/html/documentation12/extensibility/extension-functions.md) you can now easily use camel as shown in the below example:

_Java-only: registering Saxon extension functions and using them in a route_

```java
SimpleRegistry registry = new SimpleRegistry();
registry.put("function1", new MyExtensionFunction1());
registry.put("function2", new MyExtensionFunction2());

from("direct:start")
    .to("xslt-saxon:org/apache/camel/component/xslt/extensions/extensions.xslt?saxonExtensionFunctions=#function1,#function2");
```

With Spring XML:

_XML-only: registering Saxon extension functions as Spring beans_

```xml
<bean id="function1" class="org.apache.camel.component.xslt.extensions.MyExtensionFunction1"/>
<bean id="function2" class="org.apache.camel.component.xslt.extensions.MyExtensionFunction2"/>

<camelContext xmlns="http://camel.apache.org/schema/spring">
  <route>
    <from uri="direct:extensions"/>
    <to uri="xslt-saxon:org/apache/camel/component/xslt/extensions/extensions.xslt?saxonExtensionFunctions=#function1,#function2"/>
  </route>
</camelContext>
```

### Dynamic stylesheets

To provide a dynamic stylesheet at runtime, you can either:

-   Define a dynamic URI. See [toD](eips/toD-eip.md) EIP.
    
-   Use header with the stylesheet.
    

When using a header for dynamic stylesheet, then you can either refer to the stylesheet as a `file` or `classpath` with the header `CamelXsltResourceUri`, such as:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:transform")
    .setHeader("CamelXsltResourceUri", simple("file:styles/${header.region}.xsl"))
    .to("xslt-saxon:template.xsl?allowTemplateFromHeader=true");
```

```xml
<route>
  <from uri="direct:transform"/>
  <setHeader name="CamelXsltResourceUri">
    <simple>file:styles/${header.region}.xsl</simple>
  </setHeader>
  <to uri="xslt-saxon:template.xsl?allowTemplateFromHeader=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:transform
      steps:
        - setHeader:
            name: CamelXsltResourceUri
            simple: "file:styles/${header.region}.xsl"
        - to:
            uri: xslt-saxon:template.xsl
            parameters:
              allowTemplateFromHeader: true
```

Here we set the `CamelXsltResourceUri` header to refer to a stylesheet to be loaded from the file system, with a dynamic name that is computed from another header (`region`).

Notice how the `allowTemplateFromHeader` must be set to `true` on the XSLT endpoint to support dynamic templates.

You can also use the header `CamelXsltStylesheet` which instead should contain the content of the stylesheet to use, instead of referring to a file as the example from above.

> **Tip**
> You can set `contentCache=false` and refer to a non-existing template, such as `"xslt-saxon:dummy.xsl?contentCache=false&allowTemplateFromHeader=true"` as this will tell Camel to not load `dummy.xsl` on startup but to load the stylesheet on demand. And because you provide the stylesheet via headers, then it is fully dynamic.

### Accessing warnings, errors and fatalErrors from XSLT ErrorListener

Any warning/error or fatalError is stored on the current Exchange as a property with the keys `Exchange.XSLT_ERROR`, `Exchange.XSLT_FATAL_ERROR`, or `Exchange.XSLT_WARNING` which allows end users to get hold of any errors happening during transformation.

For example, in the stylesheet below, we want to determinate whether a staff has an empty dob field. And to include a custom error message using `xsl:message`.

```xml
<xsl:template match="/">
  <html>
    <body>
      <xsl:for-each select="staff/programmer">
        <p>Name: <xsl:value-of select="name"/><br />
          <xsl:if test="dob=''">
            <xsl:message terminate="yes">Error: DOB is an empty string!</xsl:message>
          </xsl:if>
        </p>
      </xsl:for-each>
    </body>
  </html>
</xsl:template>
```

The exception is stored on the Exchange as a warning with the key `Exchange.XSLT_WARNING.`

### Consume JSON body

By default, the input body is assumed as XML. You can set `useJsonBody=true` to consume JSON data from Camel Message body.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:transform")
    .to("xslt-saxon:template.xsl?useJsonBody=true");
```

```xml
<route>
  <from uri="direct:transform"/>
  <to uri="xslt-saxon:template.xsl?useJsonBody=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:transform
      steps:
        - to:
            uri: xslt-saxon:template.xsl
            parameters:
              useJsonBody: true
```

If `useJsonBody=true` is set, the JSON body is transformed into XML representation of JSON [defined in XSLT 3.0 specification](https://www.w3.org/TR/xslt-30/#json-to-xml-mapping).

For example, when we have following JSON data

```json
{
    "name": "John Doe",
    "age": 30,
    "email": "john.doe@example.com",
    "address": {
        "street": "123 Main St",
        "city": "New York",
        "zipcode": "10001"
    },
    "hobbies": ["reading", "cycling", "swimming"]
}
```

XSLT 3.0 XML representation of JSON is

```xml
<?xml version="1.0" encoding="UTF-8"?>
<map xmlns="http://www.w3.org/2005/xpath-functions">
   <string key="name">John Doe</string>
   <number key="age">30</number>
   <string key="email">john.doe@example.com</string>
   <map key="address">
      <string key="street">123 Main St</string>
      <string key="city">New York</string>
      <string key="zipcode">10001</string>
   </map>
   <array key="hobbies">
      <string>reading</string>
      <string>cycling</string>
      <string>swimming</string>
   </array>
</map>
```