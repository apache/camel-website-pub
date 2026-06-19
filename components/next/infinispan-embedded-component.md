# Infinispan Embedded

**Since Camel 2.13**

**Both producer and consumer are supported**

This component allows you to interact with [Infinispan](http://infinispan.org/) distributed data grid / cache. Infinispan is an extremely scalable, highly available key/value data store and data grid platform written in Java.

The `camel-infinispan-embedded` component includes the following features:

-   **Local Camel Consumer**: receives cache change notifications and sends them to be processed. This can be done synchronously or asynchronously, and is also supported with a replicated or distributed cache.
    
-   **Local Camel Producer**: a producer creates and sends messages to an endpoint. The `camel-infinispan` producer uses `GET`, `PUT`, `REMOVE`, and `CLEAR` operations. The local producer is also supported with a replicated or distributed cache.
    

The events are processed asynchronously.

If you use Maven, you must add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-infinispan-embedded</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

infinispan-embedded://cacheName?\[options\]

The producer allows sending messages to a local infinispan cache. The consumer allows listening for events from local infinispan cache.

If no cache configuration is provided, embedded cacheContainer is created directly in the component.

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

The Infinispan Embedded component supports 20 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | Component configuration. |  | InfinispanEmbeddedConfiguration |
| **queryBuilder** (common) | Specifies the query builder. |  | InfinispanQueryBuilder |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **clusteredListener** (consumer) | If true, the listener will be installed for the entire cluster. | false | boolean |
| **customListener** (consumer) | Returns the custom listener in use, if provided. |  | InfinispanEmbeddedCustomListener |
| **eventTypes** (consumer) | Specifies the set of event types to register by the consumer.Multiple event can be separated by comma. The possible event types are: CACHE\_ENTRY\_ACTIVATED, CACHE\_ENTRY\_PASSIVATED, CACHE\_ENTRY\_VISITED, CACHE\_ENTRY\_LOADED, CACHE\_ENTRY\_EVICTED, CACHE\_ENTRY\_CREATED, CACHE\_ENTRY\_REMOVED, CACHE\_ENTRY\_MODIFIED, TRANSACTION\_COMPLETED, TRANSACTION\_REGISTERED, CACHE\_ENTRY\_INVALIDATED, CACHE\_ENTRY\_EXPIRED, DATA\_REHASHED, TOPOLOGY\_CHANGED, PARTITION\_STATUS\_CHANGED, PERSISTENCE\_AVAILABILITY\_CHANGED. |  | String |
| **sync** (consumer) | If true, the consumer will receive notifications synchronously. | true | boolean |
| **defaultValue** (producer) | Set a specific default value for some producer operations. |  | Object |
| **key** (producer) | Set a specific key for producer operations. |  | Object |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **oldValue** (producer) | Set a specific old value for some producer operations. |  | Object |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   PUT
    
-   PUTASYNC
    
-   PUTALL
    
-   PUTALLASYNC
    
-   PUTIFABSENT
    
-   PUTIFABSENTASYNC
    
-   GET
    
-   GETORDEFAULT
    
-   CONTAINSKEY
    
-   CONTAINSVALUE
    
-   REMOVE
    
-   REMOVEASYNC
    
-   REPLACE
    
-   REPLACEASYNC
    
-   SIZE
    
-   CLEAR
    
-   CLEARASYNC
    
-   QUERY
    
-   STATS
    
-   COMPUTE
    
-   COMPUTEASYNC
    





 | PUT | InfinispanOperation |
| **value** (producer) | Set a specific value for producer operations. |  | Object |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **cacheContainer** (advanced) | **Autowired** Specifies the cache Container to connect. |  | EmbeddedCacheManager |
| **cacheContainerConfiguration** (advanced) | **Autowired** The CacheContainer configuration. Used if the cacheContainer is not defined. |  | Configuration |
| **configurationUri** (advanced) | An implementation specific URI for the CacheManager. |  | String |
| **flags** (advanced) | A comma separated list of org.infinispan.context.Flag to be applied by default on each cache invocation. |  | String |
| **remappingFunction** (advanced) | Set a specific remappingFunction to use in a compute operation. |  | BiFunction |
| **resultHeader** (advanced) | Store the operation result in a header instead of the message body. By default, resultHeader == null and the query result is stored in the message body, any existing content in the message body is discarded. If resultHeader is set, the value is used as the name of the header to store the query result and the original message body is preserved. This value can be overridden by an in message header named: CamelInfinispanOperationResultHeader. |  | String |

## Endpoint Options

The Infinispan Embedded endpoint is configured using URI syntax:

infinispan-embedded:cacheName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheName** (common) | **Required** The name of the cache to use. Use current to use the existing cache name from the currently configured cached manager. Or use default for the default cache manager name. |  | String |

### Query Parameters (20 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **queryBuilder** (common) | Specifies the query builder. |  | InfinispanQueryBuilder |
| **clusteredListener** (consumer) | If true, the listener will be installed for the entire cluster. | false | boolean |
| **customListener** (consumer) | Returns the custom listener in use, if provided. |  | InfinispanEmbeddedCustomListener |
| **eventTypes** (consumer) | Specifies the set of event types to register by the consumer.Multiple event can be separated by comma. The possible event types are: CACHE\_ENTRY\_ACTIVATED, CACHE\_ENTRY\_PASSIVATED, CACHE\_ENTRY\_VISITED, CACHE\_ENTRY\_LOADED, CACHE\_ENTRY\_EVICTED, CACHE\_ENTRY\_CREATED, CACHE\_ENTRY\_REMOVED, CACHE\_ENTRY\_MODIFIED, TRANSACTION\_COMPLETED, TRANSACTION\_REGISTERED, CACHE\_ENTRY\_INVALIDATED, CACHE\_ENTRY\_EXPIRED, DATA\_REHASHED, TOPOLOGY\_CHANGED, PARTITION\_STATUS\_CHANGED, PERSISTENCE\_AVAILABILITY\_CHANGED. |  | String |
| **sync** (consumer) | If true, the consumer will receive notifications synchronously. | true | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **defaultValue** (producer) | Set a specific default value for some producer operations. |  | Object |
| **key** (producer) | Set a specific key for producer operations. |  | Object |
| **oldValue** (producer) | Set a specific old value for some producer operations. |  | Object |
| **operation** (producer) | 

The operation to perform.

Enum values:

-   PUT
    
-   PUTASYNC
    
-   PUTALL
    
-   PUTALLASYNC
    
-   PUTIFABSENT
    
-   PUTIFABSENTASYNC
    
-   GET
    
-   GETORDEFAULT
    
-   CONTAINSKEY
    
-   CONTAINSVALUE
    
-   REMOVE
    
-   REMOVEASYNC
    
-   REPLACE
    
-   REPLACEASYNC
    
-   SIZE
    
-   CLEAR
    
-   CLEARASYNC
    
-   QUERY
    
-   STATS
    
-   COMPUTE
    
-   COMPUTEASYNC
    





 | PUT | InfinispanOperation |
| **value** (producer) | Set a specific value for producer operations. |  | Object |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **cacheContainer** (advanced) | **Autowired** Specifies the cache Container to connect. |  | EmbeddedCacheManager |
| **cacheContainerConfiguration** (advanced) | **Autowired** The CacheContainer configuration. Used if the cacheContainer is not defined. |  | Configuration |
| **configurationUri** (advanced) | An implementation specific URI for the CacheManager. |  | String |
| **flags** (advanced) | A comma separated list of org.infinispan.context.Flag to be applied by default on each cache invocation. |  | String |
| **remappingFunction** (advanced) | Set a specific remappingFunction to use in a compute operation. |  | BiFunction |
| **resultHeader** (advanced) | Store the operation result in a header instead of the message body. By default, resultHeader == null and the query result is stored in the message body, any existing content in the message body is discarded. If resultHeader is set, the value is used as the name of the header to store the query result and the original message body is preserved. This value can be overridden by an in message header named: CamelInfinispanOperationResultHeader. |  | String |

## Message Headers

The Infinispan Embedded component supports 22 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelInfinispanEventType** (consumer) Constant: [`EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#EVENT_TYPE) | The type of the received event. |  | String |
| **CamelInfinispanIsPre** (consumer) Constant: [`IS_PRE`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#IS_PRE) | true if the notification is before the event has occurred, false if after the event has occurred. |  | boolean |
| **CamelInfinispanCacheName** (common) Constant: [`CACHE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#CACHE_NAME) | The cache participating in the operation or event. |  | String |
| **CamelInfinispanKey** (common) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#KEY) | The key to perform the operation to or the key generating the event. |  | Object |
| **CamelInfinispanValue** (producer) Constant: [`VALUE`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#VALUE) | The value to use for the operation. |  | Object |
| **CamelInfinispanDefaultValue** (producer) Constant: [`DEFAULT_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#DEFAULT_VALUE) | The default value to use for a getOrDefault. |  | Object |
| **CamelInfinispanOldValue** (producer) Constant: [`OLD_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#OLD_VALUE) | The old value to use for a replace. |  | Object |
| **CamelInfinispanMap** (producer) Constant: [`MAP`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#MAP) | A Map to use in case of CamelInfinispanOperationPutAll operation. |  | Map |
| **CamelInfinispanOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   PUT
    
-   PUTASYNC
    
-   PUTALL
    
-   PUTALLASYNC
    
-   PUTIFABSENT
    
-   PUTIFABSENTASYNC
    
-   GET
    
-   GETORDEFAULT
    
-   CONTAINSKEY
    
-   CONTAINSVALUE
    
-   REMOVE
    
-   REMOVEASYNC
    
-   REPLACE
    
-   REPLACEASYNC
    
-   SIZE
    
-   CLEAR
    
-   CLEARASYNC
    
-   QUERY
    
-   STATS
    
-   COMPUTE
    
-   COMPUTEASYNC
    





 |  | InfinispanOperation |
| **CamelInfinispanOperationResult** (producer) Constant: [`RESULT`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#RESULT) | The name of the header whose value is the result. |  | String |
| **CamelInfinispanOperationResultHeader** (producer) Constant: [`RESULT_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#RESULT_HEADER) | Store the operation result in a header instead of the message body. |  | String |
| **CamelInfinispanLifespanTime** (producer) Constant: [`LIFESPAN_TIME`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#LIFESPAN_TIME) | The Lifespan time of a value inside the cache. Negative values are interpreted as infinity. |  | long |
| **CamelInfinispanTimeUnit** (producer) Constant: [`LIFESPAN_TIME_UNIT`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#LIFESPAN_TIME_UNIT) | 

The Time Unit of an entry Lifespan Time.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 |  | TimeUnit |
| **CamelInfinispanMaxIdleTime** (producer) Constant: [`MAX_IDLE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#MAX_IDLE_TIME) | The maximum amount of time an entry is allowed to be idle for before it is considered as expired. |  | long |
| **CamelInfinispanMaxIdleTimeUnit** (producer) Constant: [`MAX_IDLE_TIME_UNIT`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#MAX_IDLE_TIME_UNIT) | 

The Time Unit of an entry Max Idle Time.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 |  | TimeUnit |
| **CamelInfinispanIgnoreReturnValues** (consumer) Constant: [`IGNORE_RETURN_VALUES`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#IGNORE_RETURN_VALUES) | Signals that a write operation’s return value will be ignored, so reading the existing value from a store or from a remote node is not necessary. | false | boolean |
| **CamelInfinispanEventData** (consumer) Constant: [`EVENT_DATA`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#EVENT_DATA) | The event data. |  | Object |
| **CamelInfinispanQueryBuilder** (producer) Constant: [`QUERY_BUILDER`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#QUERY_BUILDER) | The QueryBuilder to use for QUERY command, if not present the command defaults to InifinispanConfiguration’s one. |  | InfinispanQueryBuilder |
| **CamelInfinispanCommandRetried** (consumer) Constant: [`COMMAND_RETRIED`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#COMMAND_RETRIED) | This will be true if the write command that caused this had to be retried again due to a topology change. |  | boolean |
| **CamelInfinispanEntryCreated** (consumer) Constant: [`ENTRY_CREATED`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#ENTRY_CREATED) | Indicates whether the cache entry modification event is the result of the cache entry being created. |  | boolean |
| **CamelInfinispanOriginLocal** (consumer) Constant: [`ORIGIN_LOCAL`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#ORIGIN_LOCAL) | true if the call originated on the local cache instance; false if originated from a remote one. |  | boolean |
| **CamelInfinispanCurrentState** (consumer) Constant: [`CURRENT_STATE`](https://javadoc.io/doc/org.apache.camel/camel-infinispan-embedded/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#CURRENT_STATE) | True if this event is generated from an existing entry as the listener has Listener. |  | boolean |

## Usage

### Camel Operations

This section lists all available operations, along with their header information.

Table 1. Put Operations  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.PUT` | Put a key/value pair in the cache, optionally with expiration |
| `InfinispanOperation.PUTASYNC` | Asynchronously puts a key/value pair in the cache, optionally with expiration |
| `InfinispanOperation.PUTIFABSENT` | Put a key/value pair in the cache if it did not exist, optionally with expiration |
| `InfinispanOperation.PUTIFABSENTASYNC` | Asynchronously puts a key/value pair in the cache if it did not exist, optionally with expiration |

-   **Required Headers**:
    
    -   `CamelInfinispanKey`
        
    -   `CamelInfinispanValue`
        
    
-   **Optional Headers**:
    
    -   `CamelInfinispanLifespanTime`
        
    -   `CamelInfinispanLifespanTimeUnit`
        
    -   `CamelInfinispanMaxIdleTime`
        
    -   `CamelInfinispanMaxIdleTimeUnit`
        
    
-   **Result Header**:
    
    -   `CamelInfinispanOperationResult`
        
    

Table 2. Put All Operations  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.PUTALL` | Adds multiple entries to a cache, optionally with expiration |
| `CamelInfinispanOperation.PUTALLASYNC` | Asynchronously adds multiple entries to a cache, optionally with expiration |

-   **Required Headers**:
    
    -   CamelInfinispanMap
        
    
-   **Optional Headers**:
    
    -   `CamelInfinispanLifespanTime`
        
    -   `CamelInfinispanLifespanTimeUnit`
        
    -   `CamelInfinispanMaxIdleTime`
        
    -   `CamelInfinispanMaxIdleTimeUnit`
        
    

Table 3. Get Operations  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.GET` | Retrieve the value associated with a specific key from the cache |
| `InfinispanOperation.GETORDEFAULT` | Retrieves the value, or default value, associated with a specific key from the cache |

-   **Required Headers**:
    
    -   `CamelInfinispanKey`
        
    

Table 4. Contains Key Operation  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.CONTAINSKEY` | Determines whether a cache contains a specific key |

-   **Required Headers**
    
    -   `CamelInfinispanKey`
        
    
-   **Result Header**
    
    -   `CamelInfinispanOperationResult`
        
    

Table 5. Contains Value Operation  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.CONTAINSVALUE` | Determines whether a cache contains a specific value |

-   **Required Headers**:
    
    -   `CamelInfinispanKey`
        
    

Table 6. Remove Operations  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.REMOVE` | Removes an entry from a cache, optionally only if the value matches a given one |
| `InfinispanOperation.REMOVEASYNC` | Asynchronously removes an entry from a cache, optionally only if the value matches a given one |

-   **Required Headers**:
    
    -   `CamelInfinispanKey`
        
    
-   **Optional Headers**:
    
    -   `CamelInfinispanValue`
        
    
-   **Result Header**:
    
    -   `CamelInfinispanOperationResult`
        
    

Table 7. Replace Operations  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.REPLACE` | Conditionally replaces an entry in the cache, optionally with expiration |
| `InfinispanOperation.REPLACEASYNC` | Asynchronously conditionally replaces an entry in the cache, optionally with expiration |

-   **Required Headers**:
    
    -   `CamelInfinispanKey`
        
    -   `CamelInfinispanValue`
        
    -   `CamelInfinispanOldValue`
        
    
-   **Optional Headers**:
    
    -   `CamelInfinispanLifespanTime`
        
    -   `CamelInfinispanLifespanTimeUnit`
        
    -   `CamelInfinispanMaxIdleTime`
        
    -   `CamelInfinispanMaxIdleTimeUnit`
        
    
-   **Result Header**:
    
    -   `CamelInfinispanOperationResult`
        
    

Table 8. Clear Operations  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.CLEAR` | Clears the cache |
| `InfinispanOperation.CLEARASYNC` | Asynchronously clears the cache |Table 9. Size Operation  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.SIZE` | Returns the number of entries in the cache |

-   **Result Header**
    
    -   `CamelInfinispanOperationResult`
        
    

Table 10. Stats Operation  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.STATS` | Returns statistics about the cache |

-   **Result Header**:
    
    -   `CamelInfinispanOperationResult`
        
    

Table 11. Query Operation  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.QUERY` | Executes a query on the cache |

-   **Required Headers**:
    
    -   `CamelInfinispanQueryBuilder`
        
    
-   **Result Header**:
    
    -   `CamelInfinispanOperationResult`
        
    

> **Note**
> Write methods like put(key, value) and remove(key) do not return the previous value by default.

## Examples

-   Put a key/value into a named cache:
    
    _Java-only: uses InfinispanConstants and InfinispanOperation Java constants_
    
    ```java
    from("direct:start")
        .setHeader(InfinispanConstants.OPERATION).constant(InfinispanOperation.PUT) (1)
        .setHeader(InfinispanConstants.KEY).constant("123") (2)
        .to("infinispan:myCacheName&cacheContainer=#cacheContainer"); (3)
    ```
    
    <table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Set the operation to perform</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Set the key used to identify the element in the cache</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>Use the configured cache manager <code>cacheContainer</code> from the registry to put an element to the cache named <code>myCacheName</code></td></tr></tbody></table>
    
    It is possible to configure the lifetime and/or the idle time before the entry expires and gets evicted from the cache, as example:
    
    _Java-only: uses InfinispanConstants Java constants and TimeUnit enum_
    
    ```java
    from("direct:start")
        .setHeader(InfinispanConstants.OPERATION).constant(InfinispanOperation.GET)
        .setHeader(InfinispanConstants.KEY).constant("123")
        .setHeader(InfinispanConstants.LIFESPAN_TIME).constant(100L) (1)
        .setHeader(InfinispanConstants.LIFESPAN_TIME_UNIT).constant(TimeUnit.MILLISECONDS.toString()) (2)
        .to("infinispan:myCacheName");
    ```
    
    <table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Set the lifespan of the entry</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Set the time unit for the lifespan</td></tr></tbody></table>
    
-   Queries
    
    _Java-only: uses InfinispanQueryBuilder anonymous class and Java constants_
    
    ```java
    from("direct:start")
        .setHeader(InfinispanConstants.OPERATION, InfinispanConstants.QUERY)
        .setHeader(InfinispanConstants.QUERY_BUILDER, new InfinispanQueryBuilder() {
            @Override
            public Query build(QueryFactory<Query> qf) {
                return qf.from(User.class).having("name").like("%abc%").build();
            }
        })
        .to("infinispan:myCacheName?cacheContainer=#cacheManager") ;
    ```
    
-   Custom Listeners
    
    -   Java
        
    -   XML
        
    -   YAML
        
    
    ```java
    from("infinispan://?cacheContainer=#cacheManager&customListener=#myCustomListener")
      .to("mock:result");
    ```
    
    ```xml
    <route>
      <from uri="infinispan://?cacheContainer=#cacheManager&amp;customListener=#myCustomListener"/>
      <to uri="mock:result"/>
    </route>
    ```
    
    ```yaml
    - route:
        from:
          uri: "infinispan://"
          parameters:
            cacheContainer: "#cacheManager"
            customListener: "#myCustomListener"
        steps:
          - to:
              uri: mock:result
    ```
    
    The instance of `myCustomListener` must exist and Camel should be able to look it up from the `Registry`. Users are encouraged to extend the `org.apache.camel.component.infinispan.embedded.InfinispanEmbeddedCustomListener` class and annotate the resulting class with `@Listener` which can be found in the package `org.infinispan.notifications`.
    

### Using the Infinispan based idempotent repository

In this section, we will use the Infinispan based idempotent repository.

-   Java
    
-   XML
    

```java
InfinispanEmbeddedConfiguration conf = new InfinispanEmbeddedConfiguration(); (1)
conf.setConfigurationUri("classpath:infinispan.xml")

InfinispanEmbeddedIdempotentRepository repo = new InfinispanEmbeddedIdempotentRepository("idempotent");  (2)
repo.setConfiguration(conf);

context.addRoutes(new RouteBuilder() {
    @Override
    public void configure() {
        from("direct:start")
            .idempotentConsumer(header("MessageID"), repo) (3)
            .to("mock:result");
    }
});
```

1.  Configure the cache
    
2.  Configure the repository bean
    
3.  Set the repository to the route
    

```xml
<bean id="infinispanRepo" class="org.apache.camel.component.infinispan.embedded.InfinispanEmbeddedIdempotentRepository" destroy-method="stop">
  <constructor-arg value="idempotent"/> (1)
  <property name="configuration"> (2)
    <bean class="org.apache.camel.component.infinispan.embedded.InfinispanEmbeddedConfiguration">
      <property name="configurationUrl" value="classpath:infinispan.xml"/>
    </bean>
  </property>
</bean>

<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route>
        <from uri="direct:start" />
        <idempotentConsumer idempotentRepository="infinispanRepo"> (3)
            <header>MessageID</header>
            <to uri="mock:result" />
        </idempotentConsumer>
    </route>
</camelContext>
```

1.  Set the name of the cache that will be used by the repository
    
2.  Configure the repository bean
    
3.  Set the repository to the route
    

### Using the Infinispan based aggregation repository

In this section, we will use the Infinispan based aggregation repository.

-   Java
    
-   XML
    

```java
InfinispanEmbeddedConfiguration conf = new InfinispanEmbeddedConfiguration(); (1)
conf.setConfigurationUri("classpath:infinispan.xml");

InfinispanEmbeddedAggregationRepository repo = new InfinispanEmbeddedAggregationRepository("aggregation");  (2)
repo.setConfiguration(conf);

context.addRoutes(new RouteBuilder() {
    @Override
    public void configure() {
        from("direct:start")
                .aggregate(header("MessageID"))
                .completionSize(3)
                .aggregationRepository(repo) (3)
                .aggregationStrategy("myStrategy")
                .to("mock:result");
    }
});
```

1.  Configure the cache
    
2.  Create the repository bean
    
3.  Set the repository to the route
    

```xml
<bean id="infinispanRepo" class="org.apache.camel.component.infinispan.embedded.InfinispanEmbeddedAggregationRepository" destroy-method="stop">
  <constructor-arg value="aggregation"/> (1)
  <property name="configuration"> (2)
    <bean class="org.apache.camel.component.infinispan.embedded.InfinispanEmbeddedConfiguration">
      <property name="configurationUrl" value="classpath:infinispan.xml"/>
    </bean>
  </property>
</bean>

<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route>
        <from uri="direct:start" />
        <aggregate aggregationStrategy="myStrategy"
                   completionSize="3"
                   aggregationRepository="infinispanRepo"> (3)
            <correlationExpression>
                <header>MessageID</header>
            </correlationExpression>
            <to uri="mock:result"/>
        </aggregate>
    </route>
</camelContext>
```

1.  Set the name of the cache that will be used by the repository
    
2.  Configure the repository bean
    
3.  Set the repository to the route
    

> **Note**
> With the release of Infinispan 11, it is required to set the encoding configuration on any cache created. This is critical for consuming events too. For more information, have a look at [Data Encoding and MediaTypes](https://infinispan.org/docs/stable/titles/developing/developing.html#data_encoding) in the official Infinispan documentation.