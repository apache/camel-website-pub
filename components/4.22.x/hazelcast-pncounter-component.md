# Hazelcast PN Counter

**Since Camel 4.19**

**Only producer is supported**

The [Hazelcast](http://www.hazelcast.com/) PN Counter component is one of Camel Hazelcast Components which allows you to access a Hazelcast PN Counter (CRDT counter). A PN Counter is a Conflict-free Replicated Data Type (CRDT) that provides a distributed counter with eventual consistency guarantees.

This component is not a direct replacement for the hazelcast-atomicvalue component that is availble in Camel 2.7 → 4.19, but it does replicates most of the functionality (get / increment / decrement / getAndAdd / destroy) apart from the compare method.

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

The Hazelcast PN Counter component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **hazelcastInstance** (advanced) | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. |  | HazelcastInstance |
| **hazelcastMode** (advanced) | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |

## Endpoint Options

The Hazelcast PN Counter endpoint is configured using URI syntax:

hazelcast-pncounter:cacheName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheName** (producer) | **Required** The name of the cache. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **defaultOperation** (producer) | 
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
| **hazelcastConfigUri** (producer) | Hazelcast configuration file. |  | String |
| **hazelcastInstance** (producer) | The hazelcast instance reference which can be used for hazelcast endpoint. |  | HazelcastInstance |
| **hazelcastInstanceName** (producer) | The hazelcast instance reference name which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## PN Counter producer - to("hazelcast-pncounter:foo")

The operations for this producer are:

-   get
    
-   increment (+1)
    
-   decrement (-1)
    
-   getAndAdd
    
-   destroy
    

> **Note**
> PNCounter is a CRDT (Conflict-free Replicated Data Type) that provides eventual consistency. Operations are local and fast but do not support strong consistency operations like `compareAndSet` or `set`.

### Example for **increment**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:increment")
    .setHeader("CamelHazelcastOperationType", constant("increment"))
    .to("hazelcast-pncounter:foo");
```

```xml
<route>
    <from uri="direct:increment"/>
    <setHeader name="hazelcast.operation.type">
        <constant>increment</constant>
    </setHeader>
    <to uri="hazelcast-pncounter:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:increment
      steps:
        - setHeader:
            name: hazelcast.operation.type
            constant: increment
        - to:
            uri: hazelcast-pncounter:foo
```

The actual value (after increment) will be provided inside the message body.

### Example for **decrement**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:decrement")
    .setHeader("CamelHazelcastOperationType", constant("decrement"))
    .to("hazelcast-pncounter:foo");
```

```xml
<route>
    <from uri="direct:decrement"/>
    <setHeader name="hazelcast.operation.type">
        <constant>decrement</constant>
    </setHeader>
    <to uri="hazelcast-pncounter:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:decrement
      steps:
        - setHeader:
            name: hazelcast.operation.type
            constant: decrement
        - to:
            uri: hazelcast-pncounter:foo
```

The actual value (after decrement) will be provided inside the message body.

### Example for **get**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:get")
    .setHeader("CamelHazelcastOperationType", constant("get"))
    .to("hazelcast-pncounter:foo");
```

```xml
<route>
    <from uri="direct:get"/>
    <setHeader name="hazelcast.operation.type">
        <constant>get</constant>
    </setHeader>
    <to uri="hazelcast-pncounter:foo"/>
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
            uri: hazelcast-pncounter:foo
```

You can get the counter value with `long body = template.requestBody("direct:get", null, Long.class);`.

### Example for **getAndAdd**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:getAndAdd")
    .setHeader("CamelHazelcastOperationType", constant("getAndAdd"))
    .to("hazelcast-pncounter:foo");
```

```xml
<route>
    <from uri="direct:getAndAdd"/>
    <setHeader name="hazelcast.operation.type">
        <constant>getAndAdd</constant>
    </setHeader>
    <to uri="hazelcast-pncounter:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:getAndAdd
      steps:
        - setHeader:
            name: hazelcast.operation.type
            constant: getAndAdd
        - to:
            uri: hazelcast-pncounter:foo
```

Provide the delta value in the message body (e.g., 5 to add 5 to the counter): `long previousValue = template.requestBody("direct:getAndAdd", 5L, Long.class);`

The previous value (before the add) will be returned in the message body.

### Example for **destroy**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:destroy")
    .setHeader("CamelHazelcastOperationType", constant("destroy"))
    .to("hazelcast-pncounter:foo");
```

```xml
<route>
    <from uri="direct:destroy"/>
    <setHeader name="hazelcast.operation.type">
        <constant>destroy</constant>
    </setHeader>
    <to uri="hazelcast-pncounter:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:destroy
      steps:
        - setHeader:
            name: hazelcast.operation.type
            constant: destroy
        - to:
            uri: hazelcast-pncounter:foo
```

Destroys the PN Counter instance: `template.sendBody("direct:destroy", null);`