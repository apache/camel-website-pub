# Dynamic Router

**Since Camel 3.15**

**Only producer is supported**

The Dynamic Router Component is an implementation of the Dynamic Router EIP. Participants may send subscription messages over a special control channel, at runtime, to specify the conditions under which messages are routed to their endpoint (also provided in the control channel message). In this way, the Dynamic Router is an extension of the content-based router EIP. When a recipient wishes to remove itself, it can also send a message to unsubscribe.

Note that, while Camel Core contains an implementation of the Dynamic Router EIP, this component is a completely separate implementation that aims to be a closer reflection of the EIP description. The main differences between the Core implementation and this component implementation are as follows:

_Control Channel_

A reserved communication channel by which routing participants can subscribe or unsubscribe to receiving messages that meet their criteria.

-   **core**: does not have a communication channel for control messages. Perhaps the "re-circulation" behavior, discussed below, is the core Dynamic Router’s control channel interpretation.
    
-   **component**: provides a control channel for participants to subscribe and unsubscribe with control messages that contain a `Predicate` to determine `Exchange` suitability, and the `Endpoint` URI that a matching `Exchange` will be sent to.
    

_Dynamic Rule Base_

The Dynamic Router should have a list of routing recipients' criteria that define the terms under which an exchange is suitable for them to receive.

-   **core**: implements a dynamic version of a `Routing Slip` for this purpose, but that is not inherently dynamic in terms of its content. If the content of this slip is dynamic, it will be up to the user to define and implement that capability.
    
-   **component**: builds the rule base at runtime, and maintains it as participants subscribe or unsubscribe via the control channel.
    

_Message Re-Circulation_

The Dynamic Router EIP description does not specify any message re-circulation behavior.

-   **core**: provides a feature that continuously routes the exchange to a recipient, then back through the dynamic router, until a recipient returns `null` to signify routing termination. This may be an interpretation of the control channel feature.
    
-   **component**: does not provide a re-circulation feature. If this is the desired behavior, the user will have to define and implement this behavior. E.g., create a simple route to send a response back through the Dynamic Router under some condition(s).
    

For some use cases, the core Dynamic Router will be more appropriate. In other cases, the Dynamic Router Component will be a better fit.

## URI format

dynamic-router:channel\[?options\]

The `channel` is the routing channel that allows messaging to be logically separate from other channels. Any string that can be included in a URI is a valid channel name. Each channel can have a set of participant subscriptions, and can consume messages to be routed to appropriate recipients. The only reserved channel is the `control` channel. This is a single channel that handles control messages for participants to subscribe or unsubscribe for messaging over a desired channel.

These messages will be described in greater detail below, with examples.

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

The Dynamic Router component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Dynamic Router endpoint is configured using URI syntax:

dynamic-router:channel

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **channel** (producer) | Channel for the Dynamic Router. For example, if the Dynamic Router URI is dynamic-router://test, then the channel is test. Channels are a way of keeping routing participants, their rules, and exchanges logically separate from the participants, rules, and exchanges on other channels. This can be seen as analogous to VLANs in networking. |  | String |

