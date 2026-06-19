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

-   Java
    
-   XML
    
-   YAML
    

```java
from("zookeeper://localhost:39913/somepath/somenode").to("mock:result");
```

```xml
<route>
  <from uri="zookeeper://localhost:39913/somepath/somenode"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: zookeeper://localhost:39913/somepath/somenode
      steps:
        - to:
            uri: mock:result
```

If the node does not yet exist, then a flag can be supplied to have the endpoint await its creation:

-   Java
    
-   XML
    
-   YAML
    

```java
from("zookeeper://localhost:39913/somepath/somenode?awaitCreation=true").to("mock:result");
```

```xml
<route>
  <from uri="zookeeper://localhost:39913/somepath/somenode?awaitCreation=true"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: zookeeper://localhost:39913/somepath/somenode
      parameters:
        awaitCreation: true
      steps:
        - to:
            uri: mock:result
```

### Reading from a _znode_

When data is read due to a `WatchedEvent` received from the ZooKeeper ensemble, the `CamelZookeeperEventType` header holds ZooKeeper’s [`EventType`](http://zookeeper.apache.org/doc/current/api/org/apache/zookeeper/Watcher.Event.EventType.md) value from that `WatchedEvent`. If the data is read initially (not triggered by a `WatchedEvent`) the `CamelZookeeperEventType` header will not be set.

### Writing to a _znode_

The following snippet will write the payload of the exchange into the znode at `/somepath/somenode/` provided that it already exists:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:write-to-znode")
    .to("zookeeper://localhost:39913/somepath/somenode");
```

```xml
<route>
  <from uri="direct:write-to-znode"/>
  <to uri="zookeeper://localhost:39913/somepath/somenode"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:write-to-znode
      steps:
        - to:
            uri: zookeeper://localhost:39913/somepath/somenode
```

For flexibility, the endpoint allows the target _znode_ to be specified dynamically as a message header. If a header keyed by the string `CamelZooKeeperNode` is present then the value of the header will be used as the path to the _znode_ on the server. For instance using the same route definition above, the following code snippet will write the data not to `/somepath/somenode` but to the path from the header `/somepath/someothernode`.

> **Warning**
> the `testPayload` must be convertible to `byte[]` as the data stored in ZooKeeper is byte-based.

_Java-only: ProducerTemplate with dynamic znode header_

```java
Object testPayload = ...
template.sendBodyAndHeader("direct:write-to-znode", testPayload, "CamelZooKeeperNode", "/somepath/someothernode");
```

To also create the node if it does not exist the `create` option should be used.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:create-and-write-to-znode")
    .to("zookeeper://localhost:39913/somepath/somenode?create=true");
```

```xml
<route>
  <from uri="direct:create-and-write-to-znode"/>
  <to uri="zookeeper://localhost:39913/somepath/somenode?create=true"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:create-and-write-to-znode
      steps:
        - to:
            uri: zookeeper://localhost:39913/somepath/somenode
            parameters:
              create: true
```

It is also possible to **delete** a node using the header `CamelZookeeperOperation` by setting it to `DELETE`:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:delete-znode")
    .setHeader(ZooKeeperMessage.ZOOKEEPER_OPERATION, constant("DELETE"))
    .to("zookeeper://localhost:39913/somepath/somenode");
```

```xml
<route>
  <from uri="direct:delete-znode"/>
  <setHeader name="CamelZookeeperOperation">
    <constant>DELETE</constant>
  </setHeader>
  <to uri="zookeeper://localhost:39913/somepath/somenode"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:delete-znode
    steps:
      - setHeader:
          name: CamelZookeeperOperation
          constant: DELETE
      - to:
          uri: zookeeper://localhost:39913/somepath/somenode
```

ZooKeeper’s nodes can have different types; they can be 'Ephemeral' or 'Persistent' and 'Sequenced' or 'Unsequenced'. For further information of each type, you can check [here](http://zookeeper.apache.org/doc/trunk/zookeeperProgrammers.html#Ephemeral+Nodes). By default, endpoints will create unsequenced, ephemeral nodes, but the type can be easily manipulated via an URI config parameter or via a special message header. The values expected for the create mode are simply the names from the `CreateMode` enumeration:

-   `PERSISTENT`
    
-   `PERSISTENT_SEQUENTIAL`
    
-   `EPHEMERAL`
    
-   `EPHEMERAL_SEQUENTIAL`
    

For example, to create a persistent _znode_ via the URI config:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:create-and-write-to-persistent-znode")
    .to("zookeeper://localhost:39913/somepath/somenode?create=true&createMode=PERSISTENT");
```

```xml
<route>
  <from uri="direct:create-and-write-to-persistent-znode"/>
  <to uri="zookeeper://localhost:39913/somepath/somenode?create=true&amp;createMode=PERSISTENT"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:create-and-write-to-persistent-znode
      steps:
        - to:
            uri: zookeeper://localhost:39913/somepath/somenode
            parameters:
              create: true
              createMode: PERSISTENT
```

or using the header `CamelZookeeperCreateMode`.

> **Warning**
> the `testPayload` must be convertible to `byte[]` as the data stored in ZooKeeper is byte-based.

_Java-only: ProducerTemplate with create mode header_

```java
Object testPayload = ...
template.sendBodyAndHeader("direct:create-and-write-to-persistent-znode", testPayload, "CamelZooKeeperCreateMode", "PERSISTENT");
```