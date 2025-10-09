# Corda

> **Warning**
> **Deprecated:** This corda is deprecated and may be removed in a future release.

**Both producer and consumer are supported**

**Since Camel 2.23**

Camel connector for R3’s [Corda](https://www.corda.net/) blockchain platform using corda-rpc library. This component uses the Corda RPC client.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-corda</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI Format

corda://<host:port>\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Corda component supports 14 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (common) | To use a shared configuration. |  | CordaConfiguration |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **pageSpecification** (consumer) | PageSpecification allows specification of a page number (starting from 1) and page size (defaulting to 200 with a maximum page size of (Integer.MAX\_INT) Note: we default the page number to 200 to enable queries without requiring a page specification but enabling detection of large results sets that fall out of the 200 requirement. Max page size should be used with extreme caution as results may exceed your JVM memory footprint. | 200 | PageSpecification |
| **processSnapshot** (consumer) | Whether to process snapshots or not. | true | boolean |
| **sort** (consumer) | 
Sort allows specification of a set of entity attribute names and their associated directionality and null handling, to be applied upon processing a query specification.

Enum values:

-   ASC
    
-   DESC
    





 |  | Sort |
| **contractStateClass** (consumer (advanced)) | A contract state (or just state) contains opaque data used by a contract program. It can be thought of as a disk file that the program can use to persist data across transactions. States are immutable: once created they are never updated, instead, any changes must generate a new successor state. States can be updated (consumed) only once: the notary is responsible for ensuring there is no double spending by only signing a transaction if the input states are all free. |  | Class |
| **flowLogicArguments** (consumer (advanced)) | Start the given flow with the given arguments, returning an Observable with a single observation of the result of running the flow. The flowLogicClass must be annotated with net.corda.core.flows.StartableByRPC. |  | Object\[\] |
| **flowLogicClass** (consumer (advanced)) | Start the given flow with the given arguments, returning an Observable with a single observation of the result of running the flow. The flowLogicClass must be annotated with net.corda.core.flows.StartableByRPC. |  | Class |
| **queryCriteria** (consumer (advanced)) | QueryCriteria assumes underlying schema tables are correctly indexed for performance. |  | QueryCriteria |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | Operation to use. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **password** (security) | Password for login. |  | String |
| **username** (security) | Username for login. |  | String |

## Endpoint Options

The Corda endpoint is configured using URI syntax:

corda:node

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **node** (common) | **Required** The url for the corda node. |  | String |

### Query Parameters (14 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **pageSpecification** (consumer) | PageSpecification allows specification of a page number (starting from 1) and page size (defaulting to 200 with a maximum page size of (Integer.MAX\_INT) Note: we default the page number to 200 to enable queries without requiring a page specification but enabling detection of large results sets that fall out of the 200 requirement. Max page size should be used with extreme caution as results may exceed your JVM memory footprint. | 200 | PageSpecification |
| **processSnapshot** (consumer) | Whether to process snapshots or not. | true | boolean |
| **sort** (consumer) | 
Sort allows specification of a set of entity attribute names and their associated directionality and null handling, to be applied upon processing a query specification.

Enum values:

-   ASC
    
-   DESC
    





 |  | Sort |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **contractStateClass** (consumer (advanced)) | A contract state (or just state) contains opaque data used by a contract program. It can be thought of as a disk file that the program can use to persist data across transactions. States are immutable: once created they are never updated, instead, any changes must generate a new successor state. States can be updated (consumed) only once: the notary is responsible for ensuring there is no double spending by only signing a transaction if the input states are all free. |  | Class |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **flowLogicArguments** (consumer (advanced)) | Start the given flow with the given arguments, returning an Observable with a single observation of the result of running the flow. The flowLogicClass must be annotated with net.corda.core.flows.StartableByRPC. |  | Object\[\] |
| **flowLogicClass** (consumer (advanced)) | Start the given flow with the given arguments, returning an Observable with a single observation of the result of running the flow. The flowLogicClass must be annotated with net.corda.core.flows.StartableByRPC. |  | Class |
| **queryCriteria** (consumer (advanced)) | QueryCriteria assumes underlying schema tables are correctly indexed for performance. |  | QueryCriteria |
| **operation** (producer) | Operation to use. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **password** (security) | Password for login. |  | String |
| **username** (security) | Username for login. |  | String |

## Message Headers

The Corda component supports 9 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **OPERATION** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-corda/latest/org/apache/camel/component/corda/CordaConstants.html#OPERATION) | The operation to perform. |  | String |
| **ATTACHMENT\_QUERY\_CRITERIA** (producer) Constant: [`ATTACHMENT_QUERY_CRITERIA`](https://javadoc.io/doc/org.apache.camel/camel-corda/latest/org/apache/camel/component/corda/CordaConstants.html#ATTACHMENT_QUERY_CRITERIA) | The attachment query criteria. |  | AttachmentQueryCriteria |
| **SORT** (producer) Constant: [`SORT`](https://javadoc.io/doc/org.apache.camel/camel-corda/latest/org/apache/camel/component/corda/CordaConstants.html#SORT) | The sort. |  |  |
| **EXACT\_MATCH** (producer) Constant: [`EXACT_MATCH`](https://javadoc.io/doc/org.apache.camel/camel-corda/latest/org/apache/camel/component/corda/CordaConstants.html#EXACT_MATCH) | If true, a case sensitive match is done against each component of each X.500 name. |  | Boolean |
| **ARGUMENTS** (producer) Constant: [`ARGUMENTS`](https://javadoc.io/doc/org.apache.camel/camel-corda/latest/org/apache/camel/component/corda/CordaConstants.html#ARGUMENTS) | The arguments. |  | Object\[\] |
| **DRAINING\_MODE** (producer) Constant: [`DRAINING_MODE`](https://javadoc.io/doc/org.apache.camel/camel-corda/latest/org/apache/camel/component/corda/CordaConstants.html#DRAINING_MODE) | The value of the node’s flows draining mode. |  | Boolean |
| **SECURE\_HASH** (producer) Constant: [`SECURE_HASH`](https://javadoc.io/doc/org.apache.camel/camel-corda/latest/org/apache/camel/component/corda/CordaConstants.html#SECURE_HASH) | Container for a cryptographically secure hash value. |  | SecureHash |
| **QUERY\_CRITERIA** (producer) Constant: [`QUERY_CRITERIA`](https://javadoc.io/doc/org.apache.camel/camel-corda/latest/org/apache/camel/component/corda/CordaConstants.html#QUERY_CRITERIA) | The query criteria. |  | QueryCriteria |
| **PAGE\_SPECIFICATION** (producer) Constant: [`PAGE_SPECIFICATION`](https://javadoc.io/doc/org.apache.camel/camel-corda/latest/org/apache/camel/component/corda/CordaConstants.html#PAGE_SPECIFICATION) | The PageSpecification allows specification of a page number and page size. |  | PageSpecification |

## Samples

Subscribe for new vault state changes:

```java
from("corda://localhost:10006?username=user1&password=test&operation=VAULT_TRACK&contractStateClass=#contractStateClass")
    .to("jms:queue:vault");
```

Read the node information:

```java
from("direct:start")
    .to("corda://localhost:10006?username=user1&password=test&operation=NODE_INFO");
```

## Spring Boot Auto-Configuration

When using corda with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-corda-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 15 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.corda.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.corda.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.corda.configuration** | To use a shared configuration. The option is a org.apache.camel.component.corda.CordaConfiguration type. |  | CordaConfiguration |
| **camel.component.corda.contract-state-class** | A contract state (or just state) contains opaque data used by a contract program. It can be thought of as a disk file that the program can use to persist data across transactions. States are immutable: once created they are never updated, instead, any changes must generate a new successor state. States can be updated (consumed) only once: the notary is responsible for ensuring there is no double spending by only signing a transaction if the input states are all free. |  | Class |
| **camel.component.corda.enabled** | Whether to enable auto configuration of the corda component. This is enabled by default. |  | Boolean |
| **camel.component.corda.flow-logic-arguments** | Start the given flow with the given arguments, returning an Observable with a single observation of the result of running the flow. The flowLogicClass must be annotated with net.corda.core.flows.StartableByRPC. |  | Object\[\] |
| **camel.component.corda.flow-logic-class** | Start the given flow with the given arguments, returning an Observable with a single observation of the result of running the flow. The flowLogicClass must be annotated with net.corda.core.flows.StartableByRPC. |  | Class |
| **camel.component.corda.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.corda.operation** | Operation to use. |  | String |
| **camel.component.corda.page-specification** | PageSpecification allows specification of a page number (starting from 1) and page size (defaulting to 200 with a maximum page size of (Integer.MAX\_INT) Note: we default the page number to 200 to enable queries without requiring a page specification but enabling detection of large results sets that fall out of the 200 requirement. Max page size should be used with extreme caution as results may exceed your JVM memory footprint. The option is a net.corda.core.node.services.vault.PageSpecification type. |  | PageSpecification |
| **camel.component.corda.password** | Password for login. |  | String |
| **camel.component.corda.process-snapshot** | Whether to process snapshots or not. | true | Boolean |
| **camel.component.corda.query-criteria** | QueryCriteria assumes underlying schema tables are correctly indexed for performance. The option is a net.corda.core.node.services.vault.QueryCriteria type. |  | QueryCriteria |
| **camel.component.corda.sort** | Sort allows specification of a set of entity attribute names and their associated directionality and null handling, to be applied upon processing a query specification. |  | Sort |
| **camel.component.corda.username** | Username for login. |  | String |