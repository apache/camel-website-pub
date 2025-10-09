# Google PubSub Lite

> **Warning**
> **Deprecated:** This google-pubsub-lite is deprecated and may be removed in a future release.

**Since Camel 4.6**

**Both producer and consumer are supported**

The Google PubSub Lite component provides access to [Cloud Pub/Sub Lite Infrastructure](https://cloud.google.com/pubsub/) via the [Google Cloud Pub/Sub Lite Client for Java](https://github.com/googleapis/java-pubsublite).

The standard [Google Pub/Sub component](google-pubsub-component.md) isn’t compatible with Pub/Sub Lite service due to API and message model differences. Please refer to the following links to learn more about these differences:

-   [Pub/Sub Lite Overview](https://cloud.google.com/pubsub/docs/overview#lite)
    
-   [Choosing between Pub/Sub or Pub/Sub Lite](https://cloud.google.com/pubsub/docs/choosing-pubsub-or-lite)
    

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-pubsub-lite</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.x.x</version>
</dependency>
```

## URI Format

The Google PubSub Component uses the following URI format:

google-pubsub-lite://project-id:location:destinationName?\[options\]

Destination Name can be either a topic or a subscription name.

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

The Google PubSub Lite component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **consumerBytesOutstanding** (consumer (advanced)) | The number of quota bytes that may be outstanding to the client. Must be greater than the allowed size of the largest message (1 MiB). | 10485760 | long |
| **consumerMessagesOutstanding** (consumer (advanced)) | The number of messages that may be outstanding to the client. Must be 0. | 1000 | long |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **publisherCacheSize** (producer (advanced)) | Maximum number of producers to cache. This could be increased if you have producers for lots of different topics. | 100 | int |
| **publisherCacheTimeout** (producer (advanced)) | How many milliseconds should each producer stay alive in the cache. | 180000 | int |
| **publisherTerminationTimeout** (producer (advanced)) | How many milliseconds should a producer be allowed to terminate. | 60000 | int |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **serviceAccountKey** (security) | The Service account key that can be used as credentials for the PubSub Lite publisher/subscriber. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |

## Endpoint Options

The Google PubSub Lite endpoint is configured using URI syntax:

google-pubsub-lite:projectId:location:destinationName

With the following _path_ and _query_ parameters:

### Path Parameters (3 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **projectId** (common) | **Required** The Google Cloud PubSub Lite Project Id. |  | Long |
| **location** (common) | **Required** The Google Cloud PubSub Lite location. |  | String |
| **destinationName** (common) | **Required** The Destination Name. For the consumer this will be the subscription name, while for the producer this will be the topic name. |  | String |

### Query Parameters (12 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **loggerId** (common) | Logger ID to use when a match to the parent route required. |  | String |
| **ackMode** (consumer) | 
AUTO = exchange gets ack’ed/nack’ed on completion. NONE = downstream process has to ack/nack explicitly.

Enum values:

-   AUTO
    
-   NONE
    





 | AUTO | AckMode |
| **concurrentConsumers** (consumer) | The number of parallel streams consuming from the subscription. | 1 | Integer |
| **maxAckExtensionPeriod** (consumer) | Set the maximum period a message ack deadline will be extended. Value in seconds. | 3600 | int |
| **maxMessagesPerPoll** (consumer) | The max number of messages to receive from the server in a single API call. | 1 | Integer |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **pubsubEndpoint** (producer (advanced)) | Pub/Sub endpoint to use. Required when using message ordering, and ensures that messages are received in order even when multiple publishers are used. |  | String |
| **serializer** (producer (advanced)) | **Autowired** A custom GooglePubsubLiteSerializer to use for serializing message payloads in the producer. |  | GooglePubsubSerializer |
| **serviceAccountKey** (security) | The Service account key that can be used as credentials for the PubSub publisher/subscriber. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |

## Message Headers

The Google PubSub Lite component supports 5 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGooglePubsubMessageId** (common) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub-lite/latest/org/apache/camel/component/google/pubsublite/GooglePubsubLiteConstants.html#MESSAGE_ID) | The ID of the message, assigned by the server when the message is published. |  | String |
| **CamelGooglePubsubMsgAckId** (consumer) Constant: [`ACK_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub-lite/latest/org/apache/camel/component/google/pubsublite/GooglePubsubLiteConstants.html#ACK_ID) | The ID used to acknowledge the received message. |  | String |
| **CamelGooglePubsubPublishTime** (consumer) Constant: [`PUBLISH_TIME`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub-lite/latest/org/apache/camel/component/google/pubsublite/GooglePubsubLiteConstants.html#PUBLISH_TIME) | The time at which the message was published. |  | Timestamp |
| **CamelGooglePubsubAttributes** (common) Constant: [`ATTRIBUTES`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub-lite/latest/org/apache/camel/component/google/pubsublite/GooglePubsubLiteConstants.html#ATTRIBUTES) | The attributes of the message. |  | Map |
| **CamelGooglePubsubOrderingKey** (producer) Constant: [`ORDERING_KEY`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub-lite/latest/org/apache/camel/component/google/pubsublite/GooglePubsubLiteConstants.html#ORDERING_KEY) | If non-empty, identifies related messages for which publish order should be respected. |  | String |

## Usage

### Producer Endpoints

Google PubSub Lite expects the payload to be `byte[]` array, Producer endpoints will send:

-   String body as `byte[]` encoded as UTF-8
    
-   `byte[]` body as is
    
-   Everything else will be serialised into a `byte[]` array
    

A Map set as message header `GooglePubsubConstants.ATTRIBUTES` will be sent as PubSub attributes.

When producing messages set the message header `GooglePubsubConstants.ORDERING_KEY`. This will be set as the PubSub Lite orderingKey for the message. You can find more information on [Using ordering keys](https://cloud.google.com/pubsub/lite/docs/publishing#using_ordering_keys).

### Consumer Endpoints

Google PubSub Lite will redeliver the message if it has not been acknowledged within the time period set as a configuration option on the subscription.

The component will acknowledge the message once exchange processing has been completed.

### Message Body

The consumer endpoint returns the content of the message as `byte[]` - exactly as the underlying system sends it. It is up for the route to convert/unmarshall the contents.

## Examples

You’ll need to provide a connectionFactory to the ActiveMQ Component, to have the following examples working.

### Producer Example

```java
 from("timer://scheduler?fixedRate=true&period=5s")
            .setBody(simple("Hello World ${date:now:HH:mm:ss.SSS}"))
            .to("google-pubsub-lite:123456789012:europe-west3-a:my-topic-lite")
            .log("Message sent: ${body}");
```

### Consumer Example

```java
from("google-pubsub-lite:123456789012:europe-west3-a:my-subscription-lite")
            .log("Message received: ${body}");
```

## Spring Boot Auto-Configuration

When using google-pubsub-lite with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-pubsub-lite-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-pubsub-lite.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-pubsub-lite.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-pubsub-lite.consumer-bytes-outstanding** | The number of quota bytes that may be outstanding to the client. Must be greater than the allowed size of the largest message (1 MiB). | 10485760 | Long |
| **camel.component.google-pubsub-lite.consumer-messages-outstanding** | The number of messages that may be outstanding to the client. Must be 0. | 1000 | Long |
| **camel.component.google-pubsub-lite.enabled** | Whether to enable auto configuration of the google-pubsub-lite component. This is enabled by default. |  | Boolean |
| **camel.component.google-pubsub-lite.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-pubsub-lite.publisher-cache-size** | Maximum number of producers to cache. This could be increased if you have producers for lots of different topics. | 100 | Integer |
| **camel.component.google-pubsub-lite.publisher-cache-timeout** | How many milliseconds should each producer stay alive in the cache. | 180000 | Integer |
| **camel.component.google-pubsub-lite.publisher-termination-timeout** | How many milliseconds should a producer be allowed to terminate. | 60000 | Integer |
| **camel.component.google-pubsub-lite.service-account-key** | The Service account key that can be used as credentials for the PubSub Lite publisher/subscriber. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |