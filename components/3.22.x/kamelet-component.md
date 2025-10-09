# Kamelet

**Since Camel 3.8**

**Both producer and consumer are supported**

The Kamelet Component provides support for interacting with the [Camel Route Template](../../manual/route-template.md) engine using Endpoint semantic.

## URI format

```none
kamelet:templateId/routeId[?options]
```

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

The Kamelet component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **location** (common) | The location(s) of the Kamelets on the file system. Multiple locations can be set separated by comma. | classpath:/kamelets | String |
| **routeProperties** (common) | Set route local parameters. |  | Map |
| **templateProperties** (common) | Set template local parameters. |  | Map |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **block** (producer) | If sending a message to a kamelet endpoint which has no active consumer, then we can tell the producer to block and wait for the consumer to become active. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **timeout** (producer) | The timeout value to use if block is enabled. | 30000 | long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **routeTemplateLoaderListener** (advanced) | **Autowired** To plugin a custom listener for when the Kamelet component is loading Kamelets from external resources. |  | RouteTemplateLoaderListener |

## Endpoint Options

The Kamelet endpoint is configured using URI syntax:

kamelet:templateId/routeId

with the following path and query parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **templateId** (common) | **Required** The Route Template ID. |  | String |
| **routeId** (advanced) | The Route ID. Default value notice: The ID will be auto-generated if not provided. |  | String |

### Query Parameters (8 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **block** (producer (advanced)) | If sending a message to a direct endpoint which has no active consumer, then we can tell the producer to block and wait for the consumer to become active. | true | boolean |
| **failIfNoConsumers** (producer (advanced)) | Whether the producer should fail by throwing an exception, when sending to a kamelet endpoint with no active consumers. | true | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **timeout** (producer (advanced)) | The timeout value to use if block is enabled. | 30000 | long |
| **location** (advanced) | Location of the Kamelet to use which can be specified as a resource from file system, classpath etc. The location cannot use wildcards, and must refer to a file including extension, for example file:/etc/foo-kamelet.xml. |  | String |
> **Note**
> The **kamelet** endpoint is **lenient**, which means that the endpoint accepts additional parameters that are passed to the [Route Template](../../manual/route-template.md) engine and consumed upon route materialization.

## Discovery

If a [Route Template](../../manual/route-template.md) is not found, the **kamelet** endpoint tries to load the related **kamelet** definition from the file system (by default `classpath:/kamelets`). The default resolution mechanism expect kamelet files to have the extension `.kamelet.yaml`.

## Samples

Kamelets can be used as if they were standard Camel components. For example, suppose that we have created a Route Template as follows:

```java
routeTemplate("setMyBody")
    .templateParameter("bodyValue")
    .from("kamelet:source")
        .setBody().constant("{{bodyValue}}");
```

> **Important**
> To let the **Kamelet** component wiring the materialized route to the caller processor, we need to be able to identify the input and output endpoint of the route and this is done by using `kamelet:source` to mark the input endpoint and `kamelet:sink` for the output endpoint.

Then the template can be instantiated and invoked as shown below:

```java
from("direct:setMyBody")
    .to("kamelet:setMyBody?bodyValue=myKamelet");
```

Behind the scenes, the **Kamelet** component does the following things:

1.  it instantiates a route out of the Route Template identified by the given `templateId` path parameter (in this case `setMyBody`)
    
2.  it will act like the `direct` component and connect the current route to the materialized one.
    

If you had to do it programmatically, it would have been something like:

```java
routeTemplate("setMyBody")
    .templateParameter("bodyValue")
    .from("direct:{{foo}}")
        .setBody().constant("{{bodyValue}}");

TemplatedRouteBuilder.builder(context, "setMyBody")
    .parameter("foo", "bar")
    .parameter("bodyValue", "myKamelet")
    .add();

from("direct:template")
    .to("direct:bar");
```

## Spring Boot Auto-Configuration

When using kamelet with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-kamelet-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.kamelet.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kamelet.block** | If sending a message to a kamelet endpoint which has no active consumer, then we can tell the producer to block and wait for the consumer to become active. | true | Boolean |
| **camel.component.kamelet.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.kamelet.enabled** | Whether to enable auto configuration of the kamelet component. This is enabled by default. |  | Boolean |
| **camel.component.kamelet.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kamelet.location** | The location(s) of the Kamelets on the file system. Multiple locations can be set separated by comma. | classpath:/kamelets | String |
| **camel.component.kamelet.route-properties** | Set route local parameters. |  | Map |
| **camel.component.kamelet.route-template-loader-listener** | To plugin a custom listener for when the Kamelet component is loading Kamelets from external resources. The option is a org.apache.camel.spi.RouteTemplateLoaderListener type. |  | RouteTemplateLoaderListener |
| **camel.component.kamelet.template-properties** | Set template local parameters. |  | Map |
| **camel.component.kamelet.timeout** | The timeout value to use if block is enabled. | 30000 | Long |