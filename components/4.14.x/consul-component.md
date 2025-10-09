# Consul

**Since Camel 2.18**

**Both producer and consumer are supported**

The Consul component is a component for integrating your application with [Hashicorp Consul](https://www.consul.io/).

Maven users will need to add the following dependency to their pom.xml for this component:

```xml
    <dependency>
        <groupId>org.apache.camel</groupId>
        <artifactId>camel-consul</artifactId>
        <version>${camel-version}</version>
    </dependency>
```

## URI format

consul://domain?\[options\]

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

The Consul component supports 26 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectTimeout** (common) | Connect timeout for OkHttpClient. |  | Duration |
| **consulClient** (common) | Reference to a org.kiwiproject.consul.Consul in the registry. |  | Consul |
| **key** (common) | The default key. Can be overridden by CamelConsulKey. |  | String |
| **pingInstance** (common) | Configure if the AgentClient should attempt a ping before returning the Consul instance. | true | boolean |
| **readTimeout** (common) | Read timeout for OkHttpClient. |  | Duration |
| **tags** (common) | Set tags. You can separate multiple tags by comma. |  | String |
| **url** (common) | The Consul agent URL. |  | String |
| **writeTimeout** (common) | Write timeout for OkHttpClient. |  | Duration |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **action** (producer) | The default action. Can be overridden by CamelConsulAction. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **valueAsString** (producer) | Default to transform values retrieved from Consul i.e. on KV endpoint to string. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **configuration** (advanced) | Consul configuration. |  | ConsulConfiguration |
| **consistencyMode** (advanced) | 
The consistencyMode used for queries, default ConsistencyMode.DEFAULT.

Enum values:

-   DEFAULT
    
-   STALE
    
-   CONSISTENT
    





 | DEFAULT | ConsistencyMode |
| **datacenter** (advanced) | The data center. |  | String |
| **nearNode** (advanced) | The near node to use for queries. |  | String |
| **nodeMeta** (advanced) | The comma separated node meta-data to use for queries. |  | String |
| **aclToken** (security) | Sets the ACL token to be used with Consul. |  | String |
| **password** (security) | Sets the password to be used for basic authentication. |  | String |
| **sslContextParameters** (security) | SSL configuration using an org.apache.camel.support.jsse.SSLContextParameters instance. |  | SSLContextParameters |
| **useGlobalSslContextParameters** (security) | Enable usage of global SSL context parameters. | false | boolean |
| **userName** (security) | Sets the username to be used for basic authentication. |  | String |
| **blockSeconds** (watch) | The second to wait for a watch event, default 10 seconds. | 10 | Integer |
| **firstIndex** (watch) | The first index for watch for, default 0. | 0 | BigInteger |
| **recursive** (watch) | Recursively watch, default false. | false | boolean |

## Endpoint Options

The Consul endpoint is configured using URI syntax:

consul:apiEndpoint

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **apiEndpoint** (common) | **Required** The API endpoint. |  | String |

### Query Parameters (25 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **connectTimeout** (common) | Connect timeout for OkHttpClient. |  | Duration |
| **consulClient** (common) | Reference to a org.kiwiproject.consul.Consul in the registry. |  | Consul |
| **key** (common) | The default key. Can be overridden by CamelConsulKey. |  | String |
| **pingInstance** (common) | Configure if the AgentClient should attempt a ping before returning the Consul instance. | true | boolean |
| **readTimeout** (common) | Read timeout for OkHttpClient. |  | Duration |
| **tags** (common) | Set tags. You can separate multiple tags by comma. |  | String |
| **url** (common) | The Consul agent URL. |  | String |
| **writeTimeout** (common) | Write timeout for OkHttpClient. |  | Duration |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **action** (producer) | The default action. Can be overridden by CamelConsulAction. |  | String |
| **valueAsString** (producer) | Default to transform values retrieved from Consul i.e. on KV endpoint to string. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **consistencyMode** (advanced) | 

The consistencyMode used for queries, default ConsistencyMode.DEFAULT.

Enum values:

-   DEFAULT
    
-   STALE
    
-   CONSISTENT
    





 | DEFAULT | ConsistencyMode |
| **datacenter** (advanced) | The data center. |  | String |
| **nearNode** (advanced) | The near node to use for queries. |  | String |
| **nodeMeta** (advanced) | The comma separated node meta-data to use for queries. |  | String |
| **aclToken** (security) | Sets the ACL token to be used with Consul. |  | String |
| **password** (security) | Sets the password to be used for basic authentication. |  | String |
| **sslContextParameters** (security) | SSL configuration using an org.apache.camel.support.jsse.SSLContextParameters instance. |  | SSLContextParameters |
| **userName** (security) | Sets the username to be used for basic authentication. |  | String |
| **blockSeconds** (watch) | The second to wait for a watch event, default 10 seconds. | 10 | Integer |
| **firstIndex** (watch) | The first index for watch for, default 0. | 0 | BigInteger |
| **recursive** (watch) | Recursively watch, default false. | false | boolean |

## Message Headers

The Consul component supports 31 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelConsulAction** (producer) Constant: [`CONSUL_ACTION`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_ACTION) | The Producer action. |  | String |
| **CamelConsulKey** (common) Constant: [`CONSUL_KEY`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_KEY) | The Key on which the action should applied. |  | String |
| **CamelConsulEventId** (consumer) Constant: [`CONSUL_EVENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_EVENT_ID) | The event id. |  | String |
| **CamelConsulEventName** (consumer) Constant: [`CONSUL_EVENT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_EVENT_NAME) | The event name. |  | String |
| **CamelConsulEventLTime** (consumer) Constant: [`CONSUL_EVENT_LTIME`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_EVENT_LTIME) | The event LTime. |  | Long |
| **CamelConsulNodeFilter** (consumer) Constant: [`CONSUL_NODE_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_NODE_FILTER) | The Node filter. |  | String |
| **CamelConsulTagFilter** (consumer) Constant: [`CONSUL_TAG_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_TAG_FILTER) | The tag filter. |  | String |
| **CamelConsulSessionFilter** (consumer) Constant: [`CONSUL_SERVICE_FILTER`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_SERVICE_FILTER) | The session filter. |  | String |
| **CamelConsulVersion** (consumer) Constant: [`CONSUL_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_VERSION) | The data version. |  | Integer |
| **CamelConsulFlags** (common) Constant: [`CONSUL_FLAGS`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_FLAGS) | Flags associated with a value. |  | Long |
| **CamelConsulIndex** (producer) Constant: [`CONSUL_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_INDEX) | The optional value index. |  | BigInteger |
| **CamelConsulWait** (producer) Constant: [`CONSUL_WAIT`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_WAIT) | The optional value wait. |  | String |
| **CamelConsulCreateIndex** (consumer) Constant: [`CONSUL_CREATE_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_CREATE_INDEX) | The internal index value that represents when the entry was created. |  | Long |
| **CamelConsulLockIndex** (consumer) Constant: [`CONSUL_LOCK_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_LOCK_INDEX) | The number of times this key has successfully been acquired in a lock. |  | Long |
| **CamelConsulModifyIndex** (consumer) Constant: [`CONSUL_MODIFY_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_MODIFY_INDEX) | The last index that modified this key. |  | Long |
| **CamelConsulOptions** (common) Constant: [`CONSUL_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_OPTIONS) | Options associated to the request. |  |  |
| **CamelConsulResult** (common) Constant: [`CONSUL_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_RESULT) | true if the response has a result. |  | Boolean |
| **CamelConsulSession** (common) Constant: [`CONSUL_SESSION`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_SESSION) | The session id. |  | String |
| **CamelConsulValueAsString** (producer) Constant: [`CONSUL_VALUE_AS_STRING`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_VALUE_AS_STRING) | To transform values retrieved from Consul i.e. on KV endpoint to string. |  | Boolean |
| **CamelConsulNode** (producer) Constant: [`CONSUL_NODE`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_NODE) | The node. |  | String |
| **CamelConsulService** (producer) Constant: [`CONSUL_SERVICE`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_SERVICE) | The service. |  | String |
| **CamelConsulDatacenter** (producer) Constant: [`CONSUL_DATACENTER`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_DATACENTER) | The data center. |  | String |
| **CamelConsulNearNode** (producer) Constant: [`CONSUL_NEAR_NODE`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_NEAR_NODE) | The near node to use for queries. |  | String |
| **CamelConsulNodeMeta** (producer) Constant: [`CONSUL_NODE_META`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_NODE_META) | The note meta-data to use for queries. |  | List |
| **CamelConsulLastContact** (producer) Constant: [`CONSUL_LAST_CONTACT`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_LAST_CONTACT) | The last contact. |  | Long |
| **CamelConsulKnownLeader** (producer) Constant: [`CONSUL_KNOWN_LEADER`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_KNOWN_LEADER) | Indicates whether it is the known leader. |  | Boolean |
| **CamelConsulConsistencyMode** (producer) Constant: [`CONSUL_CONSISTENCY_MODE`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_CONSISTENCY_MODE) | The consistencyMode used for queries. | DEFAULT | ConsistencyMode |
| **CamelConsulHealthyOnly** (producer) Constant: [`CONSUL_HEALTHY_ONLY`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_HEALTHY_ONLY) | Only on healthy services. | false | Boolean |
| **CamelConsulHealthyState** (producer) Constant: [`CONSUL_HEALTHY_STATE`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_HEALTHY_STATE) | 
The state to query.

Enum values:

-   PASS
    
-   WARN
    
-   FAIL
    
-   ANY
    
-   UNKNOWN
    





 |  | State |
| **CamelConsulPreparedQueryID** (producer) Constant: [`CONSUL_PREPARED_QUERY_ID`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_PREPARED_QUERY_ID) | The id of the prepared query. |  | String |
| **CamelConsulServiceId** (producer) Constant: [`CONSUL_SERVICE_ID`](https://javadoc.io/doc/org.apache.camel/camel-consul/latest/org/apache/camel/component/consul/ConsulConstants.html#CONSUL_SERVICE_ID) | The service id for agent deregistration. |  | String |

## Usage

### Api Endpoint

The `apiEndpoint` denotes the type of [consul api](https://www.consul.io/api-docs) which should be addressed.

  
| Domain | Producer | Consumer |
| --- | --- | --- |
| kv | ConsulKeyValueProducer | ConsulKeyValueConsumer |
| event | ConsulEventProducer | ConsulEventConsumer |
| agent | ConsulAgentProducer | \- |
| coordinates | ConsulCoordinatesProducer | \- |
| health | ConsulHealthProducer | \- |
| status | ConsulStatusProducer | \- |
| preparedQuery | ConsulPreparedQueryProducer | \- |
| catalog | ConsulCatalogProducer | \- |
| session | ConsulSessionProducer | \- |

## Examples

### Producer Examples

As an example, we will show how to use the `ConsulAgentProducer` to register a service by means of the Consul agent api.

Registering and unregistering are examples for possible actions against the Consul agent api.

The desired action can be defined by setting the header `ConsulConstants.CONSUL_ACTION` to a value from the `ConsulXXXActions` interface of the respective Consul api. E.g. `ConsulAgentActions` contains the actions for the agent api.

If you set `CONSUL_ACTION` to `ConsulAgentActions.REGISTER`, the agent action `REGISTER` will be executed.

> **Tip**
> Which producer action invoked by which consul api is defined by the respective producer. E.g., the `ConsulAgentProducer` maps `ConsulAgentActions.REGISTER` to an invocation of `AgentClient.register`.

```java
from("direct:registerFooService")
    .setBody().constant(ImmutableRegistration.builder()
        .id("foo-1")
        .name("foo")
        .address("localhost")
        .port(80)
        .build())
    .setHeader(ConsulConstants.CONSUL_ACTION, constant(ConsulAgentActions.REGISTER))
    .to("consul:agent");
```

It is also possible to set a default action on the consul endpoint and do without the header:

consul:agent?action=REGISTER

## Registering Camel Routes with Consul

You can employ a `ServiceRegistrationRoutePolicy` to register Camel routes as services with Consul automatically.

```java
from("jetty:http://0.0.0.0:8080/service/endpoint").routeId("foo-1")
    .routeProperty(ServiceDefinition.SERVICE_META_ID, "foo-1")
    .routeProperty(ServiceDefinition.SERVICE_META_NAME, "foo")
    .routePolicy(new ServiceRegistrationRoutePolicy())
...
```

## Spring Boot Auto-Configuration

When using consul with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-consul-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 57 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.cloud.consul.acl-token** | Sets the ACL token to be used with Consul. |  | String |
| **camel.cloud.consul.attributes** | Custom service attributes. |  | Map |
| **camel.cloud.consul.block-seconds** | The time (in seconds) to wait for a watch event, default 10 seconds. | 10 | Integer |
| **camel.cloud.consul.connect-timeout** | Connect timeout for OkHttpClient. |  | Duration |
| **camel.cloud.consul.consistency-mode** | The consistencyMode used for queries, default ConsistencyMode.DEFAULT. | default | ConsistencyMode |
| **camel.cloud.consul.datacenter** | The data center. |  | String |
| **camel.cloud.consul.enabled** | Sets if the consul service registry should be enabled or not, default is false. | false | Boolean |
| **camel.cloud.consul.first-index** | The first index for watch for, default 0. | 0 | BigInteger |
| **camel.cloud.consul.id** | Service Registry ID. |  | String |
| **camel.cloud.consul.near-node** | The near node to use for queries. |  | String |
| **camel.cloud.consul.node-meta** | The note meta-data to use for queries. |  | String |
| **camel.cloud.consul.node-metas-as-list** |  |  | Collection |
| **camel.cloud.consul.order** | Service lookup order/priority. |  | Integer |
| **camel.cloud.consul.password** | Sets the password to be used for basic authentication. |  | String |
| **camel.cloud.consul.ping-instance** | Configure if the AgentClient should attempt a ping before returning the Consul instance. | true | Boolean |
| **camel.cloud.consul.read-timeout** | Read timeout for OkHttpClient. |  | Duration |
| **camel.cloud.consul.recursive** | Recursively watch, default false. | false | Boolean |
| **camel.cloud.consul.ssl-context-parameters** | SSL configuration using an org.apache.camel.support.jsse.SSLContextParameters instance. |  | SSLContextParameters |
| **camel.cloud.consul.tag-as-set** |  |  | Collection |
| **camel.cloud.consul.tags** | Set tags. You can separate multiple tags by comma. |  | String |
| **camel.cloud.consul.url** | The Consul agent URL. |  | String |
| **camel.cloud.consul.user-name** | Sets the username to be used for basic authentication. |  | String |
| **camel.cloud.consul.write-timeout** | Write timeout for OkHttpClient. |  | Duration |
| **camel.component.consul.acl-token** | Sets the ACL token to be used with Consul. |  | String |
| **camel.component.consul.action** | The default action. Can be overridden by CamelConsulAction. |  | String |
| **camel.component.consul.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.consul.block-seconds** | The second to wait for a watch event, default 10 seconds. | 10 | Integer |
| **camel.component.consul.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.consul.configuration** | Consul configuration. The option is a org.apache.camel.component.consul.ConsulConfiguration type. |  | ConsulConfiguration |
| **camel.component.consul.connect-timeout** | Connect timeout for OkHttpClient. |  | Duration |
| **camel.component.consul.consistency-mode** | The consistencyMode used for queries, default ConsistencyMode.DEFAULT. | default | ConsistencyMode |
| **camel.component.consul.consul-client** | Reference to a org.kiwiproject.consul.Consul in the registry. The option is a org.kiwiproject.consul.Consul type. |  | Consul |
| **camel.component.consul.datacenter** | The data center. |  | String |
| **camel.component.consul.enabled** | Whether to enable auto configuration of the consul component. This is enabled by default. |  | Boolean |
| **camel.component.consul.first-index** | The first index for watch for, default 0. The option is a java.math.BigInteger type. |  | BigInteger |
| **camel.component.consul.key** | The default key. Can be overridden by CamelConsulKey. |  | String |
| **camel.component.consul.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.consul.near-node** | The near node to use for queries. |  | String |
| **camel.component.consul.node-meta** | The comma separated node meta-data to use for queries. |  | String |
| **camel.component.consul.password** | Sets the password to be used for basic authentication. |  | String |
| **camel.component.consul.ping-instance** | Configure if the AgentClient should attempt a ping before returning the Consul instance. | true | Boolean |
| **camel.component.consul.read-timeout** | Read timeout for OkHttpClient. |  | Duration |
| **camel.component.consul.recursive** | Recursively watch, default false. | false | Boolean |
| **camel.component.consul.ssl-context-parameters** | SSL configuration using an org.apache.camel.support.jsse.SSLContextParameters instance. The option is a org.apache.camel.support.jsse.SSLContextParameters type. |  | SSLContextParameters |
| **camel.component.consul.tags** | Set tags. You can separate multiple tags by comma. |  | String |
| **camel.component.consul.url** | The Consul agent URL. |  | String |
| **camel.component.consul.use-global-ssl-context-parameters** | Enable usage of global SSL context parameters. | false | Boolean |
| **camel.component.consul.user-name** | Sets the username to be used for basic authentication. |  | String |
| **camel.component.consul.value-as-string** | Default to transform values retrieved from Consul i.e. on KV endpoint to string. | false | Boolean |
| **camel.component.consul.write-timeout** | Write timeout for OkHttpClient. |  | Duration |
| **camel.cloud.consul.check-interval** | **Deprecated** How often (in seconds) a service has to be marked as healthy if its check is TTL or how often the check should run. Default is 5 seconds. | 5 | Integer |
| **camel.cloud.consul.check-ttl** | **Deprecated** The time (in seconds) to live for TTL checks. Default is 1 minute. | 60 | Integer |
| **camel.cloud.consul.dc** | **Deprecated** Use datacenter instead. |  | String |
| **camel.cloud.consul.deregister-after** | **Deprecated** How long (in seconds) to wait to deregister a service in case of unclean shutdown. Default is 1 hour. | 3600 | Integer |
| **camel.cloud.consul.deregister-services-on-stop** | **Deprecated** Should we remove all the registered services know by this registry on stop?. | true | Boolean |
| **camel.cloud.consul.override-service-host** | **Deprecated** Should we override the service host if given ?. | true | Boolean |
| **camel.cloud.consul.service-host** | **Deprecated** Service host. |  | String |