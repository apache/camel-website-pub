# Dynamic Router Control

**Since Camel 4.4**

**Only producer is supported**

The Dynamic Router Control endpoint is a special type of endpoint in the Dynamic Router component where routing participants can subscribe or unsubscribe dynamically at runtime. By sending control messages to this endpoint, participants can specify their own routing rules and alter the dynamic rule base of the Dynamic Router component in real-time. Participants can choose between using URI query parameters, and sending a control message as the exchange message body.

## URI format

dynamic-router-control:controlAction\[?options\]

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

The Dynamic Router Control component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Dynamic Router Control endpoint is configured using URI syntax:

dynamic-router-control:controlAction

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **controlAction** (producer) | 
**Required** Control action.

Enum values:

-   subscribe
    
-   unsubscribe
    
-   update
    
-   list
    
-   statistics
    





 |  | String |

### Query Parameters (9 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **destinationUri** (control) | The destination URI for exchanges that match. |  | String |
| **expressionLanguage** (control) | The subscription predicate language. | simple | String |
| **predicate** (control) | The subscription predicate. |  | String |
| **predicateBean** (control) | A Predicate instance in the registry. |  | Predicate |
| **priority** (control) | The subscription priority. |  | Integer |
| **subscribeChannel** (control) | The channel to subscribe to. |  | String |
| **subscriptionId** (control) | The subscription ID; if unspecified, one will be assigned and returned. |  | String |
| **allowPredicateFromMessage** (security) | Whether the subscription predicate, and the language used to compile it, may be taken from the incoming control message. When disabled, the predicate and expressionLanguage configured on this endpoint are used instead. Enabling this lets the sender of a control message choose both the expression language and the expression that the Dynamic Router compiles into a live predicate, so only enable it when control messages come from a trusted source. | false | boolean |

## Message Headers

