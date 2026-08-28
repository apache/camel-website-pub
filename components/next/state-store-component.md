# State Store

**Since Camel 4.23**

**Only producer is supported**

The State Store component provides a simple, unified key-value store API backed by the `KeyValueRepository` SPI from `camel-api`. It is useful for caching, session state, and scenarios where you need a simple object store (similar to MuleSoft’s Object Store).

By default, an in-memory backend is used (`MemoryKeyValueRepository` from `camel-support`), but you can plug in any `KeyValueRepository` implementation. The same `KeyValueRepository` can also be used as the backend for the Idempotent Consumer and Aggregator EIPs via the `KeyValueIdempotentRepository` and `KeyValueAggregationRepository` adapters.

## When to use State Store vs individual components

Camel also provides dedicated components for [Infinispan](infinispan-component.md), [Redis](spring-redis-component.md), and [Caffeine](caffeine-cache-component.md). Use the dedicated component when you need the full feature set of a specific technology (e.g., Infinispan queries, Redis pub/sub, Caffeine statistics).

Use State Store when:

-   You need a **simple key-value API** and want to switch backends without changing route logic.
    
-   You are **migrating from MuleSoft** and want an Object Store equivalent.
    
-   You want **backend portability** — develop with in-memory, deploy with any `KeyValueRepository`.
    
-   Your use case is limited to **put, get, delete, contains, keys** operations.
    
-   You want a **single backend** to serve state store, idempotent consumer, and aggregation patterns.
    

## URI Format

state-store:storeName\[?options\]

Where `storeName` is a logical name for the store. Endpoints with the same `storeName` share the same backend instance within the same `CamelContext`.

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

The State Store component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The State Store endpoint is configured using URI syntax:

state-store:storeName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **storeName** (producer) | **Required** The name of the state store. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
The default operation to perform.

Enum values:

-   put
    
-   putIfAbsent
    
-   get
    
-   delete
    
-   contains
    
-   keys
    
-   size
    
-   clear
    





 |  | StateStoreOperations |
| **ttl** (producer) | Time-to-live in milliseconds for entries. 0 means no expiry. | 0 | long |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **backend** (advanced) | The backend to use. If not set, auto-discovers a single KeyValueRepository from the registry, or falls back to an in-memory store. |  | KeyValueRepository |

## Message Headers

The State Store component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelStateStoreOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-state-store/latest/org/apache/camel/component/statestore/StateStoreConstants.html#OPERATION) | 
The operation to perform.

Enum values:

-   put
    
-   putIfAbsent
    
-   get
    
-   delete
    
-   contains
    
-   keys
    
-   size
    
-   clear
    





 |  | StateStoreOperations |
