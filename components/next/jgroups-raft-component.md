# JGroups raft

**Since Camel 2.24**

**Both producer and consumer are supported**

[JGroups-raft](http://belaban.github.io/jgroups-raft/) is a [Raft](https://raftconsensus.github.io/) implementation in [JGroups](http://www.jgroups.org/). The **jgroups-raft:** component provides interoperability between camel and a JGroups-raft clusters.

Maven users will need to add the following dependency to their `pom.xml` for this component.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-jgroups-raft</artifactId>
    <!-- use the same version as your Camel core version -->
    <version>x.y.z</version>
</dependency>
```

## URI format

jgroups-raft:clusterName\[?options\]

Where **clusterName** represents the name of the JGroups-raft cluster, the component should connect to.

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

The JGroups raft component supports 7 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **channelProperties** (common) | Specifies configuration properties of the RaftHandle JChannel used by the endpoint (ignored if raftHandle ref is provided). | raft.xml | String |
| **raftHandle** (common) | RaftHandle to use. |  | RaftHandle |
| **raftId** (common) | **Required** Unique raftId to use. |  | String |
| **stateMachine** (common) | StateMachine to use. | NopStateMachine | StateMachine |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The JGroups raft endpoint is configured using URI syntax:

jgroups-raft:clusterName

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clusterName** (common) | **Required** The name of the JGroupsraft cluster the component should connect to. |  | String |

### Query Parameters (5 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **enableRoleChangeEvents** (consumer) | If set to true, the consumer endpoint will receive roleChange event as well (not just connecting and/or using the state machine). By default it is set to false. | false | boolean |
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

The JGroups raft component supports 12 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelJGroupsRaftLogSize** (consumer) Constant: [`HEADER_JGROUPSRAFT_LOG_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_LOG_SIZE) | The Raft log size in number of entries. |  | int |
| **CamelJGroupsRaftCommitIndex** (consumer) Constant: [`HEADER_JGROUPSRAFT_COMMIT_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_COMMIT_INDEX) | The commit index. |  | int |
| **CamelJGroupsRaftCurrentTerm** (consumer) Constant: [`HEADER_JGROUPSRAFT_CURRENT_TERM`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_CURRENT_TERM) | The current raft term. |  | int |
| **CamelJGroupsRaftIsLeader** (consumer) Constant: [`HEADER_JGROUPSRAFT_IS_LEADER`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_IS_LEADER) | Whether the node is the Raft Leader or not. |  | boolean |
| **CamelJGroupsRaftLastApplied** (consumer) Constant: [`HEADER_JGROUPSRAFT_LAST_APPLIED`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_LAST_APPLIED) | The index of the last log entry that was appended to the log. |  | int |
| **CamelJGroupsRaftLeaderAddress** (consumer) Constant: [`HEADER_JGROUPSRAFT_LEADER_ADDRESS`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_LEADER_ADDRESS) | The Address ot Raft Leader or not. |  | Address |
| **CamelJGroupsRaftRaftId** (consumer) Constant: [`HEADER_JGROUPSRAFT_RAFT_ID`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_RAFT_ID) | The Raft id of the node. |  | String |
| **CamelJGroupsRaftEventType** (consumer) Constant: [`HEADER_JGROUPSRAFT_EVENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_EVENT_TYPE) | 
The event type.

Enum values:

-   LEADER
    
-   FOLLOWER
    
-   APPLY
    
-   READ\_CONTENT\_FROM
    
-   WRITE\_CONTENT\_TO
    





 |  | JGroupsRaftEventType |
