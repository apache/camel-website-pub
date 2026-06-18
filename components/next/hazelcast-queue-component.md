# Hazelcast Queue

**Since Camel 2.7**

**Both producer and consumer are supported**

The [Hazelcast](http://www.hazelcast.com/) Queue component is one of Camel Hazelcast Components which allows you to access Hazelcast distributed queue.

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

The Hazelcast Queue component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **hazelcastInstance** (advanced) | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. |  | HazelcastInstance |
| **hazelcastMode** (advanced) | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |

## Endpoint Options

The Hazelcast Queue endpoint is configured using URI syntax:

hazelcast-queue:cacheName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **cacheName** (common) | **Required** The name of the cache. |  | String |

### Query Parameters (11 parameters)

   
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
| **pollingTimeout** (consumer) | Define the polling timeout of the Queue consumer in Poll mode. | 10000 | long |
| **poolSize** (consumer) | Define the Pool size for Queue Consumer Executor. | 1 | int |
| **queueConsumerMode** (consumer) | 

Define the Queue Consumer mode: Listen or Poll.

Enum values:

-   listen
    
-   poll
    





 | Listen | HazelcastQueueConsumerMode |
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

The Hazelcast Queue component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelHazelcastObjectId** (common) Constant: [`OBJECT_ID`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#OBJECT_ID) | the object id to store / find your object inside the cache. |  | String |
| **CamelHazelcastDrainToCollection** (producer) Constant: [`DRAIN_TO_COLLECTION`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#DRAIN_TO_COLLECTION) | The collection to transfer elements into. |  | Collection |
| **CamelHazelcastListenerAction** (consumer) Constant: [`LISTENER_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#LISTENER_ACTION) | The type of event - here added and removed. |  | String |
| **CamelHazelcastListenerType** (consumer) Constant: [`LISTENER_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#LISTENER_TYPE) | The map consumer. |  | String |
| **CamelHazelcastListenerTime** (consumer) Constant: [`LISTENER_TIME`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#LISTENER_TIME) | The time of the event in millis. |  | Long |
| **CamelHazelcastCacheName** (consumer) Constant: [`CACHE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#CACHE_NAME) | The name of the cache - e.g. foo. |  | String |
| **CamelHazelcastOperationType** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-hazelcast/latest/org/apache/camel/component/hazelcast/HazelcastConstants.html#OPERATION) | The operation to perform. |  | String |

## Queue producer – to(“hazelcast-queue:foo”)

The queue producer provides 12 operations:

-   add
    
-   put
    
-   poll
    
-   peek
    
-   offer
    
-   removevalue
    
-   remainingCapacity
    
-   removeAll
    
-   removeIf
    
-   drainTo
    
-   take
    
-   retainAll
    

### Example for **add**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:add")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.ADD))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:add"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>add</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:add
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: add
        - to:
            uri: hazelcast-queue:bar
```

### Example for **put**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:put")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.PUT))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:put"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>put</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
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
            uri: hazelcast-queue:bar
```

### Example for **poll**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:poll")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.POLL))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:poll"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>poll</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:poll
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: poll
        - to:
            uri: hazelcast-queue:bar
```

### Example for **peek**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:peek")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.PEEK))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:peek"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>peek</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:peek
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: peek
        - to:
            uri: hazelcast-queue:bar
```

### Example for **offer**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:offer")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.OFFER))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:offer"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>offer</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:offer
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: offer
        - to:
            uri: hazelcast-queue:bar
```

### Example for **removevalue**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:removevalue")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.REMOVE_VALUE))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:removevalue"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>removeValue</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:removevalue
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: removeValue
        - to:
            uri: hazelcast-queue:bar
```

### Example for **remaining capacity**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:remaining-capacity")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.REMAINING_CAPACITY))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:remaining-capacity"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>remainingCapacity</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:remaining-capacity
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: remainingCapacity
        - to:
            uri: hazelcast-queue:bar
```

### Example for **remove all**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:removeAll")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.REMOVE_ALL))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:removeAll"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>removeAll</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:removeAll
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: removeAll
        - to:
            uri: hazelcast-queue:bar
```

### Example for **remove if**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:removeIf")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.REMOVE_IF))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:removeIf"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>removeIf</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:removeIf
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: removeIf
        - to:
            uri: hazelcast-queue:bar
```

### Example for **drain to**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:drainTo")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.DRAIN_TO))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:drainTo"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>drainTo</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:drainTo
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: drainTo
        - to:
            uri: hazelcast-queue:bar
```

### Example for **take**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:take")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.TAKE))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:take"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>take</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:take
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: take
        - to:
            uri: hazelcast-queue:bar
```

### Example for **retain all**:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:retainAll")
    .setHeader(HazelcastConstants.OPERATION, constant(HazelcastOperation.RETAIN_ALL))
    .to("hazelcast-queue:bar");
```

```xml
<route>
  <from uri="direct:retainAll"/>
  <setHeader name="CamelHazelcastOperationType">
    <constant>retainAll</constant>
  </setHeader>
  <to uri="hazelcast-queue:bar"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:retainAll
      steps:
        - setHeader:
            name: CamelHazelcastOperationType
            constant: retainAll
        - to:
            uri: hazelcast-queue:bar
```

## Queue consumer – from(“hazelcast-queue:foo”)

The queue consumer provides two different modes:

-   Poll
    
-   Listen
    

Sample for **Poll** mode

-   Java
    
-   XML
    
-   YAML
    

```java
from("hazelcast-queue:foo?queueConsumerMode=Poll")
    .to("mock:result");
```

```xml
<route>
  <from uri="hazelcast-queue:foo?queueConsumerMode=Poll"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: hazelcast-queue:foo
      parameters:
        queueConsumerMode: Poll
      steps:
        - to:
            uri: mock:result
```

In this way, the consumer will poll the queue and return the head of the queue or null after a timeout.

In Listen mode instead, the consumer will listen for events on queue.

The queue consumer in Listen mode provides 2 operations: \* add \* remove

Sample for **Listen** mode

-   Java
    
-   XML
    
-   YAML
    

```java
from("hazelcast-queue:mm")
    .log("object...")
    .choice()
        .when(header(HazelcastConstants.LISTENER_ACTION).isEqualTo(HazelcastConstants.ADDED))
            .log("...added")
            .to("mock:added")
        .when(header(HazelcastConstants.LISTENER_ACTION).isEqualTo(HazelcastConstants.REMOVED))
            .log("...removed")
            .to("mock:removed")
        .otherwise()
            .log("fail!");
```

```xml
<route>
  <from uri="hazelcast-queue:mm"/>
  <log message="object..."/>
  <choice>
    <when>
      <simple>${header.CamelHazelcastListenerAction} == 'added'</simple>
      <log message="...added"/>
      <to uri="mock:added"/>
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
      uri: hazelcast-queue:mm
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

## Spring Boot Auto-Configuration

When using hazelcast-queue with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-hazelcast-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 68 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.hazelcast-atomicvalue.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-atomicvalue.enabled** | Whether to enable auto configuration of the hazelcast-atomicvalue component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-atomicvalue.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-atomicvalue.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-atomicvalue.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.hazelcast-instance.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-instance.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hazelcast-instance.enabled** | Whether to enable auto configuration of the hazelcast-instance component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-instance.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-instance.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-list.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-list.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hazelcast-list.enabled** | Whether to enable auto configuration of the hazelcast-list component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-list.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-list.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-list.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.hazelcast-map.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-map.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hazelcast-map.enabled** | Whether to enable auto configuration of the hazelcast-map component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-map.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-map.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-map.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.hazelcast-multimap.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-multimap.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hazelcast-multimap.enabled** | Whether to enable auto configuration of the hazelcast-multimap component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-multimap.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-multimap.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-multimap.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.hazelcast-pncounter.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-pncounter.enabled** | Whether to enable auto configuration of the hazelcast-pncounter component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-pncounter.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-pncounter.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-pncounter.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.hazelcast-queue.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-queue.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hazelcast-queue.enabled** | Whether to enable auto configuration of the hazelcast-queue component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-queue.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-queue.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-queue.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.hazelcast-replicatedmap.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-replicatedmap.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hazelcast-replicatedmap.enabled** | Whether to enable auto configuration of the hazelcast-replicatedmap component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-replicatedmap.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-replicatedmap.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-replicatedmap.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.hazelcast-ringbuffer.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-ringbuffer.enabled** | Whether to enable auto configuration of the hazelcast-ringbuffer component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-ringbuffer.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-ringbuffer.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-ringbuffer.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.hazelcast-seda.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-seda.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hazelcast-seda.enabled** | Whether to enable auto configuration of the hazelcast-seda component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-seda.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-seda.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-seda.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.hazelcast-set.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-set.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hazelcast-set.enabled** | Whether to enable auto configuration of the hazelcast-set component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-set.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-set.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-set.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.hazelcast-topic.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.hazelcast-topic.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.hazelcast-topic.enabled** | Whether to enable auto configuration of the hazelcast-topic component. This is enabled by default. |  | Boolean |
| **camel.component.hazelcast-topic.hazelcast-instance** | The hazelcast instance reference which can be used for hazelcast endpoint. If you don’t specify the instance reference, camel use the default hazelcast instance from the camel-hazelcast instance. The option is a com.hazelcast.core.HazelcastInstance type. |  | HazelcastInstance |
| **camel.component.hazelcast-topic.hazelcast-mode** | The hazelcast mode reference which kind of instance should be used. If you don’t specify the mode, then the node mode will be the default. | node | String |
| **camel.component.hazelcast-topic.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |