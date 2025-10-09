# Google Pubsub

**Since Camel 2.19**

**Both producer and consumer are supported**

The Google Pubsub component provides access to [Cloud Pub/Sub Infrastructure](https://cloud.google.com/pubsub/) via the [Google Cloud Java Client for Google Cloud Pub/Sub](https://github.com/googleapis/java-pubsub).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-google-pubsub</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.x.x</version>
</dependency>
```

## URI Format

The Google Pubsub Component uses the following URI format:

google-pubsub://project-id:destinationName?\[options\]

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

The Google Pubsub component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **authenticate** (common) | Use Credentials when interacting with PubSub service (no authentication is required when using emulator). | true | boolean |
| **endpoint** (common) | Endpoint to use with local Pub/Sub emulator. |  | String |
| **serviceAccountKey** (common) | The Service account key that can be used as credentials for the PubSub publisher/subscriber. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **synchronousPullRetryableCodes** (consumer) | Comma-separated list of additional retryable error codes for synchronous pull. By default the PubSub client library retries ABORTED, UNAVAILABLE, UNKNOWN. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **publisherCacheSize** (producer) | Maximum number of producers to cache. This could be increased if you have producers for lots of different topics. |  | int |
| **publisherCacheTimeout** (producer) | How many milliseconds should each producer stay alive in the cache. |  | int |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **publisherTerminationTimeout** (advanced) | How many milliseconds should a producer be allowed to terminate. |  | int |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Endpoint Options

The Google Pubsub endpoint is configured using URI syntax:

google-pubsub:projectId:destinationName

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **projectId** (common) | **Required** The Google Cloud PubSub Project Id. |  | String |
| **destinationName** (common) | **Required** The Destination Name. For the consumer this will be the subscription name, while for the producer this will be the topic name. |  | String |

### Query Parameters (19 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **ackMode** (consumer) | 
AUTO = exchange gets ack’ed/nack’ed on completion. NONE = downstream process has to ack/nack explicitly.

Enum values:

-   AUTO
    
-   NONE
    





 | AUTO | AckMode |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **concurrentConsumers** (consumer (advanced)) | The number of parallel streams consuming from the subscription. | 1 | Integer |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **maxAckExtensionPeriod** (consumer (advanced)) | Set the maximum period a message ack deadline will be extended. Value in seconds. | 3600 | int |
| **maxDeliveryAttempts** (consumer (advanced)) | The maximum number of delivery attempts for each message. When set to a positive value, the consumer will automatically nack any message whose delivery attempt count is greater than or equal to this value, allowing Pub/Sub to route it to the dead-letter topic without processing it. This prevents infinite redelivery loops when short retry delays are configured. If not explicitly set and the subscription has a dead-letter policy, the value is automatically fetched from the subscription configuration at consumer startup. Set to 0 to disable enforcement. | 0 | int |
| **maxMessagesPerPoll** (consumer (advanced)) | The max number of messages to receive from the server in a single API call. | 1 | Integer |
| **synchronousPull** (consumer (advanced)) | Synchronously pull batches of messages. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **messageOrderingEnabled** (producer (advanced)) | Should message ordering be enabled. | false | boolean |
| **pubsubEndpoint** (producer (advanced)) | Pub/Sub endpoint to use. Required when using message ordering, and ensures that messages are received in order even when multiple publishers are used. |  | String |
| **retry** (producer (advanced)) | A custom RetrySettings to control how the publisher handles retry-able failures. |  | RetrySettings |
| **serializer** (producer (advanced)) | **Autowired** A custom GooglePubsubSerializer to use for serializing message payloads in the producer. |  | GooglePubsubSerializer |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter headers to and from Camel message. |  | HeaderFilterStrategy |
| **includeAllGoogleProperties** (advanced) | Whether to include all Google headers when mapping from Pubsub to Camel Message. Setting this to true will include properties such as x-goog etc. | false | boolean |
| **loggerId** (advanced) | **Deprecated** To use a custom logger name. |  | String |
| **authenticate** (security) | Use Credentials when interacting with PubSub service (no authentication is required when using emulator). | true | boolean |
| **serviceAccountKey** (security) | The Service account key that can be used as credentials for the PubSub publisher/subscriber. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |

## Message Headers

The Google Pubsub component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelGooglePubsubMessageId** (common) Constant: [`MESSAGE_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub/latest/org/apache/camel/component/google/pubsub/GooglePubsubConstants.html#MESSAGE_ID) | The ID of the message, assigned by the server when the message is published. |  | String |
| **CamelGooglePubsubMsgAckId** (consumer) Constant: [`ACK_ID`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub/latest/org/apache/camel/component/google/pubsub/GooglePubsubConstants.html#ACK_ID) | The ID used to acknowledge the received message. |  | String |
| **CamelGooglePubsubPublishTime** (consumer) Constant: [`PUBLISH_TIME`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub/latest/org/apache/camel/component/google/pubsub/GooglePubsubConstants.html#PUBLISH_TIME) | The time at which the message was published. |  | Timestamp |
| **CamelGooglePubsubAttributes** (common) Constant: [`ATTRIBUTES`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub/latest/org/apache/camel/component/google/pubsub/GooglePubsubConstants.html#ATTRIBUTES) | **Deprecated** The attributes of the message. |  | Map |
| **CamelGooglePubsubOrderingKey** (producer) Constant: [`ORDERING_KEY`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub/latest/org/apache/camel/component/google/pubsub/GooglePubsubConstants.html#ORDERING_KEY) | If non-empty, identifies related messages for which publish order should be respected. |  | String |
| **CamelGooglePubsubAcknowledge** (consumer) Constant: [`GOOGLE_PUBSUB_ACKNOWLEDGE`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub/latest/org/apache/camel/component/google/pubsub/GooglePubsubConstants.html#GOOGLE_PUBSUB_ACKNOWLEDGE) | Can be used to manually acknowledge or negative-acknowledge a message when ackMode=NONE. |  | GooglePubsubAcknowledge |
| **CamelGooglePubsubDeliveryAttempt** (consumer) Constant: [`DELIVERY_ATTEMPT`](https://javadoc.io/doc/org.apache.camel/camel-google-pubsub/latest/org/apache/camel/component/google/pubsub/GooglePubsubConstants.html#DELIVERY_ATTEMPT) | The delivery attempt counter received from PubSub. This is the approximate number of times the message has been delivered. This will be 1 for the first delivery. This feature requires a dead-letter policy to be configured on the subscription. |  | Integer |

## Usage

### Producer Endpoints

Producer endpoints can accept and deliver to PubSub individual and grouped exchanges alike. Grouped exchanges have `Exchange.GROUPED_EXCHANGE` property set.

Google PubSub expects the payload to be byte\[\] array, Producer endpoints will send:

-   String body as `byte[]` encoded as UTF-8
    
-   `byte[]` body as is
    
-   Everything else will be serialised into a `byte[]` array
    

A Map set as message header `GooglePubsubConstants.ATTRIBUTES` will be sent as PubSub attributes.

Google PubSub supports ordered message delivery.

To enable this, set the options `messageOrderingEnabled` to true, and the `pubsubEndpoint` to a GCP region.

When producing messages set the message header `GooglePubsubConstants.ORDERING_KEY` . This will be set as the PubSub orderingKey for the message.

For more information, see [Ordering messages](https://cloud.google.com/pubsub/docs/ordering).

Once exchange has been delivered to PubSub the PubSub Message ID will be assigned to the header `GooglePubsubConstants.MESSAGE_ID`.

### Consumer Endpoints

Google PubSub will redeliver the message if it has not been acknowledged within the time period set as a configuration option on the subscription.

The component will acknowledge the message once exchange processing has been completed.

If the route throws an exception, the exchange is marked as failed, and the component will NACK the message. It will be redelivered immediately.

To ack/nack the message the component uses Acknowledgement ID stored as header `GooglePubsubConstants.ACK_ID`. If the header is removed or tampered with, the ack will fail and the message will be redelivered again after the ack deadline.

### Delivery Attempts and Dead Letter Queues

When a subscription has a [dead-letter policy](https://cloud.google.com/pubsub/docs/dead-letter-topics) configured, the component exposes the delivery attempt count via the header `GooglePubsubConstants.DELIVERY_ATTEMPT`. This header contains an `Integer` representing the approximate number of times the message has been delivered. The first delivery will have a value of `1`.

> **Note**
> The delivery attempt header is only available when the subscription has a dead-letter policy configured. Without a dead-letter policy, the header will not be set.

This allows routes to implement custom retry logic based on the delivery attempt count:

```java
from("google-pubsub:{{project.name}}:{{subscription.name}}")
    .process(exchange -> {
        Integer deliveryAttempt = exchange.getIn().getHeader(GooglePubsubConstants.DELIVERY_ATTEMPT, Integer.class);
        if (deliveryAttempt != null && deliveryAttempt > 3) {
            // Custom handling for messages that have been redelivered multiple times
            log.warn("Message has been delivered {} times", deliveryAttempt);
        }
        // Process the message
    });
```

With a dead-letter policy, after the configured maximum delivery attempts are exceeded, the message will automatically be forwarded to the dead-letter topic by Google PubSub.

#### Automatic Max Delivery Attempts Enforcement

The component can enforce the subscription’s `maxDeliveryAttempts` setting at the consumer level. When enabled, messages whose delivery attempt count is greater than or equal to the configured maximum will be automatically nacked without processing, allowing Pub/Sub to route them to the dead-letter topic. This prevents infinite redelivery loops that can occur with short retry delays.

The `maxDeliveryAttempts` value is resolved as follows:

1.  If explicitly set via the endpoint option, that value is used.
    
2.  If not explicitly set, the component attempts to auto-fetch the value from the subscription’s dead-letter policy at consumer startup.
    
3.  If auto-fetch fails (e.g., insufficient permissions or no dead-letter policy), enforcement is disabled and a warning is logged.
    
4.  A value of `0` disables enforcement.
    

```java
// Explicit configuration
from("google-pubsub:{{project.name}}:{{subscription.name}}?maxDeliveryAttempts=5")
    .to("direct:process");

// Auto-fetch from subscription dead-letter policy (default behavior when not set)
from("google-pubsub:{{project.name}}:{{subscription.name}}")
    .to("direct:process");
```

### Message Body

The consumer endpoint returns the content of the message as `byte[]`. Exactly as the underlying system sends it. It is up for the route to convert/unmarshall the contents.

### Authentication Configuration

By default, this component acquires credentials using `GoogleCredentials.getApplicationDefault()`. This behavior can be disabled by setting _authenticate_ option to `false`, in which case requests to Google API will be made without authentication details. This is only desirable when developing against an emulator. This behavior can be altered by supplying a path to a service account key file.

#### Workload Identity Federation (WIF)

All Google components support [Workload Identity Federation](https://cloud.google.com/iam/docs/workload-identity-federation), which enables workloads running outside of Google Cloud (e.g., on AWS, Azure, GitHub Actions) or on GKE to authenticate without service account key files.

**On GKE with Workload Identity:** No configuration is needed. Application Default Credentials (ADC) automatically detects the GKE environment and uses the Kubernetes service account’s associated GCP identity.

**With an explicit WIF configuration file:** Set `useWorkloadIdentityFederation=true` and provide the path to the WIF JSON config file via `workloadIdentityConfig`. This is the typical setup for GitHub Actions, AWS, and Azure workloads.

```java
// GKE with Workload Identity - ADC handles it automatically
from("google-pubsub:my-project:my-subscription")
    .to("direct:process");

// GitHub Actions / AWS / Azure with WIF config file
GooglePubsubEndpoint endpoint = context.getEndpoint("google-pubsub:my-project:my-subscription", GooglePubsubEndpoint.class);
endpoint.setUseWorkloadIdentityFederation(true);
endpoint.setWorkloadIdentityConfig("/path/to/wif-config.json");
```

**With Service Account Impersonation:** Set `impersonatedServiceAccount` to a target service account email. The external credentials obtained via WIF will impersonate that service account, inheriting its permissions.

```java
// WIF with service account impersonation
GooglePubsubEndpoint endpoint = context.getEndpoint("google-pubsub:my-project:my-subscription", GooglePubsubEndpoint.class);
endpoint.setUseWorkloadIdentityFederation(true);
endpoint.setWorkloadIdentityConfig("/path/to/wif-config.json");
endpoint.setImpersonatedServiceAccount("my-sa@my-project.iam.gserviceaccount.com");
```

> **Note**
> Workload Identity Federation support is available in all Google components (PubSub, Storage, BigQuery, Firestore, Sheets, Calendar, Drive, Mail, Functions, Secret Manager, Vision, Vertex AI, Speech-to-Text, Text-to-Speech) through the common `GoogleCommonConfiguration` interface.

## Spring Boot Auto-Configuration

When using google-pubsub with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-google-pubsub-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 12 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.google-pubsub.authenticate** | Use Credentials when interacting with PubSub service (no authentication is required when using emulator). | true | Boolean |
| **camel.component.google-pubsub.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.google-pubsub.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.google-pubsub.enabled** | Whether to enable auto configuration of the google-pubsub component. This is enabled by default. |  | Boolean |
| **camel.component.google-pubsub.endpoint** | Endpoint to use with local Pub/Sub emulator. |  | String |
| **camel.component.google-pubsub.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.google-pubsub.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.google-pubsub.publisher-cache-size** | Maximum number of producers to cache. This could be increased if you have producers for lots of different topics. |  | Integer |
| **camel.component.google-pubsub.publisher-cache-timeout** | How many milliseconds should each producer stay alive in the cache. |  | Integer |
| **camel.component.google-pubsub.publisher-termination-timeout** | How many milliseconds should a producer be allowed to terminate. |  | Integer |
| **camel.component.google-pubsub.service-account-key** | The Service account key that can be used as credentials for the PubSub publisher/subscriber. It can be loaded by default from classpath, but you can prefix with classpath:, file:, or http: to load the resource from different systems. |  | String |
| **camel.component.google-pubsub.synchronous-pull-retryable-codes** | Comma-separated list of additional retryable error codes for synchronous pull. By default the PubSub client library retries ABORTED, UNAVAILABLE, UNKNOWN. |  | String |

### Manual Acknowledgement

By default, the PubSub consumer will acknowledge messages once the exchange has been processed, or negative-acknowledge them if the exchange has failed.

If the _ackMode_ option is set to `NONE`, the component will not acknowledge messages, and it is up to the route to do so. In this case, a `GooglePubsubAcknowledge` object is stored in the header `GooglePubsubConstants.GOOGLE_PUBSUB_ACKNOWLEDGE` and can be used to acknowledge messages:

```java
from("google-pubsub:{{project.name}}:{{subscription.name}}?ackMode=NONE")
    .process(exchange -> {
        GooglePubsubAcknowledge acknowledge = exchange.getIn().getHeader(GooglePubsubConstants.GOOGLE_PUBSUB_ACKNOWLEDGE, GooglePubsubAcknowledge.class);
        acknowledge.ack(exchange); // or .nack(exchange)
    });
```

Manual acknowledgement works with both the asynchronous and synchronous consumers and will use the acknowledgement id which is stored in `GooglePubsubConstants.ACK_ID`.