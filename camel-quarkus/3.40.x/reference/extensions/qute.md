# Qute

JVM since1.0.0 Native since1.0.0

Transform messages using Quarkus Qute templating engine

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-qute)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-qute</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Qute component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **quteEngine** (advanced) | To use the Engine otherwise a new engine is created. |  | Engine |

## Endpoint Options

The Qute endpoint is configured using URI syntax:

qute:resourceUri

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** Path to the resource. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the resource using these protocols (classpath is default). ref will lookup the resource in the registry. bean will call a method on a bean to be used as the resource. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters (5 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However, this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **encoding** (producer) | Character encoding of the resource content. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Qute component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelQuteResourceUri** (producer) Constant: [`QUTE_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel.quarkus/camel-quarkus-qute-component/latest/org/apache/camel/component/qute/QuteConstants.html#QUTE_RESOURCE_URI) | A URI for the template resource to use instead of the endpoint configured one. |  | String |
| **CamelQuteTemplate** (producer) Constant: [`QUTE_TEMPLATE`](https://javadoc.io/doc/org.apache.camel.quarkus/camel-quarkus-qute-component/latest/org/apache/camel/component/qute/QuteConstants.html#QUTE_TEMPLATE) | The template to use instead of the endpoint configured one. |  | String |
| **CamelQuteTemplateInstance** (producer) Constant: [`QUTE_TEMPLATE_INSTANCE`](https://javadoc.io/doc/org.apache.camel.quarkus/camel-quarkus-qute-component/latest/org/apache/camel/component/qute/QuteConstants.html#QUTE_TEMPLATE_INSTANCE) | The template instance to use instead of the endpoint configured one. |  | TemplateInstance |
| **CamelQuteTemplateData** (producer) Constant: [`QUTE_TEMPLATE_DATA`](https://javadoc.io/doc/org.apache.camel.quarkus/camel-quarkus-qute-component/latest/org/apache/camel/component/qute/QuteConstants.html#QUTE_TEMPLATE_DATA) | The template model data. |  | Map |
| **CamelQuteTemplateContentType** (producer) Constant: [`QUTE_TEMPLATE_CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel.quarkus/camel-quarkus-qute-component/latest/org/apache/camel/component/qute/QuteConstants.html#QUTE_TEMPLATE_CONTENT_TYPE) | The content type to use for templates rendered from content provided from the CamelQuteTemplate header. |  | String |

### Qute template data

Camel will populate the Qute `TemplateInstance` data model with exchange information. The following options are available within Qute templates as variables:

 
| key | value |
| --- | --- |
| `exchange` | The `Exchange` itself. |
| `exchange.properties` | The `Exchange` properties. |
| `variables` | The exchange variables |
| `headers` | The headers of the In message. |
| `camelContext` | The Camel Context. |
| `request` | The In message. |
| `body` | The In message body. |
| `response` | The Out message (only for InOut message exchange pattern). |

You can configure your own template data with the message header `CamelQuteTemplateData` like this.

```java
Map<String, Object> variableMap = new HashMap<String, Object>();
variableMap.put("headers", headersMap);
variableMap.put("body", "Monday");
variableMap.put("exchange", exchange);
exchange.getMessage().setHeader("CamelQuteTemplateData", variableMap);
```

### Dynamic templates

Camel provides headers `CamelQuteResourceUri`, `CamelQuteTemplate` and `CamelQuteTemplateInstance` which can be used to define a different resource location for a template, or provide the template instance itself. If any of these headers is set, then Camel uses this over the endpoint configured resource. This allows you to provide a dynamic template at runtime.

### Examples

Processing an exchange with a Qute template read from the classpath.

```java
from("direct:start")
    .to("qute:org/acme/myTemplate.txt");
```

Processing an exchange with a Qute template read from a file-based resource.

```java
from("direct:start")
    .to("qute:file://path/to/myTemplate.txt");
```

Dynamic template path URI.

```java
from("direct:start")
    .setHeader(QuteConstants.QUTE_RESOURCE_URI).constant("org/acme/template.txt")
    .to("qute:dynamic?allowTemplateFromHeader=true");
```

Dynamic template content.

```java
from("direct:start")
    .setHeader(QuteConstants.QUTE_TEMPLATE).constant("<hello>{headers.greeting}</hello>")
    .to("qute:dynamic?allowTemplateFromHeader=true");
```

Dynamic template content with specified content type.

```java
from("direct:start")
    .setHeader(QuteConstants.QUTE_TEMPLATE).constant("<hello>{headers.greeting}</hello>")
    .setHeader(QuteConstants.QUTE_TEMPLATE_CONTENT_TYPE).constant("text/html")
    .to("qute:dynamic?allowTemplateFromHeader=true");
```

Dynamic template instance.

```java
from("direct:start")
    .setHeader(QuteConstants.QUTE_TEMPLATE_INSTANCE).constant(myTemplateInstance)
    .to("qute:dynamic?allowTemplateFromHeader=true");
```

Qute template example.

Dear {headers.lastName}, {headers.firstName}

Thanks for the order of {headers.item}.

Regards Camel Riders Bookstore
{body}

### Quarkus Qute documentation

For more information about Qute, please refer to the [Quarkus Qute](https://quarkus.io/guides/qute) documentation.

## Camel Quarkus limitations

## allowContextMapAll option in native mode

The `allowContextMapAll` option is not supported in native mode as it requires reflective access to security sensitive camel core classes such as `CamelContext` & `Exchange`. This is considered a security risk and thus access to the feature is not provided by default.

## Additional Camel Quarkus configuration

By default, all files located in the src/main/resources/templates directory and its subdirectories are registered as templates. Templates are validated during startup and watched for changes in the development mode.