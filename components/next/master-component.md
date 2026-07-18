# Master

**Since Camel 2.20**

**Only consumer is supported**

The Camel-Master endpoint provides a way to ensure only a single consumer in a cluster consumes from a given endpoint; with automatic fail over if that JVM dies.

This can be handy if you need to consume from some legacy back end that either doesn’t support concurrent consumption or due to commercial or stability reasons, you can only have a single connection at any point in time.

## URI format

master:namespace:endpoint\[?options\]

Where endpoint is any Camel endpoint, you want to run in master/slave mode.

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

The Master component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **backOffDelay** (advanced) | When the master becomes leader then backoff is in use to repeat starting the consumer until the consumer is successfully started or max attempts reached. This option is the delay in millis between start attempts. |  | long |
| **backOffMaxAttempts** (advanced) | When the master becomes leader then backoff is in use to repeat starting the consumer until the consumer is successfully started or max attempts reached. This option is the maximum number of attempts to try. |  | int |
| **service** (advanced) | Inject the service to use. |  | CamelClusterService |
| **serviceSelector** (advanced) | Inject the service selector used to lookup the CamelClusterService to use. |  | Selector |

## Endpoint Options

The Master endpoint is configured using URI syntax:

master:namespace:delegateUri

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **namespace** (consumer) | **Required** The name of the cluster namespace to use. |  | String |
| **delegateUri** (consumer) | **Required** The endpoint uri to use in master/slave mode. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |

## Usage

### Using the master endpoint

Prefix any camel endpoint with **master:someName:** where _someName_ is a logical name and is used to acquire the master lock. For instance:

-   Java
    
-   XML
    
-   YAML
    

```java
from("master:cheese:jms:foo")
    .to("activemq:wine");
```

```xml
<route>
  <from uri="master:cheese:jms:foo"/>
  <to uri="activemq:wine"/>
</route>
```

```yaml
- route:
    from:
      uri: master:cheese:jms:foo
      steps:
        - to:
            uri: activemq:wine
```

In this example, the master component ensures that the route is only active in one node, at any given time, in the cluster. So if there are 8 nodes in the cluster, then the master component will elect one route to be the leader, and only this route will be active, and hence only this route will consume messages from `jms:foo`. In case this route is stopped or unexpectedly terminated, then the master component will detect this, and re-elect another node to be active, which will then become active and start consuming messages from `jms:foo`.

> **Tip**
> Apache ActiveMQ 5.x has such a feature out of the box called [Exclusive Consumers](https://activemq.apache.org/exclusive-consumer.md).

## Example

You can protect a clustered Camel application to only consume files from one active node.

_Java-only: string concatenation to build the master endpoint URI_

```java
// the file endpoint we want to consume from
String url = "file:target/inbox?delete=true";

// use the camel master component in the clustered group named myGroup
// to run a master/slave mode in the following Camel url
from("master:myGroup:" + url)
    .log(name + " - Received file: ${file:name}")
    .delay(delay)
    .log(name + " - Done file:     ${file:name}")
    .to("file:target/outbox");
```

The master component leverages CamelClusterService you can configure using

-   **Java**
    
    _Java-only: programmatic ZooKeeperClusterService configuration_
    
    ```java
    ZooKeeperClusterService service = new ZooKeeperClusterService();
    service.setId("camel-node-1");
    service.setNodes("myzk:2181");
    service.setBasePath("/camel/cluster");
    
    context.addService(service)
    ```
    
-   **Xml (Spring)**
    
    ```xml
    <beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
         http://www.springframework.org/schema/beans
         http://www.springframework.org/schema/beans/spring-beans.xsd
         http://camel.apache.org/schema/spring
         http://camel.apache.org/schema/spring/camel-spring.xsd">
    
    
      <bean id="cluster" class="org.apache.camel.component.zookeeper.cluster.ZooKeeperClusterService">
        <property name="id" value="camel-node-1"/>
        <property name="basePath" value="/camel/cluster"/>
        <property name="nodes" value="myzk:2181"/>
      </bean>
    
      <camelContext xmlns="http://camel.apache.org/schema/spring" autoStartup="false">
        ...
      </camelContext>
    
    </beans>
    ```
    
-   **Spring boot**
    
    ```properties
    camel.component.zookeeper.cluster.service.enabled   = true
    camel.component.zookeeper.cluster.service.id        = camel-node-1
    camel.component.zookeeper.cluster.service.base-path = /camel/cluster
    camel.component.zookeeper.cluster.service.nodes     = myzk:2181
    ```
    

## Implementations

Camel provides the following ClusterService implementations:

-   camel-consul
    
-   camel-file
    
-   camel-infinispan
    
-   camel-jgroups-raft
    
-   camel-jgroups
    
-   camel-kubernetes
    
-   camel-zookeeper