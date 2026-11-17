# Direct

**Since Camel 1.0**

**Both producer and consumer are supported**

The Direct component provides direct, synchronous invocation of any consumers when a producer sends a message exchange. This endpoint can be used to connect existing routes in the **same** camel context.

> **Tip**
> **Asynchronous**
>
> The [SEDA](seda-component.md) component provides asynchronous invocation of any consumers when a producer sends a message exchange.

## URI format

direct:someId\[?options\]

Where _someId_ can be any string to uniquely identify the endpoint.

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

The Direct component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **block** (producer) | If sending a message to a direct endpoint which has no active consumer, then we can tell the producer to block and wait for the consumer to become active. | true | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **timeout** (producer) | The timeout value to use if block is enabled. | 30000 | long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Direct endpoint is configured using URI syntax:

direct:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** Name of direct endpoint. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **block** (producer) | If sending a message to a direct endpoint which has no active consumer, then we can tell the producer to block and wait for the consumer to become active. | true | boolean |
| **failIfNoConsumers** (producer) | Whether the producer should fail by throwing an exception, when sending to a DIRECT endpoint with no active consumers. | true | boolean |
| **timeout** (producer) | The timeout value to use if block is enabled. | 30000 | long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **synchronous** (advanced) | Whether synchronous processing is forced. If enabled, then the producer thread will be forced to wait until the message has been completed before the same thread will continue processing. If disabled, the default, then the producer thread may be freed and can do other work while the message is continued processed by other threads (reactive). | false | boolean |

## Message Body

The message body at each side of the Direct component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `unchanged` | The body the caller sent. |
| **Producer input** | `any` | 
 |
| **Producer output** | `unknown` | The body the route it calls ends with. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

The route that consumes from a direct endpoint runs in the thread of the producer, and the producer continues with the message as that route leaves it. A direct endpoint is therefore called like a method: from Java code, call a route with `requestBody` of a [ProducerTemplate](../../manual/producertemplate.md) to get its reply:

```java
String reply = template.requestBody("direct:processOrder", order, String.class);
```

### One route per endpoint

Only one route can consume from a direct endpoint. A second route that consumes from the same endpoint fails to start with `Multiple consumers for the same endpoint is not allowed: direct://processOrder`. To send a message to several routes, use the [Multicast](eips/multicast-eip.md) or [Recipient List](eips/recipientList-eip.md) EIP, or the [SEDA](seda-component.md) component with `multipleConsumers=true`.

### When no route consumes from the endpoint

When no started route consumes from the endpoint, the producer waits up to `timeout` milliseconds (30 seconds by default) for one to start, for example while Camel starts or reloads routes. Then the exchange fails with `DirectConsumerNotAvailableException`. Its message starts with `No consumers available on endpoint:`, and says which route consumes from the endpoint and its status, or that no route does (with a similar endpoint name when there is one), and how long the producer waited.

Set `block=false` to fail without waiting, or `failIfNoConsumers=false` to drop the message (logged at `DEBUG`) instead of failing.

The common causes are:

-   The route is not loaded. With Spring Boot, the `RouteBuilder` class must be a Spring bean, for example annotated with `@Component`. With Camel Quarkus, a `RouteBuilder` class from another jar is only found when that jar has a Jandex index. XML and YAML routes must be in the files Camel loads routes from.
    
-   The producer and the route use a different name, for example because of a typo.
    
-   The route is stopped or suspended, or it did not start because of `autoStartup=false`.
    
-   The route is in another CamelContext: a direct endpoint only reaches the routes of its own CamelContext.
    
-   With the [Rest DSL](../../manual/rest-dsl.md), a direct route that only one REST service calls is inlined into that service (the `inlineRoutes` option, enabled by default), so other routes cannot call it.
    

> **Note**
> A `ProducerTemplate` sends only once the CamelContext has started. Sending earlier, for example from a Spring `@PostConstruct` method, fails with another exception, before any direct endpoint is called.

## Examples

In the route below, we use the direct component to link the two routes together:

-   Java
    
-   XML
    
-   YAML
    

```java
from("activemq:queue:order.in")
    .to("bean:orderService?method=validate")
    .to("direct:processOrder");

from("direct:processOrder")
    .to("bean:orderService?method=process")
    .to("activemq:queue:order.out");
```

```xml
<route>
 <from uri="activemq:queue:order.in"/>
 <to uri="bean:orderService?method=validate"/>
 <to uri="direct:processOrder"/>
</route>

<route>
 <from uri="direct:processOrder"/>
 <to uri="bean:orderService?method=process"/>
 <to uri="activemq:queue:order.out"/>
</route>
```

```yaml
- route:
    from:
      uri: activemq:queue:order.in
      steps:
        - to:
            uri: bean:orderService
            parameters:
              method: validate
        - to:
            uri: direct:processOrder
- route:
    from:
      uri: direct:processOrder
      steps:
        - to:
            uri: bean:orderService
            parameters:
              method: process
        - to:
            uri: activemq:queue:order.out
```

See also samples from the [SEDA](seda-component.md) component, how they can be used together.