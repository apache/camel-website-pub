# Hazelcast Replicated Map

**Since Camel 2.16**

**Both producer and consumer are supported**

The [Hazelcast](http://www.hazelcast.com/) instance component is one of Camel Hazelcast Components which allows you to consume join/leave events of the cache instance in the cluster. A replicated map is a weakly consistent, distributed key-value data structure with no data partition.

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

The Hazelcast Replicated Map component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **hazelcastInstance** (advanced) | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. |  | HazelcastInstance |
| **hazelcastMode** (advanced) | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |

## Endpoint Options

The Hazelcast Replicated Map endpoint is configured using URI syntax:

hazelcast-replicatedmap:cacheName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheName** (common) | **Required** The name of the cache. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **defaultOperation** (common) | 
To specify a default operation to use, if no operation header has been provided.

Enum values:

-   put
    
-   delete
    
-   get
    
-   update
    
-   query
    
-   getAll
    
-   clear
    
-   putIfAbsent
    
-   addAll
    
-   removeAll
    
-   retainAll
    
-   evict
    
-   evictAll
    
-   valueCount
    
-   containsKey
    
-   containsValue
    
-   getKeys
    
-   removeValue
    
-   increment
    
-   decrement
    
-   setValue
    
-   destroy
    
-   compareAndSet
    
-   getAndAdd
    
-   add
    
-   offer
    
-   peek
    
-   poll
    
-   remainingCapacity
    
-   drainTo
    
-   removeIf
    
-   take
    
-   publish
    
-   readOnceHead
    
-   readOnceTail
    
-   capacity
    





 |  | HazelcastOperation |
| **hazelcastConfigUri** (common) | Hazelcast configuration file. |  | String |
| **hazelcastInstance** (common) | The hazelcast instance reference which can be used for hazelcast endpoint. |  | HazelcastInstance |
| **hazelcastInstanceName** (common) | The hazelcast instance reference name which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. |  | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Hazelcast Replicated Map component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHazelcastObjectId** (common) Constant: [`OBJECT_ID`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#OBJECT_ID) | the object id to store / find your object inside the cache. |  | String |
| **CamelHazelcastListenerAction** (consumer) Constant: [`LISTENER_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#LISTENER_ACTION) | The type of event - here added and removed. |  | String |
| **CamelHazelcastListenerType** (consumer) Constant: [`LISTENER_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#LISTENER_TYPE) | The map consumer. |  | String |
| **CamelHazelcastListenerTime** (consumer) Constant: [`LISTENER_TIME`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#LISTENER_TIME) | The time of the event in millis. |  | Long |
| **CamelHazelcastCacheName** (consumer) Constant: [`CACHE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#CACHE_NAME) | The name of the cache - e.g. foo. |  | String |
| **CamelHazelcastOperationType** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#OPERATION) | The operation to perform. |  | String |

## replicatedmap cache producer

The replicatedmap producer provides 6 operations:

-   put
    
-   get
    
-   delete
    
-   clear
    
-   containsKey
    
-   containsValue
    

### Example for **put**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:put")
    .setHeader("CamelHazelcastOperationType", constant("put"))
    .to("hazelcast-replicatedmap:bar");
```

```xml
<route>
    <from uri="direct:put"/>
    <log message="put.."/>
    <setHeader name="hazelcast.operation.type">
        <constant>put</constant>
    </setHeader>
    <to uri="hazelcast-replicatedmap:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:put
      steps:
        - setHeader:
            name: hazelcast.operation.type
            constant: put
        - to:
            uri: hazelcast-replicatedmap:foo
```

### Example for **get**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:get")
    .setHeader("CamelHazelcastOperationType", constant("get"))
    .to("hazelcast-replicatedmap:bar")
    .to("seda:out");
```

```xml
<route>
    <from uri="direct:get"/>
    <log message="get.."/>
    <setHeader name="hazelcast.operation.type">
        <constant>get</constant>
    </setHeader>
    <to uri="hazelcast-replicatedmap:foo"/>
    <to uri="seda:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:get
      steps:
        - setHeader:
            name: hazelcast.operation.type
            constant: get
        - to:
            uri: hazelcast-replicatedmap:foo
        - to:
            uri: seda:out
```

### Example for **delete**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:delete")
    .setHeader("CamelHazelcastOperationType", constant("delete"))
    .to("hazelcast-replicatedmap:bar");
```

```xml
<route>
    <from uri="direct:delete"/>
    <log message="delete.."/>
    <setHeader name="hazelcast.operation.type">
        <constant>delete</constant>
    </setHeader>
    <to uri="hazelcast-replicatedmap:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:delete
      steps:
        - setHeader:
            name: hazelcast.operation.type
            constant: delete
        - to:
            uri: hazelcast-replicatedmap:foo
```

You can call them in your test class with:

_Java-only: uses ProducerTemplate API and Java constants_

```java
template.sendBodyAndHeader("direct:[put|get|delete|clear]", "my-foo", "CamelHazelcastObjectId", "4711");
```

## replicatedmap cache consumer

For the multimap cache, this component provides the same listeners / variables as for the map cache consumer (except the update and enviction listener). The only difference is the **multimap** prefix inside the URI. Here is a sample:

_Java-only: uses Java constants, string formatting, and choice/when/otherwise_

```java
from("hazelcast-multimap:bar")
.log("object...")
.choice()
    .when(header("CamelHazelcastListenerAction").isEqualTo("added"))
        .log("...added")
                .to("mock:added")
        //.when(header("CamelHazelcastListenerAction").isEqualTo("envicted"))
        //        .log("...envicted")
        //        .to("mock:envicted")
        .when(header("CamelHazelcastListenerAction").isEqualTo("removed"))
                .log("...removed")
                .to("mock:removed")
        .otherwise()
                .log("fail!");
```

Header Variables inside the response message:

  
| Name | Type | Description |
| --- | --- | --- |
| `CamelHazelcastListenerTime` | `Long` | time of the event in millis |
| `CamelHazelcastListenerType` | `String` | the map consumer sets here "cachelistener" |
| `CamelHazelcastListenerAction` | `String` | type of event - here **added** and **removed** (and soon **envicted**) |
| `CamelHazelcastObjectId` | `String` | the oid of the object |
| `CamelHazelcastCacheName` | `String` | the name of the cache (e.g., "foo") |
| `CamelHazelcastCacheType` | `String` | the type of the cache (e.g., replicatedmap) |