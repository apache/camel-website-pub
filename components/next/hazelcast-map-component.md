# Hazelcast Map

**Since Camel 2.7**

**Both producer and consumer are supported**

The [Hazelcast](http://www.hazelcast.com/) Map component is one of Camel Hazelcast Components which allows you to access a Hazelcast distributed map.

## Options

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

The Hazelcast Map component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **hazelcastInstance** (advanced) | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. |  | HazelcastInstance |
| **hazelcastMode** (advanced) | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |

## Endpoint Options

The Hazelcast Map endpoint is configured using URI syntax:

hazelcast-map:cacheName

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

The Hazelcast Map component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHazelcastObjectId** (common) Constant: [`OBJECT_ID`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#OBJECT_ID) | the object id to store / find your object inside the cache. |  | String |
| **CamelHazelcastObjectValue** (producer) Constant: [`OBJECT_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#OBJECT_VALUE) | The old value. |  | Object |
| **CamelHazelcastObjectTtlValue** (producer) Constant: [`TTL_VALUE`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#TTL_VALUE) | The value of the TTL. |  | Integer |
| **CamelHazelcastObjectTtlUnit** (producer) Constant: [`TTL_UNIT`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#TTL_UNIT) | 
The value of time unit ( DAYS / HOURS / MINUTES / …​.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 |  | TimeUnit |
| **CamelHazelcastQuery** (producer) Constant: [`QUERY`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#QUERY) | The query to execute against the map with a sql like syntax (see [http://www.hazelcast.com/](http://www.hazelcast.com/)). |  | String |
| **CamelHazelcastListenerAction** (consumer) Constant: [`LISTENER_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#LISTENER_ACTION) | The type of event - here added and removed. |  | String |
| **CamelHazelcastListenerType** (consumer) Constant: [`LISTENER_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#LISTENER_TYPE) | The map consumer. |  | String |
| **CamelHazelcastListenerTime** (consumer) Constant: [`LISTENER_TIME`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#LISTENER_TIME) | The time of the event in millis. |  | Long |
| **CamelHazelcastCacheName** (consumer) Constant: [`CACHE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#CACHE_NAME) | The name of the cache - e.g. foo. |  | String |
| **CamelHazelcastOperationType** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#OPERATION) | The operation to perform. |  | String |

## Map cache producer - to("hazelcast-map:foo")

If you want to store a value in a map, you can use the map cache producer.

The map cache producer provides follow operations specified by **CamelHazelcastOperationType** header:

-   put
    
-   putIfAbsent
    
-   get
    
-   getAll
    
-   keySet
    
-   containsKey
    
-   containsValue
    
-   delete
    
-   update
    
-   query
    
-   clear
    
-   evict
    
-   evictAll
    

You can call the samples with:

_Java-only: calling producer operations using ProducerTemplate_

```java
template.sendBodyAndHeader("direct:[put|get|update|delete|query|evict]", "my-foo", "CamelHazelcastObjectId", "4711");
```

### Example for **put**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:put")
.setHeader("CamelHazelcastOperationType", constant("put"))
.to("hazelcast-map:foo");
```

```xml
<route>
    <from uri="direct:put"/>
    <setHeader name="CamelHazelcastOperationType">
        <constant>put</constant>
    </setHeader>
    <to uri="hazelcast-map:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:put
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: put
        - to:
            uri: hazelcast-map:foo
```

Sample for **put** with eviction:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:put")
.setHeader("CamelHazelcastOperationType", constant("put"))
.setHeader("CamelHazelcastObjectTtlValue", constant(Long.valueOf(1)))
.setHeader("CamelHazelcastObjectTtlUnit", constant(TimeUnit.MINUTES))
.to("hazelcast-map:foo");
```

```xml
<route>
    <from uri="direct:put"/>
    <setHeader name="CamelHazelcastOperationType">
        <constant>put</constant>
    </setHeader>
    <setHeader name="CamelHazelcastObjectTtlValue">
        <constant>1</constant>
    </setHeader>
    <setHeader name="CamelHazelcastObjectTtlUnit">
        <constant>MINUTES</constant>
    </setHeader>
    <to uri="hazelcast-map:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:put
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: put
        - setHeader:
            name: CamelHazelcastObjectTtlValue
            constant: 1
        - setHeader:
            name: CamelHazelcastObjectTtlUnit
            constant: MINUTES
        - to:
            uri: hazelcast-map:foo
```

### Example for **get**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:get")
.setHeader("CamelHazelcastOperationType", constant("get"))
.to("hazelcast-map:foo")
.to("seda:out");
```

```xml
<route>
    <from uri="direct:get"/>
    <setHeader name="CamelHazelcastOperationType">
        <constant>get</constant>
    </setHeader>
    <to uri="hazelcast-map:foo"/>
    <to uri="seda:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:get
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: get
        - to:
            uri: hazelcast-map:foo
        - to:
            uri: seda:out
```

### Example for **update**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:update")
.setHeader("CamelHazelcastOperationType", constant("update"))
.to("hazelcast-map:foo");
```

```xml
<route>
    <from uri="direct:update"/>
    <setHeader name="CamelHazelcastOperationType">
        <constant>update</constant>
    </setHeader>
    <to uri="hazelcast-map:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:update
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: update
        - to:
            uri: hazelcast-map:foo
```

### Example for **delete**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:delete")
.setHeader("CamelHazelcastOperationType", constant("delete"))
.to("hazelcast-map:foo");
```

```xml
<route>
    <from uri="direct:delete"/>
    <setHeader name="CamelHazelcastOperationType">
        <constant>delete</constant>
    </setHeader>
    <to uri="hazelcast-map:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:delete
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: delete
        - to:
            uri: hazelcast-map:foo
```

### Example for **query**

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:query")
.setHeader("CamelHazelcastOperationType", constant("query"))
.to("hazelcast-map:foo")
.to("seda:out");
```

```xml
<route>
    <from uri="direct:query"/>
    <setHeader name="CamelHazelcastOperationType">
        <constant>query</constant>
    </setHeader>
    <to uri="hazelcast-map:foo"/>
    <to uri="seda:out"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:query
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: query
        - to:
            uri: hazelcast-map:foo
        - to:
            uri: seda:out
```

For the query operation Hazelcast offers an SQL like syntax to query your distributed map.

_Java-only: sending a query predicate using ProducerTemplate_

```java
String q1 = "bar > 1000";
template.sendBodyAndHeader("direct:query", null, "CamelHazelcastQuery", q1);
```

## Map cache consumer - from("hazelcast-map:foo")

Hazelcast provides event listeners on their data grid. If you want to be notified if a cache is manipulated, you can use the map consumer. There are four events: **put**, **update**, **delete** and **envict**. The event type will be stored in the "**hazelcast.listener.action**" header variable. The map consumer provides some additional information inside these variables:

Header Variables inside the response message:

  
| Name | Type | Description |
| --- | --- | --- |
| `CamelHazelcastListenerTime` | `Long` | time of the event in millis |
| `CamelHazelcastListenerType` | `String` | the map consumer sets here "cachelistener" |
| `CamelHazelcastListenerAction` | `String` | type of event (**added**, **updated**, **envicted** and **removed**). |
| `CamelHazelcastObjectId` | `String` | the oid of the object |
| `CamelHazelcastCacheName` | `String` | the name of the cache (e.g., "foo") |
| `CamelHazelcastCacheType` | `String` | the type of the cache (e.g., map) |

The object value will be stored within **put** and **update** actions inside the message body.

Here’s a sample:

-   Java
    
-   XML
    
-   YAML
    

```java
from("hazelcast-map:foo")
    .log("object...")
    .choice()
        .when(header("CamelHazelcastListenerAction").isEqualTo("added"))
            .log("...added")
            .to("mock:added")
        .when(header("CamelHazelcastListenerAction").isEqualTo("envicted"))
            .log("...envicted")
            .to("mock:envicted")
        .when(header("CamelHazelcastListenerAction").isEqualTo("updated"))
            .log("...updated")
            .to("mock:updated")
        .when(header("CamelHazelcastListenerAction").isEqualTo("removed"))
            .log("...removed")
            .to("mock:removed")
        .otherwise()
            .log("fail!");
```

```xml
<route>
  <from uri="hazelcast-map:foo"/>
  <log message="object..."/>
  <choice>
    <when>
      <simple>${header.CamelHazelcastListenerAction} == 'added'</simple>
      <log message="...added"/>
      <to uri="mock:added"/>
    </when>
    <when>
      <simple>${header.CamelHazelcastListenerAction} == 'envicted'</simple>
      <log message="...envicted"/>
      <to uri="mock:envicted"/>
    </when>
    <when>
      <simple>${header.CamelHazelcastListenerAction} == 'updated'</simple>
      <log message="...updated"/>
      <to uri="mock:updated"/>
    </when>
    <when>
      <simple>${header.CamelHazelcastListenerAction} == 'removed'</simple>
      <log message="...removed"/>
      <to uri="mock:removed"/>
    </when>
    <otherwise>
      <log message="fail!"/>
    </otherwise>
  </choice>
</route>
```

```yaml
- route:
    from:
      uri: hazelcast-map:foo
      steps:
        - log:
            message: "object..."
        - choice:
            when:
              - simple: "${header.CamelHazelcastListenerAction} == 'added'"
                steps:
                  - log:
                      message: "...added"
                  - to:
                      uri: mock:added
              - simple: "${header.CamelHazelcastListenerAction} == 'envicted'"
                steps:
                  - log:
                      message: "...envicted"
                  - to:
                      uri: mock:envicted
              - simple: "${header.CamelHazelcastListenerAction} == 'updated'"
                steps:
                  - log:
                      message: "...updated"
                  - to:
                      uri: mock:updated
              - simple: "${header.CamelHazelcastListenerAction} == 'removed'"
                steps:
                  - log:
                      message: "...removed"
                  - to:
                      uri: mock:removed
            otherwise:
              steps:
                - log:
                    message: "fail!"
```