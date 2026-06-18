# JTE

**Since Camel 4.4**

**Only producer is supported**

The **jte:** component allows for processing a message using a [JTE](https://jte.gg/) template. The JTE is a Java Template Engine, which means you write templates that resemble Java code, which in fact gets transformed into .java source files that gets compiled to have very fast performance.

Only use this component if you are familiar with Java programming.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jte</artifactId>
    <version>x.x.x</version> <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

jte:templateName\[?options\]

Where **templateName** is the classpath-local URI of the template to invoke; or the complete URL of the remote template (e.g.: `file://folder/myfile.jte`).

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

The JTE component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **contentType** (producer) | 
Content type the JTE engine should use.

Enum values:

-   Plain
    
-   Html
    





 | Plain | ContentType |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **preCompile** (producer) | To speed up startup and rendering on your production server, it is possible to precompile all templates during the build. This way, the template engine can load each template’s .class file directly without first compiling it. | false | boolean |
| **workDir** (producer) | Work directory where JTE will store compiled templates. | jte-classes | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The JTE endpoint is configured using URI syntax:

jte:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** Path to the resource. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the resource using these protocols (classpath is default). ref will lookup the resource in the registry. bean will call a method on a bean to be used as the resource. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The JTE component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelJteResourceUri** (producer) Constant: [`JTE_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-jte/latest/org/apache/camel/component/jte/JteConstants.html#JTE_RESOURCE_URI) | A URI for the template resource to use instead of the endpoint configured. |  | String |
| **CamelJteTemplate** (producer) Constant: [`JTE_TEMPLATE`](https://javadoc.io/doc/org.apache.camel/camel-jte/latest/org/apache/camel/component/jte/JteConstants.html#JTE_TEMPLATE) | The template to use instead of the endpoint configured. |  | String |
| **CamelJteDataModel** (producer) Constant: [`JTE_DATA_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-jte/latest/org/apache/camel/component/jte/JteConstants.html#JTE_DATA_MODEL) | The data model. |  | Object |

## Usage

### JTE Context

Camel will provide exchange information in the JTE context, as a `org.apache.camel.component.jte.Model` class with the following information:

 
| key | value |
| --- | --- |
| `exchange` | The `Exchange` itself (only if allowContextMapAll=true). |
| `headers` | The headers of the message as `java.util.Map`. |
| `body` | The message body as `Object`. |
| `strBody()` | The message body converted to a String |
| `header("key")` | Message header with the given key converted to a String value. |
| `exchangeProperty("key")` | Exchange property with the given key converted to a String value (only if allowContextMapAll=true). |

You can set up your custom JTE data model in the message header with the key "**CamelJteDataModel**" just like this

### Dynamic templates

Camel provides two headers by which you can define a different resource location for a template or the template content itself. If any of these headers is set, then Camel uses this over the endpoint configured resource. This allows you to provide a dynamic template at runtime.

## Examples

For example, you could use something like:

-   Java
    
-   XML
    
-   YAML
    

```java
from("rest:get:item/{id}")
    .to("jte:com/acme/response.jte");
```

```xml
<route>
  <from uri="rest:get:item/{id}"/>
  <to uri="jte:com/acme/response.jte"/>
</route>
```

```yaml
- route:
    from:
      uri: rest:get:item/{id}
      steps:
        - to:
            uri: jte:com/acme/response.jte
```

To use a JTE template to formulate a response to the REST get call:

_Java-only: example JTE template file content_

```java
@import org.apache.camel.component.jte.Model
@param Model model

The item ${model.header("id")} is being processed.
```

## Spring Boot Auto-Configuration

When using jte with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jte-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jte.allow-context-map-all** | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | Boolean |
| **camel.component.jte.allow-template-from-header** | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | Boolean |
| **camel.component.jte.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.jte.content-cache** | Sets whether to use resource content cache or not. | true | Boolean |
| **camel.component.jte.content-type** | Content type the JTE engine should use. | plain | ContentType |
| **camel.component.jte.enabled** | Whether to enable auto configuration of the jte component. This is enabled by default. |  | Boolean |
| **camel.component.jte.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.jte.pre-compile** | To speed up startup and rendering on your production server, it is possible to precompile all templates during the build. This way, the template engine can load each template’s .class file directly without first compiling it. | false | Boolean |
| **camel.component.jte.work-dir** | Work directory where JTE will store compiled templates. | jte-classes | String |