# XJ

**Since Camel 3.0**

**Only producer is supported**

The XJ component allows you to convert XML and JSON documents directly forth and back without the need of intermediate java objects. You can even specify an XSLT stylesheet to convert directly to the target JSON / XML (domain) model.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-xj</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

xj:templateName?transformDirection=XML2JSON|JSON2XML\[&options\]

> **Tip**
> **More documentation**
>
> The XJ component extends the XSLT component, and therefore it supports all options provided by the XSLT component as well. At least look at the XSLT component documentation how to configure the xsl template.

The **transformDirection** option is mandatory and must be either XML2JSON or JSON2XML.

The **templateName** parameter allows using _identify transforma_ by specifying the name `identity`.

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

The XJ component supports the following options which are listed below.

   
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
| **xpathTotalOpLimit** (advanced) | Limits the total number of XPath operators in an XSL Stylesheet. The default (from JDK) is 10000. Configuring this corresponds to setting JVM system property: jdk.xml.xpathTotalOpLimit. | 10000 | int |

## Endpoint Options

The XJ endpoint is configured using URI syntax:

xj:resourceUri

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
| **transformDirection** (producer) | 

**Required** Transform direction. Either XML2JSON or JSON2XML.

Enum values:

-   XML2JSON
    
-   JSON2XML
    





 |  | TransformDirection |
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
| **xsltMessageLogger** (advanced) | A consumer to messages generated during XSLT transformations. |  | XsltMessageLogger |

## Message Headers

