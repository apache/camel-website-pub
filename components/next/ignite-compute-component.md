# Ignite Compute

**Since Camel 2.17**

**Only producer is supported**

The Ignite Compute endpoint is one of camel-ignite endpoints which allows you to run [compute operations](https://apacheignite.readme.io/docs/compute-grid) on the cluster by passing in an IgniteCallable, an IgniteRunnable, an IgniteClosure, or collections of them, along with their parameters if necessary.

The host part of the endpoint URI is a symbolic endpoint ID, it is not used for any purposes.

The endpoint tries to run the object passed in the body of the IN message as the compute job. It expects different payload types depending on the execution type.

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

The Ignite Compute component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configurationResource** (producer) | The resource from where to load the configuration. It can be a: URL, String or InputStream type. |  | Object |
| **ignite** (producer) | To use an existing Ignite instance. |  | Ignite |
| **igniteConfiguration** (producer) | Allows the user to set a programmatic ignite configuration. |  | IgniteConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Ignite Compute endpoint is configured using URI syntax:

ignite-compute:endpointId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **endpointId** (producer) | **Required** The endpoint ID (not used). |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **clusterGroupExpression** (producer) | An expression that returns the Cluster Group for the IgniteCompute instance. |  | ClusterGroupExpression |
| **computeName** (producer) | The name of the compute job, which will be set via IgniteCompute#withName(String). |  | String |
| **executionType** (producer) | 
**Required** The compute operation to perform. Possible values: CALL, BROADCAST, APPLY, EXECUTE, RUN, AFFINITY\_CALL, AFFINITY\_RUN. The component expects different payload types depending on the operation.

Enum values:

-   CALL
    
-   BROADCAST
    
-   APPLY
    
-   EXECUTE
    
-   RUN
    
-   AFFINITY\_CALL
    
-   AFFINITY\_RUN
    





 |  | IgniteComputeExecutionType |
| **propagateIncomingBodyIfNoReturnValue** (producer) | Sets whether to propagate the incoming body if the return type of the underlying Ignite operation is void. | true | boolean |
| **taskName** (producer) | The task name, only applicable if using the IgniteComputeExecutionType#EXECUTE execution type. |  | String |
| **timeoutMillis** (producer) | The timeout interval for triggered jobs, in milliseconds, which will be set via IgniteCompute#withTimeout(long). |  | Long |
| **treatCollectionsAsCacheObjects** (producer) | Sets whether to treat Collections as cache objects or as Collections of items to insert/update/compute, etc. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Ignite Compute component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIgniteComputeExecutionType** (producer) Constant: [`IGNITE_COMPUTE_EXECUTION_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_COMPUTE_EXECUTION_TYPE) | 
Allows you to dynamically change the compute operation to perform.

Enum values:

-   CALL
    
-   BROADCAST
    
-   APPLY
    
-   EXECUTE
    
-   RUN
    
-   AFFINITY\_CALL
    
-   AFFINITY\_RUN
    





 |  | IgniteComputeExecutionType |
| **CamelIgniteComputeParameters** (producer) Constant: [`IGNITE_COMPUTE_PARAMS`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_COMPUTE_PARAMS) | Parameters for APPLY, BROADCAST and EXECUTE operations. |  | Any object or Collection of objects |
| **CamelIgniteComputeReducer** (producer) Constant: [`IGNITE_COMPUTE_REDUCER`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_COMPUTE_REDUCER) | Reducer for the APPLY and CALL operations. |  | IgniteReducer |
| **CamelIgniteComputeAffinityCacheName** (producer) Constant: [`IGNITE_COMPUTE_AFFINITY_CACHE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_COMPUTE_AFFINITY_CACHE_NAME) | Affinity cache name for the AFFINITY\_CALL and AFFINITY\_RUN operations. |  | String |
| **CamelIgniteComputeAffinityKey** (producer) Constant: [`IGNITE_COMPUTE_AFFINITY_KEY`](https://javadoc.io/doc/org.apache.camel/camel-ignite/latest/org/apache/camel/component/ignite/IgniteConstants.html#IGNITE_COMPUTE_AFFINITY_KEY) | Affinity key for the AFFINITY\_CALL and AFFINITY\_RUN operations. |  | Object |

## Expected payload types

Each operation expects the indicated types:

 
| Operation | Expected payloads |
| --- | --- |
| CALL | Collection of IgniteCallable, or a single IgniteCallable. |
| BROADCAST | IgniteCallable, IgniteRunnable, IgniteClosure. |
| APPLY | IgniteClosure. |
| EXECUTE | ComputeTask, Class<? extends ComputeTask> or an object representing parameters if the taskName option is not null. |
| RUN | A Collection of IgniteRunnables, or a single IgniteRunnable. |
| AFFINITY\_CALL | IgniteCallable. |
| AFFINITY\_RUN | IgniteRunnable. |