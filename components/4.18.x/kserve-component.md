# KServe

**Since Camel 4.10**

**Only producer is supported**

The KServe component provides the ability to access various AI model servers using the [KServe Open Inference Protocl V2](https://kserve.github.io/website/latest/modelserving/data_plane/v2_protocol/). This allows Camel to remotely perform inference with AI models on various model servers that support the KServe V2 protocol.

> **Note**
> Currently, this component only supports [GRPC API](https://kserve.github.io/website/latest/reference/swagger-ui/#grpc).

To use the KServe component, Maven users will need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-kserve</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

kserve:api\[?options\]

Where `api` represents one of the [KServe Open Inference Protocol GRPC API](https://kserve.github.io/website/latest/reference/swagger-ui/#grpc).

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

The KServe component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration. |  | KServeConfiguration |
| **modelName** (common) | The name of the model used for inference. |  | String |
| **modelVersion** (common) | The version of the model used for inference. |  | String |
| **target** (common) | The target URI of the client. See: [https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29](https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29). | localhost:8001 | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **credentials** (security) | The credentials of the client. |  | ChannelCredentials |

## Endpoint Options

The KServe endpoint is configured using URI syntax:

kserve:api

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **api** (producer) | 
**Required** The KServe API.

Enum values:

-   infer
    
-   model/ready
    
-   model/metadata
    
-   server/ready
    
-   server/live
    
-   server/metadata
    





 |  | String |

### Query Parameters (5 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **modelName** (common) | The name of the model used for inference. |  | String |
| **modelVersion** (common) | The version of the model used for inference. |  | String |
| **target** (common) | The target URI of the client. See: [https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29](https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29). | localhost:8001 | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **credentials** (security) | The credentials of the client. |  | ChannelCredentials |

## Message Headers

The KServe component supports 2 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelKServeModelName** (producer) Constant: [`MODEL_NAME`](https://javadoc.io/doc/org.apache.camel/camel-kserve/latest/org/apache/camel/component/kserve/KServeConstants.html#MODEL_NAME) | The name of the model used for inference. |  | String |
| **CamelKServeModelVersion** (producer) Constant: [`MODEL_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-kserve/latest/org/apache/camel/component/kserve/KServeConstants.html#MODEL_VERSION) | The version of the model used for inference. |  | String |

## Usage

The component supports the following APIs.

kserve:<api>\[?options\]

    
| API | Description | Options | Input (Message Body) | Result (Message Body) |
| --- | --- | --- | --- | --- |
| `infer` | Performs inference using the specified model. | `modelName`  
`modelVersion` | `ModelInferRequest` \[[1](#_footnotedef_1 "View footnote.")\] | `ModelInferResponse` \[[2](#_footnotedef_2 "View footnote.")\] |
| `model/ready` | Indicates if a specific model is ready for inferencing. | `modelName`  
`modelVersion` | `ModelReadyRequest` \[[3](#_footnotedef_3 "View footnote.")\]  
(optional) | `ModelReadyResponse` \[[4](#_footnotedef_4 "View footnote.")\] |
| `model/metadata` | Provides information about a model. | `modelName`  
`modelVersion` | `ModelMetadataRequest` \[[5](#_footnotedef_5 "View footnote.")\]  
(optional) | `ModelMetadataResponse` \[[6](#_footnotedef_6 "View footnote.")\] |
| `server/ready` | Indicates if the server is ready for inferencing. |  |  | `ServerReadyResponse` \[[7](#_footnotedef_7 "View footnote.")\] |
| `server/live` | Indicates if the inference server is able to receive and respond to metadata and inference requests. |  |  | `ServerLiveResponse` \[[8](#_footnotedef_8 "View footnote.")\] |
| `server/metadata` | Provides information about the server. |  |  | `ServerMetadataResponse` \[[9](#_footnotedef_9 "View footnote.")\] |

## Examples

### Infer (ModelInfer) API

Perform inference

```java
from("direct:infer")
    .setBody(constant(createRequest()))
    .to("kserve:infer?modelName=simple&modelVersion=1")
    .process(this::postprocess)
    .log("Result: ${body}");

// Helper methods

ModelInferRequest createRequest() {
    // How to create a request differs depending on the input types of the model.
    var ints0 = IntStream.range(1, 17).boxed().collect(Collectors.toList());
    var content0 = InferTensorContents.newBuilder().addAllIntContents(ints0);
    var input0 = ModelInferRequest.InferInputTensor.newBuilder()
            .setName("INPUT0").setDatatype("INT32").addShape(1).addShape(16)
            .setContents(content0);
    var ints1 = IntStream.range(0, 16).boxed().collect(Collectors.toList());
    var content1 = InferTensorContents.newBuilder().addAllIntContents(ints1);
    var input1 = ModelInferRequest.InferInputTensor.newBuilder()
            .setName("INPUT1").setDatatype("INT32").addShape(1).addShape(16)
            .setContents(content1);
    return ModelInferRequest.newBuilder()
            .addInputs(0, input0).addInputs(1, input1)
            .build();
}

void postprocess(Exchange exchange) {
    // How to post-process the response differs depending on the output types
    // of the model.
    var response = exchange.getMessage().getBody(ModelInferResponse.class);
    var content = response.getRawOutputContents(0);
    var buffer = content.asReadOnlyByteBuffer().order(ByteOrder.LITTLE_ENDIAN).asIntBuffer();
    var ints = new ArrayList<Integer>(buffer.remaining());
    while (buffer.hasRemaining()) {
        ints.add(buffer.get());
    }
    exchange.getMessage().setBody(ints);
}
```

Specify the model name and version with headers

```java
from("direct:infer-with-headers")
    .setBody(constant(createRequest()))
    .setHeader(KServeConstants.MODEL_NAME, constant("simple"))
    .setHeader(KServeConstants.MODEL_VERSION, constant("1"))
    .to("kserve:infer")
    .process(this::postprocess)
    .log("Result: ${body}");

// ... Same as the previous example
```

### ModelReady API

Check if a model is ready

```java
from("direct:model-ready")
    .to("kserve:model/ready?modelName=simple&modelVersion=1")
    .log("Status: ${body.ready}");
```

Specify the model name and version with headers

```java
from("direct:model-ready-with-headers")
    .setHeader(KServeConstants.MODEL_NAME, constant("simple"))
    .setHeader(KServeConstants.MODEL_VERSION, constant("1"))
    .to("kserve:model/ready")
    .log("Status: ${body.ready}");
```

### ModelMetadata API

Fetch model metadata

```java
from("direct:model-metadata")
    .to("kserve:model/metadata?modelName=simple&modelVersion=1")
    .log("Metadata: ${body}");
```

Specify the model name and version with headers

```java
from("direct:model-metadata-with-headers")
    .setHeader(KServeConstants.MODEL_NAME, constant("simple"))
    .setHeader(KServeConstants.MODEL_VERSION, constant("1"))
    .to("kserve:model/metadata")
    .log("Metadata: ${body}");
```

### ServerReady API

Check if the server is ready

```java
from("direct:server-ready")
    .to("kserve:server/ready")
    .log("Status: ${body.ready}");
```

### ServerLive API

Check if the server is live

```java
from("direct:server-live")
    .to("kserve:server/live")
    .log("Status: ${body.live}");
```

### ServerMetadata API

Fetch server metadata

```java
from("direct:server-metadata")
    .to("kserve:server/metadata")
    .log("Metadata: ${body}");
```

## Spring Boot Auto-Configuration

When using kserve with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-kserve-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.kserve.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.kserve.configuration** | The configuration. The option is a org.apache.camel.component.kserve.KServeConfiguration type. |  | KServeConfiguration |
| **camel.component.kserve.credentials** | The credentials of the client. The option is a io.grpc.ChannelCredentials type. |  | ChannelCredentials |
| **camel.component.kserve.enabled** | Whether to enable auto configuration of the kserve component. This is enabled by default. |  | Boolean |
| **camel.component.kserve.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.kserve.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.kserve.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.kserve.model-name** | The name of the model used for inference. |  | String |
| **camel.component.kserve.model-version** | The version of the model used for inference. |  | String |
| **camel.component.kserve.target** | The target URI of the client. See: [https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29](https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29). | localhost:8001 | String |

* * *

[1](#_footnoteref_1). `inference.GrpcPredictV2.ModelInferRequest`

[2](#_footnoteref_2). `inference.GrpcPredictV2.ModelInferResponse`

[3](#_footnoteref_3). `inference.GrpcPredictV2.ModelReadyRequest`

[4](#_footnoteref_4). `inference.GrpcPredictV2.ModelReadyResponse`

[5](#_footnoteref_5). `inference.GrpcPredictV2.ModelMetadataRequest`

[6](#_footnoteref_6). `inference.GrpcPredictV2.ModelMetadataResponse`

[7](#_footnoteref_7). `inference.GrpcPredictV2.ServerReadyResponse`

[8](#_footnoteref_8). `inference.GrpcPredictV2.ServerLiveResponse`

[9](#_footnoteref_9). `inference.GrpcPredictV2.ServerMetadataResponse`