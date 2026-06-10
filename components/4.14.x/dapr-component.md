# Dapr

**Since Camel 4.12**

**Both producer and consumer are supported**

The Dapr Component provides support for interacting with the [Dapr Building Blocks](https://docs.dapr.io/developing-applications/building-blocks/).

## URI format

dapr:operation\[?options\]

Where **operation** indicates the specific Dapr building block to interact with.

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

The Dapr component supports 24 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configKeys** (common) | List of keys for configuration operation. |  | String |
| **configStore** (common) | The name of the Dapr configuration store to interact with, defined in statestore.yaml config. |  | String |
| **configuration** (common) | The component configurations. |  | DaprConfiguration |
| **contentType** (common) | The contentType for the Pub/Sub component to use. |  | String |
| **pubSubName** (common) | The name of the Dapr Pub/Sub component to use. This identifies which underlying messaging system Dapr will interact with for publishing or subscribing to events. |  | String |
| **topic** (common) | The name of the topic to subscribe to. The topic must exist in the Pub/Sub component configured under the given pubsubName. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **previewClient** (consumer) | **Autowired** The client to consume messages by the consumer. |  | DaprPreviewClient |
| **bindingName** (producer) | The name of the Dapr binding to invoke. |  | String |
| **bindingOperation** (producer) | The operation to perform on the binding. |  | String |
| **concurrency** (producer) | 
Concurrency mode to use with state operations.

Enum values:

-   FIRST\_WRITE
    
-   LAST\_WRITE
    





 |  | Concurrency |
| **consistency** (producer) | 

Consistency level to use with state operations.

Enum values:

-   EVENTUAL
    
-   STRONG
    





 |  | Consistency |
| **eTag** (producer) | The eTag for optimistic concurrency during state save or delete operations. |  | String |
| **httpExtension** (producer) | **Autowired** HTTP method to use when invoking the service. Accepts verbs like GET, POST, PUT, DELETE, etc. Creates a minimal HttpExtension with no headers or query params. Takes precedence over verb. |  | HttpExtension |
| **key** (producer) | The key used to identify the state/secret object within the specified state/secret store. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **methodToInvoke** (producer) | The name of the method or route to invoke on the target service. |  | String |
| **secretStore** (producer) | The name of the Dapr secret store to interact with, defined in local-secret-store.yaml config. |  | String |
| **serviceToInvoke** (producer) | Target service to invoke. Can be a Dapr App ID, a named HTTPEndpoint, or a FQDN/public URL. |  | String |
| **stateOperation** (producer) | 

The state operation to perform on the state store. Required for DaprOperation.state operation.

Enum values:

-   save
    
-   saveBulk
    
-   get
    
-   getBulk
    
-   delete
    
-   executeTransaction
    





 | get | StateOperation |
| **stateStore** (producer) | The name of the Dapr state store to interact with, defined in statestore.yaml config. |  | String |
| **verb** (producer) | The HTTP verb to use for invoking the method. | POST | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Endpoint Options

The Dapr endpoint is configured using URI syntax:

dapr:operation

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The Dapr building block operation to perform with this component.

Enum values:

-   invokeService
    
-   state
    





 |  | DaprOperation |

### Query Parameters (24 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configKeys** (common) | List of keys for configuration operation. |  | String |
| **configStore** (common) | The name of the Dapr configuration store to interact with, defined in statestore.yaml config. |  | String |
| **contentType** (common) | The contentType for the Pub/Sub component to use. |  | String |
| **pubSubName** (common) | The name of the Dapr Pub/Sub component to use. This identifies which underlying messaging system Dapr will interact with for publishing or subscribing to events. |  | String |
| **topic** (common) | The name of the topic to subscribe to. The topic must exist in the Pub/Sub component configured under the given pubsubName. |  | String |
| **previewClient** (consumer) | **Autowired** The client to consume messages by the consumer. |  | DaprPreviewClient |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **bindingName** (producer) | The name of the Dapr binding to invoke. |  | String |
| **bindingOperation** (producer) | The operation to perform on the binding. |  | String |
| **concurrency** (producer) | 

Concurrency mode to use with state operations.

Enum values:

-   FIRST\_WRITE
    
-   LAST\_WRITE
    





 |  | Concurrency |
| **consistency** (producer) | 

Consistency level to use with state operations.

Enum values:

-   EVENTUAL
    
-   STRONG
    





 |  | Consistency |
| **eTag** (producer) | The eTag for optimistic concurrency during state save or delete operations. |  | String |
| **httpExtension** (producer) | **Autowired** HTTP method to use when invoking the service. Accepts verbs like GET, POST, PUT, DELETE, etc. Creates a minimal HttpExtension with no headers or query params. Takes precedence over verb. |  | HttpExtension |
| **key** (producer) | The key used to identify the state/secret object within the specified state/secret store. |  | String |
| **methodToInvoke** (producer) | The name of the method or route to invoke on the target service. |  | String |
| **secretStore** (producer) | The name of the Dapr secret store to interact with, defined in local-secret-store.yaml config. |  | String |
| **serviceToInvoke** (producer) | Target service to invoke. Can be a Dapr App ID, a named HTTPEndpoint, or a FQDN/public URL. |  | String |
| **stateOperation** (producer) | 

The state operation to perform on the state store. Required for DaprOperation.state operation.

Enum values:

-   save
    
-   saveBulk
    
-   get
    
-   getBulk
    
-   delete
    
-   executeTransaction
    





 | get | StateOperation |
| **stateStore** (producer) | The name of the Dapr state store to interact with, defined in statestore.yaml config. |  | String |
| **verb** (producer) | The HTTP verb to use for invoking the method. | POST | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Message Headers

The Dapr component supports 35 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDaprServiceToInvoke** (producer) Constant: [`SERVICE_TO_INVOKE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#SERVICE_TO_INVOKE) | Target service to invoke. Can be a Dapr App ID, a named HTTPEndpoint, or a FQDN/public URL. |  | String |
| **CamelDaprMethodToInvoke** (producer) Constant: [`METHOD_TO_INVOKE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#METHOD_TO_INVOKE) | The name of the method or route to invoke on the target service. |  | String |
| **CamelDaprVerb** (producer) Constant: [`VERB`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#VERB) | The HTTP verb to use for service invocation. |  | String |
| **CamelDaprQueryParameters** (producer) Constant: [`QUERY_PARAMETERS`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#QUERY_PARAMETERS) | The query parameters for HTTP requests. |  | Map |
| **CamelDaprHttpHeaders** (producer) Constant: [`HTTP_HEADERS`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#HTTP_HEADERS) | The headers for HTTP requests. |  | Map |
| **CamelDaprHttpExtension** (producer) Constant: [`HTTP_EXTENSION`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#HTTP_EXTENSION) | The HttpExtension object for service invocation. Takes precedence over verb. |  | HttpExtension |
| **CamelDaprStateOperation** (producer) Constant: [`STATE_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#STATE_OPERATION) | The state operation to perform on the state store. Required for DaprOperation.state operation. | get | StateOperation |
| **CamelDaprStateStore** (producer) Constant: [`STATE_STORE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#STATE_STORE) | The name of the Dapr state store to interact with, defined in statestore.yaml config. |  | String |
| **CamelDaprSecretStore** (producer) Constant: [`SECRET_STORE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#SECRET_STORE) | The name of the Dapr secret store to interact with, defined in local-secret-store.yaml config. |  | String |
| **CamelDaprConfigStore** (producer) Constant: [`CONFIG_STORE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#CONFIG_STORE) | The name of the Dapr config store to interact with, defined in statestore.yaml config. |  | String |
| **CamelDaprKey** (producer) Constant: [`KEY`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#KEY) | The key used to identify the state/secret object within the specified state/secret store. |  | String |
| **CamelDaprETag** (producer) Constant: [`E_TAG`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#E_TAG) | The eTag for optimistic concurrency during state save or delete operations. |  | String |
| **CamelDaprConcurrency** (producer) Constant: [`CONCURRENCY`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#CONCURRENCY) | 
Concurrency mode to use with state operations.

Enum values:

-   FIRST\_WRITE
    
-   LAST\_WRITE
    





 |  | Concurrency |
| **CamelDaprConsistency** (producer) Constant: [`CONSISTENCY`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#CONSISTENCY) | 

Consistency level to use with state operations.

Enum values:

-   EVENTUAL
    
-   STRONG
    





 |  | Consistency |
| **CamelDaprMetadata** (producer) Constant: [`METADATA`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#METADATA) | Additional key-value pairs to be passed to the state store. |  | Map |
| **CamelDaprStates** (producer) Constant: [`STATES`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#STATES) | List of states for bulk save operation. |  | List |
| **CamelDaprKeys** (producer) Constant: [`KEYS`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#KEYS) | List of keys for bulk get operation. |  | List |
| **CamelDaprTransactions** (producer) Constant: [`TRANSACTIONS`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#TRANSACTIONS) | List of transactions for execute transactions state operations. |  | List |
| **CamelDaprPubSubName** (common) Constant: [`PUBSUB_NAME`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#PUBSUB_NAME) | The name of the Dapr Pub/Sub component to use. This identifies which underlying messaging system Dapr will interact with for publishing or subscribing to events. |  | String |
| **CamelDaprTopic** (common) Constant: [`TOPIC`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#TOPIC) | The name of the topic to subscribe to. The topic must exist in the Pub/Sub component configured under the given pubsubName. |  | String |
| **CamelDaprContentType** (common) Constant: [`CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#CONTENT_TYPE) | The content type for the Pub/Sub component to use. |  | String |
| **CamelDaprID** (consumer) Constant: [`ID`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#ID) | Gets the unique identifier for the event, used to distinguish it from other events. |  | String |
| **CamelDaprSource** (consumer) Constant: [`SOURCE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#SOURCE) | Gets the origin of the event, typically a URI indicating the component or service that generated the event. |  | String |
| **CamelDaprType** (consumer) Constant: [`TYPE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#TYPE) | Gets the string indicating the type of cloud event. |  | String |
| **CamelDaprSpecificVersion** (consumer) Constant: [`SPECIFIC_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#SPECIFIC_VERSION) | Gets the version of the CloudEvents specification that the event conforms to. |  | String |
| **CamelDaprDataContentType** (consumer) Constant: [`DATA_CONTENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#DATA_CONTENT_TYPE) | Gets the content type of the event data. |  | String |
| **CamelDaprBinaryData** (consumer) Constant: [`BINARY_DATA`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#BINARY_DATA) | Gets the raw binary data payload of the event, if present (for events where data\_base64 is used instead of data). |  | byte\[\] |
| **CamelDaprTime** (consumer) Constant: [`TIME`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#TIME) | Gets the timestamp of when the event occurred. |  | OffsetDateTime |
| **CamelDaprTraceParent** (consumer) Constant: [`TRACE_PARENT`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#TRACE_PARENT) | Gets tracing info for following the event across services (includes trace ID and span ID). |  | String |
| **CamelDaprTraceState** (consumer) Constant: [`TRACE_STATE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#TRACE_STATE) | Gets additional vendor-specific trace context. |  | String |
| **CamelDaprBindingName** (producer) Constant: [`BINDING_NAME`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#BINDING_NAME) | The name of the Dapr binding to invoke. |  | String |
| **CamelDaprBindingOperation** (producer) Constant: [`BINDING_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#BINDING_OPERATION) | The operation to perform on the binding. |  | String |
| **CamelDaprConfigKeys** (producer) Constant: [`CONFIG_KEYS`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#CONFIG_KEYS) | List of keys for configuration operation. |  | String |
| **CamelDaprSubscriptionId** (consumer) Constant: [`SUBSCRIPTION_ID`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#SUBSCRIPTION_ID) | The id for configuration change subscription. |  | String |
| **CamelDaprRawConfigResponse** (common) Constant: [`RAW_CONFIG_RESPONSE`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#RAW_CONFIG_RESPONSE) | The raw configuration update response. |  | ConfigurationItem |

### Dapr Producer operations

Camel Dapr component provides a wide range of operations on the producer side:

### 1\. **invokeService**:

Using service invocation, your application can reliably and securely communicate with other applications using the standard HTTP protocol. For this operation `serviceToInvoke` and `methodToInvoke` are mandatory.

### 2\. **state**:

State management in Dapr allows your application to save, get and delete key-value pairs in a reliable and consistent way. For these operations `stateStore` is required.

#### State Operations

 
| Operation | Description |
| --- | --- |
| `save` | Store or update a single key-value pair in the state store. For this operation `payload` and `key` are required. |
| `saveBulk` | Store or update multiple key-value pairs in the state store in a single operation. For this operation (List<State<?>>) `states` is a required field. |
| `get` | Retrieve the value of a specific key from the state store. For this operation `key` is a required field. |
| `getBulk` | Retrieve values for multiple keys from the state store in a single request. For this operation (List<String>) `keys` is a required field. |
| `delete` | Remove a specific key and its associated value from the state store. For this operation `key` is a required field. |
| `executeTransaction` | Execute a batch of operations (save or delete) atomically within a transaction. For this operation (List<TransactionalStateOperation<?>>) `transactions` is a required field. |

### 2\. **pubSub**:

Dapr’s publish-subscribe (Pub/Sub) building block enables asynchronous, event-driven communication between microservices. For this operation, the pubSubName and topic are required.

### 3\. **invokeBinding**:

Dapr’s bindings building block allows interaction with external systems via input/output bindings. The invokeBinding operation enables sending data to a configured output binding. This operation requires specifying the bindingName (the name of the binding component) and the bindingOperation (such as create, get, or delete, depending on the binding’s capabilities).

### 4\. **secret**:

Dapr’s secret management building block enables secure retrieval of secrets from external secret stores. The secret operation fetches a secret from the specified secret store. If a key is provided, the operation retrieves the corresponding secret; if no key is specified, a bulk retrieval of all secrets from the store is performed. This operation requires the secretStore name, and optionally the key.

### 5\. **configuration**:

Dapr’s configuration building block allows applications to retrieve dynamic configuration values from external configuration stores. The configuration operation fetches values associated with keys specified in configKeys. This operation requires the configStore name, and the configKeys.

### Dapr Consumer operations

### 1\. **pubSub**:

The Dapr PubSub Consumer in Apache Camel allows your route to consume events from a Dapr-supported Pub/Sub system. It subscribes to a specified topic on a given pubsub component (pubSubName) and processes incoming CloudEvents as Camel Exchange objects.

To configure a consumer, the pubSubName and topic must be provided. Alternatively, a preconfigured DaprPreviewClient can be registered in the Camel registry to allow the consumer to reuse it instead of creating a new one internally.

### 2\. **configuration**:

The Dapr Configuration Consumer in Apache Camel allows your route to receive real-time updates from a Dapr-supported configuration store. It listens for changes to specified keys in the configuration store and processes the updates as Camel Exchange objects.

To configure the consumer, the configStore name and configKeys must be provided.

## Examples

### Producer Operations Examples

-   `invokeService` -
    

```java
from("direct:start")
  .process(exchange -> {
    // set the header you want the producer to evaluate, refer to the previous
    // section to learn about the headers that can be set
    // e.g.:
    exchange.getIn().setHeader(DaprConstants.VERB, "GET");
  })
  .to("dapr:invokeService?serviceToInvoke=myService&methodToInvoke=myMethod")
  .to("mock:result");
```

-   `state: save` -
    

```java
from("direct:start")
  .process(exchange -> {
    // set the payload you want to save as state
    exchange.getIn().setBody("myValue");
  })
  .to("dapr:state?stateOperation=save&stateStore=myStore&key=myKey")
  .to("mock:result");
```

-   `state: saveBulk` -
    

```java
from("direct:start")
  .process(exchange -> {
    // set the list of states you want to save
    State<String> state1 = new State<>("key1", "val1", "etag1");
    State<String> state2 = new State<>("key2", "val1", "etag2");
    List<State<?>> states = List.of(state1, state2);
    exchange.getMessage().setHeader(DaprConstants.STATES, states);
  })
  .to("dapr:state?stateOperation=saveBulk&stateStore=myStore")
  .to("mock:result");
```

-   `state: get` -
    

```java
from("direct:start")
  .process(exchange -> {
    // set the header you want the producer to evaluate, refer to the previous
    // section to learn about the headers that can be set
    // e.g.:
    exchange.getIn().setHeader(DaprConstants.CONCURRENCY, "FIRST_WRITE");
    exchange.getIn().setHeader(DaprConstants.CONSISTENCY, "EVENTUAL");
  })
  .to("dapr:state?stateOperation=get&stateStore=myStore&key=myKey")
  .to("mock:result");
```

-   `state: getBulk` -
    

```java
from("direct:start")
  .process(exchange -> {
    // set the header you want the producer to evaluate, refer to the previous
    // section to learn about the headers that can be set
    // e.g.:
    exchange.getIn().setHeader(DaprConstants.KEYS, List.of("key1", "key2"));
  })
  .to("dapr:state?stateOperation=getBulk&stateStore=myStore")
  .to("mock:result");
```

-   `state: delete` -
    

```java
from("direct:start")
  .process(exchange -> {
    // set the header you want the producer to evaluate, refer to the previous
    // section to learn about the headers that can be set
    // e.g.:
    exchange.getIn().setHeader(DaprConstants.METADATA, Map.of("partitionKey", "myPartitionKey"));
  })
  .to("dapr:state?stateOperation=delete&stateStore=myStore&key=myKey")
  .to("mock:result");
```

-   `state: executeTransaction` -
    

```java
from("direct:start")
  .process(exchange -> {
    // set the header you want the producer to evaluate, refer to the previous
    // section to learn about the headers that can be set
    // e.g.:
    TransactionalStateOperation.OperationType op = TransactionalStateOperation.OperationType.UPSERT;
    List<TransactionalStateOperation<?>> transactions = List.of(new TransactionalStateOperation<>(op, new State<>("myKey")));
    exchange.getIn().setHeader(DaprConstants.TRANSACTIONS, transactions);
  })
  .to("dapr:state?stateOperation=executeTransaction&stateStore=myStore")
  .to("mock:result");
```

-   `pubSub` -
    

```java
from("direct:start")
  .process(exchange -> {
    // set the header you want the producer to evaluate, refer to the previous
    // section to learn about the headers that can be set
    // e.g.:
    exchange.getIn().setHeader(DaprConstants.CONTENT_TYPE, "application/json");
  })
  .to("dapr:pubSub?pubSubName=myPubSub&topic=myTopic")
  .to("mock:result");
```

-   `invokeBinding` -
    

```java
from("direct:start")
  .process(exchange -> {
    // set the message body to the payload to send to the output binding
    // e.g.:
    exchange.getMessage().setBody("myBody");
  })
  .to("dapr:invokeBinding?bindingName=myBinding&bindingOperation=myOperation")
  .to("mock:result");
```

-   `secret` -
    

```java
from("direct:start")
  .to("dapr:secret?secretStore=myStore&key=mySecret")
  .log("Received secret from Dapr: ${body}")
  .to("mock:result");
```

-   `secret: bulk` -
    

```java
from("direct:start")
  // when no secret key is passed, bulk retrieval is performed on secret store
  .to("dapr:secret?secretStore=myStore")
  .log("Received bulk secrets from Dapr: ${body}")
  .to("mock:result");
```

-   `configuration` -
    

```java
from("direct:start")
  .process(exchange -> {
    // set the header you want the producer to evaluate, refer to the previous
    // section to learn about the headers that can be set
    // e.g.:
    exchange.getIn().setHeader(DaprConstants.CONFIG_KEYS, List.of("k1", "k2"));
  })
  .to("dapr:configuration?configStore=myStore")
  .log("Received config updates from Dapr: ${body}")
  .to("mock:result");
```

### Consumer Operations Examples

-   `pubSub` -
    

```java
from("dapr:pubSub?pubSubName=myPubSub&topic=myTopic")
  .log("Received message from Dapr pubsub: ${body}")
  .to("mock:result");
```

-   `configuration` -
    

```java
from("dapr:configuration?configStore=myStore&configKeys=k1,k2")
  .log("Received config updates from Dapr: ${body}")
  .to("mock:result");
```

## Spring Boot Auto-Configuration

When using dapr with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-dapr-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 24 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.dapr.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.dapr.binding-name** | The name of the Dapr binding to invoke. |  | String |
| **camel.component.dapr.binding-operation** | The operation to perform on the binding. |  | String |
| **camel.component.dapr.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.dapr.concurrency** | Concurrency mode to use with state operations. |  | StateOptions$Concurrency |
| **camel.component.dapr.config-keys** | List of keys for configuration operation. |  | String |
| **camel.component.dapr.config-store** | The name of the Dapr configuration store to interact with, defined in statestore.yaml config. |  | String |
| **camel.component.dapr.configuration** | The component configurations. The option is a org.apache.camel.component.dapr.DaprConfiguration type. |  | DaprConfiguration |
| **camel.component.dapr.consistency** | Consistency level to use with state operations. |  | StateOptions$Consistency |
| **camel.component.dapr.content-type** | The contentType for the Pub/Sub component to use. |  | String |
| **camel.component.dapr.e-tag** | The eTag for optimistic concurrency during state save or delete operations. |  | String |
| **camel.component.dapr.enabled** | Whether to enable auto configuration of the dapr component. This is enabled by default. |  | Boolean |
| **camel.component.dapr.http-extension** | HTTP method to use when invoking the service. Accepts verbs like GET, POST, PUT, DELETE, etc. Creates a minimal HttpExtension with no headers or query params. Takes precedence over verb. The option is a io.dapr.client.domain.HttpExtension type. |  | HttpExtension |
| **camel.component.dapr.key** | The key used to identify the state/secret object within the specified state/secret store. |  | String |
| **camel.component.dapr.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.dapr.method-to-invoke** | The name of the method or route to invoke on the target service. |  | String |
| **camel.component.dapr.preview-client** | The client to consume messages by the consumer. The option is a io.dapr.client.DaprPreviewClient type. |  | DaprPreviewClient |
| **camel.component.dapr.pub-sub-name** | The name of the Dapr Pub/Sub component to use. This identifies which underlying messaging system Dapr will interact with for publishing or subscribing to events. |  | String |
| **camel.component.dapr.secret-store** | The name of the Dapr secret store to interact with, defined in local-secret-store.yaml config. |  | String |
| **camel.component.dapr.service-to-invoke** | Target service to invoke. Can be a Dapr App ID, a named HTTPEndpoint, or a FQDN/public URL. |  | String |
| **camel.component.dapr.state-operation** | The state operation to perform on the state store. Required for DaprOperation.state operation. | get | StateOperation |
| **camel.component.dapr.state-store** | The name of the Dapr state store to interact with, defined in statestore.yaml config. |  | String |
| **camel.component.dapr.topic** | The name of the topic to subscribe to. The topic must exist in the Pub/Sub component configured under the given pubsubName. |  | String |
| **camel.component.dapr.verb** | The HTTP verb to use for invoking the method. | POST | String |