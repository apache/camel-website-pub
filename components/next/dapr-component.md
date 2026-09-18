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

The Dapr component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **client** (common) | **Autowired** The Dapr Client. |  | DaprClient |
| **configKeys** (common) | List of keys for configuration operation. |  | String |
| **configStore** (common) | The name of the Dapr configuration store to interact with, defined in statestore.yaml config. |  | String |
| **configuration** (common) | The component configurations. |  | DaprConfiguration |
| **contentType** (common) | The contentType for the Pub/Sub component to use. |  | String |
| **previewClient** (common) | **Autowired** The Dapr Preview Client. |  | DaprPreviewClient |
| **pubSubName** (common) | The name of the Dapr Pub/Sub component to use. This identifies which underlying messaging system Dapr will interact with for publishing or subscribing to events. |  | String |
| **topic** (common) | The name of the topic to subscribe to. The topic must exist in the Pub/Sub component configured under the given pubsubName. |  | String |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
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
| **eventName** (producer) | The name of the event. Event names are case-insensitive. |  | String |
| **expiryInSeconds** (producer) | The expiry time in seconds for the lock. |  | Integer |
| **getWorkflowIO** (producer) | Set true to fetch the workflow instance’s inputs, outputs, and custom status, or false to omit. | false | boolean |
| **httpExtension** (producer) | **Autowired** HTTP method to use when invoking the service. Accepts verbs like GET, POST, PUT, DELETE, etc. Creates a minimal HttpExtension with no headers or query params. Takes precedence over verb. |  | HttpExtension |
| **key** (producer) | The key used to identify the state/secret object within the specified state/secret store. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **lockOperation** (producer) | 

The lock operation to perform on the store. Required for DaprOperation.lock operation.

Enum values:

-   tryLock
    
-   unlock
    





 | tryLock | LockOperation |
| **lockOwner** (producer) | The lock owner identifier for the lock. |  | String |
| **methodToInvoke** (producer) | The name of the method or route to invoke on the target service. |  | String |
| **reason** (producer) | Reason for suspending/resuming the workflow instance. |  | String |
| **resourceId** (producer) | The resource Id for the lock. |  | String |
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
| **storeName** (producer) | The lock store name. |  | String |
| **timeout** (producer) | The amount of time to wait for the workflow instance to start/complete. |  | Duration |
| **verb** (producer) | The HTTP verb to use for invoking the method. | POST | String |
| **workflowClass** (producer) | The FQCN of the class which implements io.dapr.workflows.Workflow. |  | String |
| **workflowClient** (producer) | **Autowired** The Dapr Workflow Client. |  | DaprWorkflowClient |
| **workflowInstanceId** (producer) | The instance ID of the workflow. |  | String |
| **workflowOperation** (producer) | 

The workflow operation to perform. Required for DaprOperation.workflow operation.

Enum values:

-   scheduleNew
    
-   terminate
    
-   purge
    
-   suspend
    
-   resume
    
-   state
    
-   waitForInstanceStart
    
-   waitForInstanceCompletion
    
-   raiseEvent
    





 | scheduleNew | WorkflowOperation |
| **workflowStartTime** (producer) | The start time of the new workflow. |  | Instant |
| **workflowVersion** (producer) | The version of the workflow to start. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Endpoint Options

The Dapr endpoint is configured using URI syntax:

dapr:operation

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operation** (producer) | 
**Required** The Dapr building block operation to perform with this component.

Enum values:

-   invokeService
    
-   state
    
-   pubSub
    
-   invokeBinding
    
-   secret
    
-   configuration
    
-   lock
    
-   workflow
    





 |  | DaprOperation |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **client** (common) | **Autowired** The Dapr Client. |  | DaprClient |