The Dynamic Router Control component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDynamicRouterControlAction** (producer) Constant: [`CONTROL_ACTION_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-dynamic-router/latest/org/apache/camel/component/dynamicrouter/control/DynamicRouterControlConstants.html#CONTROL_ACTION_HEADER) | The control action header. |  | String |
| **CamelDynamicRouterSubscribeChannel** (producer) Constant: [`CONTROL_SUBSCRIBE_CHANNEL`](https://javadoc.io/doc/org.apache.camel/camel-dynamic-router/latest/org/apache/camel/component/dynamicrouter/control/DynamicRouterControlConstants.html#CONTROL_SUBSCRIBE_CHANNEL) | The Dynamic Router channel that the subscriber is subscribing on. |  | String |
| **CamelDynamicRouterSubscriptionId** (producer) Constant: [`CONTROL_SUBSCRIPTION_ID`](https://javadoc.io/doc/org.apache.camel/camel-dynamic-router/latest/org/apache/camel/component/dynamicrouter/control/DynamicRouterControlConstants.html#CONTROL_SUBSCRIPTION_ID) | The subscription ID. |  | String |
| **CamelDynamicRouterDestinationUri** (producer) Constant: [`CONTROL_DESTINATION_URI`](https://javadoc.io/doc/org.apache.camel/camel-dynamic-router/latest/org/apache/camel/component/dynamicrouter/control/DynamicRouterControlConstants.html#CONTROL_DESTINATION_URI) | The URI on which the routing participant wants to receive matching exchanges. |  | String |
| **CamelDynamicRouterPriority** (producer) Constant: [`CONTROL_PRIORITY`](https://javadoc.io/doc/org.apache.camel/camel-dynamic-router/latest/org/apache/camel/component/dynamicrouter/control/DynamicRouterControlConstants.html#CONTROL_PRIORITY) | The priority of this subscription. |  | String |
| **CamelDynamicRouterPredicate** (producer) Constant: [`CONTROL_PREDICATE`](https://javadoc.io/doc/org.apache.camel/camel-dynamic-router/latest/org/apache/camel/component/dynamicrouter/control/DynamicRouterControlConstants.html#CONTROL_PREDICATE) | The predicate to evaluate exchanges for this subscription. |  | String |
| **CamelDynamicRouterPredicateBean** (producer) Constant: [`CONTROL_PREDICATE_BEAN`](https://javadoc.io/doc/org.apache.camel/camel-dynamic-router/latest/org/apache/camel/component/dynamicrouter/control/DynamicRouterControlConstants.html#CONTROL_PREDICATE_BEAN) | The name of the bean in the registry that identifies the subscription predicate. |  | String |
| **CamelDynamicRouterExpressionLanguage** (producer) Constant: [`CONTROL_EXPRESSION_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-dynamic-router/latest/org/apache/camel/component/dynamicrouter/control/DynamicRouterControlConstants.html#CONTROL_EXPRESSION_LANGUAGE) | The language for the predicate when supplied as a string. |  | String |

## Supplying the subscription predicate

A subscription needs a predicate that decides which exchanges the participant receives. There are three ways to supply one, and they differ in who chooses it:

-   `predicateBean` — the name of a `Predicate` bound in the registry. The route author decides which predicates exist, and the control message only selects one of them by name.
    
-   `predicate` and `expressionLanguage` as control endpoint URI parameters — the route author writes the expression, and every subscription made through that endpoint uses it.
    
-   `predicate` and `expressionLanguage` carried in the control message, in its body or its headers — the sender of the control message chooses both the expression language and the expression.
    

The third form is disabled by default. The predicate is compiled and then evaluated against every exchange on the channel, so letting the control message choose both the language and the expression means the sender of that message decides what runs inside the Camel process. Set `allowPredicateFromMessage=true` on the control endpoint to enable it, and only do so when control messages can only come from a trusted source:

```java
from("kafka:subscriptions")
    .unmarshal().json(DynamicRouterControlMessage.class)
    .to("dynamic-router-control:subscribe?allowPredicateFromMessage=true");
```

When `allowPredicateFromMessage` is `false`, which is the default, a control message that supplies a `predicate` or an `expressionLanguage` is rejected with an `IllegalArgumentException`. Prefer `predicateBean`, or configure the predicate on the endpoint, when control messages arrive from outside the application.

Subscription parameters that the control message does not carry fall back to the values configured on the control endpoint, so a participant can send only the parameters that identify it and let the endpoint supply the rest.

## Subscribing

Subscribing can be achieved by using query parameters in the control endpoint URI, or by sending a `DynamicRouterControlMessage` to the control endpoint URI.

### URI examples

Example Java URI `RouteBuilder` Subscription

```java
// Send a subscribe request to the dynamic router that will match every exchange and route messages to the URI: "direct:myDestination"
from("direct:subscribe").to("dynamic-router-control:subscribe?subscribeChannel=myChannel&subscriptionId=mySubId&destinationUri=direct:myDestination&priority=5&predicate=true&expressionLanguage=simple");
```

Example Java URI `ProducerTemplate` Subscription

```java
CamelContext context = new DefaultCamelContext();
context.start();
ProducerTemplate template = context.createProducerTemplate();
RouteBuilder.addRoutes(context, rb -> {
    // Route for subscriber destination
    rb.from("direct:myDestination")
            .to("log:dynamicRouterExample?showAll=true&multiline=true");
    // Route for subscribing
    rb.from("direct://subscribe")
            .toD("dynamic-router-control://subscribe" +
                    "?subscribeChannel=${header.subscribeChannel}" +
                    "&subscriptionId=${header.subscriptionId}" +
                    "&destinationUri=${header.destinationUri}" +
                    "&priority=${header.priority}" +
                    "&predicateBean=${header.predicateBean}");
});
Predicate predicate = PredicateBuilder.constant(true);
context.getRegistry().bind("predicate", predicate);
template.sendBodyAndHeaders("direct:subscribe", "",
        Map.of("subscribeChannel", "test",
                "subscriptionId", "testSubscription1",
                "destinationUri", "direct:myDestination",
                "priority", "1",
                "predicateBean", "predicate"));
```

Above, because the control URI is dynamic, and since a `ProducerTemplate` does not have a built-in way to send to a dynamic URI, we have to send subscription parameters from a `ProducerTemplate` in a different way. The dynamic-aware endpoint uses headers "under the hood", because the URI params are converted to headers, so we can set the headers deliberately.

### DynamicRouterControlMessage example

Example Java `DynamicRouterControlMessage` Subscription

```java
DynamicRouterControlMessage controlMessage = DynamicRouterControlMessage.newBuilder()
    .subscribeChannel("myChannel")
    .subscriptionId("mySubId")
    .destinationUri("direct:myDestination")
    .priority(5)
    .predicate("true")
    .expressionLanguage("simple")
    .build();
producerTemplate.sendBody("dynamic-router-control:subscribe", controlMessage);
```

## Unsubscribing

Like subscribing, unsubscribing can also be achieved by using query parameters in the control endpoint URI, or by sending a `DynamicRouterControlMessage` to the control endpoint URI. The difference is that unsubscribing can be achieved by using either one or two parameters.

### URI examples

Example Java URI `RouteBuilder` Unsubscribe

```java
from("direct:subscribe").to("dynamic-router-control:unsubscribe?subscribeChannel=myChannel&subscriptionId=mySubId");
```

Example Java URI `ProducerTemplate` Unsubscribe

```java
CamelContext context = new DefaultCamelContext();
context.start();
ProducerTemplate template = context.createProducerTemplate();
RouteBuilder.addRoutes(context, rb -> {
    // Route for unsubscribing
    rb.from("direct://unsubscribe")
            .toD("dynamic-router-control://unsubscribe" +
                    "?subscribeChannel=${header.subscribeChannel}" +
                    "&subscriptionId=${header.subscriptionId}");
});
template.sendBodyAndHeaders("direct:unsubscribe", "",
        Map.of("subscribeChannel", "test",
                "subscriptionId", "testSubscription1"));
```

Above, because the control URI is dynamic, we have to send it from a `ProducerTemplate` in a different way. The dynamic-aware endpoint uses headers, rather than URI params, so we set the headers deliberately.

### DynamicRouterControlMessage example

Example Java `DynamicRouterControlMessage` Unsubscribe

```java
DynamicRouterControlMessage controlMessage = DynamicRouterControlMessage.newBuilder()
    .subscribeChannel("myChannel")
    .subscriptionId("mySubId")
    .build();
producerTemplate.sendBody("dynamic-router-control:unsubscribe", controlMessage);
```

## The Dynamic Rule Base

To determine if an exchange is suitable for any of the participants, all predicates for the participants that are subscribed to the channel are evaluated until the first result of "true" is found, by default. If the Dynamic Router is configured with the `recipientMode` set to `allMatch`, then all recipients with matching predicates will be selected. The exchange will be routed to the corresponding endpoint(s). The rule base contains a default filter registered at the least priority (which is the highest integer number). Like the "default" case of a switch statement in Java, any message that is not appropriate for any registered participants will be processed by this filter. The filter logs information about the dropped message at **debug** level, by default. To turn the level up to **warn**, include `warnDroppedMessage=true` in the component URI.

Rules are registered in a channel, and they are logically separate from rules in another channel. Subscription IDs must be unique within a channel, although multiple subscriptions of the same name may coexist in a dynamic router instance if they are in separate channels.

The Dynamic Router employs the use of [Predicate](../../manual/predicate.md) as rules. Any valid predicate may be used to determine the suitability of exchanges for a participating recipient, whether they are simple or compound predicates. Although it is advised to view the complete documentation, an example simple predicate might look like the following:

Example simple predicate

```java
// The "messageType" must be "payment"
Predicate msgType = header("messageType").isEqualTo("payment");
```

## JMX Control and Monitoring Operations

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