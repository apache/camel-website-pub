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

-   **core**: implements a dynamic version of a `Routing Slip` for this purpose, but that is not inherently dynamic in terms of its content. If the content of this slip will be dynamic, it will be up to the user to define and implement that capability.
    
-   **component**: builds the rule base at runtime, and maintains it as participants subscribe or unsubscribe via the control channel.
    

_Message Re-Circulation_

The Dynamic Router EIP description does not specify any message re-circulation behavior.

-   **core**: provides a feature that continuously routes the exchange to a recipient, then back through the dynamic router, until a recipient returns `null` to signify routing termination. This may be an interpretation of the control channel feature.
    
-   **component**: does not provide a re-circulation feature. If this is the desired behavior, the user will have to define and implement this behavior. E.g., create a simple route to send a response back through the Dynamic Router under some condition(s).
    

For some use cases, the core Dynamic Router will be more appropriate. In other cases, the Dynamic Router Component will be a better fit.

## URI format

```none
dynamic-router:channel[?options]
```

## Control URI format

```none
dynamic-router:control/controlAction/subscribeChannel[?options]
```

The `channel` is the routing channel that allows messaging to be logically separate from other channels. Any string that can be included in a URI is a valid channel name. Each channel can have a set of participant subscriptions, and can consume messages to be routed to appropriate recipients. The only reserved channel is the `control` channel. This is a single channel that handles control messages for participants to subscribe or unsubscribe for messaging over a desired channel.

For control channel messages, the chanel must have a literal value of `control`. The value of `controlAction` must be `subscribe` or `unsubscribe`. The channel to which the action applies is specified as the `subscribeChannel` param.

These messages will be described in greater detail below, with examples.

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

The Dynamic Router component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Dynamic Router endpoint is configured using URI syntax:

dynamic-router:channel

with the following path and query parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **channel** (common) | **Required** Channel of the Dynamic Router. |  | String |
| **controlAction** (control) | 
Control channel action: subscribe or unsubscribe.

Enum values:

-   subscribe
    
-   unsubscribe
    





 |  | String |
| **subscribeChannel** (control) | The channel to subscribe to. |  | String |

### Query Parameters (10 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **recipientMode** (common) | 
Recipient mode: firstMatch or allMatch.

Enum values:

-   firstMatch
    
-   allMatch
    





 | firstMatch | String |
| **synchronous** (common) | Flag to ensure synchronous processing. | false | boolean |
| **warnDroppedMessage** (common) | Flag to log a warning if no predicates match for an exchange. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **destinationUri** (control) | The destination URI for exchanges that match. |  | String |
| **expressionLanguage** (control) | The subscription predicate language. | simple | String |
| **predicate** (control) | The subscription predicate. |  | String |
| **predicateBean** (control) | A Predicate instance in the registry. |  | Predicate |
| **priority** (control) | The subscription priority. |  | Integer |
| **subscriptionId** (control) | The subscription ID; if unspecified, one will be assigned and returned. |  | String |

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

The Dynamic Router component is used in the same way that other components are used. Simply include the dynamic-router URI as a consumer in a route, along with the channel name.

In Java:

Example Java DSL Route Definition

```java
// Send message to the Dynamic Router channel named "jupiter"
from("direct:start").to("dynamic-router:jupiter");
```

And the same route using XML DSL:

Example XML Route Definition

```xml
<route>
   <from uri="direct:start"/>
   <to uri="dynamic-router:jupiter"/>
</route>
```

## Subscribing

### Method 1: Subscribe Message POJO

Participating recipients may subscribe by sending a `DynamicRouterControlMessage` to the `control` channel. An example subscribe message might look like the following:

Example Subscribe Message as POJO

```java
// Send a message to the Dynamic Router "billing" channel
// to subscribe to billing messages, with a priority of 10
DynamicRouterControlMessage billingSubMsg = new SubscribeMessageBuilder()
                .id("billingSubscription")
                .channel("billing")
                .priority(10)
                .endpointUri(myBillingNotificationUri)
                .predicate(new SomeBillingPredicate())
                .build();
template.sendBody("dynamic-router:control", billingSubMsg);
```

The parameters, in order, are:

1.  _Subscription ID_: When unsubscribing, this is the only way to identify the subscription to remove.
    
2.  _Channel Name_: The dynamic router can have multiple channels, where the subscriptions (the registered rules and endpoints) are kept completely separate from the other channels. This is equivalent to a VLAN in networking.
    
3.  _Priority_: A new subscription will be inserted into the rule base in order of precedence; lower numbers have higher priority.
    
