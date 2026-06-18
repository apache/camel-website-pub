# JCache

**Since Camel 2.17**

**Both producer and consumer are supported**

The JCache component enables you to perform caching operations using JSR107/JCache as cache implementation.

## URI Format

jcache:cacheName\[?options\]

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

The JCache component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheConfiguration** (common) | A Configuration for the Cache. |  | Configuration |
| **cacheConfigurationProperties** (common) | Properties to configure jcache. |  | Map |
| **cacheConfigurationPropertiesRef** (common) | References to an existing Properties or Map to lookup in the registry to use for configuring jcache. |  | String |
| **cachingProvider** (common) | The fully qualified class name of the javax.cache.spi.CachingProvider. |  | String |
| **configurationUri** (common) | An implementation specific URI for the CacheManager. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The JCache endpoint is configured using URI syntax:

jcache:cacheName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheName** (common) | **Required** The name of the cache. |  | String |

### Query Parameters (23 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheConfigurationProperties** (common) | The Properties for the javax.cache.spi.CachingProvider to create the CacheManager. |  | Properties |
| **cachingProvider** (common) | The fully qualified class name of the javax.cache.spi.CachingProvider. |  | String |
| **configurationUri** (common) | An implementation specific URI for the CacheManager. |  | String |
| **managementEnabled** (common) | Whether management gathering is enabled. | false | boolean |
| **readThrough** (common) | If read-through caching should be used. | false | boolean |
| **statisticsEnabled** (common) | Whether statistics gathering is enabled. | false | boolean |
| **storeByValue** (common) | If cache should use store-by-value or store-by-reference semantics. | true | boolean |
| **writeThrough** (common) | If write-through caching should be used. | false | boolean |
| **filteredEvents** (consumer) | 
Events a consumer should filter (multiple events can be separated by comma). If using filteredEvents option, then eventFilters one will be ignored.

Enum values:

-   CREATED
    
-   UPDATED
    
-   REMOVED
    
-   EXPIRED
    





 |  | String |
| **oldValueRequired** (consumer) | if the old value is required for events. | false | boolean |
| **synchronous** (consumer) | if the event listener should block the thread causing the event. | false | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **eventFilters** (consumer (advanced)) | The CacheEntryEventFilter. If using eventFilters option, then filteredEvents one will be ignored. |  | List |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **action** (producer) | To configure using a cache operation by default. If an operation in the message header, then the operation from the header takes precedence. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **cacheConfiguration** (advanced) | A Configuration for the Cache. |  | Configuration |
| **cacheLoaderFactory** (advanced) | The CacheLoader factory. |  | Factory |
| **cacheWriterFactory** (advanced) | The CacheWriter factory. |  | Factory |
| **createCacheIfNotExists** (advanced) | Configure if a cache need to be created if it does exist or can’t be pre-configured. | true | boolean |
| **expiryPolicyFactory** (advanced) | The ExpiryPolicy factory. |  | Factory |
| **lookupProviders** (advanced) | Configure if a camel-cache should try to find implementations of jcache api in runtimes like OSGi. | false | boolean |

## Message Headers