The XJ component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelXsltFileName** (producer) Constant: [`XSLT_FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-xj/latest/org/apache/camel/component/xj/XJConstants.html#XSLT_FILE_NAME) | The XSLT file name. |  | String |
| **CamelXsltResourceUri** (producer) Constant: [`XSLT_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-xj/latest/org/apache/camel/component/xslt/XsltConstants.html#XSLT_RESOURCE_URI) | A URI for the template resource to load and use instead of the endpoint configured. |  | String |
| **CamelXsltStylesheet** (producer) Constant: [`XSLT_STYLESHEET`](https://javadoc.io/doc/org.apache.camel/camel-xj/latest/org/apache/camel/component/xslt/XsltConstants.html#XSLT_STYLESHEET) | The template to use instead of the endpoint configured. |  | String |

## Usage

### Converting JSON to XML

The following route does an "identity" transform of the message because no xslt stylesheet is given. In the context of XML to XML transformations, "Identity" transform means that the output document is just a copy of the input document. In the case of XJ, it means it transforms the JSON document to an equivalent XML representation.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("xj:identity?transformDirection=JSON2XML");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="xj:identity?transformDirection=JSON2XML"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: xj:identity
            parameters:
              transformDirection: JSON2XML
```

Sample:

The input:

```json
{
  "firstname": "camel",
  "lastname": "apache",
  "personalnumber": 42,
  "active": true,
  "ranking": 3.1415926,
  "roles": [
    "a",
    {
      "x": null
    }
  ],
  "state": {
    "needsWater": true
  }
}
```

Will output:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<object xmlns:xj="http://camel.apache.org/component/xj" xj:type="object">
    <object xj:name="firstname" xj:type="string">camel</object>
    <object xj:name="lastname" xj:type="string">apache</object>
    <object xj:name="personalnumber" xj:type="int">42</object>
    <object xj:name="active" xj:type="boolean">true</object>
    <object xj:name="ranking" xj:type="float">3.1415926</object>
    <object xj:name="roles" xj:type="array">
        <object xj:type="string">a</object>
        <object xj:type="object">
            <object xj:name="x" xj:type="null">null</object>
        </object>
    </object>
    <object xj:name="state" xj:type="object">
        <object xj:name="needsWater" xj:type="boolean">true</object>
    </object>
</object>
```

As can be seen in the output above, XJ writes some metadata in the resulting xml that can be used in further processing:

-   XJ metadata nodes are always in the `[http://camel.apache.org/component/xj](http://camel.apache.org/component/xj)` namespace.
    
-   JSON key names are placed in the xj:name attribute.
    
-   The parsed JSON type can be found in the xj:type attribute. The above example already contains all possible types.
    
-   Generated XML elements are always named "object".
    

Now we can apply a stylesheet, e.g.:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<xsl:stylesheet version="1.0"
                xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                xmlns:xj="http://camel.apache.org/component/xj"
                exclude-result-prefixes="xj">

    <xsl:output omit-xml-declaration="no" encoding="UTF-8" method="xml" indent="yes"/>

    <xsl:template match="/">
        <person>
            <xsl:apply-templates select="//object"/>
        </person>
    </xsl:template>

    <xsl:template match="object[@xj:type != 'object' and @xj:type != 'array' and string-length(@xj:name) > 0]">
        <xsl:variable name="name" select="@xj:name"/>
        <xsl:element name="{$name}">
            <xsl:value-of select="text()"/>
        </xsl:element>
    </xsl:template>

    <xsl:template match="@*|node()"/>
</xsl:stylesheet>
```

To the above sample by specifying the template on the endpoint:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("xj:com/example/json2xml.xsl?transformDirection=JSON2XML");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="xj:com/example/json2xml.xsl?transformDirection=JSON2XML"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: xj:com/example/json2xml.xsl
            parameters:
              transformDirection: JSON2XML
```

And get the following output:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<person>
    <firstname>camel</firstname>
    <lastname>apache</lastname>
    <personalnumber>42</personalnumber>
    <active>true</active>
    <ranking>3.1415926</ranking>
    <x>null</x>
    <needsWater>true</needsWater>
</person>
```

### Converting XML to JSON

Based on the explanations above, an _identity_ transform will be performed when no stylesheet is given:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("xj:identity?transformDirection=XML2JSON");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="xj:identity?transformDirection=XML2JSON"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: xj:identity
            parameters:
              transformDirection: XML2JSON
```

Given the sample input

```xml
<?xml version="1.0" encoding="UTF-8"?>
<person>
    <firstname>camel</firstname>
    <lastname>apache</lastname>
    <personalnumber>42</personalnumber>
    <active>true</active>
    <ranking>3.1415926</ranking>
    <roles>
        <entry>a</entry>
        <entry>
            <x>null</x>
        </entry>
    </roles>
    <state>
        <needsWater>true</needsWater>
    </state>
</person>
```

will result in

```json
{
  "firstname": "camel",
  "lastname": "apache",
  "personalnumber": "42",
  "active": "true",
  "ranking": "3.1415926",
  "roles": [
    "a",
    {
      "x": "null"
    }
  ],
  "state": {
    "needsWater": "true"
  }
}
```

You may have noted that the input XML and output JSON are very similar to the examples above when converting from json to xml, although nothing special is done here. We only transformed an arbitrary XML document to JSON. XJ uses the following rules by default:

-   The XML root element can be named somehow, it will always end in a JSON root object declaration `{}`
    
-   The JSON key name is the name of the XML element
    
-   If there is a name clash as in `<roles>` above where two `<entry>` elements exist a json array will be generated.
    
-   XML elements with text-only-child-nodes will result in the usual key/string-value pair. Mixed content elements result in a key/child-object pair as seen in `<state>` above.
    

Now we can apply again a stylesheet, e.g.:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<xsl:stylesheet version="1.0"
                xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
                xmlns:xj="http://camel.apache.org/component/xj"
                exclude-result-prefixes="xj">

    <xsl:output omit-xml-declaration="no" encoding="UTF-8" method="xml" indent="yes"/>

    <xsl:template match="/">
        <xsl:apply-templates/>
    </xsl:template>

    <xsl:template match="personalnumber">
        <xsl:element name="{local-name()}">
            <xsl:attribute name="xj:type">
                <xsl:value-of select="'int'"/>
            </xsl:attribute>
            <xsl:apply-templates/>
        </xsl:element>
    </xsl:template>

    <xsl:template match="active|needsWater">
        <xsl:element name="{local-name()}">
            <xsl:attribute name="xj:type">
                <xsl:value-of select="'boolean'"/>
            </xsl:attribute>
            <xsl:apply-templates/>
        </xsl:element>
    </xsl:template>

    <xsl:template match="ranking">
        <xsl:element name="{local-name()}">
            <xsl:attribute name="xj:type">
                <xsl:value-of select="'float'"/>
            </xsl:attribute>
            <xsl:apply-templates/>
        </xsl:element>
    </xsl:template>

    <xsl:template match="roles">
        <xsl:element name="{local-name()}">
            <xsl:attribute name="xj:type">
                <xsl:value-of select="'array'"/>
            </xsl:attribute>
            <xsl:apply-templates/>
        </xsl:element>
    </xsl:template>

    <xsl:template match="*[normalize-space(text()) = 'null']">
        <xsl:element name="{local-name()}">
            <xsl:attribute name="xj:type">
                <xsl:value-of select="'null'"/>
            </xsl:attribute>
            <xsl:apply-templates/>
        </xsl:element>
    </xsl:template>

    <xsl:template match="@*|node()">
        <xsl:copy>
            <xsl:apply-templates select="@*|node()"/>
        </xsl:copy>
    </xsl:template>
</xsl:stylesheet>
```

to the sample above by specifying the template on the endpoint:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("xj:com/example/xml2json.xsl?transformDirection=XML2JSON");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="xj:com/example/xml2json.xsl?transformDirection=XML2JSON"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: xj:com/example/xml2json.xsl
            parameters:
              transformDirection: XML2JSON
```

and get the following output:

```json
{
  "firstname": "camel",
  "lastname": "apache",
  "personalnumber": 42,
  "active": true,
  "ranking": 3.1415926,
  "roles": [
    "a",
    {
      "x": null
    }
  ],
  "state": {
    "needsWater": true
  }
}
```

Note, this transformation resulted in exactly the same JSON document as we used as input to the _json2xml_ conversion. What did the stylesheet do? We just gave some hints to XJ on how to write the JSON document. The following XML document is that what is passed to XJ after XSL transformation:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<person>
    <firstname>camel</firstname>
    <lastname>apache</lastname>
    <personalnumber xmlns:xj="http://camel.apache.org/component/xj" xj:type="int">42</personalnumber>
    <active xmlns:xj="http://camel.apache.org/component/xj" xj:type="boolean">true</active>
    <ranking xmlns:xj="http://camel.apache.org/component/xj" xj:type="float">3.1415926</ranking>
    <roles xmlns:xj="http://camel.apache.org/component/xj" xj:type="array">
        <entry>a</entry>
        <entry>
            <x xj:type="null">null</x>
        </entry>
    </roles>
    <state>
        <needsWater xmlns:xj="http://camel.apache.org/component/xj" xj:type="boolean">true</needsWater>
    </state>
</person>
```

In the stylesheet we just provided the minimal required type hints to get the same result. The supported type hints are exactly the same as XJ writes to an XML document when converting from json to xml.

In the end, that means that we can feed back in the result document from the JSON to XML transformation sample above:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<object xmlns:xj="http://camel.apache.org/component/xj" xj:type="object">
    <object xj:name="firstname" xj:type="string">camel</object>
    <object xj:name="lastname" xj:type="string">apache</object>
    <object xj:name="personalnumber" xj:type="int">42</object>
    <object xj:name="active" xj:type="boolean">true</object>
    <object xj:name="ranking" xj:type="float">3.1415926</object>
    <object xj:name="roles" xj:type="array">
        <object xj:type="string">a</object>
        <object xj:type="object">
            <object xj:name="x" xj:type="null">null</object>
        </object>
    </object>
    <object xj:name="state" xj:type="object">
        <object xj:name="needsWater" xj:type="boolean">true</object>
    </object>
</object>
```

and get the same output again:

```json
{
  "firstname": "camel",
  "lastname": "apache",
  "personalnumber": 42,
  "active": true,
  "ranking": 3.1415926,
  "roles": [
    "a",
    {
      "x": null
    }
  ],
  "state": {
    "needsWater": true
  }
}
```

As seen in the example above:

-   xj:type lets you specify exactly the desired output type
    
-   xj:name lets you overrule the JSON key name.
    

This is required when you want to generate key names that contain chars that aren’t allowed in XML element names.

### Available type hints

 
| @xj:type= | Description |
| --- | --- |
| `object` | Generate a JSON object |
| `array` | Generate a JSON array |
| `string` | Generate a JSON string |
| `int` | Generate a JSON number without fractional part |
| `float` | Generate a JSON number with fractional part |
| `boolean` | Generate a JSON boolean |
| `null` | Generate an empty value using the word null |