### Query Parameters (20 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **aggregationStrategy** (common) | Refers to an AggregationStrategy to be used to assemble the replies from the multicasts, into a single outgoing message from the Multicast. By default, Camel will use the last reply as the outgoing message. You can also use a POJO as the AggregationStrategy. |  | String |
| **aggregationStrategyBean** (common) | Refers to an AggregationStrategy to be used to assemble the replies from the multicasts, into a single outgoing message from the Multicast. By default, Camel will use the last reply as the outgoing message. You can also use a POJO as the AggregationStrategy. |  | AggregationStrategy |
| **aggregationStrategyMethodAllowNull** (common) | If this option is false then the aggregate method is not used if there was no data to enrich. If this option is true then null values is used as the oldExchange (when no data to enrich), when using POJOs as the AggregationStrategy. | false | boolean |
| **aggregationStrategyMethodName** (common) | You can use a POJO as the AggregationStrategy. This refers to the name of the method that aggregates the exchanges. |  | String |
| **cacheSize** (common) | When caching producer endpoints, this is the size of the cache. Default is 100. | 100 | int |
| **executorService** (common) | Refers to a custom Thread Pool to be used for parallel processing. Notice that, if you set this option, then parallel processing is automatically implied, and you do not have to enable that option in addition to this one. |  | String |
| **executorServiceBean** (common) | Refers to a custom Thread Pool to be used for parallel processing. Notice that, if you set this option, then parallel processing is automatically implied, and you do not have to enable that option in addition to this one. |  | ExecutorService |
| **ignoreInvalidEndpoints** (common) | Ignore the invalid endpoint exception when attempting to create a producer with an invalid endpoint. | false | boolean |
| **onPrepare** (common) | Uses the Processor when preparing the org.apache.camel.Exchange to be sent. This can be used to deep-clone messages that should be sent, or to provide any custom logic that is needed before the exchange is sent. This is the name of a bean in the registry. |  | String |
| **onPrepareProcessor** (common) | Uses the Processor when preparing the org.apache.camel.Exchange to be sent. This can be used to deep-clone messages that should be sent, or to provide any custom logic that is needed before the exchange is sent. This is a Processor instance. |  | Processor |
| **parallelAggregate** (common) | If enabled then the aggregate method on AggregationStrategy can be called concurrently. Notice that this would require the implementation of AggregationStrategy to be implemented as thread-safe. By default, this is false, meaning that Camel synchronizes the call to the aggregate method. Though, in some use-cases, this can be used to archive higher performance when the AggregationStrategy is implemented as thread-safe. | false | boolean |
| **parallelProcessing** (common) | If enabled, then sending via multicast occurs concurrently. Note that the caller thread will still wait until all messages have been fully processed before it continues. It is only the sending and processing of the replies from the multicast recipients that happens concurrently. When parallel processing is enabled, then the Camel routing engine will continue processing using the last used thread from the parallel thread pool. However, if you want to use the original thread that called the multicast, then make sure to enable the synchronous option as well. | false | boolean |
| **recipientMode** (common) | 
Recipient mode: firstMatch or allMatch.

Enum values:

-   firstMatch
    
-   allMatch
    





 | firstMatch | String |
| **shareUnitOfWork** (common) | Shares the org.apache.camel.spi.UnitOfWork with the parent and each of the sub messages. Multicast will, by default, not share a unit of work between the parent exchange and each multicasted exchange. This means each sub exchange has its own individual unit of work. | false | boolean |
| **stopOnException** (common) | Will stop further processing if an exception or failure occurred during processing of an org.apache.camel.Exchange and the caused exception will be thrown. Will also stop if processing the exchange failed (has a fault message), or an exception was thrown and handled by the error handler (such as using onException). In all situations, the multicast will stop further processing. This is the same behavior as in the pipeline that is used by the routing engine. The default behavior is to not stop, but to continue processing until the end. | false | boolean |
| **streaming** (common) | If enabled, then Camel will process replies out-of-order (e.g., in the order they come back). If disabled, Camel will process replies in the same order as defined by the multicast. | false | boolean |
| **synchronous** (common) | Sets whether synchronous processing should be strictly used. When enabled then the same thread is used to continue routing after the multicast is complete, even if parallel processing is enabled. | false | boolean |
| **timeout** (common) | Sets a total timeout specified in millis, when using parallel processing. If the Dynamic Router hasn’t been able to send and process all replies within the given timeframe, then the timeout triggers and the Dynamic Router breaks out and continues. The timeout method is invoked before breaking out. If the timeout is reached with running tasks still remaining, certain tasks for which it is difficult for Camel to shut down in a graceful manner may continue to run. So use this option with a bit of care. | \-1 | long |
| **warnDroppedMessage** (common) | Flag to log a warning if no predicates match for an exchange. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Usage

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-dynamic-router</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

Gradle users will need to add the following dependency to their `build.gradle` for this component:

