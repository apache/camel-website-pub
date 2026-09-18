# JSLT

**Since Camel 3.1**

**Only producer is supported**

The JSLT component allows you to process JSON messages using an [JSLT](https://github.com/schibsted/jslt) expression. This can be ideal when doing JSON to JSON transformation or querying data.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jslt</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

jslt:specName\[?options\]

Where **specName** is the classpath-local URI of the specification to invoke; or the complete URL of the remote specification (e.g.: `file://folder/myfile.vm`).

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

The JSLT component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **functions** (advanced) | JSLT can be extended by plugging in functions written in Java. |  | Collection |
| **objectFilter** (advanced) | JSLT can be extended by plugging in a custom jslt object filter. |  | JsonFilter |

## Endpoint Options

The JSLT endpoint is configured using URI syntax:

jslt:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** Path to the resource. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the resource using these protocols (classpath is default). ref will lookup the resource in the registry. bean will call a method on a bean to be used as the resource. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **mapBigDecimalAsFloats** (producer) | If true, the mapper will use the USE\_BIG\_DECIMAL\_FOR\_FLOATS in serialization features. | false | boolean |
| **objectMapper** (producer) | Setting a custom JSON Object Mapper to be used. |  | ObjectMapper |
| **prettyPrint** (common) | If true, JSON in output message is pretty printed. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The JSLT component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelJsltString** (producer) Constant: [`HEADER_JSLT_STRING`](https://javadoc.io/doc/org.apache.camel/camel-jslt/latest/org/apache/camel/component/jslt/JsltConstants.html#HEADER_JSLT_STRING) | The JSLT Template as String. |  | String |
| **CamelJsltResourceUri** (producer) Constant: [`HEADER_JSLT_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-jslt/latest/org/apache/camel/component/jslt/JsltConstants.html#HEADER_JSLT_RESOURCE_URI) | The resource URI. |  | String |

## Usage

### Passing values to JSLT

Camel can supply exchange information as variables when applying a JSLT expression on the body. The available variables from the **Exchange** are:

 
| name | value |
| --- | --- |
| headers | The headers of the In message as a json object |
| variables | The variables |
| exchange.properties | The **Exchange** properties as a json object. `exchange` is the name of the variable and `properties` is the path to the exchange properties. Available if `allowContextMapAll` option is true. |

All the values that cannot be converted to json with Jackson are denied and will not be available in the jslt expression.

For example, the header named `type` and the exchange property `instance` can be accessed like

```json
{
  "type": $headers.type,
  "instance": $exchange.properties.instance
}
```

## Examples

For example, you could use something like:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("jslt:com/acme/MyResponse.json");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="jslt:com/acme/MyResponse.json"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: jslt:com/acme/MyResponse.json
```

And a file-based resource:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("jslt:file://myfolder/MyResponse.json?contentCache=true")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="jslt:file://myfolder/MyResponse.json?contentCache=true"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: jslt:file://myfolder/MyResponse.json
            parameters:
              contentCache: true
        - to:
            uri: activemq:Another.Queue
```

You can also specify which JSLT expression the component should use dynamically via a header, so, for example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .setHeader("CamelJsltResourceUri").constant("path/to/my/spec.json")
    .to("jslt:dummy?allowTemplateFromHeader=true");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelJsltResourceUri">
    <constant>path/to/my/spec.json</constant>
  </setHeader>
  <to uri="jslt:dummy?allowTemplateFromHeader=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelJsltResourceUri
            expression:
              constant:
                expression: path/to/my/spec.json
        - to:
            uri: jslt:dummy
            parameters:
              allowTemplateFromHeader: true
```

Or send whole jslt expression via header: (suitable for querying)

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .setHeader("CamelJsltString").constant(".published")
    .to("jslt:dummy?allowTemplateFromHeader=true");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelJsltString">
    <constant>.published</constant>
  </setHeader>
  <to uri="jslt:dummy?allowTemplateFromHeader=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelJsltString
            expression:
              constant:
                expression: ".published"
        - to:
            uri: jslt:dummy
            parameters:
              allowTemplateFromHeader: true
```

Passing exchange properties to the jslt expression can be done like this

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .to("jslt:com/acme/MyResponse.json?allowContextMapAll=true");
```

```xml
<route>
  <from uri="direct:in"/>
  <to uri="jslt:com/acme/MyResponse.json?allowContextMapAll=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - to:
            uri: jslt:com/acme/MyResponse.json
            parameters:
              allowContextMapAll: true
```