# Mustache

**Since Camel 2.12**

**Only producer is supported**

The Mustache component allows for processing a message using a [Mustache](http://mustache.github.io/) template. This can be ideal when using Templating to generate responses for requests.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
<groupId>org.apache.camel</groupId>
<artifactId>camel-mustache</artifactId>
<version>x.x.x</version> <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

mustache:templateName\[?options\]

Where **templateName** is the classpath-local URI of the template to invoke; or the complete URL of the remote template (e.g.: `file://folder/myfile.mustache`).

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

The Mustache component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **mustacheFactory** (advanced) | **Autowired** To use a custom MustacheFactory. |  | MustacheFactory |

## Endpoint Options

The Mustache endpoint is configured using URI syntax:

mustache:resourceUri

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
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **encoding** (producer) | Character encoding of the resource content. |  | String |
| **endDelimiter** (producer) | Characters used to mark template code end. | }} | String |
| **startDelimiter** (producer) | Characters used to mark template code beginning. | {{ | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Mustache component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **MustacheResourceUri** (producer) Constant: [`MUSTACHE_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-mustache/latest/org/apache/camel/component/mustache/MustacheConstants.html#MUSTACHE_RESOURCE_URI) | A URI for the template resource to use instead of the endpoint. |  | String |
| **MustacheTemplate** (producer) Constant: [`MUSTACHE_TEMPLATE`](https://javadoc.io/doc/org.apache.camel/camel-mustache/latest/org/apache/camel/component/mustache/MustacheConstants.html#MUSTACHE_TEMPLATE) | The template to use instead of the endpoint configured. |  | String |

## Usage

### Mustache Context

Camel will provide exchange information in the Mustache context (just a `Map`). The `Exchange` is transferred as:

 
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

### Dynamic templates

Camel provides two headers by which you can define a different resource location for a template or the template content itself. If any of these headers is set, then Camel uses this over the endpoint configured resource. This allows you to provide a dynamic template at runtime.

## Examples

For example, you could use something like:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("mustache:com/acme/MyResponse.mustache");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="mustache:com/acme/MyResponse.mustache"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: mustache:com/acme/MyResponse.mustache
```

To use a Mustache template to formulate a response for a message for InOut message exchanges (where there is a `JMSReplyTo` header).

If you want to use InOnly and consume the message and send it to another destination, you could use:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("mustache:com/acme/MyResponse.mustache")
    .to("activemq:Another.Queue");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="mustache:com/acme/MyResponse.mustache"/>
  <to uri="activemq:Another.Queue"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: mustache:com/acme/MyResponse.mustache
        - to:
            uri: activemq:Another.Queue
```

It’s possible to specify what template the component should use dynamically via a header, so for example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .setHeader("MustacheResourceUri").constant("path/to/my/template.mustache")
    .to("mustache:dummy?allowTemplateFromHeader=true");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="MustacheResourceUri">
    <constant>path/to/my/template.mustache</constant>
  </setHeader>
  <to uri="mustache:dummy?allowTemplateFromHeader=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: MustacheResourceUri
            expression:
              constant:
                expression: path/to/my/template.mustache
        - to:
            uri: mustache:dummy
            parameters:
              allowTemplateFromHeader: true
```

### The Email Example

In this sample, we want to use Mustache templating for an order confirmation email. The email template is laid out in Mustache as:

Dear {{headers.lastName}}, {{headers.firstName}}

Thanks for the order of {{headers.item}}.

Regards Camel Riders Bookstore
{{body}}

## Spring Boot Auto-Configuration

When using mustache with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-mustache-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.mustache.allow-context-map-all** | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | Boolean |
| **camel.component.mustache.allow-template-from-header** | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | Boolean |
| **camel.component.mustache.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.mustache.content-cache** | Sets whether to use resource content cache or not. | true | Boolean |
| **camel.component.mustache.enabled** | Whether to enable auto configuration of the mustache component. This is enabled by default. |  | Boolean |
| **camel.component.mustache.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.mustache.mustache-factory** | To use a custom MustacheFactory. The option is a com.github.mustachejava.MustacheFactory type. |  | MustacheFactory |