# TorchServe

> **Warning**
> **Deprecated:** This torchserve is deprecated and may be removed in a future release.

**Since Camel 4.9**

**Only producer is supported**

The TorchServe component provides support for invoking the [TorchServe REST API](https://pytorch.org/serve/rest_api.md). It enables Camel to access PyTorch TorchServe servers to run inference with PyTorch models remotely.

To use the TorchServe component, Maven users will need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-torchserve</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

torchserve:api/operation\[?options\]

Where `api` represents one of the [TorchServe REST API](https://pytorch.org/serve/rest_api.md), and `operation` represents a specific operation supported by the API.

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

The TorchServe component supports 22 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration. |  | TorchServeConfiguration |
| **modelName** (common) | The name of model. |  | String |
| **modelVersion** (common) | The version of model. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **inferenceAddress** (inference) | The address of the inference API endpoint. |  | String |
| **inferencePort** (inference) | The port of the inference API endpoint. | 8080 | int |
| **listLimit** (management) | The maximum number of items to return for the list operation. When this value is present, TorchServe does not return more than the specified number of items, but it might return fewer. This value is optional. If you include a value, it must be between 1 and 1000, inclusive. If you do not include a value, it defaults to 100. | 100 | int |
| **listNextPageToken** (management) | The token to retrieve the next set of results for the list operation. TorchServe provides the token when the response from a previous call has more results than the maximum page size. |  | String |
| **managementAddress** (management) | The address of the management API endpoint. |  | String |
| **managementPort** (management) | The port of the management API endpoint. | 8081 | int |
| **registerOptions** (management) | Additional options for the register operation. |  | RegisterOptions |
| **scaleWorkerOptions** (management) | Additional options for the scale-worker operation. |  | ScaleWorkerOptions |
| **unregisterOptions** (management) | Additional options for the unregister operation. |  | UnregisterOptions |
| **url** (management) | Model archive download url, support local file or HTTP(s) protocol. For S3, consider using pre-signed url. |  | String |
| **metricsAddress** (metrics) | The address of the metrics API endpoint. |  | String |
| **metricsName** (metrics) | Names of metrics to filter. |  | String |
| **metricsPort** (metrics) | The port of the metrics API endpoint. | 8082 | int |
| **inferenceKey** (security) | The token authorization key for accessing the inference API. |  | String |
| **managementKey** (security) | The token authorization key for accessing the management API. |  | String |

## Endpoint Options

The TorchServe endpoint is configured using URI syntax:

torchserve:api/operation

With the following _path_ and _query_ parameters:

### Path Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **api** (producer) | 
**Required** The TorchServe API.

Enum values:

-   inference
    
-   management
    
-   metrics
    





 |  | String |
| **operation** (producer) | 

**Required** The API operation.

Enum values:

-   ping
    
-   predictions
    
-   explanations
    
-   register
    
-   scale-worker
    
-   describe
    
-   unregister
    
-   list
    
-   set-default
    
-   metrics
    





 |  | String |

### Query Parameters (18 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **modelName** (common) | The name of model. |  | String |
| **modelVersion** (common) | The version of model. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **inferenceAddress** (inference) | The address of the inference API endpoint. |  | String |
| **inferencePort** (inference) | The port of the inference API endpoint. | 8080 | int |
| **listLimit** (management) | The maximum number of items to return for the list operation. When this value is present, TorchServe does not return more than the specified number of items, but it might return fewer. This value is optional. If you include a value, it must be between 1 and 1000, inclusive. If you do not include a value, it defaults to 100. | 100 | int |
| **listNextPageToken** (management) | The token to retrieve the next set of results for the list operation. TorchServe provides the token when the response from a previous call has more results than the maximum page size. |  | String |
| **managementAddress** (management) | The address of the management API endpoint. |  | String |
| **managementPort** (management) | The port of the management API endpoint. | 8081 | int |
| **registerOptions** (management) | Additional options for the register operation. |  | RegisterOptions |
| **scaleWorkerOptions** (management) | Additional options for the scale-worker operation. |  | ScaleWorkerOptions |
| **unregisterOptions** (management) | Additional options for the unregister operation. |  | UnregisterOptions |
| **url** (management) | Model archive download url, support local file or HTTP(s) protocol. For S3, consider using pre-signed url. |  | String |
| **metricsAddress** (metrics) | The address of the metrics API endpoint. |  | String |
| **metricsName** (metrics) | Names of metrics to filter. |  | String |
| **metricsPort** (metrics) | The port of the metrics API endpoint. | 8082 | int |
| **inferenceKey** (security) | The token authorization key for accessing the inference API. |  | String |
| **managementKey** (security) | The token authorization key for accessing the management API. |  | String |

## Message Headers

The TorchServe component supports 9 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelTorchServeModelName** (producer) Constant: [`MODEL_NAME`](https://javadoc.io/doc/org.apache.camel/camel-torchserve/latest/org/apache/camel/component/torchserve/TorchServeConstants.html#MODEL_NAME) | The name of model. |  | String |
| **CamelTorchServeModelVersion** (producer) Constant: [`MODEL_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-torchserve/latest/org/apache/camel/component/torchserve/TorchServeConstants.html#MODEL_VERSION) | The version of model. |  | String |
| **CamelTorchServeUrl** (producer) Constant: [`URL`](https://javadoc.io/doc/org.apache.camel/camel-torchserve/latest/org/apache/camel/component/torchserve/TorchServeConstants.html#URL) | Model archive download url, support local file or HTTP(s) protocol. For S3, consider using pre-signed url. |  | String |
| **CamelTorchServeRegisterOptions** (producer) Constant: [`REGISTER_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-torchserve/latest/org/apache/camel/component/torchserve/TorchServeConstants.html#REGISTER_OPTIONS) | Additional options for the register operation. |  | RegisterOptions |
| **CamelTorchServeScaleWorkerOptions** (producer) Constant: [`SCALE_WORKER_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-torchserve/latest/org/apache/camel/component/torchserve/TorchServeConstants.html#SCALE_WORKER_OPTIONS) | Additional options for the scale-worker operation. |  | ScaleWorkerOptions |
| **CamelTorchServeUnrsegisterOptions** (producer) Constant: [`UNREGISTER_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-torchserve/latest/org/apache/camel/component/torchserve/TorchServeConstants.html#UNREGISTER_OPTIONS) | Additional options for the unregister operation. |  | UnregisterOptions |
| **CamelTorchServeListLimit** (producer) Constant: [`LIST_LIMIT`](https://javadoc.io/doc/org.apache.camel/camel-torchserve/latest/org/apache/camel/component/torchserve/TorchServeConstants.html#LIST_LIMIT) | The maximum number of items to return for the list operation. When this value is present, TorchServe does not return more than the specified number of items, but it might return fewer. This value is optional. If you include a value, it must be between 1 and 1000, inclusive. If you do not include a value, it defaults to 100. |  | Integer |
| **CamelTorchServeListNextPageToken** (producer) Constant: [`LIST_NEXT_PAGE_TOKEN`](https://javadoc.io/doc/org.apache.camel/camel-torchserve/latest/org/apache/camel/component/torchserve/TorchServeConstants.html#LIST_NEXT_PAGE_TOKEN) | The token to retrieve the next set of results for the list operation. TorchServe provides the token when the response from a previous call has more results than the maximum page size. |  | String |
| **CamelTorchServeMetricsName** (producer) Constant: [`METRICS_NAME`](https://javadoc.io/doc/org.apache.camel/camel-torchserve/latest/org/apache/camel/component/torchserve/TorchServeConstants.html#METRICS_NAME) | Names of metrics to filter. |  | String |

## Usage

Each API endpoint supports the following operations.

### Inference API

The Inference API provides the inference operations.

torchserve:inference/<operation>\[?options\]

   
| Operation | Description | Options | Result |
| --- | --- | --- | --- |
| `ping` | Get TorchServe status. | \- | `String` |
| `predictions` | Predictions entry point to get inference using a model. | `modelName`  
`modelVersion` | `Object` |
| `explanations` | Not supported yet. | \- | `Object` |

### Management API

The Management API provides the operations to manage models at runtime.

torchserve:management/<operation>\[?options\]

   
| Operation | Description | Options | Result |
| --- | --- | --- | --- |
| `register` | Register a new model in TorchServe. | `url`  
`registerOptions` | `String` |
| `scale-worker` | Configure number of workers for a model. This is an asynchronous call by default. Caller need to call `describe` to check if the model workers has been changed. | `modelName`  
`modelVersion`  
`scaleWorkerOptions` | `String` |
| `describe` | Provides detailed information about a model. If "all" is specified as version, returns the details about all the versions of the model. | `modelName`  
`modelVersion` | `List<ModelDetail>` \[[1](#_footnotedef_1 "View footnote.")\] |
| `unregister` | Unregister a model from TorchServe. This is an asynchronous call by default. Caller can call `list` to confirm the model is unregistered. | `modelName`  
`modelVersion`  
`unregisterOptions` | `String` |
| `list` | List registered models in TorchServe. | `listLimit`  
`listNextPageToken` | `ModelList` \[[2](#_footnotedef_2 "View footnote.")\] |
| `set-default` | Set default version of a model. | `modelName`  
`modelVersion` | `String` |

### Metrics API

The Metrics API provides the operations to fetch metrics in the Prometheus format.

torchserve:metrics/<operation>\[?options\]

   
| Operation | Description | Options | Result |
| --- | --- | --- | --- |
| `metrics` | Get TorchServe application metrics in prometheus format. | `metricsName` | `String` |

## Examples

### Inference API

Health checking

```java
from("direct:ping")
    .to("torchserve:inference/ping")
    .log("Status: ${body}");
```

Prediction

```java
from("file:data/kitten.jpg")
    .to("torchserve:inference/predictions?modelName=squeezenet1_1")
    .log("Result: ${body}");
```

### Management API

Register a model

```java
from("direct:register")
    .to("torchserve:management/register?url=https://torchserve.pytorch.org/mar_files/mnist_v2.mar")
    .log("Status: ${body}");
```

Scale workers for a registered model

```java
from("direct:scale-worker")
    .setHeader(TorchServeConstants.SCALE_WORKER_OPTIONS,
        constant(ScaleWorkerOptions.builder().minWorker(1).maxWorker(2).build()))
    .to("torchserve:management/scale-worker?modelName=mnist_v2")
    .log("Status: ${body}");
```

Get the detailed information about a model

```java
from("direct:describe")
    .to("torchserve:management/describe?modelName=mnist_v2")
    .log("${body[0]}");
```

Unregister a model

```java
from("direct:register")
    .to("torchserve:management/unregister?modelName=mnist_v2")
    .log("Status: ${body}");
```

List models

```java
from("direct:list")
    .to("torchserve:management/list")
    .log("${body.models}");
```

Set the default version of a model

```java
from("direct:set-default")
    .to("torchserve:management/set-default?modelName=mnist_v2&modelVersion=2.0")
    .log("Status: ${body}");
```

### Metrics API

All metrics

```java
from("direct:metrics")
    .to("torchserve:metrics/metrics");
```

`MemoryUsed` metrics only

```java
from("direct:metrics")
    .to("torchserve:metrics/metrics?metricsName=MemoryUsed");
```

## Spring Boot Auto-Configuration

When using torchserve with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-torchserve-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 23 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.torchserve.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.torchserve.configuration** | The configuration. The option is a org.apache.camel.component.torchserve.TorchServeConfiguration type. |  | TorchServeConfiguration |
| **camel.component.torchserve.enabled** | Whether to enable auto configuration of the torchserve component. This is enabled by default. |  | Boolean |
| **camel.component.torchserve.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.torchserve.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.torchserve.inference-address** | The address of the inference API endpoint. |  | String |
| **camel.component.torchserve.inference-key** | The token authorization key for accessing the inference API. |  | String |
| **camel.component.torchserve.inference-port** | The port of the inference API endpoint. | 8080 | Integer |
| **camel.component.torchserve.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.torchserve.list-limit** | The maximum number of items to return for the list operation. When this value is present, TorchServe does not return more than the specified number of items, but it might return fewer. This value is optional. If you include a value, it must be between 1 and 1000, inclusive. If you do not include a value, it defaults to 100. | 100 | Integer |
| **camel.component.torchserve.list-next-page-token** | The token to retrieve the next set of results for the list operation. TorchServe provides the token when the response from a previous call has more results than the maximum page size. |  | String |
| **camel.component.torchserve.management-address** | The address of the management API endpoint. |  | String |
| **camel.component.torchserve.management-key** | The token authorization key for accessing the management API. |  | String |
| **camel.component.torchserve.management-port** | The port of the management API endpoint. | 8081 | Integer |
| **camel.component.torchserve.metrics-address** | The address of the metrics API endpoint. |  | String |
| **camel.component.torchserve.metrics-name** | Names of metrics to filter. |  | String |
| **camel.component.torchserve.metrics-port** | The port of the metrics API endpoint. | 8082 | Integer |
| **camel.component.torchserve.model-name** | The name of model. |  | String |
| **camel.component.torchserve.model-version** | The version of model. |  | String |
| **camel.component.torchserve.register-options** | Additional options for the register operation. The option is a org.apache.camel.component.torchserve.client.model.RegisterOptions type. |  | RegisterOptions |
| **camel.component.torchserve.scale-worker-options** | Additional options for the scale-worker operation. The option is a org.apache.camel.component.torchserve.client.model.ScaleWorkerOptions type. |  | ScaleWorkerOptions |
| **camel.component.torchserve.unregister-options** | Additional options for the unregister operation. The option is a org.apache.camel.component.torchserve.client.model.UnregisterOptions type. |  | UnregisterOptions |
| **camel.component.torchserve.url** | Model archive download url, support local file or HTTP(s) protocol. For S3, consider using pre-signed url. |  | String |

* * *

[1](#_footnoteref_1). `org.apache.camel.component.torchserve.client.model.ModelDetail`

[2](#_footnoteref_2). `org.apache.camel.component.torchserve.client.model.ModelList`