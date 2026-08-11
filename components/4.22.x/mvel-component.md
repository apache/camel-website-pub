# MVEL

**Since Camel 2.12**

**Only producer is supported**

The MVEL component allows you to process a message using an [MVEL](http://mvel.documentnode.com/) template. This can be ideal when using templating to generate responses for requests.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-mvel</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

mvel:templateName\[?options\]

Where **templateName** is the classpath-local URI of the template to invoke; or the complete URL of the remote template (e.g.: `file://folder/myfile.mvel`).

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

The MVEL component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The MVEL endpoint is configured using URI syntax:

mvel:resourceUri

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
| **encoding** (producer) | Character encoding of the resource content. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The MVEL component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelMvelResourceUri** (producer) Constant: [`MVEL_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-mvel/latest/org/apache/camel/component/mvel/MvelConstants.html#MVEL_RESOURCE_URI) | A URI for the template resource to use instead of the endpoint configured. |  | String |
| **CamelMvelTemplate** (producer) Constant: [`MVEL_TEMPLATE`](https://javadoc.io/doc/org.apache.camel/camel-mvel/latest/org/apache/camel/component/mvel/MvelConstants.html#MVEL_TEMPLATE) | The template to use instead of the endpoint configured. |  | String |

## Usage

### MVEL Context

Camel will provide exchange information in the MVEL context (just a `Map`). The `Exchange` is transferred as:

 
| key | value |
| --- | --- |
| `` `exchange` `` | The `Exchange` itself |
| `` `exchange.properties` `` | The `Exchange` properties |
| `` `variables` `` | The variables |
| `` `headers` `` | The headers of the message |
| `` `camelContext` `` | The `CamelContext` |
| `` `request` `` | The message |
| `` `in` `` | The message |
| `` `body` `` | The message body |
| `` `out` `` | The Out message (only for InOut message exchange pattern). |
| `` `response` `` | The Out message (only for InOut message exchange pattern). |

### Hot reloading

The mvel template resource is, by default, hot reloadable for both file and classpath resources (expanded jar). If you set `contentCache=true`, Camel will only load the resource once, and thus hot reloading is not possible. This scenario can be used in production when the resource never changes.

### Dynamic templates

Camel provides two headers by which you can define a different resource location for a template, or the template content itself. If any of these headers is set, then Camel uses this over the endpoint configured resource. This allows you to provide a dynamic template at runtime.

## Examples

For example, you could use something like

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:My.Queue")
    .to("mvel:com/acme/MyResponse.mvel");
```

```xml
<route>
  <from uri="activemq:My.Queue"/>
  <to uri="mvel:com/acme/MyResponse.mvel"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:My.Queue
      steps:
        - to:
            uri: mvel:com/acme/MyResponse.mvel
```

To use a MVEL template to formulate a response to a message for InOut message exchanges (where there is a `JMSReplyTo` header).

To specify what template the component should use dynamically via a header, so for example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .setHeader("CamelMvelResourceUri").constant("path/to/my/template.mvel")
    .to("mvel:dummy?allowTemplateFromHeader=true");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMvelResourceUri">
    <constant>path/to/my/template.mvel</constant>
  </setHeader>
  <to uri="mvel:dummy?allowTemplateFromHeader=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelMvelResourceUri
            expression:
              constant:
                expression: path/to/my/template.mvel
        - to:
            uri: mvel:dummy
            parameters:
              allowTemplateFromHeader: true
```

To specify a template directly as a header, the component should use dynamically via a header, so for example:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:in")
    .setHeader("CamelMvelTemplate").constant("@{\"The result is \" + request.body * 3}\" }")
    .to("mvel:dummy?allowTemplateFromHeader=true");
```

```xml
<route>
  <from uri="direct:in"/>
  <setHeader name="CamelMvelTemplate">
    <constant>@{"The result is " + request.body * 3}" }</constant>
  </setHeader>
  <to uri="mvel:dummy?allowTemplateFromHeader=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:in
      steps:
        - setHeader:
            name: CamelMvelTemplate
            expression:
              constant:
                expression: "@{\"The result is \" + request.body * 3}\" }"
        - to:
            uri: mvel:dummy
            parameters:
              allowTemplateFromHeader: true
```