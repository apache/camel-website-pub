# Ehcache

**Since Camel 2.18**

**Both producer and consumer are supported**

The Ehcache component enables you to perform caching operations using Ehcache 3 as the Cache Implementation.

The Cache consumer is an event based consumer and can be used to listen and respond to specific cache activities.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ehcache</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

ehcache://cacheName\[?options\]

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

The Ehcache component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheManager** (common) | The cache manager. |  | CacheManager |
| **cacheManagerConfiguration** (common) | The cache manager configuration. |  | Configuration |
| **configurationUri** (common) | URI pointing to the Ehcache XML configuration file’s location. |  | String |
| **createCacheIfNotExist** (common) | Configure if a cache need to be created if it does exist or can’t be pre-configured. | true | boolean |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **eventFiring** (consumer) | 
Set the delivery mode (synchronous, asynchronous).

Enum values:

-   ASYNCHRONOUS
    
-   SYNCHRONOUS
    





 | ASYNCHRONOUS | EventFiring |
| **eventOrdering** (consumer) | 

Set the delivery mode (ordered, unordered).

Enum values:

-   UNORDERED
    
-   ORDERED
    





 | ORDERED | EventOrdering |
| **eventTypes** (consumer) | 

Set the type of events to listen for (EVICTED,EXPIRED,REMOVED,CREATED,UPDATED). You can specify multiple entries separated by comma.

Enum values:

-   EVICTED
    
-   EXPIRED
    
-   REMOVED
    
-   CREATED
    
-   UPDATED
    





 |  | String |
| **action** (producer) | 

To configure the default cache action. If an action is set in the message header, then the operation from the header takes precedence.

Enum values:

-   CLEAR
    
-   PUT
    
-   PUT\_ALL
    
-   PUT\_IF\_ABSENT
    
-   GET
    
-   GET\_ALL
    
-   REMOVE
    
-   REMOVE\_ALL
    
-   REPLACE
    





 |  | String |
| **key** (producer) | To configure the default action key. If a key is set in the message header, then the key from the header takes precedence. |  | Object |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | The default cache configuration to be used to create caches. |  | CacheConfiguration |
| **configurations** (advanced) | A map of cache configuration to be used to create caches. |  | Map |
| **keyType** (advanced) | The cache key type, default java.lang.Object. |  | String |
| **valueType** (advanced) | The cache value type, default java.lang.Object. |  | String |

## Endpoint Options

The Ehcache endpoint is configured using URI syntax:

ehcache:cacheName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheName** (common) | **Required** the cache name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheManager** (common) | The cache manager. |  | CacheManager |
| **cacheManagerConfiguration** (common) | The cache manager configuration. |  | Configuration |
| **configurationUri** (common) | URI pointing to the Ehcache XML configuration file’s location. |  | String |
| **createCacheIfNotExist** (common) | Configure if a cache need to be created if it does exist or can’t be pre-configured. | true | boolean |
| **eventFiring** (consumer) | 
Set the delivery mode (synchronous, asynchronous).

Enum values:

-   ASYNCHRONOUS
    
-   SYNCHRONOUS
    





 | ASYNCHRONOUS | EventFiring |
| **eventOrdering** (consumer) | 

Set the delivery mode (ordered, unordered).

Enum values:

-   UNORDERED
    
-   ORDERED
    





 | ORDERED | EventOrdering |
| **eventTypes** (consumer) | 

Set the type of events to listen for (EVICTED,EXPIRED,REMOVED,CREATED,UPDATED). You can specify multiple entries separated by comma.

Enum values:

-   EVICTED
    
-   EXPIRED
    
-   REMOVED
    
-   CREATED
    
-   UPDATED
    





 |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **action** (producer) | 

To configure the default cache action. If an action is set in the message header, then the operation from the header takes precedence.

Enum values:

-   CLEAR
    
-   PUT
    
-   PUT\_ALL
    
-   PUT\_IF\_ABSENT
    
-   GET
    
-   GET\_ALL
    
-   REMOVE
    
-   REMOVE\_ALL
    
-   REPLACE
    





 |  | String |
| **key** (producer) | To configure the default action key. If a key is set in the message header, then the key from the header takes precedence. |  | Object |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **configuration** (advanced) | The default cache configuration to be used to create caches. |  | CacheConfiguration |
| **configurations** (advanced) | A map of cache configuration to be used to create caches. |  | Map |
| **keyType** (advanced) | The cache key type, default java.lang.Object. |  | String |
| **valueType** (advanced) | The cache value type, default java.lang.Object. |  | String |

## Message Headers

