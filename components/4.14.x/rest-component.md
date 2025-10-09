# REST

**Since Camel 2.14**

**Both producer and consumer are supported**

The REST component allows defining REST endpoints (consumer) using the Rest DSL and plugin to other Camel components as the REST transport.

The REST component can also be used as a client (producer) to call REST services.

## URI format

rest://method:path\[:uriTemplate\]?\[options\]

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

The REST component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerComponentName** (consumer) | The Camel Rest component to use for the consumer REST transport, such as jetty, servlet, undertow. If no component has been explicitly configured, then Camel will lookup if there is a Camel component that integrates with the Rest DSL, or if a org.apache.camel.spi.RestConsumerFactory is registered in the registry. If either one is found, then that is being used. |  | String |
| **apiDoc** (producer) | The swagger api doc resource to use. The resource is loaded from classpath by default and must be in JSON format. |  | String |
| **host** (producer) | Host and port of HTTP service to use (override host in swagger schema). |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **producerComponentName** (producer) | The Camel Rest component to use for the producer REST transport, such as http, undertow. If no component has been explicitly configured, then Camel will lookup if there is a Camel component that integrates with the Rest DSL, or if a org.apache.camel.spi.RestProducerFactory is registered in the registry. If either one is found, then that is being used. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Endpoint Options

The REST endpoint is configured using URI syntax:

rest:method:path:uriTemplate

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **method** (common) | 
**Required** HTTP method to use.

Enum values:

-   get
    
-   post
    
-   put
    
-   delete
    
-   patch
    
-   head
    
-   trace
    
-   connect
    
-   options
    





 |  | String |
| **path** (common) | **Required** The base path, can use \* as path suffix to support wildcard HTTP route matching. |  | String |
| **uriTemplate** (common) | The uri template. |  | String |

### Query Parameters (16 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **consumes** (common) | Media type such as: 'text/xml', or 'application/json' this REST service accepts. By default we accept all kinds of types. |  | String |
| **inType** (common) | To declare the incoming POJO binding type as a FQN class name. |  | String |
| **outType** (common) | To declare the outgoing POJO binding type as a FQN class name. |  | String |
| **produces** (common) | Media type such as: 'text/xml', or 'application/json' this REST service returns. |  | String |
| **routeId** (common) | Name of the route this REST services creates. |  | String |
| **consumerComponentName** (consumer) | The Camel Rest component to use for the consumer REST transport, such as jetty, servlet, undertow. If no component has been explicitly configured, then Camel will lookup if there is a Camel component that integrates with the Rest DSL, or if a org.apache.camel.spi.RestConsumerFactory is registered in the registry. If either one is found, then that is being used. |  | String |
| **description** (consumer) | Human description to document this REST service. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **apiDoc** (producer) | The openapi api doc resource to use. The resource is loaded from classpath by default and must be in JSON format. |  | String |
| **bindingMode** (producer) | 

Configures the binding mode for the producer. If set to anything other than 'off' the producer will try to convert the body of the incoming message from inType to the json or xml, and the response from json or xml to outType.

Enum values:

-   auto
    
-   off
    
-   json
    
-   xml
    
-   json\_xml
    





 |  | RestBindingMode |
