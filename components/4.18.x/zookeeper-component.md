# ZooKeeper

**Since Camel 2.9**

**Both producer and consumer are supported**

The ZooKeeper component allows interaction with a [ZooKeeper](https://zookeeper.apache.org/) cluster and exposes the following features to Camel:

1.  Creation of nodes in any of the ZooKeeper create modes.
    
2.  Get and Set the data contents of arbitrary cluster nodes (data being set must be convertible to `byte[]`).
    
3.  Create and retrieve the list of the child nodes attached to a particular node.
    

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-zookeeper</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

zookeeper://zookeeper-server\[:port\]\[/path\]\[?options\]

The path from the URI specifies the node in the ZooKeeper server (a.k.a. _znode_) that will be the target of the endpoint:

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

The ZooKeeper component supports 11 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **listChildren** (common) | Whether the children of the node should be listed. | false | boolean |
| **timeout** (common) | The time interval to wait on connection before timing out. | 5000 | int |
| **backoff** (consumer) | The time interval to backoff for after an error before retrying. | 5000 | long |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **repeat** (consumer) | Should changes to the znode be 'watched' and repeatedly processed. | false | boolean |
| **sendEmptyMessageOnDelete** (consumer) | Upon the delete of a znode, should an empty message be send to the consumer. | true | boolean |
| **create** (producer) | Should the endpoint create the node if it does not currently exist. | false | boolean |
| **createMode** (producer) | 
The create mode that should be used for the newly created node.

Enum values:

-   PERSISTENT
    
-   PERSISTENT\_SEQUENTIAL
    
-   EPHEMERAL
    
-   EPHEMERAL\_SEQUENTIAL
    





 | EPHEMERAL | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | To use a shared ZooKeeperConfiguration. |  | ZooKeeperConfiguration |

## Endpoint Options

The ZooKeeper endpoint is configured using URI syntax:

zookeeper:serverUrls/path

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serverUrls** (common) | **Required** The zookeeper server hosts (multiple servers can be separated by comma). |  | String |
| **path** (common) | **Required** The node in the ZooKeeper server (aka znode). |  | String |

### Query Parameters (11 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **listChildren** (common) | Whether the children of the node should be listed. | false | boolean |
| **timeout** (common) | The time interval to wait on connection before timing out. | 5000 | int |
| **backoff** (consumer) | The time interval to backoff for after an error before retrying. | 5000 | long |
| **repeat** (consumer) | Should changes to the znode be 'watched' and repeatedly processed. | false | boolean |
| **sendEmptyMessageOnDelete** (consumer) | Upon the delete of a znode, should an empty message be send to the consumer. | true | boolean |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **create** (producer) | Should the endpoint create the node if it does not currently exist. | false | boolean |
| **createMode** (producer) | 

The create mode that should be used for the newly created node.

Enum values:

-   PERSISTENT
    
-   PERSISTENT\_SEQUENTIAL
    
-   EPHEMERAL
    
-   EPHEMERAL\_SEQUENTIAL
    





 | EPHEMERAL | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The ZooKeeper component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelZooKeeperNode** (common) Constant: [`ZOOKEEPER_NODE`](https://javadoc.io/doc/org.apache.camel/camel-zookeeper/latest/org/apache/camel/component/zookeeper/ZooKeeperMessage.html#ZOOKEEPER_NODE) | The node. |  | String |
| **CamelZooKeeperVersion** (common) Constant: [`ZOOKEEPER_NODE_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-zookeeper/latest/org/apache/camel/component/zookeeper/ZooKeeperMessage.html#ZOOKEEPER_NODE_VERSION) | The node version. | \-1 | Integer |
| **CamelZookeeperAcl** (common) Constant: [`ZOOKEEPER_ACL`](https://javadoc.io/doc/org.apache.camel/camel-zookeeper/latest/org/apache/camel/component/zookeeper/ZooKeeperMessage.html#ZOOKEEPER_ACL) | The ACL. | Ids.OPEN\_ACL\_UNSAFE | List |
| **CamelZookeeperCreateMode** (common) Constant: [`ZOOKEEPER_CREATE_MODE`](https://javadoc.io/doc/org.apache.camel/camel-zookeeper/latest/org/apache/camel/component/zookeeper/ZooKeeperMessage.html#ZOOKEEPER_CREATE_MODE) | The create mode. |  | CreateMode or String |
| **CamelZookeeperStatistics** (common) Constant: [`ZOOKEEPER_STATISTICS`](https://javadoc.io/doc/org.apache.camel/camel-zookeeper/latest/org/apache/camel/component/zookeeper/ZooKeeperMessage.html#ZOOKEEPER_STATISTICS) | The statistics. |  | Stat |
| **CamelZookeeperEventType** (common) Constant: [`ZOOKEEPER_EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-zookeeper/latest/org/apache/camel/component/zookeeper/ZooKeeperMessage.html#ZOOKEEPER_EVENT_TYPE) | 
The event type.

Enum values:

-   None
    
-   NodeCreated
    
-   NodeDeleted
    
-   NodeDataChanged
    
-   NodeChildrenChanged
    
-   DataWatchRemoved
    
-   ChildWatchRemoved
    
-   PersistentWatchRemoved
    





 |  | EventType |
| **CamelZookeeperOperation** (producer) Constant: [`ZOOKEEPER_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-zookeeper/latest/org/apache/camel/component/zookeeper/ZooKeeperMessage.html#ZOOKEEPER_OPERATION) | The operation to perform. |  | String |

## Usage

### Reading from a _znode_

The following snippet will read the data from the _znode_ `/somepath/somenode/` provided that it already exists. The data retrieved will be placed into an exchange and passed onto the rest of the route:

```java
from("zookeeper://localhost:39913/somepath/somenode").to("mock:result");
```

If the node does not yet exist, then a flag can be supplied to have the endpoint await its creation:

```java
from("zookeeper://localhost:39913/somepath/somenode?awaitCreation=true").to("mock:result");
```

### Reading from a _znode_

When data is read due to a `WatchedEvent` received from the ZooKeeper ensemble, the `CamelZookeeperEventType` header holds ZooKeeper’s [`EventType`](http://zookeeper.apache.org/doc/current/api/org/apache/zookeeper/Watcher.Event.EventType.md) value from that `WatchedEvent`. If the data is read initially (not triggered by a `WatchedEvent`) the `CamelZookeeperEventType` header will not be set.

### Writing to a _znode_

The following snippet will write the payload of the exchange into the znode at `/somepath/somenode/` provided that it already exists:

```java
from("direct:write-to-znode")
    .to("zookeeper://localhost:39913/somepath/somenode");
```

For flexibility, the endpoint allows the target _znode_ to be specified dynamically as a message header. If a header keyed by the string `CamelZooKeeperNode` is present then the value of the header will be used as the path to the _znode_ on the server. For instance using the same route definition above, the following code snippet will write the data not to `/somepath/somenode` but to the path from the header `/somepath/someothernode`.

> **Warning**
> the `testPayload` must be convertible to `byte[]` as the data stored in ZooKeeper is byte-based.

```java
Object testPayload = ...
template.sendBodyAndHeader("direct:write-to-znode", testPayload, "CamelZooKeeperNode", "/somepath/someothernode");
```

To also create the node if it does not exist the `create` option should be used.

```java
from("direct:create-and-write-to-znode")
    .to("zookeeper://localhost:39913/somepath/somenode?create=true");
```

It is also possible to **delete** a node using the header `CamelZookeeperOperation` by setting it to `DELETE`:

```java
from("direct:delete-znode")
    .setHeader(ZooKeeperMessage.ZOOKEEPER_OPERATION, constant("DELETE"))
    .to("zookeeper://localhost:39913/somepath/somenode");
```

or equivalently:

```xml
<route>
  <from uri="direct:delete-znode" />
  <setHeader name="CamelZookeeperOperation">
     <constant>DELETE</constant>
  </setHeader>
  <to uri="zookeeper://localhost:39913/somepath/somenode" />
</route>
```

ZooKeeper’s nodes can have different types; they can be 'Ephemeral' or 'Persistent' and 'Sequenced' or 'Unsequenced'. For further information of each type, you can check [here](http://zookeeper.apache.org/doc/trunk/zookeeperProgrammers.html#Ephemeral+Nodes). By default, endpoints will create unsequenced, ephemeral nodes, but the type can be easily manipulated via an URI config parameter or via a special message header. The values expected for the create mode are simply the names from the `CreateMode` enumeration:

-   `PERSISTENT`
    
-   `PERSISTENT_SEQUENTIAL`
    
-   `EPHEMERAL`
    
-   `EPHEMERAL_SEQUENTIAL`
    

For example, to create a persistent _znode_ via the URI config:

```java
from("direct:create-and-write-to-persistent-znode")
    .to("zookeeper://localhost:39913/somepath/somenode?create=true&createMode=PERSISTENT");
```

or using the header `CamelZookeeperCreateMode`.

> **Warning**
> the `testPayload` must be convertible to `byte[]` as the data stored in ZooKeeper is byte-based.

```java
Object testPayload = ...
template.sendBodyAndHeader("direct:create-and-write-to-persistent-znode", testPayload, "CamelZooKeeperCreateMode", "PERSISTENT");
```

## Spring Boot Auto-Configuration

When using zookeeper with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-zookeeper-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 36 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.cloud.zookeeper.attributes** | Custom service attributes. |  | Map |
| **camel.cloud.zookeeper.auth-info-list** | List of AuthInfo objects with scheme and auth. |  | List |
| **camel.cloud.zookeeper.base-path** | The base path to store in ZooKeeper. |  | String |
| **camel.cloud.zookeeper.connection-timeout** | Connection timeout. | 15000 | Long |
| **camel.cloud.zookeeper.connection-timeout-unit** | Connection timeout TimeUnit. Default is TimeUnit.MILLISECONDS. | milliseconds | TimeUnit |
| **camel.cloud.zookeeper.curator-framework** | Zookeeper CuratorFramework-style client. |  | CuratorFramework |
| **camel.cloud.zookeeper.enabled** | Sets if the zookeeper service registry should be enabled or not, default is false. | false | Boolean |
| **camel.cloud.zookeeper.id** | Service Registry ID. |  | String |
| **camel.cloud.zookeeper.max-close-wait** | Time to wait during close to join background threads. | 1000 | Long |
| **camel.cloud.zookeeper.max-close-wait-unit** | MaxCloseWait TimeUnit. Default is TimeUnit.MILLISECONDS. | milliseconds | TimeUnit |
| **camel.cloud.zookeeper.namespace** | ZooKeeper namespace. If a namespace is set here, all paths will get pre-pended with the namespace. |  | String |
| **camel.cloud.zookeeper.nodes** | The Zookeeper server hosts (multiple servers can be separated by comma). |  | List |
| **camel.cloud.zookeeper.order** | Service lookup order/priority. |  | Integer |
| **camel.cloud.zookeeper.reconnect-base-sleep-time** | Initial amount of time to wait between retries. | 0 | Long |
| **camel.cloud.zookeeper.reconnect-base-sleep-time-unit** | ReconnectBaseSleepTime TimeUnit. Default is TimeUnit.MILLISECONDS. | milliseconds | TimeUnit |
| **camel.cloud.zookeeper.reconnect-max-retries** | Max number of times to retry. | 3 | Integer |
| **camel.cloud.zookeeper.reconnect-max-sleep-time** | Max time to sleep on each retry. Default is Integer.MAX\_VALUE. |  | Long |
| **camel.cloud.zookeeper.reconnect-max-sleep-time-unit** | ReconnectMaxSleepTimeUnit TimeUnit. Default is TimeUnit.MILLISECONDS. | milliseconds | TimeUnit |
| **camel.cloud.zookeeper.retry-policy** | Retry policy to use. |  | RetryPolicy |
| **camel.cloud.zookeeper.session-timeout** | Session timeout. | 60000 | Long |
| **camel.cloud.zookeeper.session-timeout-unit** | Session timeout TimeUnit. Default is TimeUnit.MILLISECONDS. | milliseconds | TimeUnit |
| **camel.component.zookeeper.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.zookeeper.backoff** | The time interval to backoff for after an error before retrying. | 5000 | Long |
| **camel.component.zookeeper.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.zookeeper.configuration** | To use a shared ZooKeeperConfiguration. The option is a org.apache.camel.component.zookeeper.ZooKeeperConfiguration type. |  | ZooKeeperConfiguration |
| **camel.component.zookeeper.create** | Should the endpoint create the node if it does not currently exist. | false | Boolean |
| **camel.component.zookeeper.create-mode** | The create mode that should be used for the newly created node. | EPHEMERAL | String |
| **camel.component.zookeeper.enabled** | Whether to enable auto configuration of the zookeeper component. This is enabled by default. |  | Boolean |
| **camel.component.zookeeper.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.zookeeper.list-children** | Whether the children of the node should be listed. | false | Boolean |
| **camel.component.zookeeper.repeat** | Should changes to the znode be 'watched' and repeatedly processed. | false | Boolean |
| **camel.component.zookeeper.send-empty-message-on-delete** | Upon the delete of a znode, should an empty message be send to the consumer. | true | Boolean |
| **camel.component.zookeeper.timeout** | The time interval to wait on connection before timing out. | 5000 | Integer |
| **camel.cloud.zookeeper.deregister-services-on-stop** | **Deprecated** Should we remove all the registered services know by this registry on stop ? Default is true. | true | Boolean |
| **camel.cloud.zookeeper.override-service-host** | **Deprecated** Should we override the service host if given ? Default is true. | true | Boolean |
| **camel.cloud.zookeeper.service-host** | **Deprecated** Service host. |  | String |