The Ehcache component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelEhcacheAction** (common) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-ehcache/latest/org/apache/camel/component/ehcache/EhcacheConstants.html#ACTION) | The operation to be performed on the cache, valid options are: CLEAR PUT PUT\_ALL PUT\_IF\_ABSENT GET GET\_ALL REMOVE REMOVE\_ALL REPLACE. |  | String |
| **CamelEhcacheActionHasResult** (common) Constant: [`ACTION_HAS_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-ehcache/latest/org/apache/camel/component/ehcache/EhcacheConstants.html#ACTION_HAS_RESULT) | Set to true if the action has a result. |  | Boolean |
| **CamelEhcacheActionSucceeded** (common) Constant: [`ACTION_SUCCEEDED`](https://javadoc.io/doc/org.apache.camel/camel-ehcache/latest/org/apache/camel/component/ehcache/EhcacheConstants.html#ACTION_SUCCEEDED) | Set to true if the action was successful. |  | Boolean |
| **CamelEhcacheKey** (common) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-ehcache/latest/org/apache/camel/component/ehcache/EhcacheConstants.html#KEY) | The cache key used for an action. |  | Object |
| **CamelEhcacheKeys** (common) Constant: [`KEYS`](https://javadoc.io/doc/org.apache.camel/camel-ehcache/latest/org/apache/camel/component/ehcache/EhcacheConstants.html#KEYS) | A list of keys, used in PUT\_ALL GET\_ALL REMOVE\_ALL. |  | Set |
| **CamelEhcacheValue** (common) Constant: [`VALUE`](https://javadoc.io/doc/org.apache.camel/camel-ehcache/latest/org/apache/camel/component/ehcache/EhcacheConstants.html#VALUE) | The value to put in the cache or the result of an operation. |  | Object |
| **CamelEhcacheOldValue** (common) Constant: [`OLD_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-ehcache/latest/org/apache/camel/component/ehcache/EhcacheConstants.html#OLD_VALUE) | The old value associated to a key for actions like PUT\_IF\_ABSENT or the Object used for comparison for actions like REPLACE. |  | Object |
| **CamelEhcacheEventType** (common) Constant: [`EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-ehcache/latest/org/apache/camel/component/ehcache/EhcacheConstants.html#EVENT_TYPE) | The type of event received. |  | EventType |

## Examples

### Ehcache based idempotent repository example:

_Java-only: programmatic CacheManager and idempotent repository configuration_

```java
CacheManager manager = CacheManagerBuilder.newCacheManager(new XmlConfiguration("ehcache.xml"));
EhcacheIdempotentRepository repo = new EhcacheIdempotentRepository(manager, "idempotent-cache");

from("direct:in")
    .idempotentConsumer(header("messageId"), idempotentRepo)
    .to("mock:out");
```

### Ehcache based aggregation repository example:

_Java-only: full test class with aggregation repository configuration_

```java
public class EhcacheAggregationRepositoryRoutesTest extends CamelTestSupport {
    private static final String ENDPOINT_MOCK = "mock:result";
    private static final String ENDPOINT_DIRECT = "direct:one";
    private static final int[] VALUES = generateRandomArrayOfInt(10, 0, 30);
    private static final int SUM = IntStream.of(VALUES).reduce(0, (a, b) -> a + b);
    private static final String CORRELATOR = "CORRELATOR";

    @EndpointInject(ENDPOINT_MOCK)
    private MockEndpoint mock;

    @Produce(uri = ENDPOINT_DIRECT)
    private ProducerTemplate producer;

    @Test
    public void checkAggregationFromOneRoute() throws Exception {
        mock.expectedMessageCount(VALUES.length);
        mock.expectedBodiesReceived(SUM);

        IntStream.of(VALUES).forEach(
            i -> producer.sendBodyAndHeader(i, CORRELATOR, CORRELATOR)
        );

        mock.assertIsSatisfied();
    }

    private Exchange aggregate(Exchange oldExchange, Exchange newExchange) {
        if (oldExchange == null) {
            return newExchange;
        } else {
            Integer n = newExchange.getIn().getBody(Integer.class);
            Integer o = oldExchange.getIn().getBody(Integer.class);
            Integer v = (o == null ? 0 : o) + (n == null ? 0 : n);

            oldExchange.getIn().setBody(v, Integer.class);

            return oldExchange;
        }
    }

    @Override
    protected RoutesBuilder createRouteBuilder() throws Exception {
        return new RouteBuilder() {
            @Override
            public void configure() throws Exception {
                from(ENDPOINT_DIRECT)
                    .routeId("AggregatingRouteOne")
                    .aggregate(header(CORRELATOR))
                    .aggregationRepository(createAggregateRepository())
                    .aggregationStrategy(EhcacheAggregationRepositoryRoutesTest.this::aggregate)
                    .completionSize(VALUES.length)
                        .to("log:org.apache.camel.component.ehcache.processor.aggregate.level=INFO&showAll=true&mulltiline=true")
                        .to(ENDPOINT_MOCK);
            }
        };
    }

    protected EhcacheAggregationRepository createAggregateRepository() throws Exception {
        CacheManager cacheManager = CacheManagerBuilder.newCacheManager(new XmlConfiguration("ehcache.xml"));
        cacheManager.init();

        EhcacheAggregationRepository repository = new EhcacheAggregationRepository();
        repository.setCacheManager(cacheManager);
        repository.setCacheName("aggregate");

        return repository;
    }
}
```