| **CamelJGroupsRaftSetOffset** (producer) Constant: [`HEADER_JGROUPSRAFT_SET_OFFSET`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_SET_OFFSET) | Offset to use in the byte buffer to be set(). |  | Integer |
| **CamelJGroupsRaftSetLength** (producer) Constant: [`HEADER_JGROUPSRAFT_SET_LENGTH`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_SET_LENGTH) | Length to use in the byte buffer to be set(). |  | Integer |
| **CamelJGroupsRaftSetTimeout** (producer) Constant: [`HEADER_JGROUPSRAFT_SET_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_SET_TIMEOUT) | Timeout to be used in set() operation. |  | Long |
| **CamelJGroupsRaftSetTimeUnit** (producer) Constant: [`HEADER_JGROUPSRAFT_SET_TIMEUNIT`](https://javadoc.io/doc/org.apache.camel/camel-jgroups-raft/latest/org/apache/camel/component/jgroups/raft/JGroupsRaftConstants.html#HEADER_JGROUPSRAFT_SET_TIMEUNIT) | 

Timeunit to be used in set() operation.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 |  | TimeUnit |

## Usage

Using `jgroups-raft` component with `enableRoleChangeEvents=true` on the consumer side of the route will capture change in JGroups-raft role and forward them to the Camel route. JGroups-raft consumer processes incoming messages [asynchronously](http://camel.apache.org/asynchronous-routing-engine.md).

-   Java
    
-   XML
    
-   YAML
    

```java
from("jgroups-raft:clusterName?enableRoleChangeEvents=true").to("seda:queue");
```

```xml
<route>
  <from uri="jgroups-raft:clusterName?enableRoleChangeEvents=true"/>
  <to uri="seda:queue"/>
</route>
```

```yaml
- route:
    from:
      uri: jgroups-raft:clusterName
      parameters:
        enableRoleChangeEvents: true
      steps:
        - to:
            uri: seda:queue
```

Using `jgroups-raft` component on the producer side of the route will use the body of the camel exchange (which must be a `byte[]`) to perform a setX() operation on the raftHandle associated with the endpoint.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start").to("jgroups-raft:clusterName");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="jgroups-raft:clusterName"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: jgroups-raft:clusterName
```

## Examples

### Receive cluster view change notifications

The snippet below demonstrates how to create the consumer endpoint listening to the change role events. By default, this option is off.

-   Java
    
-   XML
    
-   YAML
    

```java
from("jgroups-raft:clusterName?enableRoleChangeEvents=true")
    .to("mock:mockEndpoint");
```

```xml
<route>
  <from uri="jgroups-raft:clusterName?enableRoleChangeEvents=true"/>
  <to uri="mock:mockEndpoint"/>
</route>
```

```yaml
- route:
    from:
      uri: jgroups-raft:clusterName
      parameters:
        enableRoleChangeEvents: true
      steps:
        - to:
            uri: mock:mockEndpoint
```

### Keeping singleton route within the cluster

The snippet below demonstrates how to keep the singleton consumer route in the cluster of Camel Contexts. As soon as the master node dies, one of the slaves will be elected as a new master and started. In this particular example, we want to keep singleton [jetty](jetty-component.md) instance listening for the requests on address\` [http://localhost:8080/orders\`](http://localhost:8080/orders`).

_Java-only: programmatic JGroupsRaftClusterService configuration_

```java
JGroupsRaftClusterService service = new JGroupsRaftClusterService();
service.setId("raftId");
service.setRaftId("raftId");
service.setJgroupsClusterName("clusterName");
...
context.addService(service);

from("master:mycluster:jetty:http://localhost:8080/orders").to("jms:orders");
```

## Spring Boot Auto-Configuration

When using jgroups-raft with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-jgroups-raft-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.jgroups-raft.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.jgroups-raft.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.jgroups-raft.channel-properties** | Specifies configuration properties of the RaftHandle JChannel used by the endpoint (ignored if raftHandle ref is provided). | raft.xml | String |
| **camel.component.jgroups-raft.enabled** | Whether to enable auto configuration of the jgroups-raft component. This is enabled by default. |  | Boolean |
| **camel.component.jgroups-raft.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.jgroups-raft.raft-handle** | RaftHandle to use. The option is a org.jgroups.raft.RaftHandle type. |  | RaftHandle |
| **camel.component.jgroups-raft.raft-id** | Unique raftId to use. |  | String |
| **camel.component.jgroups-raft.state-machine** | StateMachine to use. The option is a org.jgroups.raft.StateMachine type. |  | StateMachine |