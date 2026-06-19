# Caffeine LoadCache

**Since Camel 2.20**

**Only producer is supported**

The Caffeine LoadCache component enables you to perform caching operations using the LoadingCache from Caffeine.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-caffeine</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

caffeine-loadcache://cacheName\[?options\]

You can append query options to the URI in the following format: `?option=value&option=#beanRef&…​`

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

The Caffeine LoadCache component supports 16 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
To configure the default cache action. If an action is set in the message header, then the operation from the header takes precedence.

Enum values:

-   GET
    
-   GET\_ALL
    
-   PUT
    
-   PUT\_ALL
    
-   INVALIDATE
    
-   INVALIDATE\_ALL
    
-   CLEANUP
    
-   AS\_MAP
    





 |  | String |
| **createCacheIfNotExist** (producer) | Automatic create the Caffeine cache if none has been configured or exists in the registry. | true | boolean |
| **evictionType** (producer) | 

Set the eviction Type for this cache.

Enum values:

-   SIZE\_BASED
    
-   TIME\_BASED
    





 | SIZE\_BASED | EvictionType |
| **expireAfterAccessTime** (producer) | Specifies that each entry should be automatically removed from the cache once a fixed duration has elapsed after the entry’s creation, the most recent replacement of its value, or its last read. Access time is reset by all cache read and write operations. The unit is in seconds. | 300 | int |
| **expireAfterWriteTime** (producer) | Specifies that each entry should be automatically removed from the cache once a fixed duration has elapsed after the entry’s creation, or the most recent replacement of its value. The unit is in seconds. | 300 | int |
| **initialCapacity** (producer) | Sets the minimum total size for the internal data structures. Providing a large enough estimate at construction time avoids the need for expensive resizing operations later, but setting this value unnecessarily high wastes memory. |  | Integer |
| **key** (producer) | To configure the default action key. If a key is set in the message header, then the key from the header takes precedence. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maximumSize** (producer) | Specifies the maximum number of entries the cache may contain. Note that the cache may evict an entry before this limit is exceeded or temporarily exceed the threshold while evicting. As the cache size grows close to the maximum, the cache evicts entries that are less likely to be used again. For example, the cache may evict an entry because it hasn’t been used recently or very often. When size is zero, elements will be evicted immediately after being loaded into the cache. This can be useful in testing or to disable caching temporarily without a code change. As eviction is scheduled on the configured executor, tests may instead prefer to configure the cache to execute tasks directly on the same thread. |  | Integer |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **cacheLoader** (advanced) | To configure a CacheLoader in case of a LoadCache use. |  | CacheLoader |
| **configuration** (advanced) | Sets the global component configuration. |  | CaffeineConfiguration |
| **removalListener** (advanced) | Set a specific removal Listener for the cache. |  | RemovalListener |
| **statsCounter** (advanced) | Set a specific Stats Counter for the cache stats. |  | StatsCounter |
| **statsEnabled** (advanced) | To enable stats on the cache. | false | boolean |
| **valueType** (advanced) | The cache value type, default java.lang.Object. |  | String |

## Endpoint Options

The Caffeine LoadCache endpoint is configured using URI syntax:

caffeine-loadcache:cacheName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheName** (producer) | **Required** the cache name. |  | String |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
To configure the default cache action. If an action is set in the message header, then the operation from the header takes precedence.

Enum values:

-   GET
    
-   GET\_ALL
    
-   PUT
    
-   PUT\_ALL
    
-   INVALIDATE
    
-   INVALIDATE\_ALL
    
-   CLEANUP
    
-   AS\_MAP
    





 |  | String |
| **createCacheIfNotExist** (producer) | Automatic create the Caffeine cache if none has been configured or exists in the registry. | true | boolean |
| **evictionType** (producer) | 

Set the eviction Type for this cache.

Enum values:

-   SIZE\_BASED
    
-   TIME\_BASED
    





 | SIZE\_BASED | EvictionType |