The JCache component supports 8 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelJCacheAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-jcache/latest/org/apache/camel/component/jcache/JCacheConstants.html#ACTION) | The cache operation to perform. |  | String |
| **CamelJCacheResult** (producer) Constant: [`RESULT`](https://javadoc.io/doc/org.apache.camel/camel-jcache/latest/org/apache/camel/component/jcache/JCacheConstants.html#RESULT) | The result of the cache operation. |  | boolean |
| **CamelJCacheEventType** (consumer) Constant: [`EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-jcache/latest/org/apache/camel/component/jcache/JCacheConstants.html#EVENT_TYPE) | The type of event received. |  | String |
| **CamelJCacheKey** (common) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-jcache/latest/org/apache/camel/component/jcache/JCacheConstants.html#KEY) | The key of the cache entry. |  | Object |
| **CamelJCacheKeys** (producer) Constant: [`KEYS`](https://javadoc.io/doc/org.apache.camel/camel-jcache/latest/org/apache/camel/component/jcache/JCacheConstants.html#KEYS) | The collection of keys against which the action should be performed. |  | Set |
| **CamelJCacheOldValue** (consumer) Constant: [`OLD_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-jcache/latest/org/apache/camel/component/jcache/JCacheConstants.html#OLD_VALUE) | The old value of the cache entry. |  | Object |
| **CamelJCacheEntryProcessor** (producer) Constant: [`ENTRY_PROCESSOR`](https://javadoc.io/doc/org.apache.camel/camel-jcache/latest/org/apache/camel/component/jcache/JCacheConstants.html#ENTRY_PROCESSOR) | The EntryProcessor to invoke. |  | EntryProcessor |
| **CamelJCacheEntryArgs** (producer) Constant: [`ARGUMENTS`](https://javadoc.io/doc/org.apache.camel/camel-jcache/latest/org/apache/camel/component/jcache/JCacheConstants.html#ARGUMENTS) | The additional arguments to pass to the EntryProcessor. |  | Collection |

## Usage

### JCache Policy

The JCachePolicy is an interceptor around a route that caches the "result of the route" (the message body) after the route is completed. If the next time the route is called with a "similar" Exchange, the cached value is used on the Exchange instead of executing the route. The policy uses the JSR107/JCache API of a cache implementation, so it’s required to add one (e.g., Hazelcast, Ehcache) to the classpath.

The policy takes a _key_ value from the received Exchange to get or store values in the cache. By default, the _key_ is the message body. For example, if the route - having a JCachePolicy - receives an Exchange with a String body _"fruit"_ and the body at the end of the route is "apple", it stores a _key/value_ pair _"fruit=apple"_ in the cache. If next time another Exchange arrives with a body _"fruit"_, the value _"apple"_ is taken from the cache instead of letting the route process the Exchange.

So by default, the message body at the beginning of the route is the cache _key_ and the body at the end is the stored _value_. It’s possible to use something else as a _key_ by setting a Camel Expression via `.setKeyExpression()` that will be used to determine the key.

The policy needs a JCache Cache. It can be set directly by `.setCache()` or the policy will try to get or create the Cache based on the other parameters set.

Similar caching solution is available, for example, in Spring using the @Cacheable annotation.

### JCachePolicy Fields

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cache** | The Cache to use to store the cached values. If this value is set, `cacheManager`, `cacheName` and `cacheConfiguration` is ignored. |  | Cache |
| **cacheManager** | The CacheManager to use to look up or create the Cache. Used only if `cache` is not set. | Try to find a `CacheManager` in the `CamelContext` registry or calls the standard JCache `Caching.getCachingProvider().getCacheManager()`. | CacheManager |
| **cacheName** | Name of the cache. Get the Cache from `cacheManager` or create a new one if it doesn’t exist. | RouteId of the route. | String |
| **cacheConfiguration** | JCache cache configuration to use if a new Cache is created | Default new `MutableConfiguration` object. | CacheConfiguration |
| **keyExpression** | An Expression to evaluate to determine the cache key. | Exchange body | Expression |
| **enabled** | If the policy is not enabled, no wrapper processor is added to the route. It has impact only during startup, not during runtime. For example, it can be used to disable caching from properties. | true | boolean |

### How to determine cache to use?

### Set cache

The cache used by the policy can be set directly. This means you have to configure the cache yourself and get a JCache Cache object, but this gives the most flexibility. For example, it can be setup in the config xml of the cache provider (Hazelcast, EhCache, …​) and used here. Or it’s possible to use the standard Caching API as below:

_Java-only: Java programmatic cache configuration with JCachePolicy_

```java
MutableConfiguration configuration = new MutableConfiguration<>();
configuration.setTypes(String.class, Object.class);
configuration.setExpiryPolicyFactory(CreatedExpiryPolicy.factoryOf(new Duration(TimeUnit.MINUTES, 60)));
CacheManager cacheManager = Caching.getCachingProvider().getCacheManager();
Cache cache = cacheManager.createCache("orders",configuration);

JCachePolicy jcachePolicy = new JCachePolicy();
jcachePolicy.setCache(cache);

from("direct:get-orders")
    .policy(jcachePolicy)
    .log("Getting order with id: ${body}")
    .bean(OrderService.class,"findOrderById(${body})");
```

### Set cacheManager

If the `cache` is not set, the policy will try to look up or create the cache automatically. If the `cacheManager` is set on the policy, it will try to get cache with the set `cacheName` (routeId by default) from the CacheManager. If the cache does not exist, it will create a new one using the `cacheConfiguration` (new MutableConfiguration by default).

_Java-only: Java programmatic CacheManager configuration_

```java
//In a Spring environment, for example, the CacheManager may already exist as a bean
@Autowire
CacheManager cacheManager;
...

//Cache "items" is used or created if not exists
JCachePolicy jcachePolicy = new JCachePolicy();
jcachePolicy.setCacheManager(cacheManager);
jcachePolicy.setCacheName("items")
```

### Find cacheManager

If `cacheManager` (and the `cache`) is not set, the policy will try to find a JCache CacheManager object:

-   Lookup a CacheManager in Camel registry. That falls back on JNDI or Spring context based on the environment
    
-   Use the standard api `Caching.getCachingProvider().getCacheManager()`
    

_Java-only: Java DSL with JCachePolicy_

```java
//A Cache "getorders" will be used (or created) from the found CacheManager
from("direct:get-orders").routeId("getorders")
    .policy(new JCachePolicy())
    .log("Getting order with id: ${body}")
    .bean(OrderService.class,"findOrderById(${body})");
```

### Partially wrapped route

In the examples above, the whole route was executed or skipped. A policy can be used to wrap only a segment of the route instead of all processors.

_Java-only: Java DSL with partial JCachePolicy wrapping_

```java
from("direct:get-orders")
    .log("Order requested: ${body}")
    .policy(new JCachePolicy())
        .log("Getting order with id: ${body}")
        .bean(OrderService.class,"findOrderById(${body})")
    .end()
    .log("Order found: ${body}");
```

The `.log()` at the beginning and at the end of the route is always called, but the section inside `.policy()` and `.end()` is executed based on the cache.

### KeyExpression

By default, the policy uses the received Exchange body as the _key_, so the default expression is like `simple("${body}")`. We can set a different Camel Expression as `keyExpression` which will be evaluated to determine the key. For example, if we try to find an `order` by an `orderId` which is in the message headers, set `header("orderId")` (or `simple("$\{header.orderId\}")` as `keyExpression`.

The expression is evaluated only once at the beginning of the route to determine the _key_. If nothing was found in cache, this _key_ is used to store the _value_ in cache at the end of the route.

_Java-only: Java programmatic JCachePolicy with keyExpression_

```java
MutableConfiguration configuration = new MutableConfiguration<>();
configuration.setTypes(String.class, Order.class);
configuration.setExpiryPolicyFactory(CreatedExpiryPolicy.factoryOf(new Duration(TimeUnit.MINUTES, 10)));

JCachePolicy jcachePolicy = new JCachePolicy();
jcachePolicy.setCacheConfiguration(configuration);
jcachePolicy.setCacheName("orders")
jcachePolicy.setKeyExpression(simple("${header.orderId}))

//The cache key is taken from "orderId" header.
from("direct:get-orders")
    .policy(jcachePolicy)
    .log("Getting order with id: ${header.orderId}")
    .bean(OrderService.class,"findOrderById(${header.orderId})");
```

### BypassExpression

The `JCachePolicy` can be configured with an `Expression` that can per `Exchange` determine whether to look up the value from the cache or bypass. If the expression is evaluated to `false` then the route is executed as normal, and the returned value is inserted into the cache for future lookup.

### Camel XML DSL examples

### Use JCachePolicy in an XML route

In Camel XML DSL, we need a named reference to the JCachePolicy instance (registered in CamelContext or simply in Spring). We have to wrap the route between `<policy>…​</policy>` tags after `<from>`.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:get-order")
    .policy("jCachePolicy")
        .setBody().method("orderService", "findOrderById(${body})")
    .end();
```

```xml
<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route>
        <from uri="direct:get-order"/>
        <policy ref="jCachePolicy" >
            <setBody>
                <method ref="orderService" method="findOrderById(${body})"/>
            </setBody>
        </policy>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:get-order
      steps:
        - policy:
            ref: jCachePolicy
            steps:
              - setBody:
                  method:
                    ref: orderService
                    method: "findOrderById(${body})"
```

See this example when only a part of the route is wrapped:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:get-order")
    .log("Start - This is always called. body:${body}")
    .policy("jCachePolicy")
        .log("Executing route, not found in cache. body:${body}")
        .setBody().method("orderService", "findOrderById(${body})")
    .end()
    .log("End - This is always called. body:${body}");
```

```xml
<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route>
        <from uri="direct:get-order"/>
        <log message="Start - This is always called. body:${body}"/>
        <policy ref="jCachePolicy" >
            <log message="Executing route, not found in cache. body:${body}"/>
            <setBody>
                <method ref="orderService" method="findOrderById(${body})"/>
            </setBody>
        </policy>
        <log message="End - This is always called. body:${body}"/>
    </route>
</camelContext>
```

```yaml
- route:
    from:
      uri: direct:get-order
      steps:
        - log:
            message: "Start - This is always called. body:${body}"
        - policy:
            ref: jCachePolicy
            steps:
              - log:
                  message: "Executing route, not found in cache. body:${body}"
              - setBody:
                  method:
                    ref: orderService
                    method: "findOrderById(${body})"
        - log:
            message: "End - This is always called. body:${body}"
```

### Define CachePolicy in Spring

It’s more convenient to create a JCachePolicy in Java, especially within a RouteBuilder using the Camel DSL expressions, but see this example to define it in a Spring XML:

```xml
<bean id="jCachePolicy" class="org.apache.camel.component.jcache.policy.JCachePolicy">
    <property name="cacheName" value="spring"/>
    <property name="keyExpression">
        <bean class="org.apache.camel.model.language.SimpleExpression">
            <property name="expression" value="${header.mykey}"/>
        </bean>
    </property>
</bean>
```

### Create Cache from XML

It’s not strictly speaking related to Camel XML DSL, but JCache providers usually have a way to configure the cache in an XML file. For example with Hazelcast, you can add a `hazelcast.xml` to classpath to configure the cache "spring" used in the example above.

```xml
<hazelcast xmlns="http://www.hazelcast.com/schema/config"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.hazelcast.com/schema/config http://www.hazelcast.com/schema/config/hazelcast-config-4.0.xsd">

    <cache name="spring">
        <key-type class-name="java.lang.String"/>
        <value-type class-name="java.lang.String"/>
        <expiry-policy-factory>
            <timed-expiry-policy-factory expiry-policy-type="CREATED" duration-amount="60" time-unit="MINUTES"/>
        </expiry-policy-factory>
    </cache>

</hazelcast>
```

### Special scenarios and error handling

If the Cache used by the policy is closed (can be done dynamically), the whole caching functionality is skipped, the route will be executed every time.

If the determined _key_ is _null_, nothing is looked up or stored in cache.

In case of an exception during the route, the error handled is called as always. If the exception gets `handled()`, the policy stores the Exchange body. Otherwise, nothing is added to the cache. If an exception happens during evaluating the keyExpression, the routing fails, the error handler is called as normally.

## Spring Boot Auto-Configuration

When using jcache with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jcache-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jcache.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.jcache.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.jcache.cache-configuration** | A Configuration for the Cache. The option is a javax.cache.configuration.Configuration type. |  | Configuration |
| **camel.component.jcache.cache-configuration-properties** | Properties to configure jcache. |  | Map |
| **camel.component.jcache.cache-configuration-properties-ref** | References to an existing Properties or Map to lookup in the registry to use for configuring jcache. |  | String |
| **camel.component.jcache.caching-provider** | The fully qualified class name of the javax.cache.spi.CachingProvider. |  | String |
| **camel.component.jcache.configuration-uri** | An implementation specific URI for the CacheManager. |  | String |
| **camel.component.jcache.enabled** | Whether to enable auto configuration of the jcache component. This is enabled by default. |  | Boolean |
| **camel.component.jcache.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |