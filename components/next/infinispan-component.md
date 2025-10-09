# Infinispan

**Since Camel 2.13**

**Both producer and consumer are supported**

This component allows you to interact with [Infinispan](http://infinispan.org/) distributed data grid / cache using the Hot Rod protocol. Infinispan is an extremely scalable, highly available key/value data store and data grid platform written in Java.

If you use Maven, you must add the following dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-infinispan</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

infinispan://cacheName?\[options\]

The producer allows sending messages to a remote cache using the HotRod protocol. The consumer allows listening for events from a remote cache using the HotRod protocol.

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

The Infinispan component supports 33 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | Component configuration. |  | InfinispanRemoteConfiguration |
| **hosts** (common) | Specifies the host of the cache on Infinispan instance. Multiple hosts can be separated by semicolon. |  | String |
| **queryBuilder** (common) | Specifies the query builder. |  | InfinispanQueryBuilder |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **customListener** (consumer) | Returns the custom listener in use, if provided. |  | InfinispanRemoteCustomListener |
| **eventTypes** (consumer) | Specifies the set of event types to register by the consumer.Multiple event can be separated by comma. The possible event types are: CLIENT\_CACHE\_ENTRY\_CREATED, CLIENT\_CACHE\_ENTRY\_MODIFIED, CLIENT\_CACHE\_ENTRY\_REMOVED, CLIENT\_CACHE\_ENTRY\_EXPIRED, CLIENT\_CACHE\_FAILOVER. |  | String |
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
| **embeddingStoreDimension** (producer (advanced)) | The dimension size used to store vector embeddings. This should be equal to the dimension size of the model used to create the vector embeddings. This option is mandatory if the embedding store is enabled. |  | int |
| **embeddingStoreDistance** (producer (advanced)) | The distance to use for kNN search queries in relation to the configured vector similarity. | 3 | int |
| **embeddingStoreEnabled** (producer (advanced)) | Whether to enable the embedding store. When enabled, the embedding store will be configured automatically when Camel starts. Note that this feature requires camel-langchain4j-embeddings to be on the classpath. | true | boolean |
| **embeddingStoreRegisterSchema** (producer (advanced)) | Whether to automatically register the proto schema for the types required by embedding store cache put and query operations. | true | boolean |
| **embeddingStoreSchemaRegistrationTimeout** (producer (advanced)) | Maximum time to wait for the Infinispan server to be ready when registering the embedding store schema. This handles the case where Camel and the Infinispan server start concurrently. | 60s | Duration |
| **embeddingStoreTypeName** (producer (advanced)) | The name of the type used to store embeddings. The default is 'InfinispanRemoteEmbedding' suffixed with the value of the embeddingStoreDimension option. E.g. CamelInfinispanRemoteEmbedding384. |  | String |
| **embeddingStoreVectorSimilarity** (producer (advanced)) | 

The vector similarity algorithm used to store embeddings.

Enum values:

-   L2
    
-   INNER\_PRODUCT
    
-   MAX\_INNER\_PRODUCT
    
-   COSINE
    





 | COSINE | VectorSimilarity |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **cacheContainer** (advanced) | **Autowired** Specifies the cache Container to connect. |  | RemoteCacheManager |
| **cacheContainerConfiguration** (advanced) | **Autowired** The CacheContainer configuration. Used if the cacheContainer is not defined. |  | Configuration |
| **configurationProperties** (advanced) | Implementation specific properties for the CacheManager. |  | Map |
| **configurationUri** (advanced) | An implementation specific URI for the CacheManager. |  | String |
| **flags** (advanced) | A comma separated list of org.infinispan.client.hotrod.Flag to be applied by default on each cache invocation. |  | String |
| **remappingFunction** (advanced) | Set a specific remappingFunction to use in a compute operation. |  | BiFunction |
| **resultHeader** (advanced) | Store the operation result in a header instead of the message body. By default, resultHeader == null and the query result is stored in the message body, any existing content in the message body is discarded. If resultHeader is set, the value is used as the name of the header to store the query result and the original message body is preserved. This value can be overridden by an in message header named: CamelInfinispanOperationResultHeader. |  | String |
| **password** (security) | Define the password to access the infinispan instance. |  | String |
| **saslMechanism** (security) | Define the SASL Mechanism to access the infinispan instance. |  | String |
| **secure** (security) | Define if we are connecting to a secured Infinispan instance. | false | boolean |
| **securityRealm** (security) | Define the security realm to access the infinispan instance. |  | String |
| **securityServerName** (security) | Define the security server name to access the infinispan instance. |  | String |
| **username** (security) | Define the username to access the infinispan instance. |  | String |

## Endpoint Options

The Infinispan endpoint is configured using URI syntax:

infinispan:cacheName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheName** (common) | **Required** The name of the cache to use. Use current to use the existing cache name from the currently configured cached manager. Or use default for the default cache manager name. |  | String |

### Query Parameters (33 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **hosts** (common) | Specifies the host of the cache on Infinispan instance. Multiple hosts can be separated by semicolon. |  | String |
| **queryBuilder** (common) | Specifies the query builder. |  | InfinispanQueryBuilder |
| **customListener** (consumer) | Returns the custom listener in use, if provided. |  | InfinispanRemoteCustomListener |
| **eventTypes** (consumer) | Specifies the set of event types to register by the consumer.Multiple event can be separated by comma. The possible event types are: CLIENT\_CACHE\_ENTRY\_CREATED, CLIENT\_CACHE\_ENTRY\_MODIFIED, CLIENT\_CACHE\_ENTRY\_REMOVED, CLIENT\_CACHE\_ENTRY\_EXPIRED, CLIENT\_CACHE\_FAILOVER. |  | String |
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
| **embeddingStoreDimension** (producer (advanced)) | The dimension size used to store vector embeddings. This should be equal to the dimension size of the model used to create the vector embeddings. This option is mandatory if the embedding store is enabled. |  | int |
| **embeddingStoreDistance** (producer (advanced)) | The distance to use for kNN search queries in relation to the configured vector similarity. | 3 | int |
| **embeddingStoreEnabled** (producer (advanced)) | Whether to enable the embedding store. When enabled, the embedding store will be configured automatically when Camel starts. Note that this feature requires camel-langchain4j-embeddings to be on the classpath. | true | boolean |
| **embeddingStoreRegisterSchema** (producer (advanced)) | Whether to automatically register the proto schema for the types required by embedding store cache put and query operations. | true | boolean |
| **embeddingStoreSchemaRegistrationTimeout** (producer (advanced)) | Maximum time to wait for the Infinispan server to be ready when registering the embedding store schema. This handles the case where Camel and the Infinispan server start concurrently. | 60s | Duration |
| **embeddingStoreTypeName** (producer (advanced)) | The name of the type used to store embeddings. The default is 'InfinispanRemoteEmbedding' suffixed with the value of the embeddingStoreDimension option. E.g. CamelInfinispanRemoteEmbedding384. |  | String |
| **embeddingStoreVectorSimilarity** (producer (advanced)) | 

The vector similarity algorithm used to store embeddings.

Enum values:

-   L2
    
-   INNER\_PRODUCT
    
-   MAX\_INNER\_PRODUCT
    
-   COSINE
    





 | COSINE | VectorSimilarity |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **cacheContainer** (advanced) | **Autowired** Specifies the cache Container to connect. |  | RemoteCacheManager |
| **cacheContainerConfiguration** (advanced) | **Autowired** The CacheContainer configuration. Used if the cacheContainer is not defined. |  | Configuration |
| **configurationProperties** (advanced) | Implementation specific properties for the CacheManager. |  | Map |
| **configurationUri** (advanced) | An implementation specific URI for the CacheManager. |  | String |
| **flags** (advanced) | A comma separated list of org.infinispan.client.hotrod.Flag to be applied by default on each cache invocation. |  | String |
| **remappingFunction** (advanced) | Set a specific remappingFunction to use in a compute operation. |  | BiFunction |
| **resultHeader** (advanced) | Store the operation result in a header instead of the message body. By default, resultHeader == null and the query result is stored in the message body, any existing content in the message body is discarded. If resultHeader is set, the value is used as the name of the header to store the query result and the original message body is preserved. This value can be overridden by an in message header named: CamelInfinispanOperationResultHeader. |  | String |
| **password** (security) | Define the password to access the infinispan instance. |  | String |
| **saslMechanism** (security) | Define the SASL Mechanism to access the infinispan instance. |  | String |
| **secure** (security) | Define if we are connecting to a secured Infinispan instance. | false | boolean |
| **securityRealm** (security) | Define the security realm to access the infinispan instance. |  | String |
| **securityServerName** (security) | Define the security server name to access the infinispan instance. |  | String |
| **username** (security) | Define the username to access the infinispan instance. |  | String |

## Message Headers

The Infinispan component supports 18 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelInfinispanEventType** (consumer) Constant: [`EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#EVENT_TYPE) | The type of the received event. |  | String |
| **CamelInfinispanCacheName** (common) Constant: [`CACHE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#CACHE_NAME) | The cache participating in the operation or event. |  | String |
| **CamelInfinispanKey** (common) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#KEY) | The key to perform the operation to or the key generating the event. |  | Object |
| **CamelInfinispanValue** (producer) Constant: [`VALUE`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#VALUE) | The value to use for the operation. |  | Object |
| **CamelInfinispanDefaultValue** (producer) Constant: [`DEFAULT_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#DEFAULT_VALUE) | The default value to use for a getOrDefault. |  | Object |
| **CamelInfinispanOldValue** (producer) Constant: [`OLD_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#OLD_VALUE) | The old value to use for a replace. |  | Object |
| **CamelInfinispanMap** (producer) Constant: [`MAP`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#MAP) | A Map to use in case of CamelInfinispanOperationPutAll operation. |  | Map |
| **CamelInfinispanOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#OPERATION) | 
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
| **CamelInfinispanOperationResult** (producer) Constant: [`RESULT`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#RESULT) | The name of the header whose value is the result. |  | String |
| **CamelInfinispanOperationResultHeader** (producer) Constant: [`RESULT_HEADER`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#RESULT_HEADER) | Store the operation result in a header instead of the message body. |  | String |
| **CamelInfinispanLifespanTime** (producer) Constant: [`LIFESPAN_TIME`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#LIFESPAN_TIME) | The Lifespan time of a value inside the cache. Negative values are interpreted as infinity. |  | long |
| **CamelInfinispanTimeUnit** (producer) Constant: [`LIFESPAN_TIME_UNIT`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#LIFESPAN_TIME_UNIT) | 

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
| **CamelInfinispanMaxIdleTime** (producer) Constant: [`MAX_IDLE_TIME`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#MAX_IDLE_TIME) | The maximum amount of time an entry is allowed to be idle for before it is considered as expired. |  | long |
| **CamelInfinispanMaxIdleTimeUnit** (producer) Constant: [`MAX_IDLE_TIME_UNIT`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#MAX_IDLE_TIME_UNIT) | 

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
| **CamelInfinispanEventData** (consumer) Constant: [`EVENT_DATA`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#EVENT_DATA) | The event data. |  | Object |
| **CamelInfinispanQueryBuilder** (producer) Constant: [`QUERY_BUILDER`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#QUERY_BUILDER) | The QueryBuilder to use for QUERY command, if not present the command defaults to InifinispanConfiguration’s one. |  | InfinispanQueryBuilder |
| **CamelInfinispanEntryVersion** (consumer) Constant: [`ENTRY_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#ENTRY_VERSION) | Provides access to the version of the created cache entry. |  | long |
| **CamelInfinispanCommandRetried** (consumer) Constant: [`COMMAND_RETRIED`](https://javadoc.io/doc/org.apache.camel/camel-infinispan/latest/org/apache/camel/component/infinispan/InfinispanConstants.html#COMMAND_RETRIED) | This will be true if the write command that caused this had to be retried again due to a topology change. |  | boolean |

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
    
    -   `CamelInfinispanMap`
        
    
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
    
    -   `CamelInfinispanKey` The resulting value is returned in the exchange **body**.
        
    

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
    
    -   `CamelInfinispanValue`
        
    
-   **Result Header**
    
    -   `CamelInfinispanOperationResult`
        
    

Table 6. Remove Operations  
| Operation Name | Description |
| --- | --- |
| `InfinispanOperation.REMOVE` | Removes an entry from a cache, optionally only if the value matches a given one |
| `InfinispanOperation.REMOVEASYNC` | Asynchronously removes an entry from a cache, optionally only if the value matches a given one |

-   **Required Headers**:
    
    -   `CamelInfinispanValue`
        
    
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
    
    -   `CamelInfinispanQueryBuilder` The resulting value is returned in the exchange **body**.
        
    

> **Note**
> Write methods like put(key, value) and remove(key) do not return the previous value by default.

## Examples

-   Put a key/value into a named cache:
    
    ```java
    from("direct:start")
        .setHeader(InfinispanConstants.OPERATION).constant(InfinispanOperation.PUT) (1)
        .setHeader(InfinispanConstants.KEY).constant("123") (2)
        .to("infinispan:myCacheName&cacheContainer=#cacheContainer"); (3)
    ```
    
    <table><tbody><tr><td><i class="conum" data-value="1"></i><b>1</b></td><td>Set the operation to perform</td></tr><tr><td><i class="conum" data-value="2"></i><b>2</b></td><td>Set the key used to identify the element in the cache</td></tr><tr><td><i class="conum" data-value="3"></i><b>3</b></td><td>Use the configured cache manager <code>cacheContainer</code> from the registry to put an element to the cache named <code>myCacheName</code></td></tr></tbody></table>
    
    It is possible to configure the lifetime and/or the idle time before the entry expires and gets evicted from the cache, as example:
    
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
    
    > **Note**
    > The .proto descriptors for domain objects must be registered with the remote Data Grid server, see [Remote Query Example](https://infinispan.org/docs/stable/titles/developing/developing.html#remote_query_example) in the official Infinispan documentation.
    
-   Custom Listeners
    
    ```java
    from("infinispan://?cacheContainer=#cacheManager&customListener=#myCustomListener")
      .to("mock:result");
    ```
    
    The instance of `myCustomListener` must exist and Camel should be able to look it up from the `Registry`. Users are encouraged to extend the `org.apache.camel.component.infinispan.remote.InfinispanRemoteCustomListener` class and annotate the resulting class with `@ClientListener` which can be found in the package `org.infinispan.client.hotrod.annotation`.
    

### Using the Infinispan based idempotent repository

In this section, we will use the Infinispan based idempotent repository.

-   Java
    
-   XML
    

```java
InfinispanRemoteConfiguration conf = new InfinispanRemoteConfiguration(); (1)
conf.setHosts("localhost:1122");

InfinispanRemoteIdempotentRepository repo = new InfinispanRemoteIdempotentRepository("idempotent");  (2)
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
<bean id="infinispanRepo" class="org.apache.camel.component.infinispan.remote.InfinispanRemoteIdempotentRepository" destroy-method="stop">
  <constructor-arg value="idempotent"/> (1)
  <property name="configuration"> (2)
    <bean class="org.apache.camel.component.infinispan.remote.InfinispanRemoteConfiguration">
      <property name="hosts" value="localhost:11222"/>
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
InfinispanRemoteConfiguration conf = new InfinispanRemoteConfiguration(); (1)
conf.setHosts("localhost:1122");

InfinispanRemoteAggregationRepository repo = new InfinispanRemoteAggregationRepository();  (2)
repo.setCacheName("aggregation");
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
<bean id="infinispanRepo" class="org.apache.camel.component.infinispan.remote.InfinispanRemoteAggregationRepository" destroy-method="stop">
  <constructor-arg value="aggregation"/> (1)
  <property name="configuration"> (2)
    <bean class="org.apache.camel.component.infinispan.remote.InfinispanRemoteConfiguration">
      <property name="hosts" value="localhost:11222"/>
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
    

### Embedding store support with camel-langchain4j-embeddings

This component provides the capability to store and query vector embeddings. To activate this functionality, add `camel-langchain4j-embeddings` to your project.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-langchain4j-embeddings</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.x.x</version>
</dependency>
```

If you want to disable this functionality, set the `embeddingStoreEnabled` option to `false`.

To store an embedding:

```java
from("direct:put")
    // Create an embedding from the message body
    .to("langchain4j-embeddings:create")
    .setHeader(InfinispanConstants.OPERATION).constant(InfinispanOperation.PUT)
    // Transform the embedding to a format usable by Infinispan
    .transformDataType(new DataType("infinispan:embeddings"))
    // Store the embedding
    .to("infinispan:myCache?embeddingStoreDimension=384");
```

The `embeddingStoreDimension` option **must** be specified. It must also match the dimension of the embedding model used by the `langchain4j-embeddings` endpoint.

To query embeddings:

```java
from("direct:query")
    // Create an embedding from the message body
    .to("langchain4j-embeddings:create")
    .setHeader(InfinispanConstants.OPERATION).constant(InfinispanOperation.QUERY)
    // Transforms the embedding to a vector kNN search
    .transformDataType(new DataType("infinispan:embeddings"))
    // Query embeddings
    .to("infinispan:myCache?embeddingStoreDimension=384");
```

By default, a simple [vector kNN search](https://infinispan.org/docs/stable/titles/query/query.html#vector-search_ickle-query-language) query is executed that looks like the following.

```sql
select i, score(i) from InfinispanRemoteEmbedding i
where i.embedding <-> [the vector embedding]~3
```

The `~3` part determines the distance from the search vector embedding, in relation to the configured vector similarity. These can be modified via the `embeddingStoreDistance` and `embeddingStoreVectorSimilarity` options.

The result of the query operation is `List<Object[]>`. The elements of the `Object` array are as follows.

  
| Index | Type | Description |
| --- | --- | --- |
| 0 | `InfinispanRemoteEmbedding` | Information about the embedding such as the embedding text and its `float` array representation. |
| 1 | `Float` | The score in relation to how closely the embedding matches the search text. |
> **Note**
> With the release of Infinispan 11, it is required to set the encoding configuration on any cache created. This is critical for consuming events too. For more information, have a look at [Data Encoding and MediaTypes](https://infinispan.org/docs/stable/titles/developing/developing.html#data_encoding) in the official Infinispan documentation.

## Spring Boot Auto-Configuration

When using infinispan with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-infinispan-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 30 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.infinispan.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.infinispan.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.infinispan.cache-container** | Specifies the cache Container to connect. The option is a org.infinispan.client.hotrod.RemoteCacheManager type. |  | RemoteCacheManager |
| **camel.component.infinispan.cache-container-configuration** | The CacheContainer configuration. Used if the cacheContainer is not defined. The option is a org.infinispan.client.hotrod.configuration.Configuration type. |  | Configuration |
| **camel.component.infinispan.configuration** | Component configuration. The option is a org.apache.camel.component.infinispan.remote.InfinispanRemoteConfiguration type. |  | InfinispanRemoteConfiguration |
| **camel.component.infinispan.configuration-properties** | Implementation specific properties for the CacheManager. |  | Map |
| **camel.component.infinispan.configuration-uri** | An implementation specific URI for the CacheManager. |  | String |
| **camel.component.infinispan.custom-listener** | Returns the custom listener in use, if provided. The option is a org.apache.camel.component.infinispan.remote.InfinispanRemoteCustomListener type. |  | InfinispanRemoteCustomListener |
| **camel.component.infinispan.embedding-store-dimension** | The dimension size used to store vector embeddings. This should be equal to the dimension size of the model used to create the vector embeddings. This option is mandatory if the embedding store is enabled. |  | Integer |
| **camel.component.infinispan.embedding-store-distance** | The distance to use for kNN search queries in relation to the configured vector similarity. | 3 | Integer |
| **camel.component.infinispan.embedding-store-enabled** | Whether to enable the embedding store. When enabled, the embedding store will be configured automatically when Camel starts. Note that this feature requires camel-langchain4j-embeddings to be on the classpath. | true | Boolean |
| **camel.component.infinispan.embedding-store-register-schema** | Whether to automatically register the proto schema for the types required by embedding store cache put and query operations. | true | Boolean |
| **camel.component.infinispan.embedding-store-schema-registration-timeout** | Maximum time to wait for the Infinispan server to be ready when registering the embedding store schema. This handles the case where Camel and the Infinispan server start concurrently. | 60000ms | Duration |
| **camel.component.infinispan.embedding-store-type-name** | The name of the type used to store embeddings. The default is 'InfinispanRemoteEmbedding' suffixed with the value of the embeddingStoreDimension option. E.g. CamelInfinispanRemoteEmbedding384. |  | String |
| **camel.component.infinispan.embedding-store-vector-similarity** | The vector similarity algorithm used to store embeddings. | cosine | VectorSimilarity |
| **camel.component.infinispan.enabled** | Whether to enable auto configuration of the infinispan component. This is enabled by default. |  | Boolean |
| **camel.component.infinispan.event-types** | Specifies the set of event types to register by the consumer.Multiple event can be separated by comma. The possible event types are: CLIENT\_CACHE\_ENTRY\_CREATED, CLIENT\_CACHE\_ENTRY\_MODIFIED, CLIENT\_CACHE\_ENTRY\_REMOVED, CLIENT\_CACHE\_ENTRY\_EXPIRED, CLIENT\_CACHE\_FAILOVER. |  | String |
| **camel.component.infinispan.flags** | A comma separated list of org.infinispan.client.hotrod.Flag to be applied by default on each cache invocation. |  | String |
| **camel.component.infinispan.hosts** | Specifies the host of the cache on Infinispan instance. Multiple hosts can be separated by semicolon. |  | String |
| **camel.component.infinispan.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.infinispan.operation** | The operation to perform. | put | InfinispanOperation |
| **camel.component.infinispan.password** | Define the password to access the infinispan instance. |  | String |
| **camel.component.infinispan.query-builder** | Specifies the query builder. The option is a org.apache.camel.component.infinispan.InfinispanQueryBuilder type. |  | InfinispanQueryBuilder |
| **camel.component.infinispan.remapping-function** | Set a specific remappingFunction to use in a compute operation. The option is a java.util.function.BiFunction type. |  | BiFunction |
| **camel.component.infinispan.result-header** | Store the operation result in a header instead of the message body. By default, resultHeader == null and the query result is stored in the message body, any existing content in the message body is discarded. If resultHeader is set, the value is used as the name of the header to store the query result and the original message body is preserved. This value can be overridden by an in message header named: CamelInfinispanOperationResultHeader. |  | String |
| **camel.component.infinispan.sasl-mechanism** | Define the SASL Mechanism to access the infinispan instance. |  | String |
| **camel.component.infinispan.secure** | Define if we are connecting to a secured Infinispan instance. | false | Boolean |
| **camel.component.infinispan.security-realm** | Define the security realm to access the infinispan instance. |  | String |
| **camel.component.infinispan.security-server-name** | Define the security server name to access the infinispan instance. |  | String |
| **camel.component.infinispan.username** | Define the username to access the infinispan instance. |  | String |