| **configKeys** (common) | List of keys for configuration operation. |  | String |
| **configStore** (common) | The name of the Dapr configuration store to interact with, defined in statestore.yaml config. |  | String |
| **contentType** (common) | The contentType for the Pub/Sub component to use. |  | String |
| **previewClient** (common) | **Autowired** The Dapr Preview Client. |  | DaprPreviewClient |
| **pubSubName** (common) | The name of the Dapr Pub/Sub component to use. This identifies which underlying messaging system Dapr will interact with for publishing or subscribing to events. |  | String |
| **topic** (common) | The name of the topic to subscribe to. The topic must exist in the Pub/Sub component configured under the given pubsubName. |  | String |
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
| **eventName** (producer) | The name of the event. Event names are case-insensitive. |  | String |
| **expiryInSeconds** (producer) | The expiry time in seconds for the lock. |  | Integer |
| **getWorkflowIO** (producer) | Set true to fetch the workflow instance’s inputs, outputs, and custom status, or false to omit. | false | boolean |
| **httpExtension** (producer) | **Autowired** HTTP method to use when invoking the service. Accepts verbs like GET, POST, PUT, DELETE, etc. Creates a minimal HttpExtension with no headers or query params. Takes precedence over verb. |  | HttpExtension |
| **key** (producer) | The key used to identify the state/secret object within the specified state/secret store. |  | String |
| **lockOperation** (producer) | 

The lock operation to perform on the store. Required for DaprOperation.lock operation.

Enum values:

-   tryLock
    
-   unlock
    





 | tryLock | LockOperation |
| **lockOwner** (producer) | The lock owner identifier for the lock. |  | String |
| **methodToInvoke** (producer) | The name of the method or route to invoke on the target service. |  | String |
| **reason** (producer) | Reason for suspending/resuming the workflow instance. |  | String |
| **resourceId** (producer) | The resource Id for the lock. |  | String |
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
| **storeName** (producer) | The lock store name. |  | String |
| **timeout** (producer) | The amount of time to wait for the workflow instance to start/complete. |  | Duration |
| **verb** (producer) | The HTTP verb to use for invoking the method. | POST | String |
| **workflowClass** (producer) | The FQCN of the class which implements io.dapr.workflows.Workflow. |  | String |
| **workflowClient** (producer) | **Autowired** The Dapr Workflow Client. |  | DaprWorkflowClient |
| **workflowInstanceId** (producer) | The instance ID of the workflow. |  | String |
| **workflowOperation** (producer) | 

The workflow operation to perform. Required for DaprOperation.workflow operation.

Enum values:

-   scheduleNew
    
-   terminate
    
-   purge
    
-   suspend
    
-   resume
    
-   state
    
-   waitForInstanceStart
    
-   waitForInstanceCompletion
    
-   raiseEvent
    





 | scheduleNew | WorkflowOperation |
| **workflowStartTime** (producer) | The start time of the new workflow. |  | Instant |
| **workflowVersion** (producer) | The version of the workflow to start. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **headerFilterStrategy** (advanced) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Message Headers