```groovy
implementation group: 'org.apache.camel', name: 'camel-dynamic-router', version: 'x.x.x'
// use the same version as your Camel core version
```

The Dynamic Router component is used in the same way that other components are used. Include the dynamic-router URI as a consumer in a route, along with the channel name.

-   Java
    
-   XML
    
-   YAML
    

Example Java DSL Route Definition

```java
// Send a message to the Dynamic Router channel named "orders"
from("direct:start").to("dynamic-router:orders");
```

Example XML Route Definition

```xml
<route>
   <from uri="direct:start"/>
   <to uri="dynamic-router:orders"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: dynamic-router:orders
```

## Examples

The benefit of the Dynamic Router EIP Component can best be seen, perhaps, through looking at some use cases. These examples are not the only possibilities with this component, but they show the basics of two main usages — message routing within a single JVM, and message routing across multiple JVMs.

### Dynamic Router within a single JVM or Application

The Dynamic Router EIP component can receive messages from a single source and dispatch them to interested recipients. If we have a simple point-of-sale application, we might have services that:

1.  Process orders
    
2.  Adjust inventory counts
    
3.  Process returns
    

For the purpose of this example, the exact steps that each service carries out are not as important as the fact that each service needs to be notified that it needs to do something under the right condition(s). So, each service will subscribe to participate in routing:

Orders processing service subscription

```java
DynamicRouterControlMessage controlMessage = DynamicRouterControlMessage.newBuilder()
    .subscribeChannel("orders")
    .subscriptionId("orderProcessing")
    .destinationUri("direct:orders")
    .priority(5)
    .predicate("{(headers.command == 'processOrder'}")
    .expressionLanguage("simple")
    .build();
producerTemplate.sendBody("dynamic-router-control:subscribe", controlMessage);
```

Inventory service subscription

```java
DynamicRouterControlMessage controlMessage = DynamicRouterControlMessage.newBuilder()
    .subscribeChannel("orders")
    .subscriptionId("inventoryProcessing")
    .destinationUri("direct:orders")
    .priority(5)
    .predicate("{headers.command == 'processOrder' or headers.command == 'processReturn'}")
    .expressionLanguage("simple")
    .build();
producerTemplate.sendBody("dynamic-router-control:subscribe", controlMessage);
```

Returns processing service subscription

```java
DynamicRouterControlMessage controlMessage = DynamicRouterControlMessage.newBuilder()
    .subscribeChannel("orders")
    .subscriptionId("orderProcessing")
    .destinationUri("direct:orders")
    .priority(5)
    .predicate("{(headers.command == 'processReturn'}")
    .expressionLanguage("simple")
    .build();
producerTemplate.sendBody("dynamic-router-control:subscribe", controlMessage);
```

Above, we have the Orders service subscribing for all messages where the `command` header is "processOrder", and the Returns service subscribing for all messages where the `command` header is "processReturn". The Inventory service is interested in **both** types of messages, since it must deduct from the inventory when an order request comes through, and it must add to inventory counts when a return request comes through. So, for either type of message, two services will be notified.

The order messages get sent to the dynamic router:

Routing order/return request messages

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .process(myOrderProcessor)
    .to("dynamic-router:orders");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="bean:myOrderProcessor"/>
  <to uri="dynamic-router:orders"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: bean:myOrderProcessor
        - to:
            uri: dynamic-router:orders
