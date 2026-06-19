# String Template

**Since Camel 1.2**

**Only producer is supported**

The String Template component allows you to process a message using a [String Template](http://www.stringtemplate.org/). This can be ideal when using Templating to generate responses for requests.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-stringtemplate</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

string-template:templateName\[?options\]

Where **templateName** is the classpath-local URI of the template to invoke; or the complete URL of the remote template.

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

The String Template component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The String Template endpoint is configured using URI syntax:

string-template:resourceUri

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** Path to the resource. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the resource using these protocols (classpath is default). ref will lookup the resource in the registry. bean will call a method on a bean to be used as the resource. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters (6 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **delimiterStart** (producer) | The variable start delimiter. | < | char |
| **delimiterStop** (producer) | The variable end delimiter. | \> | char |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The String Template component supports 3 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelStringTemplateResourceUri** (producer) Constant: [`STRINGTEMPLATE_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-stringtemplate/latest/org/apache/camel/component/stringtemplate/StringTemplateConstants.html#STRINGTEMPLATE_RESOURCE_URI) | A URI for the template resource to use instead of the endpoint configured. |  | String |
| **CamelStringTemplateVariableMap** (producer) Constant: [`STRINGTEMPLATE_VARIABLE_MAP`](https://javadoc.io/doc/org.apache.camel/camel-stringtemplate/latest/org/apache/camel/component/stringtemplate/StringTemplateConstants.html#STRINGTEMPLATE_VARIABLE_MAP) | Map of the variables which are made available to a script or template. |  | Map |
| **CamelStringTemplateTemplate** (producer) Constant: [`STRINGTEMPLATE_TEMPLATE`](https://javadoc.io/doc/org.apache.camel/camel-stringtemplate/latest/org/apache/camel/component/stringtemplate/StringTemplateConstants.html#STRINGTEMPLATE_TEMPLATE) | The template to use instead of the endpoint configured. |  | String |

## Usage

### Headers

Camel will store a reference to the resource in the message header with key, `org.apache.camel.stringtemplate.resource`. The Resource is an `org.springframework.core.io.Resource` object.

### String Template Context

Camel will provide exchange information in the String Template context (just a `Map`). The `Exchange` is transferred as:

 
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

### Hot reloading

The string template resource is by default hot-reloadable for both file and classpath resources (expanded jar). If you set `contentCache=true`, Camel loads the resource only once and hot-reloading is not possible. This scenario can be used in production when the resource never changes.

### Dynamic templates

Camel provides two headers by which you can define a different resource location for a template or the template content itself. If any of these headers is set, then Camel uses this over the endpoint configured resource. This allows you to provide a dynamic template at runtime.

### StringTemplate Attributes

You can define the custom context map by setting the message header "**CamelStringTemplateVariableMap**" just like the below code.

_Java-only: setting up a custom StringTemplate variable map_

```java
Map<String, Object> variableMap = new HashMap<String, Object>();
Map<String, Object> headersMap = new HashMap<String, Object>();
headersMap.put("name", "Willem");
variableMap.put("headers", headersMap);
variableMap.put("body", "Monday");
variableMap.put("exchange", exchange);
exchange.getIn().setHeader("CamelStringTemplateVariableMap", variableMap);
```

## Examples

For example, you could use a string template as follows in order to formulate a response to a message:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("string-template:com/acme/MyResponse.tm");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="string-template:com/acme/MyResponse.tm"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: string-template:com/acme/MyResponse.tm
```

### The Email Example

In this sample, we want to use a string template to send an order confirmation email. The email template is laid out in `StringTemplate` as:

Dear <headers.lastName>, <headers.firstName>

Thanks for the order of <headers.item>.

Regards Camel Riders Bookstore
<body>