| **host** (producer) | Host and port of HTTP service to use (override host in openapi schema). |  | String |
| **producerComponentName** (producer) | The Camel Rest component to use for the producer REST transport, such as http, undertow. If no component has been explicitly configured, then Camel will lookup if there is a Camel component that integrates with the Rest DSL, or if a org.apache.camel.spi.RestProducerFactory is registered in the registry. If either one is found, then that is being used. |  | String |
| **queryParameters** (producer) | Query parameters for the HTTP service to call. The query parameters can contain multiple parameters separated by ampersand such such as foo=123&bar=456. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The REST component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelRestHttpQuery** (producer) Constant: [`REST_HTTP_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-rest/latest/org/apache/camel/component/rest/RestConstants.html#REST_HTTP_QUERY) | The query parameters for the rest call to be used. |  | String |
| **CamelRestHttpUri** (producer) Constant: [`REST_HTTP_URI`](https://javadoc.io/doc/org.apache.camel/camel-rest/latest/org/apache/camel/component/rest/RestConstants.html#REST_HTTP_URI) | The http uri for the rest call to be used. |  | String |
| **CamelHttpMethod** (producer) Constant: [`HTTP_METHOD`](https://javadoc.io/doc/org.apache.camel/camel-rest/latest/org/apache/camel/component/rest/RestConstants.html#HTTP_METHOD) | The method should be in upper case. |  | String |
| **Content-Type** (producer) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-rest/latest/org/apache/camel/component/rest/RestConstants.html#CONTENT_TYPE) | The media type such as: 'text/xml', or 'application/json' this REST service returns. |  | String |
| **Accept** (producer) Constant: [`ACCEPT`](https://javadoc.io/doc/org.apache.camel/camel-rest/latest/org/apache/camel/component/rest/RestConstants.html#ACCEPT) | The media type such as: 'text/xml', or 'application/json' this REST service accepts. |  | String |
| **CamelHttpResponseCode** (producer) Constant: [`HTTP_RESPONSE_CODE`](https://javadoc.io/doc/org.apache.camel/camel-rest/latest/org/apache/camel/component/rest/RestConstants.html#HTTP_RESPONSE_CODE) | The http response code. |  | Integer |

## Supported REST components

The following components support the REST consumer (Rest DSL):

-   camel-netty-http
    
-   camel-jetty
    
-   camel-servlet
    
-   camel-undertow
    
-   camel-platform-http
    

The following components support the REST producer:

-   camel-http
    
-   camel-netty-http
    
-   camel-undertow
    
-   camel-vertx-http
    

## Usage

### Path and uriTemplate syntax

The path and uriTemplate option is defined using a REST syntax where you define the REST context path using support for parameters.

> **Tip**
> If no uriTemplate is configured then `path` option works the same way.
>
> It does not matter if you configure only `path` or if you configure both options. Though configuring both a path and uriTemplate is a more common practice with REST.

The following is a Camel route using a path only

```java
from("rest:get:hello")
  .transform().constant("Bye World");
```

And the following route uses a parameter which is mapped to a Camel header with the key "me".

```java
from("rest:get:hello/{me}")
  .transform().simple("Bye ${header.me}");
```

The following examples have configured a base path as "hello" and then have two REST services configured using uriTemplates.

```java
from("rest:get:hello:/{me}")
  .transform().simple("Hi ${header.me}");

from("rest:get:hello:/french/{me}")
  .transform().simple("Bonjour ${header.me}");
```

## Examples

### Rest producer examples

You can use the REST component to call REST services like any other Camel component.

For example, to call a REST service on using `hello/{me}` you can do

```java
from("direct:start")
  .to("rest:get:hello/{me}");
```

And then the dynamic value `{me}` is mapped to a header or variable with the same name. So to call this REST service, you can send an empty message body and a header as shown:

```java
template.sendBodyAndHeader("direct:start", null, "me", "Donald Duck");
```

Instead of a header you can also use exchange variable such as:

```java
String response = template.withVariable("me", "Donald Duck").to("direct:start").request(String.class);
```

The Rest producer needs to know the hostname and port of the REST service, which you can configure using the host option as shown:

```java
from("direct:start")
  .to("rest:get:hello/{me}?host=myserver:8080/foo");
```

Instead of using the host option, you can configure the host on the `restConfiguration` as shown:

```java
restConfiguration().host("myserver:8080/foo");

from("direct:start")
  .to("rest:get:hello/{me}");
```

You can use the `producerComponent` to select which Camel component to use as the HTTP client, for example to use http, you can do:

```java
restConfiguration().host("myserver:8080/foo").producerComponent("http");

from("direct:start")
  .to("rest:get:hello/{me}");
```

### Rest producer binding

The REST producer supports binding using JSON or XML like the rest-dsl does.

For example, to use jetty with JSON binding mode turned on, you can configure this in the REST configuration:

```java
restConfiguration().component("jetty").host("localhost").port(8080).bindingMode(RestBindingMode.json);

from("direct:start")
  .to("rest:post:user");
```

Then when calling the REST service using the REST producer, it will automatically bind any POJOs to JSON before calling the REST service:

```java
  UserPojo user = new UserPojo();
  user.setId(123);
  user.setName("Donald Duck");

  template.sendBody("direct:start", user);
```

In the example above we send a POJO instance `UserPojo` as the message body. And because we have turned on JSON binding in the REST configuration, then the POJO will be marshalled from POJO to JSON before calling the REST service.

However, if you want to also perform binding for the response message (e.g., what the REST service sends back, as response) you would need to configure the `outType` option to specify what is the class name of the POJO to unmarshal from JSON to POJO.

For example, if the REST service returns a JSON payload that binds to `com.foo.MyResponsePojo` you can configure this as shown:

```java
  restConfiguration().component("jetty").host("localhost").port(8080).bindingMode(RestBindingMode.json);

  from("direct:start")
    .to("rest:post:user?outType=com.foo.MyResponsePojo");
```

> **Important**
> You must configure `outType` option if you want POJO binding to happen for the response messages received from calling the REST service.

### More examples

See Rest DSL, which offers more examples and how you can use the Rest DSL to define those in a nicer, restful way.

There is a **camel-example-servlet-rest-tomcat** example in the Apache Camel distribution, that demonstrates how to use the Rest DSL with Servlet as transport that can be deployed on Apache Tomcat, or similar web containers.

## Spring Boot Auto-Configuration

When using rest with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-rest-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 13 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.rest-api.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.rest-api.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.rest-api.consumer-component-name** | The Camel Rest API component to use for the consumer REST transport, such as jetty, servlet, undertow. If no component has been explicitly configured, then Camel will lookup if there is a Camel component that integrates with the Rest DSL, or if a org.apache.camel.spi.RestApiConsumerFactory is registered in the registry. If either one is found, then that is being used. |  | String |
| **camel.component.rest-api.enabled** | Whether to enable auto configuration of the rest-api component. This is enabled by default. |  | Boolean |
| **camel.component.rest.api-doc** | The swagger api doc resource to use. The resource is loaded from classpath by default and must be in JSON format. |  | String |
| **camel.component.rest.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.rest.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.rest.consumer-component-name** | The Camel Rest component to use for the consumer REST transport, such as jetty, servlet, undertow. If no component has been explicitly configured, then Camel will lookup if there is a Camel component that integrates with the Rest DSL, or if a org.apache.camel.spi.RestConsumerFactory is registered in the registry. If either one is found, then that is being used. |  | String |
| **camel.component.rest.enabled** | Whether to enable auto configuration of the rest component. This is enabled by default. |  | Boolean |
| **camel.component.rest.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.rest.host** | Host and port of HTTP service to use (override host in swagger schema). |  | String |
| **camel.component.rest.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.rest.producer-component-name** | The Camel Rest component to use for the producer REST transport, such as http, undertow. If no component has been explicitly configured, then Camel will lookup if there is a Camel component that integrates with the Rest DSL, or if a org.apache.camel.spi.RestProducerFactory is registered in the registry. If either one is found, then that is being used. |  | String |