```

Note the `.process(myOrderProcessor)` step. If incoming messages need to be validated, enriched, transformed, or otherwise augmented, that can be done before the Dynamic Router receives the message. Then, when the Dynamic Router receives a message, it checks the `Exchange` against all subscriptions for the _orders_ channel to determine if it is suitable for any of the recipients. Orders should have a header (`command` → `processOrder`), so the message will be routed to the _orders_ service, and the inventory service. The system will process the order details, and then the inventory service will deduct from merchandize counts. Likewise, returns should have a header (`command` → `processReturn`), so the message will be routed to the returns service, where the return details will be processed, and the inventory service will increase the relevant merchandise counts.

#### Further learning: a complete Spring Boot example

In the `camel-spring-boot-examples` project, the `dynamic-router-eip` module serves as a complete example in this category that you can run and/or experiment with to get a practical feel for how you might use this in your own single-JVM application.

### Dynamic Router across multiple JVMs or Applications

The Dynamic Router EIP component is particularly well-suited to serve as the primary orchestration mechanism between various applications and services that comprise an application stack. Note that the Dynamic Router cannot achieve this by itself, and that some other transport is required to allow messages to pass between services that exist in separate JVMs. For example, a message transport implementation like Kafka, Artemis, or Protocol Buffers, could be used.

Let’s look at the point-of-sale example in a different context. In a microservice architecture, this system would have several separate application modules, with the orders service, inventory service, and returns service, contained within their own microservice (application). Similar to the single-JVM example, all services will subscribe, but they will need to send their subscriptions through a transport that can communicate to another JVM. Their subscriptions might look like:

Orders processing service subscription

```java
DynamicRouterControlMessage controlMessage = DynamicRouterControlMessage.newBuilder()
    .subscribeChannel("orders")
    .subscriptionId("orderProcessing")
    .destinationUri("direct:orders")
    .priority(5)
    .predicate("{(headers.command == 'processOrder'}")
    .expressionLanguage("simple")
    .build();
ObjectMapper mapper = new ObjectMapper(new JsonFactory());
producerTemplate.sendBody("kafka://subscriptions", mapper.writeValueAsString(controlMessage));
```

Inventory service subscription

```java
DynamicRouterControlMessage controlMessage = DynamicRouterControlMessage.newBuilder()
    .subscribeChannel("orders")
    .subscriptionId("inventoryProcessing")
    .destinationUri("direct:orders")
    .priority(5)
    .predicate("{headers.command == 'processOrder' or headers.command == 'processReturn'}")
    .expressionLanguage("simple")
    .build();
ObjectMapper mapper = new ObjectMapper(new JsonFactory());
producerTemplate.sendBody("kafka://subscriptions", mapper.writeValueAsString(controlMessage));
```

Returns processing service subscription

```java
DynamicRouterControlMessage controlMessage = DynamicRouterControlMessage.newBuilder()
    .subscribeChannel("orders")
    .subscriptionId("orderProcessing")
    .destinationUri("direct:orders")
    .priority(5)
    .predicate("{(headers.command == 'processReturn'}")
    .expressionLanguage("simple")
    .build();
ObjectMapper mapper = new ObjectMapper(new JsonFactory());
producerTemplate.sendBody("kafka://subscriptions", mapper.writeValueAsString(controlMessage));
```

In another module, additional routing will serve as a bridge to get the message from Kafka to the control channel of the Dynamic Router:

Bridge from Kafka to the Dynamic Router control channel

-   Java
    
-   XML
    
-   YAML
    

```java
from("kafka:subscriptions")
    .unmarshal().json(DynamicRouterControlMessage.class)
    .to("dynamic-router-control:subscribe");
```

```xml
<route>
  <from uri="kafka:subscriptions"/>
  <unmarshal>
    <json library="Jackson" unmarshalType="org.apache.camel.component.dynamicrouter.control.DynamicRouterControlMessage"/>
  </unmarshal>
  <to uri="dynamic-router-control:subscribe"/>
</route>
```

```yaml
- route:
    from:
      uri: kafka:subscriptions
      steps:
        - unmarshal:
            json:
              library: Jackson
              unmarshalType: org.apache.camel.component.dynamicrouter.control.DynamicRouterControlMessage
        - to:
            uri: dynamic-router-control:subscribe
```

Order requests or return requests might also arrive via Kafka. The route is essentially the same as the route in the single-JVM example. Instead of forwarding the incoming message, as-is, from the "direct" component to the router, the messages are deserialized from a String, and converted to an instance of the "order" object. Then, it can be sent to the Dynamic Router for evaluation and distribution to the appropriate subscribing recipients:

Routing order/return request messages from Kafka to the Dynamic Router

-   Java
    
-   XML
    
-   YAML
    

```java
from("kafka://orders")
    .unmarshal().json(MyOrderMessage.class)
    .process(myOrderProcessor)
    .to("dynamic-router:orders");
