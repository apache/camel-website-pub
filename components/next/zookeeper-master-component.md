# ZooKeeper Master

**Since Camel 2.19**

**Only consumer is supported**

The **zookeeper-master:** endpoint provides a way to ensure only a single consumer in a cluster consumes from a given endpoint; with automatic fails over if that JVM dies.

This can be beneficial if you need to consume from some legacy back end that either doesn’t support concurrent consumption or due to commercial or stability reasons, you can only have a single connection at any point in time.

## Using the master endpoint

Prefix any camel endpoint with **zookeeper-master:someName:** where _someName_ is a logical name and is used to acquire the master lock. e.g.

-   Java
    
-   XML
    
-   YAML
    

```java
from("zookeeper-master:cheese:jms:foo")
    .to("activemq:wine");
```

```xml
<route>
  <from uri="zookeeper-master:cheese:jms:foo"/>
  <to uri="activemq:wine"/>
</route>
```

```yaml
- route:
    from:
      uri: zookeeper-master:cheese:jms:foo
      steps:
        - to:
            uri: activemq:wine
```

The above simulates the \[Exclusive Consumers\]([http://activemq.apache.org/exclusive-consumer.html](http://activemq.apache.org/exclusive-consumer.md)) type feature in ActiveMQ; but on any third party JMS provider that maybe doesn’t support exclusive consumers.

## URI format

zookeeper-master:name:endpoint\[?options\]

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

The ZooKeeper Master component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **maximumConnectionTimeout** (consumer) | Timeout in millis to use when connecting to the zookeeper ensemble. | 10000 | int |
| **zkRoot** (consumer) | The root path to use in zookeeper where information is stored which nodes are master/slave etc. Will by default use: /camel/zookeepermaster/clusters/master. | /camel/zookeepermaster/clusters/master | String |
| **zooKeeperUrl** (consumer) | The url for the zookeeper ensemble. | localhost:2181 | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **containerIdFactory** (advanced) | To use a custom ContainerIdFactory for creating container ids. |  | ContainerIdFactory |
| **curator** (advanced) | To use a custom configured CuratorFramework as connection to zookeeper ensemble. |  | CuratorFramework |
| **zooKeeperPassword** (security) | The password to use when connecting to the zookeeper ensemble. |  | String |

## Endpoint Options

The ZooKeeper Master endpoint is configured using URI syntax:

zookeeper-master:groupName:consumerEndpointUri

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **groupName** (consumer) | **Required** The name of the cluster group to use. |  | String |
| **consumerEndpointUri** (consumer) | **Required** The consumer endpoint to use in master/slave mode. |  | String |

### Query Parameters (3 parameters)

   
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

## Examples

You can protect a clustered Camel application to only consume files from one active node.

-   Java
    
-   XML
    
-   YAML
    

```java
from("zookeeper-master:myGroup:file:target/inbox?delete=true")
    .log(name + " - Received file: ${file:name}")
    .delay(delay)
    .log(name + " - Done file:     ${file:name}")
    .to("file:target/outbox");
```

```xml
<route>
  <from uri="zookeeper-master:myGroup:file:target/inbox?delete=true"/>
  <log message="${file:name}"/>
  <to uri="file:target/outbox"/>
</route>
```

```yaml
- route:
    from:
      uri: zookeeper-master:myGroup:file:target/inbox?delete=true
      steps:
        - log:
            message: "${file:name}"
        - to:
            uri: file:target/outbox
```

ZooKeeper will by default connect to `localhost:2181`, but you can configure this on the component level.

_Java-only: programmatic component configuration_

```java
MasterComponent master = new MasterComponent();
master.setZooKeeperUrl("myzookeeper:2181");
```

However, you can also configure the url of the ZooKeeper ensemble using environment variables.

```bash
export ZOOKEEPER_URL = "myzookeeper:2181"
```

### Master RoutePolicy

You can also use a `RoutePolicy` to control routes in master/slave mode.

When doing so, you must configure the route policy with

-   url to zookeeper ensemble
    
-   name of the cluster group
    
-   **important** and set the route to not auto startup
    

A little example

_Java-only: programmatic RoutePolicy configuration_

```java
MasterRoutePolicy master = new MasterRoutePolicy();
master.setZooKeeperUrl("localhost:2181");
master.setGroupName("myGroup");

// its import to set the route to not auto startup
// as we let the route policy start/stop the routes when it becomes a master/slave, etc.
from("file:target/inbox?delete=true").noAutoStartup()
    // use the zookeeper master route policy in the clustered group
    // to run this route in master/slave mode
    .routePolicy(master)
    .log(name + " - Received file: ${file:name}")
    .delay(delay)
    .log(name + " - Done file:     ${file:name}")
    .to("file:target/outbox");
```