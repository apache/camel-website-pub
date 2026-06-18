# Freemarker

**Since Camel 2.10**

**Only producer is supported**

The **freemarker:** component allows for processing a message using a [FreeMarker](http://freemarker.org/) template. This can be ideal when using Templating to generate responses for requests.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-freemarker</artifactId>
    <version>x.x.x</version> <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

freemarker:templateName\[?options\]

Where **templateName** is the classpath-local URI of the template to invoke; or the complete URL of the remote template (e.g.: `file://folder/myfile.ftl`).

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

The Freemarker component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **localizedLookup** (producer) | Enables/disables localized template lookup. Disabled by default. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | To use an existing freemarker.template.Configuration instance as the configuration. |  | Configuration |

## Endpoint Options

The Freemarker endpoint is configured using URI syntax:

freemarker:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** Path to the resource. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the resource using these protocols (classpath is default). ref will lookup the resource in the registry. bean will call a method on a bean to be used as the resource. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **configuration** (producer) | Sets the Freemarker configuration to use. |  | Configuration |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **encoding** (producer) | Sets the encoding to be used for loading the template file. |  | String |
| **templateUpdateDelay** (producer) | Number of seconds the loaded template resource will remain in the cache. |  | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Freemarker component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelFreemarkerResourceUri** (producer) Constant: [`FREEMARKER_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-freemarker/latest/org/apache/camel/component/freemarker/FreemarkerConstants.html#FREEMARKER_RESOURCE_URI) | A URI for the template resource to use instead of the endpoint configured. |  | String |
| **CamelFreemarkerTemplate** (producer) Constant: [`FREEMARKER_TEMPLATE`](https://javadoc.io/doc/org.apache.camel/camel-freemarker/latest/org/apache/camel/component/freemarker/FreemarkerConstants.html#FREEMARKER_TEMPLATE) | The template to use instead of the endpoint configured. |  | String |
| **CamelFreemarkerDataModel** (producer) Constant: [`FREEMARKER_DATA_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-freemarker/latest/org/apache/camel/component/freemarker/FreemarkerConstants.html#FREEMARKER_DATA_MODEL) | The data model. |  | Object |

## Headers

Headers set during the FreeMarker evaluation are returned to the message and added as headers. This provides a mechanism for the FreeMarker component to return values to the Message.

For example, set the header value of `fruit` in the FreeMarker template:

${request.setHeader('fruit', 'Apple')}

The header, `fruit`, is now accessible from the `message.out.headers`.

## Usage

### FreeMarker Context

Camel will provide exchange information in the FreeMarker context (just a `Map`). The `Exchange` is transferred as:

 
| key | value |
| --- | --- |
| `exchange` | The `Exchange` itself. |
| `exchange.properties` | The `Exchange` properties. |
| `variables` | The variables |
| `headers` | The headers of the In message. |
| `camelContext` | The Camel Context. |
| `request` | The In message. |
| `body` | The In message body. |
| `response` | The Out message (only for InOut message exchange pattern). |

You can set up your custom FreeMarker context in the message header with the key "**CamelFreemarkerDataModel**" just like this

_Java-only: setting a custom FreeMarker data model via headers_

```java
Map<String, Object> variableMap = new HashMap<String, Object>();
variableMap.put("headers", headersMap);
variableMap.put("body", "Monday");
variableMap.put("exchange", exchange);
exchange.getIn().setHeader("CamelFreemarkerDataModel", variableMap);
```

### Hot reloading

The FreeMarker template resource is by default **not** hot reloadable for both file and classpath resources (expanded jar). If you set `contentCache=false`, then Camel will not cache the resource and hot reloading is thus enabled. This scenario can be used in development.

### Dynamic templates

Camel provides two headers by which you can define a different resource location for a template or the template content itself. If any of these headers is set, then Camel uses this over the endpoint configured resource. This allows you to provide a dynamic template at runtime.

## Examples

For example, you could use something like:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("freemarker:com/acme/MyResponse.ftl");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="freemarker:com/acme/MyResponse.ftl"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: freemarker:com/acme/MyResponse.ftl
```

To use a FreeMarker template to formulate a response for a message for InOut message exchanges (where there is a `JMSReplyTo` header).

If you want to use InOnly and consume the message and send it to another destination, you could use:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("freemarker:com/acme/MyResponse.ftl")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="freemarker:com/acme/MyResponse.ftl"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: freemarker:com/acme/MyResponse.ftl
        - to:
            uri: activemq:Another.Queue
```

And to disable the content cache, e.g., for development usage where the `.ftl` template should be hot reloaded:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("freemarker:com/acme/MyResponse.ftl?contentCache=false")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="freemarker:com/acme/MyResponse.ftl?contentCache=false"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: freemarker:com/acme/MyResponse.ftl
            parameters:
              contentCache: false
        - to:
            uri: activemq:Another.Queue
```

And a file-based resource:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("freemarker:file://myfolder/MyResponse.ftl?contentCache=false")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="freemarker:file://myfolder/MyResponse.ftl?contentCache=false"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: freemarker:file://myfolder/MyResponse.ftl
            parameters:
              contentCache: false
        - to:
            uri: activemq:Another.Queue
```

It’s possible to specify what template the component should use dynamically via a header, so for example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .setHeader("FreemarkerResourceUri").constant("path/to/my/template.ftl")
    .to("freemarker:dummy?allowTemplateFromHeader=true");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="FreemarkerResourceUri">
    <constant>path/to/my/template.ftl</constant>
  </setHeader>
  <to uri="freemarker:dummy?allowTemplateFromHeader=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: FreemarkerResourceUri
            expression:
              constant:
                expression: path/to/my/template.ftl
        - to:
            uri: freemarker:dummy
            parameters:
              allowTemplateFromHeader: true
```

### The Email Example

In this sample, we want to use FreeMarker templating for an order confirmation email. The email template is laid out in FreeMarker as:

Dear ${headers.lastName}, ${headers.firstName}

Thanks for the order of ${headers.item}.

Regards Camel Riders Bookstore
${body}

## Spring Boot Auto-Configuration

When using freemarker with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-freemarker-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.freemarker.allow-context-map-all** | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | Boolean |
| **camel.component.freemarker.allow-template-from-header** | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | Boolean |
| **camel.component.freemarker.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.freemarker.configuration** | To use an existing freemarker.template.Configuration instance as the configuration. The option is a freemarker.template.Configuration type. |  | Configuration |
| **camel.component.freemarker.content-cache** | Sets whether to use resource content cache or not. | true | Boolean |
| **camel.component.freemarker.enabled** | Whether to enable auto configuration of the freemarker component. This is enabled by default. |  | Boolean |
| **camel.component.freemarker.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.freemarker.localized-lookup** | Enables/disables localized template lookup. Disabled by default. | false | Boolean |