```

```xml
<route>
  <from uri="kafka://orders"/>
  <unmarshal>
    <json library="Jackson" unmarshalType="com.example.MyOrderMessage"/>
  </unmarshal>
  <to uri="bean:myOrderProcessor"/>
  <to uri="dynamic-router:orders"/>
</route>
```

```yaml
- route:
    from:
      uri: kafka://orders
      steps:
        - unmarshal:
            json:
              library: Jackson
              unmarshalType: com.example.MyOrderMessage
        - to:
            uri: bean:myOrderProcessor
        - to:
            uri: dynamic-router:orders
```

Note the `.process(myOrderProcessor)` step. If incoming messages need to be validated, enriched, transformed, or otherwise augmented, that can be done before the Dynamic Router receives the message. Then, when the Dynamic Router receives a message, it checks the `Exchange` against all subscriptions for the "orders" channel to determine if it is suitable for any of the recipients. Orders should have a header (`command` → `processOrder`), so the message will be routed to the orders service, and the inventory service. The system will process the order details, and then the inventory service will deduct from merchandise counts. Likewise, returns should have a header (`command` → `processReturn`), so the message will be routed to the returns service, where the return details will be processed, and the inventory service will increase the relevant merchandise counts.

#### Further learning: a complete Spring Boot example

In the `camel-spring-boot-examples` project, the `dynamic-router-eip-multimodule` module serves as a complete example in this category that you can run and/or experiment with to get a practical feel for how you might use this in your own multi-JVM application stack.

### JMX Control and Monitoring Operations

The Dynamic Router Control component supports some JMX operations that allow you to control and monitor the component. It is beyond the scope of this document to go into detail about JMX, so this is a list of the operations that are supported. For more information about JMX, see the [JMX](../../manual/jmx.md) documentation.

Subscribing with a predicate expression

```java
String subscribeWithPredicateExpression(String, String, String, int, String, String, boolean)
```

This operation provides the ability to subscribe to a channel with a predicate expression. The parameters, in order, are as follows:

-   subscription ID
    
-   channel name
    
-   destination URI
    
-   priority
    
-   predicate expression
    
-   expression language
    
-   update the subscription (true), or add a new one (false)
    

Subscribing with a predicate bean

```java
String subscribeWithPredicateBean(String, String, String, int, String, boolean)
```

This operation provides the ability to subscribe to a channel with the name of a Predicate that has been bound in the registry. The parameters, in order, are as follows:

-   subscription ID
    
-   channel name
    
-   destination URI
    
-   priority
    
-   predicate bean name
    
-   update the subscription (true), or add a new one (false)
    

Subscribing with a predicate instance

```java
String subscribeWithPredicateInstance(String, String, String, int, Object, boolean)
```

This operation provides the ability to subscribe to a channel with an instance of a Predicate. The parameters, in order, are as follows:

-   subscription ID
    
-   channel name
    
-   destination URI
    
-   priority
    
-   predicate instance
    
-   update the subscription (true), or add a new one (false)
    

Unsubscribing

```java
boolean removeSubscription(String, String)
```

This operation provides the ability to unsubscribe from a channel. The parameters, in order, are as follows:

-   subscription ID
    
-   channel name
    

Getting the subscriptions map

```java
Map<String, ConcurrentSkipListSet<PrioritizedFilter>> getSubscriptionsMap()
```

This operation provides the ability to get the subscriptions map. The map is keyed by channel name, and the values are a set of prioritized filters.

Getting the subscriptions statistics map

```java
Map<String, List<PrioritizedFilterStatistics>> getSubscriptionsStatisticsMap()
```

This operation provides the ability to get the subscriptions statistics map. The map is keyed by channel name, and the values are a list of prioritized filter statistics, including the number of messages that have matched the filter, and had the exchange sent to the destination URI.