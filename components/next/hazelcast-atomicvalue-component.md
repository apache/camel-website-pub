# Hazelcast Atomic Number

> **Warning**
> **Deprecated:** This hazelcast-atomicvalue is deprecated and may be removed in a future release.

**Since Camel 2.7**

**Only producer is supported**

> **Warning**
> **Deprecated**: This component is deprecated as of Camel 4.19.0 and will be removed in a future release.
>
> Since Hazelcast 5.5, IAtomicLong requires the CP Subsystem which is only available in Hazelcast Enterprise Edition. This component will throw `UnsupportedOperationException` at runtime when used with Hazelcast Community Edition 5.5+.

The [Hazelcast](http://www.hazelcast.com/) atomic number component is one of Camel Hazelcast Components which allows you to access Hazelcast atomic number. An atomic number is an object that simply provides a grid wide number (long).

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

The Hazelcast Atomic Number component supports 4 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **hazelcastInstance** (advanced) | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. |  | HazelcastInstance |
| **hazelcastMode** (advanced) | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |

## Endpoint Options

The Hazelcast Atomic Number endpoint is configured using URI syntax:

hazelcast-atomicvalue:cacheName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheName** (producer) | **Required** The name of the cache. |  | String |

### Query Parameters (5 parameters)

   
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

## Message Headers

The Hazelcast Atomic Number component supports 1 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHazelcastOperationType** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#OPERATION) | The operation to perform. |  | String |

## atomic number producer - to("hazelcast-atomicvalue:foo")

The operations for this producer are:

-   setvalue (set the number with a given value)
    
-   get
    
-   increment (+1)
    
-   decrement (-1)
    
-   destroy
    
-   compareAndSet
    
-   getAndAdd
    

### Example for **set**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:set")
    .setHeader("CamelHazelcastOperationType", constant("setValue"))
    .to("hazelcast-atomicvalue:foo");
```

```xml
<route>
    <from uri="direct:set"/>
    <setHeader name="hazelcast.operation.type">
        <constant>setvalue</constant>
    </setHeader>
    <to uri="hazelcast-atomicvalue:foo"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:set
      steps:
        - setHeader:
            name: hazelcast.operation.type
            constant: setvalue
        - to:
            uri: hazelcast-atomicvalue:foo
```

Provide the value to set inside the message body (here the value is 10): `template.sendBody("direct:set", 10);`

### Example for **get**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:get")
    .setHeader("CamelHazelcastOperationType", constant("get"))
    .to("hazelcast-atomicvalue:foo");
```

```xml
<route>
    <from uri="direct:get"/>
    <setHeader name="hazelcast.operation.type">
        <constant>get</constant>
    </setHeader>
    <to uri="hazelcast-atomicvalue:foo"/>
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
            uri: hazelcast-atomicvalue:foo
```

You can get the number with `long body = template.requestBody("direct:get", null, Long.class);`.

### Example for **increment**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:increment")
    .setHeader("CamelHazelcastOperationType", constant("increment"))
    .to("hazelcast-atomicvalue:foo");
```

```xml
<route>
    <from uri="direct:increment"/>
    <setHeader name="hazelcast.operation.type">
        <constant>increment</constant>
    </setHeader>
    <to uri="hazelcast-atomicvalue:foo"/>
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
            uri: hazelcast-atomicvalue:foo
```

The actual value (after increment) will be provided inside the message body.

### Example for **decrement**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:decrement")
    .setHeader("CamelHazelcastOperationType", constant("decrement"))
    .to("hazelcast-atomicvalue:foo");
```

```xml
<route>
    <from uri="direct:decrement"/>
    <setHeader name="hazelcast.operation.type">
        <constant>decrement</constant>
    </setHeader>
    <to uri="hazelcast-atomicvalue:foo"/>
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
            uri: hazelcast-atomicvalue:foo
```

The actual value (after decrement) will be provided inside the message body.

### Example for **destroy**

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:destroy")
    .setHeader("CamelHazelcastOperationType", constant("destroy"))
    .to("hazelcast-atomicvalue:foo");
```

```xml
<route>
    <from uri="direct:destroy"/>
    <setHeader name="hazelcast.operation.type">
        <constant>destroy</constant>
    </setHeader>
    <to uri="hazelcast-atomicvalue:foo"/>
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
            uri: hazelcast-atomicvalue:foo
```