4.  _Endpoint URI_: If an evaluation of the rules in the rule base determines that the exchange is appropriate for the recipient, it is sent to this URI.
    
5.  _Predicate_: For evaluating the exchange to determine if a message should be routed to the supplied URI.
    

### Method 2: URI Only

You can also use a simplified method for subscribing using URL parameters, if you wish. The subscribe message, detailed above, can be sent via the control URI like this (with an empty body, since it will be ignored):

Example Subscribe Message Using URI

```java
template.sendBody("dynamic-router:control/subscribe/billing?subscriptionId=billingSubscription&priority=10&destinationUri=<URI here>&predicate=<text predicate>", "");
```

### Method 3: URI and Predicate as Bean

The predicate can also be supplied as a bean in the Camel context registry. The URI example is modified slightly:

Example Subscribe Message Using URI and Predicate Bean

```java
// Register a bean, somehow, in the registry:
camelContext.getRegistry().bind("predicateBean", Predicate.class, PredicateBuilder.constant(true));
template.sendBody("dynamic-router:control/subscribe/billing?subscriptionId=billingSubscription&priority=10&destinationUri=<URI here>&predicate=#bean:predicateBean", "");
```

### Method 4: URI and Predicate as Message Body

As a final example, the URI subscription method can be modified, once again, to eliminate the `predicate` parameter altogether, and supply the `Predicate` as the message body:

Example Subscribe Message Using URI and Predicate as Message Body

```java
// Register a bean, somehow, in the registry:
Predicate predicate = PredicateBuilder.constant(true));
template.sendBody("dynamic-router:control/subscribe/billing?subscriptionId=billingSubscription&priority=10&destinationUri=<URI here>", predicate);
```

### Note: Subscription ID is Generated if Not Supplied

For any of the URI subscription examples, the `subscriptionId` URI parameter may be omitted, and a subscription ID will be generated and returned as the message body. It will have the form of a UUID string. As an example:

Example Subscribe Message Using URI and Omitting Subscription ID

```java
Predicate predicate = PredicateBuilder.constant(true));
// Capture the generated subscription ID from the returned message body:
String generatedId = (String) template.sendBody("dynamic-router:control/subscribe/billing?priority=10&destinationUri=<URI here>", ExchangePattern.InOut, predicate);
```

The `generatedId` variable will contain the generated UUID string. If you are going to unsubscribe, you will need this ID.

## Unsubscribing

### Method 1: Unsubscribe Message POJO

Participating recipients may unsubscribe by sending a `DynamicRouterControlMessage` to the `control` channel. An example unsubscribe message might look like the following:

Example Unsubscribe Message Using POJO

```java
// Send message to the Dynamic Router "billing" channel
// to unsubscribe from billing messages
DynamicRouterControlMessage unsubscribeMsg = new UnsubscribeMessageBuilder()
                .id("billingSubscription")
                .channel("billing")
                .build();
template.sendBody("dynamic-router:control", unsubscribeMsg);
```

The builder for an unsubscribe message only requires the id and channel name.

### Method 2: URI Only

You can also use a simplified method for unsubscribing using URL parameters, if you wish. The unsubscribe message, detailed above, can be sent via the control URI like this (with an empty body, since it will be ignored):

Example Unsubscribe Message Using URI

```java
template.sendBody("dynamic-router:control/unsubscribe/billing?subscriptionId=billingSubscription", "");
```

## The Dynamic Rule Base

To determine if an exchange is suitable for any of the participants, all predicates for the participants that are subscribed to the channel are evaluated until the first result of "true" is found, by default. If the Dynamic Router is configured with the `recipientMode` set to `allMatch`, then all recipients with matching predicates will be selected. The exchange will be routed to the corresponding endpoint(s). The rule base contains a default filter that is registered at the least priority (which is the highest integer number). Like the "default" case of a switch statement in Java, any message that is not appropriate for any registered participants will be processed by this filter. The filter logs information about the dropped message at **debug** level, by default. To turn the level up to **warn**, include `warnDroppedMessage=true` in the component URI.

Rules are registered in a channel, and they are logically separate from rules in another channel. Subscription IDs must be unique within a channel, although multiple subscriptions of the same name may coexist in a dynamic router instance if they are in separate channels.

The Dynamic Router employs the use of [Predicate](../../manual/predicate.md) as rules. Any valid predicate may be used to determine the suitability of exchanges for a participating recipient, whether they are simple or compound predicates. Although it is advised to view the complete documentation, an example simple predicate might look like the following:

Example simple predicate

```java
// The "messageType" must be "payment"
Predicate msgType = header("messageType").isEqualTo("payment");
```