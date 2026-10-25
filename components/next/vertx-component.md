# Vert.x

**Since Camel 2.12**

**Both producer and consumer are supported**

The Vert.x component is for working with the [Vertx](http://vertx.io/) [EventBus](https://vertx.io/docs/vertx-core/java/#event_bus).

The vertx [EventBus](https://vertx.io/docs/vertx-core/java/#event_bus) sends and receives Java objects that it has a message codec for: a `String`, a byte array, a number or a boolean, a `JsonObject`, a `JsonArray`, a `Buffer`, or a `Serializable` object.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-vertx</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

vertx:channelName\[?options\]

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

The Vert.x component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **host** (common) | Hostname for creating an embedded clustered EventBus. |  | String |
| **port** (common) | Port for creating an embedded clustered EventBus. |  | int |
| **timeout** (common) | Timeout in seconds to wait for clustered Vertx EventBus to be ready. The default value is 60. | 60 | int |
| **vertx** (common) | **Autowired** To use the given vertx EventBus instead of creating a new embedded EventBus. |  | Vertx |
| **vertxOptions** (common) | Options to use for creating vertx. |  | VertxOptions |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **vertxFactory** (advanced) | To use a custom VertxFactory implementation. |  | VertxBuilder |

## Endpoint Options

The Vert.x endpoint is configured using URI syntax:

vertx:address

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **address** (common) | **Required** Sets the event bus address used to communicate. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **pubSub** (common) | Whether to use publish/subscribe instead of point to point when sending to a vertx endpoint. | false | Boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Body

The message body at each side of the Vert.x component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Consumer** | `unknown` | The body of the event bus message, as the sender sent it: a String, a byte array, a number or a boolean, a JsonObject or a JsonArray, or a Serializable object such as a HashMap. A Buffer becomes a stream with stream caching enabled. |
| **Consumer reply** | `text`, `bytes`, `value`, `map`, `list`, `pojo` or `null` | A message with a reply address is answered with the body the route ends with, as the producer sends it. A stream, such as a received Buffer the route did not change, or a POJO that is not Serializable sends no reply, and the requester times out. |
| **Producer input** | `text`, `bytes`, `value`, `map`, `list` or `pojo` | Sent as is, with the event bus codec of its type: a String, a byte array, a number or a boolean, a JsonObject, a JsonArray or a Buffer, or a Serializable object such as a HashMap. A stream, a POJO that is not Serializable (without a codec registered for it) or no body fails: convert it first. |
| **Producer output** | `unknown` | 
Unchanged for a message that expects no reply (InOnly). A message that expects one (InOut) is sent as a request, also with pubSub, and gets the body of the reply.

-   With `exchangePattern=InOnly`: `unchanged`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Usage

The producer sends the message body to the event bus address, and a consumer of that address receives it. A message goes to one consumer, or to all consumers with `pubSub`:

```yaml
- route:
    from:
      uri: timer:orders
      parameters:
        period: 5000
      steps:
        - setBody:
            expression:
              constant:
                expression: '{"orderId": 123}'
        - to:
            uri: vertx:orders
            parameters:
              pubSub: true
- route:
    from:
      uri: vertx:orders
      steps:
        - log:
            message: "Received order ${body}"
```

The body is sent as is, without type conversion: a stream, or a POJO that is not `Serializable` and has no codec registered on the event bus, fails with `No message codec for type`, so convert it to a `String` or a byte array first. A message without a body fails as well.

When the exchange is InOut, the producer sends a request and the reply of the consumer becomes the message body:

```yaml
- route:
    from:
      uri: direct:greet
      steps:
        - to:
            uri: vertx:greeter
            pattern: InOut
        - log:
            message: "The reply is ${body}"
- route:
    from:
      uri: vertx:greeter
      steps:
        - setBody:
            expression:
              simple:
                expression: "Hello ${body}"
```

The consumer replies with the body the route ends with, which needs a codec too. A `Buffer` the consumer receives is a stream when stream caching is enabled (the default), so convert a stream body before the route ends.

## Connecting to the existing Vert.x instance

If you would like to connect to the Vert.x instance already existing in your JVM, you can set the instance on the component level:

_Java-only: connecting to an existing Vert.x instance_

```java
Vertx vertx = ...;
VertxComponent vertxComponent = new VertxComponent();
vertxComponent.setVertx(vertx);
camelContext.addComponent("vertx", vertxComponent);
```