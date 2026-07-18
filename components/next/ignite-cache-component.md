# Ignite Cache

**Since Camel 2.17**

**Both producer and consumer are supported**

The Ignite Cache endpoint is one of camel-ignite endpoints that allow you to interact with an [Ignite Cache](https://apacheignite.readme.io/docs/data-grid). This offers both a Producer (to invoke cache operations on an Ignite cache) and a Consumer (to consume changes from a continuous query).

The cache value is always the body of the message, whereas the cache key is always stored in the `CamelIgniteCacheKey` message header.

Even if you configure a fixed operation in the endpoint URI, you can vary it per-exchange by setting the `CamelIgniteCacheOperation` message header.

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

The Ignite Cache component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configurationResource** (common) | The resource from where to load the configuration. It can be a: URL, String or InputStream type. |  | Object |
| **ignite** (common) | To use an existing Ignite instance. |  | Ignite |
| **igniteConfiguration** (common) | Allows the user to set a programmatic ignite configuration. |  | IgniteConfiguration |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Ignite Cache endpoint is configured using URI syntax:

ignite-cache:cacheName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheName** (common) | **Required** The cache name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **propagateIncomingBodyIfNoReturnValue** (common) | Sets whether to propagate the incoming body if the return type of the underlying Ignite operation is void. | true | boolean |
| **treatCollectionsAsCacheObjects** (common) | Sets whether to treat Collections as cache objects or as Collections of items to insert/update/compute, etc. | false | boolean |
| **autoUnsubscribe** (consumer) | Whether auto unsubscribe is enabled in the Continuous Query Consumer. Default value notice: ContinuousQuery.DFLT\_AUTO\_UNSUBSCRIBE. | true | boolean |
| **fireExistingQueryResults** (consumer) | Whether to process existing results that match the query. Used on initialization of the Continuous Query Consumer. | false | boolean |
| **oneExchangePerUpdate** (consumer) | Whether to pack each update in an individual Exchange, even if multiple updates are received in one batch. Only used by the Continuous Query Consumer. | true | boolean |
| **pageSize** (consumer) | The page size. Only used by the Continuous Query Consumer. Default value notice: ContinuousQuery.DFLT\_PAGE\_SIZE. | 1 | int |
| **query** (consumer) | The Query to execute, only needed for operations that require it, and for the Continuous Query Consumer. |  | Query |
| **remoteFilter** (consumer) | The remote filter, only used by the Continuous Query Consumer. |  | CacheEntryEventSerializableFilter |
| **timeInterval** (consumer) | The time interval for the Continuous Query Consumer. Default value notice: ContinuousQuery.DFLT\_TIME\_INTERVAL. | 0 | long |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **cachePeekMode** (producer) | 

The CachePeekMode, only needed for operations that require it (IgniteCacheOperation#SIZE).

Enum values:

-   ALL
    
-   NEAR
    
-   PRIMARY
    
-   BACKUP
    
-   ONHEAP
    
-   OFFHEAP
    





 | ALL | CachePeekMode |
| **failIfInexistentCache** (producer) | Whether to fail the initialization if the cache doesn’t exist. | false | boolean |
| **operation** (producer) | 

The cache operation to invoke. Possible values: GET, PUT, REMOVE, SIZE, REBALANCE, QUERY, CLEAR.

Enum values:

-   GET
    
-   PUT
    
-   REMOVE
    
-   SIZE
    
-   REBALANCE
    
-   QUERY
    
-   CLEAR
    
-   REPLACE
    





 |  | IgniteCacheOperation |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Ignite Cache component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIgniteCacheKey** (common) Constant: [`IGNITE_CACHE_KEY`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_CACHE_KEY) | The cache key for the entry value in the message body. |  | Object |
| **CamelIgniteCacheQuery** (producer) Constant: [`IGNITE_CACHE_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_CACHE_QUERY) | The query to run when invoking the QUERY operation. |  | Query |
| **CamelIgniteCacheOperation** (producer) Constant: [`IGNITE_CACHE_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_CACHE_OPERATION) | 
Allows you to dynamically change the cache operation to execute.

Enum values:

-   GET
    
-   PUT
    
-   REMOVE
    
-   SIZE
    
-   REBALANCE
    
-   QUERY
    
-   CLEAR
    
-   REPLACE
    





 |  | IgniteCacheOperation |
| **CamelIgniteCachePeekMode** (producer) Constant: [`IGNITE_CACHE_PEEK_MODE`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_CACHE_PEEK_MODE) | 

Allows you to dynamically change the cache peek mode when running the SIZE operation.

Enum values:

-   ALL
    
-   NEAR
    
-   PRIMARY
    
-   BACKUP
    
-   ONHEAP
    
-   OFFHEAP
    





 |  | CachePeekMode |
| **CamelIgniteCacheEventType** (consumer) Constant: [`IGNITE_CACHE_EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_CACHE_EVENT_TYPE) | 

This header carries the received event type when using the continuous query consumer.

Enum values:

-   CREATED
    
-   UPDATED
    
-   REMOVED
    
-   EXPIRED
    





 |  | EventType |
| **CamelIgniteCacheName** (consumer) Constant: [`IGNITE_CACHE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_CACHE_NAME) | This header carries the cache name for which a continuous query event was received (consumer). It does not allow you to dynamically change the cache against which a producer operation is performed. Use EIPs for that (e.g. recipient list, dynamic router). |  | String |
| **CamelIgniteCacheOldValue** (common) Constant: [`IGNITE_CACHE_OLD_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_CACHE_OLD_VALUE) | (producer) The old cache value to be replaced when invoking the REPLACE operation. (consumer) This header carries the old cache value when passed in the incoming cache event. |  | Object |