| **CamelStateStoreKey** (producer) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-state-store/latest/org/apache/camel/component/statestore/StateStoreConstants.html#KEY) | The key to use for the operation. |  | String |
| **CamelStateStoreTtl** (producer) Constant: [`TTL`](https://javadoc.io/doc/org.apache.camel/camel-state-store/latest/org/apache/camel/component/statestore/StateStoreConstants.html#TTL) | Per-message TTL override in milliseconds. Takes precedence over the endpoint ttl option. |  | Long |

## Operations

The operation to perform is set via the URI option `operation` or the header `CamelStateStoreOperation`.

   
| Operation | Description | Body (input) | Result (body output) |
| --- | --- | --- | --- |
| `put` | Store a value | The value to store | The previous value (or null) |
| `putIfAbsent` | Store only if key absent | The value to store | The existing value (or null if stored) |
| `get` | Retrieve a value | ignored | The stored value (or null) |
| `delete` | Remove a value | ignored | The removed value (or null) |
| `contains` | Check if key exists | ignored | Boolean |
| `keys` | List all keys | ignored | Set<String> |
| `size` | Count entries | ignored | Integer |
| `clear` | Remove all entries | ignored | null |

The key is specified via the header `CamelStateStoreKey` (required for `put`, `putIfAbsent`, `get`, `delete`, `contains`).

## TTL (Time-to-Live)

You can set a TTL (in milliseconds) for entries in two ways:

-   **Endpoint option**: applies to all `put`/`putIfAbsent` operations on that endpoint.
    
    state-store:myStore?operation=put&ttl=60000
    
-   **Per-message header**: the header `CamelStateStoreTtl` (Long) overrides the endpoint TTL for that message.
    
    ```java
    from("direct:store")
        .setHeader("CamelStateStoreKey", constant("myKey"))
        .setHeader("CamelStateStoreTtl", constant(30000L))
        .to("state-store:myStore?operation=put");
    ```
    

A TTL of `0` (default) means no expiry.

## Examples

### Java DSL

-   Put and Get
    
-   Dynamic operation via header
    
-   Put if absent
    

```java
from("direct:store")
    .setHeader("CamelStateStoreKey", constant("myKey"))
    .to("state-store:myStore?operation=put");

from("direct:retrieve")
    .setHeader("CamelStateStoreKey", constant("myKey"))
    .to("state-store:myStore?operation=get");
```

```java
from("direct:dynamic")
    .setHeader("CamelStateStoreOperation", constant("put"))
    .setHeader("CamelStateStoreKey", constant("myKey"))
    .to("state-store:myStore");
```

```java
from("direct:init")
    .setHeader("CamelStateStoreKey", constant("counter"))
    .to("state-store:myStore?operation=putIfAbsent");
```

### YAML DSL

```yaml
- route:
    from:
      uri: direct:store
    steps:
      - setHeader:
          name: CamelStateStoreKey
          constant: myKey
      - to:
          uri: state-store:myStore?operation=put
```

## Backends

### Backend auto-discovery

If no `backend` option is specified on the endpoint, the component automatically looks up a `KeyValueRepository` bean from the Camel registry. If exactly one is found, it is used for all endpoints. If none is found, the default in-memory backend (`MemoryKeyValueRepository`) is used.

This means you can configure a backend once (via Java or properties) and all `state-store` endpoints will use it without needing `backend=#beanName` on each endpoint URI.

### In-Memory (default)

The default backend (`MemoryKeyValueRepository`) stores entries in a `ConcurrentHashMap`. TTL expiry is lazy — entries are checked and removed on access rather than by a background thread.

No additional dependency is needed beyond `camel-state-store`.

## Custom Backend

Implement the `KeyValueRepository` interface (from `org.apache.camel.spi`) to create your own backend:

```java
public class MyCustomBackend extends ServiceSupport implements KeyValueRepository {

    @Override
    public Object get(String key) {
        // retrieve the value
    }

    @Override
    public Object put(String key, Object value, long ttlMillis) {
        // store the value; return the previous value or null
    }

    @Override
    public Object delete(String key) {
        // remove and return the value
    }

    @Override
    public boolean contains(String key) {
        // check existence
    }

    @Override
    public Set<String> keys() {
        // return all keys
    }

    @Override
    public void clear() {
        // remove all entries
    }
}
```

The `putIfAbsent` and `size` methods have default implementations but can be overridden for better performance with backends that support these operations natively.

Then reference it via bean or let auto-discovery find it:

```java
from("direct:store")
    .to("state-store:myStore?operation=put&backend=#myCustomBackend");
```

### Sharing a backend across patterns

Because `KeyValueRepository` is the unified SPI, the same implementation can be reused as the backend for the Idempotent Consumer and Aggregator EIPs:

```java
@BindToRegistry("kvRepo")
public KeyValueRepository kvRepo() {
    return new MemoryKeyValueRepository();
}
```

With a single `KeyValueRepository` in the registry:

-   The State Store component auto-discovers and uses it.
    
-   The Idempotent Consumer EIP auto-discovers and wraps it in a `KeyValueIdempotentRepository`.
    
-   The Aggregator EIP auto-discovers and wraps it in a `KeyValueAggregationRepository`.
    

No explicit wiring is needed — all three patterns share the same backend.