| **expireAfterAccessTime** (producer) | Specifies that each entry should be automatically removed from the cache once a fixed duration has elapsed after the entry’s creation, the most recent replacement of its value, or its last read. Access time is reset by all cache read and write operations. The unit is in seconds. | 300 | int |
| **expireAfterWriteTime** (producer) | Specifies that each entry should be automatically removed from the cache once a fixed duration has elapsed after the entry’s creation, or the most recent replacement of its value. The unit is in seconds. | 300 | int |
| **initialCapacity** (producer) | Sets the minimum total size for the internal data structures. Providing a large enough estimate at construction time avoids the need for expensive resizing operations later, but setting this value unnecessarily high wastes memory. |  | Integer |
| **key** (producer) | To configure the default action key. If a key is set in the message header, then the key from the header takes precedence. |  | String |
| **maximumSize** (producer) | Specifies the maximum number of entries the cache may contain. Note that the cache may evict an entry before this limit is exceeded or temporarily exceed the threshold while evicting. As the cache size grows close to the maximum, the cache evicts entries that are less likely to be used again. For example, the cache may evict an entry because it hasn’t been used recently or very often. When size is zero, elements will be evicted immediately after being loaded into the cache. This can be useful in testing or to disable caching temporarily without a code change. As eviction is scheduled on the configured executor, tests may instead prefer to configure the cache to execute tasks directly on the same thread. |  | Integer |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **cacheLoader** (advanced) | To configure a CacheLoader in case of a LoadCache use. |  | CacheLoader |
| **removalListener** (advanced) | Set a specific removal Listener for the cache. |  | RemovalListener |
| **statsCounter** (advanced) | Set a specific Stats Counter for the cache stats. |  | StatsCounter |
| **statsEnabled** (advanced) | To enable stats on the cache. | false | boolean |
| **valueType** (advanced) | The cache value type, default java.lang.Object. |  | String |

## Message Headers

The Caffeine LoadCache component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelCaffeineAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-caffeine/latest/org/apache/camel/component/caffeine/CaffeineConstants.html#ACTION) | The action to execute. Possible values: CLEANUP PUT PUT\_ALL GET GET\_ALL INVALIDATE INVALIDATE\_ALL AS\_MAP. |  | String |
| **CamelCaffeineActionHasResult** (producer) Constant: [`ACTION_HAS_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-caffeine/latest/org/apache/camel/component/caffeine/CaffeineConstants.html#ACTION_HAS_RESULT) | The flag indicating whether the action has a result or not. |  | Boolean |
| **CamelCaffeineActionSucceeded** (producer) Constant: [`ACTION_SUCCEEDED`](https://javadoc.io/doc/org.apache.camel/camel-caffeine/latest/org/apache/camel/component/caffeine/CaffeineConstants.html#ACTION_SUCCEEDED) | The flag indicating whether the action was successful or not. |  | Boolean |
| **CamelCaffeineKey** (producer) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-caffeine/latest/org/apache/camel/component/caffeine/CaffeineConstants.html#KEY) | The key for all actions on a single entry. |  |  |
| **CamelCaffeineKeys** (producer) Constant: [`KEYS`](https://javadoc.io/doc/org.apache.camel/camel-caffeine/latest/org/apache/camel/component/caffeine/CaffeineConstants.html#KEYS) | The keys to get (GET\_ALL), to invalidate (INVALIDATE\_ALL) or existing (AS\_MAP) according to the action. |  | Set |
| **CamelCaffeineValue** (producer) Constant: [`VALUE`](https://javadoc.io/doc/org.apache.camel/camel-caffeine/latest/org/apache/camel/component/caffeine/CaffeineConstants.html#VALUE) | The value of key for all put actions (PUT or PUT\_ALL). |  |  |
| **CamelCaffeineOldValue** (producer) Constant: [`OLD_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-caffeine/latest/org/apache/camel/component/caffeine/CaffeineConstants.html#OLD_VALUE) | The old value returned according to the action. |  |  |