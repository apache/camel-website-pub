# Thymeleaf

**Since Camel 4.1**

**Only producer is supported**

The Thymeleaf component allows you to process a message using a [Thymeleaf](https://www.thymeleaf.org/) template. This can be very powerful when using Templating to generate responses for requests.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-thymeleaf</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

thymeleaf:templateName\[?options\]

Where **templateName** is the classpath-local URI of the template to invoke; or the complete URL of the remote template (e.g.: `file://folder/myfile.html`).

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

The Thymeleaf component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Thymeleaf endpoint is configured using URI syntax:

thymeleaf:resourceUri

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
| **cacheable** (producer) | Whether templates have to be considered cacheable or not. | false | Boolean |
| **cacheTimeToLive** (producer) | The cache Time To Live for templates, expressed in milliseconds. |  | Long |
| **checkExistence** (producer) | Whether a template resources will be checked for existence before being returned. | false | Boolean |
| **templateMode** (producer) | 
The template mode to be applied to templates.

Enum values:

-   HTML
    
-   XML
    
-   TEXT
    
-   JAVASCRIPT
    
-   CSS
    
-   RAW
    





 | HTML | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **encoding** (advanced) | The character encoding to be used for reading template resources. |  | String |
| **order** (advanced) | The order in which this template will be resolved as part of the resolver chain. |  | Integer |
| **prefix** (advanced) | An optional prefix added to template names to convert them into resource names. |  | String |
| **resolver** (advanced) | 

The type of resolver to be used by the template engine.

Enum values:

-   CLASS\_LOADER
    
-   DEFAULT
    
-   FILE
    
-   STRING
    
-   URL
    
-   WEB\_APP
    





 | CLASS\_LOADER | ThymeleafResolverType |
| **suffix** (advanced) | An optional suffix added to template names to convert them into resource names. |  | String |

## Message Headers

The Thymeleaf component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelThymeleafResourceUri** (producer) Constant: [`THYMELEAF_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-thymeleaf/latest/org/apache/camel/component/thymeleaf/ThymeleafConstants.html#THYMELEAF_RESOURCE_URI) | The name of the Thymeleaf template. |  | String |
| **CamelThymeleafTemplate** (producer) Constant: [`THYMELEAF_TEMPLATE`](https://javadoc.io/doc/org.apache.camel/camel-thymeleaf/latest/org/apache/camel/component/thymeleaf/ThymeleafConstants.html#THYMELEAF_TEMPLATE) | The content of the Thymeleaf template. |  | String |
| **CamelThymeleafVariableMap** (producer) Constant: [`THYMELEAF_VARIABLE_MAP`](https://javadoc.io/doc/org.apache.camel/camel-thymeleaf/latest/org/apache/camel/component/thymeleaf/ThymeleafConstants.html#THYMELEAF_VARIABLE_MAP) | The value of this header should be a Map with key/values that will be override any existing key with the same name. This can be used to preconfigure common key/values you want to reuse in your Thymeleaf endpoints. |  | Map |
| **CamelThymeleafServletContext** (producer) Constant: [`THYMELEAF_SERVLET_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-thymeleaf/latest/org/apache/camel/component/thymeleaf/ThymeleafConstants.html#THYMELEAF_SERVLET_CONTEXT) | The ServletContext for a web application. |  | ServletContext |

Headers set during the Thymeleaf evaluation are returned to the message and added as headers, thus making it possible to return values from Thymeleaf to the Message.

For example, to set the header value of `fruit` in the Thymeleaf template `fruit-template.html`:

$in.setHeader("fruit", "Apple")

The `fruit` header is now accessible from the `message.out.headers`.

## Usage

### Thymeleaf Context

Camel will provide exchange information in the Thymeleaf context (just a `Map`). The `Exchange` is transferred as:

 
| key | value |
| --- | --- |
| `exchange` | The `Exchange` itself. |
| `exchange.properties` | The `Exchange` properties. |
| `headers` | The headers of the In message. |
| `camelContext` | The Camel Context instance. |
| `request` | The In message. |
| `in` | The In message. |
| `body` | The In message body. |
| `out` | The Out message (only for InOut message exchange pattern). |
| `response` | The Out message (only for InOut message exchange pattern). |

You can set up a custom Thymeleaf Context yourself by setting property `allowTemplateFromHeader=true` and setting the message header `CamelThymeleafContext` like this

_Java-only: programmatic Thymeleaf context setup via Exchange API_

```java
EngineContext engineContext = new EngineContext(variableMap);
exchange.getIn().setHeader("CamelThymeleafContext", engineContext);
```

### Hot reloading

The Thymeleaf template resource is, by default, hot reloadable for both file and classpath resources (expanded jar). If you set `contentCache=true`, Camel will only load the resource once, and thus hot reloading is not possible. This scenario can be used in production when the resource never changes.

### Dynamic templates

Camel provides two headers by which you can define a different resource location for a template or the template content itself. If any of these headers is set, then Camel uses this over the endpoint configured resource. This allows you to provide a dynamic template at runtime.

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelThymeleafResourceUri` | `String` | A URI for the template resource to use instead of the endpoint configured. |
| `CamelThymeleafTemplate` | `String` | The template to use instead of the endpoint configured. |

## Examples

For a simple use case, you could use something like:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("thymeleaf:com/acme/MyResponse.html");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="thymeleaf:com/acme/MyResponse.html"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: thymeleaf:com/acme/MyResponse.html
```

To use a Thymeleaf template to formulate a response to a message for InOut message exchanges (where there is a `JMSReplyTo` header).

If you want to use InOnly and consume the message and send it to another destination, you could use the following route:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("thymeleaf:com/acme/MyResponse.html")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="thymeleaf:com/acme/MyResponse.html"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: thymeleaf:com/acme/MyResponse.html
        - to:
            uri: activemq:Another.Queue
```

And to use the content cache, e.g., for use in production, where the `.html` template never changes:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("thymeleaf:com/acme/MyResponse.html?contentCache=true")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="thymeleaf:com/acme/MyResponse.html?contentCache=true"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: thymeleaf:com/acme/MyResponse.html
            parameters:
              contentCache: true
        - to:
            uri: activemq:Another.Queue
```

And a file-based resource:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("thymeleaf:file://myfolder/MyResponse.html?contentCache=true")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="thymeleaf:file://myfolder/MyResponse.html?contentCache=true"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: thymeleaf:file://myfolder/MyResponse.html
            parameters:
              contentCache: true
        - to:
            uri: activemq:Another.Queue
```

It’s possible to specify what template the component should use dynamically via a header, so for example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .setHeader("CamelThymeleafResourceUri").constant("path/to/my/template.html")
    .to("thymeleaf:dummy?allowTemplateFromHeader=true");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelThymeleafResourceUri">
    <constant>path/to/my/template.html</constant>
  </setHeader>
  <to uri="thymeleaf:dummy?allowTemplateFromHeader=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelThymeleafResourceUri
            expression:
              constant:
                expression: path/to/my/template.html
        - to:
            uri: thymeleaf:dummy
            parameters:
              allowTemplateFromHeader: true
```

It’s possible to specify a template directly as a header. The component should use it dynamically via a header, so, for example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .setHeader("CamelThymeleafTemplate").constant("Hi this is a thymeleaf template that can do templating ${body}")
    .to("thymeleaf:dummy?allowTemplateFromHeader=true");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelThymeleafTemplate">
    <constant>Hi this is a thymeleaf template that can do templating ${body}</constant>
  </setHeader>
  <to uri="thymeleaf:dummy?allowTemplateFromHeader=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelThymeleafTemplate
            expression:
              constant:
                expression: "Hi this is a thymeleaf template that can do templating ${body}"
        - to:
            uri: thymeleaf:dummy
            parameters:
              allowTemplateFromHeader: true
```

### The Email Example

In this sample, we want to use Thymeleaf templating for an order confirmation email. The email template is laid out in Thymeleaf as:

letter.html

```text
Dear [(${headers.lastName})], [(${headers.firstName})]

Thanks for the order of [(${headers.item})].

Regards Camel Riders Bookstore
[(${body})]
```

And the java code (from a unit test):

_Java-only: unit test with Exchange creation and RouteBuilder_

```java
    private Exchange createLetter() {
        Exchange exchange = context.getEndpoint("direct:a").createExchange();
        Message msg = exchange.getIn();
        msg.setHeader("firstName", "Claus");
        msg.setHeader("lastName", "Ibsen");
        msg.setHeader("item", "Camel in Action");
        msg.setBody("PS: Next beer is on me, James");
        return exchange;
    }

    @Test
    public void testThymeleafLetter() throws Exception {
        MockEndpoint mock = getMockEndpoint("mock:result");
        mock.expectedMessageCount(1);
        mock.message(0).body(String.class).contains("Thanks for the order of Camel in Action");

        template.send("direct:a", createLetter());

        mock.assertIsSatisfied();
    }

    from("direct:a")
        .to("thymeleaf:org/apache/camel/component/thymeleaf/letter.txt")
        .to("mock:result");
```