The Dapr component supports the following message header(s), which is/are listed below:

   
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
| **CamelDaprLockOperation** (producer) Constant: [`LOCK_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#LOCK_OPERATION) | The lock operation to perform on the store. Required for DaprOperation.lock operation. | tryLock | LockOperation |
| **CamelDaprStoreName** (producer) Constant: [`STORE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#STORE_NAME) | The lock store name. |  | String |
| **CamelDaprResourceId** (producer) Constant: [`RESOURCE_ID`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#RESOURCE_ID) | The resource Id for the lock. |  | String |
| **CamelDaprLockOwner** (producer) Constant: [`LOCK_OWNER`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#LOCK_OWNER) | The lock owner identifier for the lock. |  | String |
| **CamelDaprExpiryInSeconds** (producer) Constant: [`EXPIRY_IN_SECONDS`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#EXPIRY_IN_SECONDS) | The expiry time in seconds for the lock. |  | Integer |
| **CamelDaprWorkflowOperation** (producer) Constant: [`WORKFLOW_OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_OPERATION) | The workflow operation to perform.Required for DaprOperation.workflow operation. | scheduleNew | WorkflowOperation |
| **CamelDaprWorkflowClass** (producer) Constant: [`WORKFLOW_CLASS`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_CLASS) | The FQCN of the class which implements io.dapr.workflows.Workflow. |  | String |
| **CamelDaprWorkflowVersion** (producer) Constant: [`WORKFLOW_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_VERSION) | The version of the workflow to start. |  | String |
| **CamelDaprWorkflowInstanceId** (producer) Constant: [`WORKFLOW_INSTANCE_ID`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_INSTANCE_ID) | The instance ID of the workflow. |  | String |
| **CamelDaprWorkflowStartTime** (producer) Constant: [`WORKFLOW_START_TIME`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_START_TIME) | The start time of the new workflow. |  | Instant |
| **CamelDaprSuspendReason** (producer) Constant: [`REASON`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#REASON) | Reason for suspending/resuming the workflow instance. |  | String |
| **CamelDaprNewWorkflowInstanceId** (producer) Constant: [`NEW_WORKFLOW_INSTANCE_ID`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#NEW_WORKFLOW_INSTANCE_ID) | The instance ID of the new scheduled workflow. |  | String |
| **CamelDaprGetWorkflowIO** (producer) Constant: [`GET_WORKFLOW_IO`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#GET_WORKFLOW_IO) | Set true to fetch the workflow instance’s inputs, outputs, and custom status, or false to omit. |  | boolean |
| **CamelDaprWorkflowName** (producer) Constant: [`WORKFLOW_NAME`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_NAME) | The workflow name. |  | String |
| **CamelDaprWorkflowCreatedAt** (producer) Constant: [`WORKFLOW_CREATED_AT`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_CREATED_AT) | Gets the workflow instance’s creation time in UTC. |  | Instant |
| **CamelDaprWorkflowUpdatedAt** (producer) Constant: [`WORKFLOW_UPDATED_AT`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_UPDATED_AT) | Gets the workflow instance’s last updated time in UTC. |  | Instant |
| **CamelDaprWorkflowSerializedInput** (producer) Constant: [`WORKFLOW_SERIALIZED_INPUT`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_SERIALIZED_INPUT) | Gets the workflow instance’s serialized input, if any. |  | String |
| **CamelDaprWorkflowSerializedOutput** (producer) Constant: [`WORKFLOW_SERIALIZED_OUTPUT`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_SERIALIZED_OUTPUT) | Gets the workflow instance’s serialized output, if any. |  | String |
| **CamelDaprWorkflowFailureDetails** (producer) Constant: [`WORKFLOW_FAILURE_DETAILS`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#WORKFLOW_FAILURE_DETAILS) | The failure details of the failed workflow instance or null. |  | WorkflowFailureDetails |
| **CamelDaprIsWorkflowRunning** (producer) Constant: [`IS_WORKFLOW_RUNNING`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#IS_WORKFLOW_RUNNING) | Set true if the workflow existed and was in a running state otherwise false. |  | boolean |
| **CamelDaprIsWorkflowCompleted** (producer) Constant: [`IS_WORKFLOW_COMPLETED`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#IS_WORKFLOW_COMPLETED) | Set true if the workflow was in a terminal state; otherwise false. |  | boolean |
| **CamelDaprTimeout** (producer) Constant: [`TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#TIMEOUT) | The amount of time to wait for the workflow instance to start/complete. |  | Duration |
| **CamelDaprEventName** (producer) Constant: [`EVENT_NAME`](https://javadoc.io/doc/org.apache.camel/camel-dapr/latest/org/apache/camel/component/dapr/DaprConstants.html#EVENT_NAME) | The name of the event. Event names are case-insensitive. |  | String |

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

### 6\. **lock**:

Lock management in Dapr allows your application to coordinate access to shared resources using a distributed lock mechanism. This is useful for ensuring mutual exclusion across services. For these operations, `storeName`, `resourceId` and `lockOwner` are mandatory.

#### Lock Operations

 
| Operation | Description |
| --- | --- |
| `tryLock` | Attempts to acquire a lock on a resource for a specific duration. For this operation `expiryInSeconds` is required. Returns a `Boolean` – `true` if the lock was successfully acquired, `false` otherwise. |
| `unlock` | Releases a previously acquired lock. Returns an `UnlockResponseStatus` enum indicating whether the lock was successfully released. |

### 7\. **workflow**:

Dapr Workflows enable developers to write long-running, persistent, and reliable processes as code. Dapr Workflow simplifies complex, stateful coordination requirements in microservice architectures.

#### Workflow Operations

 
| Operation | Description |
| --- | --- |
| `scheduleNew` | Schedules a new workflow instance to be created. Requires `workflowClass` and optional `workflowVersion`, `workflowInstanceId`, `workflowStartTime`. The message body is used as the workflow input. |
| `terminate` | Terminates a running workflow instance. Requires `workflowInstanceId`. The message body can be used to provide an output for the terminated workflow. |
| `purge` | Purges the metadata of a workflow instance from the state store. Requires `workflowInstanceId`. |
| `suspend` | Suspends a running workflow instance. Requires `workflowInstanceId` and a `reason`. |
| `resume` | Resumes a suspended workflow instance. Requires `workflowInstanceId` and a `reason`. |
| `state` | Gets the current runtime state of a workflow instance. Requires `workflowInstanceId`. |
| `waitForInstanceStart` | Waits for a workflow instance to start running. Requires `workflowInstanceId` and a `timeout`. |
| `waitForInstanceCompletion` | Waits for a workflow instance to complete. Requires `workflowInstanceId` and a `timeout`. |
| `raiseEvent` | Sends an event to a running workflow instance that is waiting for it. Requires `workflowInstanceId` and `eventName`. The message body is used as the event payload. |

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
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprVerb", constant("GET"))
    .to("dapr:invokeService?serviceToInvoke=myService&methodToInvoke=myMethod")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprVerb">
    <constant>GET</constant>
  </setHeader>
  <to uri="dapr:invokeService?serviceToInvoke=myService&amp;methodToInvoke=myMethod"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprVerb
            constant: "GET"
        - to:
            uri: dapr:invokeService
            parameters:
              serviceToInvoke: myService
              methodToInvoke: myMethod
        - to:
            uri: mock:result
```

-   `state: save` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("myValue"))
    .to("dapr:state?stateOperation=save&stateStore=myStore&key=myKey")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setBody>
    <constant>myValue</constant>
  </setBody>
  <to uri="dapr:state?stateOperation=save&amp;stateStore=myStore&amp;key=myKey"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            constant: "myValue"
        - to:
            uri: dapr:state
            parameters:
              stateOperation: save
              stateStore: myStore
              key: myKey
        - to:
            uri: mock:result
```

-   `state: saveBulk` -
    

_Java-only: uses Dapr SDK `State` types and `List.of()` to set bulk states_

```java
from("direct:start")
    .process(exchange -> {
        State<String> state1 = new State<>("key1", "val1", "etag1");
        State<String> state2 = new State<>("key2", "val1", "etag2");
        List<State<?>> states = List.of(state1, state2);
        exchange.getMessage().setHeader("CamelDaprStates", states);
    })
    .to("dapr:state?stateOperation=saveBulk&stateStore=myStore")
    .to("mock:result");
```

-   `state: get` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprConcurrency", constant("FIRST_WRITE"))
    .setHeader("CamelDaprConsistency", constant("EVENTUAL"))
    .to("dapr:state?stateOperation=get&stateStore=myStore&key=myKey")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprConcurrency">
    <constant>FIRST_WRITE</constant>
  </setHeader>
  <setHeader name="CamelDaprConsistency">
    <constant>EVENTUAL</constant>
  </setHeader>
  <to uri="dapr:state?stateOperation=get&amp;stateStore=myStore&amp;key=myKey"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprConcurrency
            constant: "FIRST_WRITE"
        - setHeader:
            name: CamelDaprConsistency
            constant: "EVENTUAL"
        - to:
            uri: dapr:state
            parameters:
              stateOperation: get
              stateStore: myStore
              key: myKey
        - to:
            uri: mock:result
```

-   `state: getBulk` -
    

_Java-only: uses `List.of()` to set bulk key list_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setHeader("CamelDaprKeys", List.of("key1", "key2"));
    })
    .to("dapr:state?stateOperation=getBulk&stateStore=myStore")
    .to("mock:result");
```

-   `state: delete` -
    

_Java-only: uses `Map.of()` to set metadata_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setHeader("CamelDaprMetadata", Map.of("partitionKey", "myPartitionKey"));
    })
    .to("dapr:state?stateOperation=delete&stateStore=myStore&key=myKey")
    .to("mock:result");
```

-   `state: executeTransaction` -
    

_Java-only: uses Dapr SDK `TransactionalStateOperation` and `State` types_

```java
from("direct:start")
    .process(exchange -> {
        TransactionalStateOperation.OperationType op = TransactionalStateOperation.OperationType.UPSERT;
        List<TransactionalStateOperation<?>> transactions = List.of(new TransactionalStateOperation<>(op, new State<>("myKey")));
        exchange.getIn().setHeader("CamelDaprTransactions", transactions);
    })
    .to("dapr:state?stateOperation=executeTransaction&stateStore=myStore")
    .to("mock:result");
```

-   `pubSub` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprContentType", constant("application/json"))
    .to("dapr:pubSub?pubSubName=myPubSub&topic=myTopic")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprContentType">
    <constant>application/json</constant>
  </setHeader>
  <to uri="dapr:pubSub?pubSubName=myPubSub&amp;topic=myTopic"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprContentType
            constant: "application/json"
        - to:
            uri: dapr:pubSub
            parameters:
              pubSubName: myPubSub
              topic: myTopic
        - to:
            uri: mock:result
```

-   `invokeBinding` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("myBody"))
    .to("dapr:invokeBinding?bindingName=myBinding&bindingOperation=myOperation")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setBody>
    <constant>myBody</constant>
  </setBody>
  <to uri="dapr:invokeBinding?bindingName=myBinding&amp;bindingOperation=myOperation"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            constant: "myBody"
        - to:
            uri: dapr:invokeBinding
            parameters:
              bindingName: myBinding
              bindingOperation: myOperation
        - to:
            uri: mock:result
```

-   `secret` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  .to("dapr:secret?secretStore=myStore&key=mySecret")
  .log("Received secret from Dapr: ${body}")
  .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="dapr:secret?secretStore=myStore&amp;key=mySecret"/>
  <log message="Received secret from Dapr: ${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: dapr:secret
            parameters:
              secretStore: myStore
              key: mySecret
        - log: "Received secret from Dapr: ${body}"
        - to:
            uri: mock:result
```

-   `secret: bulk` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
  // when no secret key is passed, bulk retrieval is performed on secret store
  .to("dapr:secret?secretStore=myStore")
  .log("Received bulk secrets from Dapr: ${body}")
  .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="dapr:secret?secretStore=myStore"/>
  <log message="Received bulk secrets from Dapr: ${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: dapr:secret
            parameters:
              secretStore: myStore
        - log: "Received bulk secrets from Dapr: ${body}"
        - to:
            uri: mock:result
```

-   `configuration` -
    

_Java-only: uses `List.of()` to set configuration key list_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setHeader("CamelDaprConfigKeys", List.of("k1", "k2"));
    })
    .to("dapr:configuration?configStore=myStore")
    .log("Received config updates from Dapr: ${body}")
    .to("mock:result");
```

-   `lock: tryLock` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprResourceId", constant("myResource"))
    .to("dapr:lock?lockOperation=tryLock&storeName=myStore&expiryInSeconds=100")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprResourceId">
    <constant>myResource</constant>
  </setHeader>
  <to uri="dapr:lock?lockOperation=tryLock&amp;storeName=myStore&amp;expiryInSeconds=100"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprResourceId
            constant: "myResource"
        - to:
            uri: dapr:lock
            parameters:
              lockOperation: tryLock
              storeName: myStore
              expiryInSeconds: 100
        - to:
            uri: mock:result
```

-   `lock: unlock` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprResourceId", constant("myResource"))
    .to("dapr:lock?lockOperation=unlock&storeName=myStore")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprResourceId">
    <constant>myResource</constant>
  </setHeader>
  <to uri="dapr:lock?lockOperation=unlock&amp;storeName=myStore"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprResourceId
            constant: "myResource"
        - to:
            uri: dapr:lock
            parameters:
              lockOperation: unlock
              storeName: myStore
        - to:
            uri: mock:result
```

-   `workflow: scheduleNew` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprWorkflowClass", constant("my.package.MyWorkflow"))
    .to("dapr:workflow?workflowOperation=scheduleNew")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprWorkflowClass">
    <constant>my.package.MyWorkflow</constant>
  </setHeader>
  <to uri="dapr:workflow?workflowOperation=scheduleNew"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprWorkflowClass
            constant: "my.package.MyWorkflow"
        - to:
            uri: dapr:workflow
            parameters:
              workflowOperation: scheduleNew
        - to:
            uri: mock:result
```

-   `workflow: terminate` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprWorkflowInstanceId", constant("myWorkflowInstanceId"))
    .to("dapr:workflow?workflowOperation=terminate")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprWorkflowInstanceId">
    <constant>myWorkflowInstanceId</constant>
  </setHeader>
  <to uri="dapr:workflow?workflowOperation=terminate"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprWorkflowInstanceId
            constant: "myWorkflowInstanceId"
        - to:
            uri: dapr:workflow
            parameters:
              workflowOperation: terminate
        - to:
            uri: mock:result
```

-   `workflow: purge` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprWorkflowInstanceId", constant("myWorkflowInstanceId"))
    .to("dapr:workflow?workflowOperation=purge")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprWorkflowInstanceId">
    <constant>myWorkflowInstanceId</constant>
  </setHeader>
  <to uri="dapr:workflow?workflowOperation=purge"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprWorkflowInstanceId
            constant: "myWorkflowInstanceId"
        - to:
            uri: dapr:workflow
            parameters:
              workflowOperation: purge
        - to:
            uri: mock:result
```

-   `workflow: suspend` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprWorkflowInstanceId", constant("myWorkflowInstanceId"))
    .setHeader("CamelDaprSuspendReason", constant("Suspended for maintenance."))
    .to("dapr:workflow?workflowOperation=suspend")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprWorkflowInstanceId">
    <constant>myWorkflowInstanceId</constant>
  </setHeader>
  <setHeader name="CamelDaprSuspendReason">
    <constant>Suspended for maintenance.</constant>
  </setHeader>
  <to uri="dapr:workflow?workflowOperation=suspend"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprWorkflowInstanceId
            constant: "myWorkflowInstanceId"
        - setHeader:
            name: CamelDaprSuspendReason
            constant: "Suspended for maintenance."
        - to:
            uri: dapr:workflow
            parameters:
              workflowOperation: suspend
        - to:
            uri: mock:result
```

-   `workflow: resume` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprWorkflowInstanceId", constant("myWorkflowInstanceId"))
    .setHeader("CamelDaprSuspendReason", constant("Maintenance complete."))
    .to("dapr:workflow?workflowOperation=resume")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprWorkflowInstanceId">
    <constant>myWorkflowInstanceId</constant>
  </setHeader>
  <setHeader name="CamelDaprSuspendReason">
    <constant>Maintenance complete.</constant>
  </setHeader>
  <to uri="dapr:workflow?workflowOperation=resume"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprWorkflowInstanceId
            constant: "myWorkflowInstanceId"
        - setHeader:
            name: CamelDaprSuspendReason
            constant: "Maintenance complete."
        - to:
            uri: dapr:workflow
            parameters:
              workflowOperation: resume
        - to:
            uri: mock:result
```

-   `workflow: state` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprWorkflowInstanceId", constant("myWorkflowInstanceId"))
    .to("dapr:workflow?workflowOperation=state")
    .log("Workflow state: ${body}")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprWorkflowInstanceId">
    <constant>myWorkflowInstanceId</constant>
  </setHeader>
  <to uri="dapr:workflow?workflowOperation=state"/>
  <log message="Workflow state: ${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprWorkflowInstanceId
            constant: "myWorkflowInstanceId"
        - to:
            uri: dapr:workflow
            parameters:
              workflowOperation: state
        - log:
            message: "Workflow state: ${body}"
        - to:
            uri: mock:result
```

-   `workflow: waitForInstanceStart` -
    

_Java-only: uses `Duration.ofSeconds()` to set timeout_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setHeader("CamelDaprWorkflowInstanceId", "myWorkflowInstanceId");
        exchange.getIn().setHeader("CamelDaprTimeout", Duration.ofSeconds(30));
    })
    .to("dapr:workflow?workflowOperation=waitForInstanceStart")
    .to("mock:result");
```

-   `workflow: waitForInstanceCompletion` -
    

_Java-only: uses `Duration.ofSeconds()` to set timeout_

```java
from("direct:start")
    .process(exchange -> {
        exchange.getIn().setHeader("CamelDaprWorkflowInstanceId", "myWorkflowInstanceId");
        exchange.getIn().setHeader("CamelDaprTimeout", Duration.ofSeconds(30));
    })
    .to("dapr:workflow?workflowOperation=waitForInstanceCompletion")
    .to("mock:result");
```

-   `workflow: raiseEvent` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("CamelDaprWorkflowInstanceId", constant("myWorkflowInstanceId"))
    .to("dapr:workflow?workflowOperation=raiseEvent&eventName=MyEvent")
    .to("mock:result");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="CamelDaprWorkflowInstanceId">
    <constant>myWorkflowInstanceId</constant>
  </setHeader>
  <to uri="dapr:workflow?workflowOperation=raiseEvent&amp;eventName=MyEvent"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: CamelDaprWorkflowInstanceId
            constant: "myWorkflowInstanceId"
        - to:
            uri: dapr:workflow
            parameters:
              workflowOperation: raiseEvent
              eventName: MyEvent
        - to:
            uri: mock:result
```

### Consumer Operations Examples

-   `pubSub` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("dapr:pubSub?pubSubName=myPubSub&topic=myTopic")
  .log("Received message from Dapr pubsub: ${body}")
  .to("mock:result");
```

```xml
<route>
  <from uri="dapr:pubSub?pubSubName=myPubSub&amp;topic=myTopic"/>
  <log message="Received message from Dapr pubsub: ${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: dapr:pubSub
      parameters:
        pubSubName: myPubSub
        topic: myTopic
      steps:
        - log: "Received message from Dapr pubsub: ${body}"
        - to:
            uri: mock:result
```

-   `configuration` -
    

-   Java
    
-   XML
    
-   YAML
    

```java
from("dapr:configuration?configStore=myStore&configKeys=k1,k2")
  .log("Received config updates from Dapr: ${body}")
  .to("mock:result");
```

```xml
<route>
  <from uri="dapr:configuration?configStore=myStore&amp;configKeys=k1,k2"/>
  <log message="Received config updates from Dapr: ${body}"/>
  <to uri="mock:result"/>
</route>
```

```yaml
- route:
    from:
      uri: dapr:configuration
      parameters:
        configStore: myStore
        configKeys: "k1,k2"
      steps:
        - log: "Received config updates from Dapr: ${body}"
        - to:
            uri: mock:result
```