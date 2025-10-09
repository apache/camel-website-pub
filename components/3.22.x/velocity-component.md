# Velocity

**Since Camel 1.2**

**Only producer is supported**

The Velocity component allows you to process a message using an [Apache Velocity](http://velocity.apache.org/) template. This can be ideal when using Templating to generate responses for requests.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-velocity</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

velocity:templateName\[?options\]

Where **templateName** is the classpath-local URI of the template to invoke; or the complete URL of the remote template (eg: file://folder/myfile.vm).

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Velocity component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **velocityEngine** (advanced) | To use the VelocityEngine otherwise a new engine is created. |  | VelocityEngine |

## Endpoint Options

The Velocity endpoint is configured using URI syntax:

velocity:resourceUri

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **resourceUri** (producer) | **Required** Path to the resource. You can prefix with: classpath, file, http, ref, or bean. classpath, file and http loads the resource using these protocols (classpath is default). ref will lookup the resource in the registry. bean will call a method on a bean to be used as the resource. For bean you can specify the method name after dot, eg bean:myBean.myMethod. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **allowContextMapAll** (producer) | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | boolean |
| **allowTemplateFromHeader** (producer) | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | boolean |
| **contentCache** (producer) | Sets whether to use resource content cache or not. | false | boolean |
| **encoding** (producer) | Character encoding of the resource content. |  | String |
| **loaderCache** (producer) | Enables / disables the velocity resource loader cache which is enabled by default. | true | boolean |
| **propertiesFile** (producer) | The URI of the properties file which is used for VelocityEngine initialization. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Velocity component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelVelocityResourceUri** (producer) Constant: [`VELOCITY_RESOURCE_URI`](https://javadoc.io/doc/org.apache.camel/camel-velocity/latest/org/apache/camel/component/velocity/VelocityConstants.html#VELOCITY_RESOURCE_URI) | The name of the velocity template. |  | String |
| **CamelVelocityTemplate** (producer) Constant: [`VELOCITY_TEMPLATE`](https://javadoc.io/doc/org.apache.camel/camel-velocity/latest/org/apache/camel/component/velocity/VelocityConstants.html#VELOCITY_TEMPLATE) | The content of the velocity template. |  | String |
| **CamelVelocityContext** (producer) Constant: [`VELOCITY_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-velocity/latest/org/apache/camel/component/velocity/VelocityConstants.html#VELOCITY_CONTEXT) | The velocity context to use. |  | Context |
| **CamelVelocitySupplementalContext** (producer) Constant: [`VELOCITY_SUPPLEMENTAL_CONTEXT`](https://javadoc.io/doc/org.apache.camel/camel-velocity/latest/org/apache/camel/component/velocity/VelocityConstants.html#VELOCITY_SUPPLEMENTAL_CONTEXT) | To add additional information to the used VelocityContext. The value of this header should be a Map with key/values that will added (override any existing key with the same name). This can be used to pre setup some common key/values you want to reuse in your velocity endpoints. |  | Map |

Headers set during the Velocity evaluation are returned to the message and added as headers. Then it is possible to return values from Velocity to the Message.

For example, to set the header value of `fruit` in the Velocity template `.tm`:

$in.setHeader("fruit", "Apple")

The `fruit` header is now accessible from the `message.out.headers`.

## Velocity Context

Camel will provide exchange information in the Velocity context (just a `Map`). The `Exchange` is transfered as:

 
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

You can setup a custom Velocity Context yourself by setting the message header \*CamelVelocityContext \*just like this

```java
VelocityContext velocityContext = new VelocityContext(variableMap);
exchange.getIn().setHeader("CamelVelocityContext", velocityContext);
```

## Hot reloading

The Velocity template resource is, by default, hot reloadable for both file and classpath resources (expanded jar). If you set `contentCache=true`, Camel will only load the resource once, and thus hot reloading is not possible. This scenario can be used in production, when the resource never changes.

## Dynamic templates

**Since Camel 2.1**  
Camel provides two headers by which you can define a different resource location for a template or the template content itself. If any of these headers is set then Camel uses this over the endpoint configured resource. This allows you to provide a dynamic template at runtime.

  
| Header | Type | Description |
| --- | --- | --- |
| CamelVelocityResourceUri | String | A URI for the template resource to use instead of the endpoint configured. |
| CamelVelocityTemplate | String | The template to use instead of the endpoint configured. |

## Samples

For example you could use something like

```java
from("activemq:My.Queue").
  to("velocity:com/acme/MyResponse.vm");
```

To use a Velocity template to formulate a response to a message for InOut message exchanges (where there is a `JMSReplyTo` header).

If you want to use InOnly and consume the message and send it to another destination, you could use the following route:

```java
from("activemq:My.Queue").
  to("velocity:com/acme/MyResponse.vm").
  to("activemq:Another.Queue");
```

And to use the content cache, e.g. for use in production, where the `.vm` template never changes:

```java
from("activemq:My.Queue").
  to("velocity:com/acme/MyResponse.vm?contentCache=true").
  to("activemq:Another.Queue");
```

And a file based resource:

```java
from("activemq:My.Queue").
  to("velocity:file://myfolder/MyResponse.vm?contentCache=true").
  to("activemq:Another.Queue");
```

It’s possible to specify what template the component should use dynamically via a header, so for example:

```java
from("direct:in").
  setHeader("CamelVelocityResourceUri").constant("path/to/my/template.vm").
  to("velocity:dummy?allowTemplateFromHeader=true"");
```

It’s possible to specify a template directly as a header the component should use dynamically via a header, so for example:

```java
from("direct:in").
  setHeader("CamelVelocityTemplate").constant("Hi this is a velocity template that can do templating ${body}").
  to("velocity:dummy?allowTemplateFromHeader=true"");
```

## The Email Sample

In this sample we want to use Velocity templating for an order confirmation email. The email template is laid out in Velocity as:

letter.vm

```text
Dear ${headers.lastName}, ${headers.firstName}

Thanks for the order of ${headers.item}.

Regards Camel Riders Bookstore
${body}
```

And the java code (from an unit test):

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
    public void testVelocityLetter() throws Exception {
        MockEndpoint mock = getMockEndpoint("mock:result");
        mock.expectedMessageCount(1);
        mock.message(0).body(String.class).contains("Thanks for the order of Camel in Action");

        template.send("direct:a", createLetter());

        mock.assertIsSatisfied();
    }

    @Override
    protected RouteBuilder createRouteBuilder() {
        return new RouteBuilder() {
            public void configure() {
                from("direct:a")
                    .to("velocity:org/apache/camel/component/velocity/letter.vm")
                    .to("mock:result");
            }
        };
    }
```

## Spring Boot Auto-Configuration

When using velocity with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-velocity-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.velocity.allow-context-map-all** | Sets whether the context map should allow access to all details. By default only the message body and headers can be accessed. This option can be enabled for full access to the current Exchange and CamelContext. Doing so impose a potential security risk as this opens access to the full power of CamelContext API. | false | Boolean |
| **camel.component.velocity.allow-template-from-header** | Whether to allow to use resource template from header or not (default false). Enabling this allows to specify dynamic templates via message header. However this can be seen as a potential security vulnerability if the header is coming from a malicious user, so use this with care. | false | Boolean |
| **camel.component.velocity.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.velocity.enabled** | Whether to enable auto configuration of the velocity component. This is enabled by default. |  | Boolean |
| **camel.component.velocity.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.velocity.velocity-engine** | To use the VelocityEngine otherwise a new engine is created. The option is a org.apache.velocity.app.VelocityEngine type. |  | VelocityEngine |