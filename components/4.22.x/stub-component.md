# Stub

**Since Camel 2.10**

**Both producer and consumer are supported**

The Stub component provides a simple way to stub out any physical endpoints while in development or testing, allowing you, for example, to run a route without needing to actually connect to a specific [SMTP](mail-component.md) or [Http](http-component.md) endpoint. Add **stub:** in front of any endpoint URI to stub out the endpoint.

## URI format

stub:someUri

Where **`someUri`** can be any URI with any query parameters.

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

The Stub component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **concurrentConsumers** (consumer) | Sets the default number of concurrent threads processing exchanges. | 1 | int |
| **defaultPollTimeout** (consumer (advanced)) | The timeout (in milliseconds) used when polling. When a timeout occurs, the consumer can check whether it is allowed to continue running. Setting a lower value allows the consumer to react more quickly upon shutdown. | 1000 | int |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **defaultBlockWhenFull** (producer (advanced)) | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will instead block and wait until the message can be accepted. | false | boolean |
| **defaultDiscardWhenFull** (producer (advanced)) | Whether a thread that sends messages to a full SEDA queue will be discarded. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will give up sending and continue, meaning that the message was not sent to the SEDA queue. | false | boolean |
| **defaultOfferTimeout** (producer (advanced)) | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, where a configured timeout can be added to the block case. Using the offer(timeout) method of the underlining java queue. |  | long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **defaultQueueFactory** (advanced) | Sets the default queue factory. |  | BlockingQueueFactory |
| **queueSize** (advanced) | Sets the default maximum capacity of the SEDA queue (i.e., the number of messages it can hold). | 1000 | int |
| **shadow** (advanced) | If shadow is enabled then the stub component will register a shadow endpoint with the actual uri that refers to the stub endpoint, meaning you can lookup the endpoint via both stub:kafka:cheese and kafka:cheese. | false | boolean |
| **shadowPattern** (advanced) | If shadow is enabled then this pattern can be used to filter which components to match. Multiple patterns can be separated by comma. |  | String |

## Endpoint Options

The Stub endpoint is configured using URI syntax:

stub:name

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (common) | **Required** Name of queue. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **size** (common) | The maximum capacity of the SEDA queue (i.e., the number of messages it can hold). Will by default use the queueSize set on the SEDA component. | 1000 | int |
| **concurrentConsumers** (consumer) | Number of concurrent threads processing exchanges. When virtualThreadPerTask is enabled, this becomes a concurrency limit (0 = unlimited) and defaults to 0 instead of 1. | 1 | int |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **limitConcurrentConsumers** (consumer (advanced)) | Whether to limit the number of concurrentConsumers to the maximum of 500. By default, an exception will be thrown if an endpoint is configured with a greater number. You can disable that check by turning this option off. | true | boolean |
| **multipleConsumers** (consumer (advanced)) | Specifies whether multiple consumers are allowed. If enabled, you can use SEDA for Publish-Subscribe messaging. That is, you can send a message to the SEDA queue and have each consumer receive a copy of the message. When enabled, this option should be specified on every consumer endpoint. | false | boolean |
| **pollTimeout** (consumer (advanced)) | The timeout (in milliseconds) used when polling. When a timeout occurs, the consumer can check whether it is allowed to continue running. Setting a lower value allows the consumer to react more quickly upon shutdown. | 1000 | int |
| **purgeWhenStopping** (consumer (advanced)) | Whether to purge the task queue when stopping the consumer/route. This allows to stop faster, as any pending messages on the queue is discarded. | false | boolean |
| **virtualThreadPerTask** (consumer (advanced)) | If enabled, spawns a new virtual thread for each message instead of using a fixed pool of consumer threads. This model is optimized for virtual threads (JDK 21) and I/O-bound workloads where creating threads is cheap. The concurrentConsumers option becomes a limit on max concurrent tasks (0 = unlimited). Requires virtual threads to be enabled via camel.threads.virtual.enabled=true. | false | boolean |
| **timeout** (producer) | Timeout before a SEDA producer will stop waiting for an asynchronous task to complete. You can disable timeout by using 0 or a negative value. | 30000 | long |
| **waitForTaskToComplete** (producer) | 

Option to specify whether the caller should wait for the async task to complete or not before continuing. The following three options are supported: Always, Never or IfReplyExpected. The first two values are self-explanatory. The last value, IfReplyExpected, will only wait if the message is Request Reply based. The default option is IfReplyExpected.

Enum values:

-   Never
    
-   IfReplyExpected
    
-   Always
    





 | IfReplyExpected | WaitForTaskToComplete |
| **blockWhenFull** (producer (advanced)) | Whether a thread that sends messages to a full SEDA queue will block until the queue’s capacity is no longer exhausted. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will instead block and wait until the message can be accepted. | false | boolean |
| **discardIfNoConsumers** (producer (advanced)) | Whether the producer should discard the message (do not add the message to the queue), when sending to a queue with no active consumers. Only one of the options discardIfNoConsumers and failIfNoConsumers can be enabled at the same time. | false | boolean |
| **discardWhenFull** (producer (advanced)) | Whether a thread that sends messages to a full SEDA queue will be discarded. By default, an exception will be thrown stating that the queue is full. By enabling this option, the calling thread will give up sending and continue, meaning that the message was not sent to the SEDA queue. | false | boolean |
| **failIfNoConsumers** (producer (advanced)) | Whether the producer should fail by throwing an exception, when sending to a queue with no active consumers. Only one of the options discardIfNoConsumers and failIfNoConsumers can be enabled at the same time. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **offerTimeout** (producer (advanced)) | Offer timeout can be added to the block case when queue is full. You can disable timeout by using 0 or a negative value. |  | long |
| **browseLimit** (advanced) | Maximum number of messages to keep in memory available for browsing. Use 0 for unlimited. | 100 | int |
| **queue** (advanced) | Define the queue instance which will be used by the endpoint. |  | BlockingQueue |

## Usage

Internally, the Stub component creates [Seda](seda-component.md) endpoints. The main difference between [Stub](#) and [Seda](seda-component.md) is that [Seda](seda-component.md) will validate the URI and parameters you give it, so putting seda: in front of a typical URI with query arguments will usually fail. Stub won’t, though, as it basically ignores all query parameters to let you quickly stub out one or more endpoints in your route temporarily.

## Examples

Here are a few samples of stubbing endpoint uris

stub:smtp://somehost.foo.com?user=whatnot&something=else
stub:http://somehost.bar.com/something