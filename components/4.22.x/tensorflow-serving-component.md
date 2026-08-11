# TensorFlow Serving

**Since Camel 4.10**

**Only producer is supported**

The TensorFlow Serving component provides support for invoking the [TensorFlow Serving Client API (gRPC)](https://github.com/tensorflow/serving/blob/2.18.0/tensorflow_serving/apis/prediction_service.proto). It enables Camel to access [TensorFlow Serving model servers](https://www.tensorflow.org/tfx/guide/serving) to run inference with TensorFlow saved models remotely.

To use the TensorFlow Serving component, Maven users will need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-tensorflow-serving</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

tensorflow-serving:api\[?options\]

Where `api` represents one of the [TensorFlow Serving Client API (gPRC)](https://github.com/tensorflow/serving/blob/2.18.0/tensorflow_serving/apis/prediction_service.proto). While its RESTful Client API is not directly supported by the component, you can refer to the [doc](https://www.tensorflow.org/tfx/serving/api_rest) to get an idea of each API that TensorFlow Serving provides.

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

The TensorFlow Serving component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration. |  | TensorFlowServingConfiguration |
| **modelName** (common) | Required servable name. |  | String |
| **modelVersion** (common) | Optional choice of which version of the model to use. Use this specific version number. |  | Long |
| **modelVersionLabel** (common) | Optional choice of which version of the model to use. Use the version associated with the given label. |  | String |
| **signatureName** (common) | A named signature to evaluate. If unspecified, the default signature will be used. |  | String |
| **target** (common) | The target URI of the client. See: [https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29](https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29). | localhost:8500 | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **credentials** (security) | The credentials of the client. |  | ChannelCredentials |

## Endpoint Options

The TensorFlow Serving endpoint is configured using URI syntax:

tensorflow-serving:api

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **api** (producer) | 
**Required** The TensorFlow Serving API.

Enum values:

-   model-status
    
-   model-metadata
    
-   classify
    
-   regress
    
-   predict
    





 |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **modelName** (common) | Required servable name. |  | String |
| **modelVersion** (common) | Optional choice of which version of the model to use. Use this specific version number. |  | Long |
| **modelVersionLabel** (common) | Optional choice of which version of the model to use. Use the version associated with the given label. |  | String |
| **signatureName** (common) | A named signature to evaluate. If unspecified, the default signature will be used. |  | String |
| **target** (common) | The target URI of the client. See: [https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29](https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29). | localhost:8500 | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **credentials** (security) | The credentials of the client. |  | ChannelCredentials |

## Message Headers

The TensorFlow Serving component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelTensorFlowServingTarget** (producer) Constant: [`TARGET`](https://javadoc.io/doc/org.apache.camel/camel-tensorflow-serving/latest/org/apache/camel/component/tensorflow/serving/TensorFlowServingConstants.html#TARGET) | The target of the client. See: [https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29](https://grpc.github.io/grpc-java/javadoc/io/grpc/Grpc.html#newChannelBuilder%28java.lang.String,io.grpc.ChannelCredentials%29). |  | String |
| **CamelTensorFlowServingCredentials** (producer) Constant: [`CREDENTIALS`](https://javadoc.io/doc/org.apache.camel/camel-tensorflow-serving/latest/org/apache/camel/component/tensorflow/serving/TensorFlowServingConstants.html#CREDENTIALS) | The credentials of the client. |  | ChannelCredentials |
| **CamelTensorFlowServingModelName** (producer) Constant: [`MODEL_NAME`](https://javadoc.io/doc/org.apache.camel/camel-tensorflow-serving/latest/org/apache/camel/component/tensorflow/serving/TensorFlowServingConstants.html#MODEL_NAME) | Required servable name. |  | String |
| **CamelTensorFlowServingModelVersion** (producer) Constant: [`MODEL_VERSION`](https://javadoc.io/doc/org.apache.camel/camel-tensorflow-serving/latest/org/apache/camel/component/tensorflow/serving/TensorFlowServingConstants.html#MODEL_VERSION) | Optional choice of which version of the model to use. Use this specific version number. |  | long |
| **CamelTensorFlowServingModelVersionLabel** (producer) Constant: [`MODEL_VERSION_LABEL`](https://javadoc.io/doc/org.apache.camel/camel-tensorflow-serving/latest/org/apache/camel/component/tensorflow/serving/TensorFlowServingConstants.html#MODEL_VERSION_LABEL) | Optional choice of which version of the model to use. Use the version associated with the given label. |  | String |
| **CamelTensorFlowServingSignatureName** (producer) Constant: [`SIGNATURE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-tensorflow-serving/latest/org/apache/camel/component/tensorflow/serving/TensorFlowServingConstants.html#SIGNATURE_NAME) | A named signature to evaluate. If unspecified, the default signature will be used. |  | String |

## Usage

The component supports the following APIs.

tensorflow-serving:<api>\[?options\]

    
| API | Description | Options | Input (Message Body) | Result (Message Body) |
| --- | --- | --- | --- | --- |
| `model-status` | Return the status of a model in the Model server. | `modelName`  
`modelVersion`  
`modelVersionLabel` | `GetModelStatusRequest` \[[1](#_footnotedef_1 "View footnote.")\]  
(optional) | `GetModelStatusResponse` \[[2](#_footnotedef_2 "View footnote.")\] |
| `model-metadata` | Return the metadata of a model in the Model server. | `modelName`  
`modelVersion`  
`modelVersionLabel` | `GetModelMetadataRequest` \[[3](#_footnotedef_3 "View footnote.")\]  
(optional) | `GetModelMetadataResponse` \[[4](#_footnotedef_4 "View footnote.")\] |
| `classify` | Run a classification with a model in the Model server. | `modelName`  
`modelVersion`  
`modelVersionLabel`  
`signatureName` | `ClassificationRequest` \[[5](#_footnotedef_5 "View footnote.")\]  
`Input` \[[6](#_footnotedef_6 "View footnote.")\] | `ClassificationResponse` \[[7](#_footnotedef_7 "View footnote.")\] |
| `regress` | Run a regression with a model in the Model server. | `modelName`  
`modelVersion`  
`modelVersionLabel`  
`signatureName` | `RegressionRequest` \[[8](#_footnotedef_8 "View footnote.")\]  
`Input` \[[9](#_footnotedef_9 "View footnote.")\] | `RegressionResponse` \[[10](#_footnotedef_10 "View footnote.")\] |
| `predict` | Provide generic access to a model in the Model server. | `modelName`  
`modelVersion`  
`modelVersionLabel`  
`signatureName` | `PredictRequest` \[[11](#_footnotedef_11 "View footnote.")\] | `PredictResponse` \[[12](#_footnotedef_12 "View footnote.")\] |

## Examples

### Model status API

Check model status

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:model-status")
    .to("tensorflow-serving:model-status?modelName=half_plus_two&modelVersion=123")
    .log("Status: ${body.getModelVersionStatus(0).state}");
```

```xml
<route>
  <from uri="direct:model-status"/>
  <to uri="tensorflow-serving:model-status?modelName=half_plus_two&amp;modelVersion=123"/>
  <log message="Status: ${body.getModelVersionStatus(0).state}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:model-status
      steps:
        - to:
            uri: tensorflow-serving:model-status
            parameters:
              modelName: half_plus_two
              modelVersion: 123
        - log:
            message: "Status: ${body.getModelVersionStatus(0).state}"
```

Specify the model name and version with headers

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:model-status-with-headers")
    .setHeader("CamelTensorFlowServingModelName", constant("half_plus_two"))
    .setHeader("CamelTensorFlowServingModelVersion", constant(123))
    .to("tensorflow-serving:model-status")
    .log("Status: ${body.getModelVersionStatus(0).state}");
```

```xml
<route>
  <from uri="direct:model-status-with-headers"/>
  <setHeader name="CamelTensorFlowServingModelName">
    <constant>half_plus_two</constant>
  </setHeader>
  <setHeader name="CamelTensorFlowServingModelVersion">
    <constant resultType="java.lang.Integer">123</constant>
  </setHeader>
  <to uri="tensorflow-serving:model-status"/>
  <log message="Status: ${body.getModelVersionStatus(0).state}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:model-status-with-headers
      steps:
        - setHeader:
            name: CamelTensorFlowServingModelName
            constant: half_plus_two
        - setHeader:
            name: CamelTensorFlowServingModelVersion
            constant: 123
        - to:
            uri: tensorflow-serving:model-status
        - log:
            message: "Status: ${body.getModelVersionStatus(0).state}"
```

### Model Metadata API

Currently, TensorFlow Serving only supports `signature_def` as the metadata field. See: [get\_model\_metadata.proto](https://github.com/tensorflow/serving/blob/2.18.0/tensorflow_serving/apis/get_model_metadata.proto#L26-L28)

Fetch model metadata

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:model-metadata")
    .to("tensorflow-serving:model-metadata?modelName=half_plus_two&modelVersion=123")
    .log("Metadata: ${body.getMetadataOrThrow('signature_def')}");
```

```xml
<route>
  <from uri="direct:model-metadata"/>
  <to uri="tensorflow-serving:model-metadata?modelName=half_plus_two&amp;modelVersion=123"/>
  <log message="Metadata: ${body.getMetadataOrThrow('signature_def')}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:model-metadata
      steps:
        - to:
            uri: tensorflow-serving:model-metadata
            parameters:
              modelName: half_plus_two
              modelVersion: 123
        - log:
            message: "Metadata: ${body.getMetadataOrThrow('signature_def')}"
```

Specify the model name and version with headers

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:model-metadata-with-headers")
    .setHeader("CamelTensorFlowServingModelName", constant("half_plus_two"))
    .setHeader("CamelTensorFlowServingModelVersion", constant(123))
    .to("tensorflow-serving:model-metadata")
    .log("Metadata: ${body.getMetadataOrThrow('signature_def')}");
```

```xml
<route>
  <from uri="direct:model-metadata-with-headers"/>
  <setHeader name="CamelTensorFlowServingModelName">
    <constant>half_plus_two</constant>
  </setHeader>
  <setHeader name="CamelTensorFlowServingModelVersion">
    <constant resultType="java.lang.Integer">123</constant>
  </setHeader>
  <to uri="tensorflow-serving:model-metadata"/>
  <log message="Metadata: ${body.getMetadataOrThrow('signature_def')}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:model-metadata-with-headers
      steps:
        - setHeader:
            name: CamelTensorFlowServingModelName
            constant: half_plus_two
        - setHeader:
            name: CamelTensorFlowServingModelVersion
            constant: 123
        - to:
            uri: tensorflow-serving:model-metadata
        - log:
            message: "Metadata: ${body.getMetadataOrThrow('signature_def')}"
```

### Classify API

The signature name should be resolved by looking up [the model metadata](#_model_metadata_api).

Classify

```java
from("direct:classify")
    .setBody(constant(InputOuterClass.Input.newBuilder()
        .setExampleList(InputOuterClass.ExampleList.newBuilder()
            .addExamples(Example.newBuilder()
                .setFeatures(Features.newBuilder()
                    .putFeature("x", Feature.newBuilder()
                        .setFloatList(FloatList.newBuilder().addValue(1.0f))
                        .build()))))
        .build()))
    .to("tensorflow-serving:classify?modelName=half_plus_two&modelVersion=123&signatureName=classify_x_to_y")
    .log("Result: ${body.result.getClassifications(0).getClasses(0).score}");
```

Specify the model and signature name with headers

```java
from("direct:classify-with-headers")
    .setBody(constant(InputOuterClass.Input.newBuilder()
        .setExampleList(InputOuterClass.ExampleList.newBuilder()
            .addExamples(Example.newBuilder()
                .setFeatures(Features.newBuilder()
                    .putFeature("x", Feature.newBuilder()
                        .setFloatList(FloatList.newBuilder().addValue(1.0f))
                        .build()))))
        .build()))
    .setHeader("CamelTensorFlowServingModelName", constant("half_plus_two"))
    .setHeader("CamelTensorFlowServingModelVersion", constant(123))
    .setHeader("CamelTensorFlowServingSignatureName", constant("classify_x_to_y"))
    .to("tensorflow-serving:classify")
    .log("Result: ${body.result.getClassifications(0).getClasses(0).score}");
```

### Regress API

The signature name should be resolved by looking up [the model metadata](#_model_metadata_api).

Regress

```java
from("direct:regress")
    .setBody(constant(InputOuterClass.Input.newBuilder()
        .setExampleList(InputOuterClass.ExampleList.newBuilder()
            .addExamples(Example.newBuilder()
                .setFeatures(Features.newBuilder()
                    .putFeature("x", Feature.newBuilder()
                        .setFloatList(FloatList.newBuilder().addValue(1.0f))
                        .build()))))
        .build()))
    .to("tensorflow-serving:regress?modelName=half_plus_two&modelVersion=123&signatureName=regress_x_to_y")
    .log("Result: ${body.result.getRegressions(0).value}");
```

Specify the model and signature name with headers

```java
from("direct:regress-with-headers")
    .setBody(constant(InputOuterClass.Input.newBuilder()
        .setExampleList(InputOuterClass.ExampleList.newBuilder()
            .addExamples(Example.newBuilder()
                .setFeatures(Features.newBuilder()
                    .putFeature("x", Feature.newBuilder()
                        .setFloatList(FloatList.newBuilder().addValue(1.0f))
                        .build()))))
        .build()))
    .setHeader("CamelTensorFlowServingModelName", constant("half_plus_two"))
    .setHeader("CamelTensorFlowServingModelVersion", constant(123))
    .setHeader("CamelTensorFlowServingSignatureName", constant("regress_x_to_y"))
    .to("tensorflow-serving:regress")
    .log("Result: ${body.result.getRegressions(0).value}");
```

### Predict API

The labels of inputs (`x`) and outputs (`y`) should be resolved by looking up [the model metadata](#_model_metadata_api).

Predict

```java
from("direct:predict")
    .setBody(constant(Predict.PredictRequest.newBuilder()
        .putInputs("x", TensorProto.newBuilder()
            .setDtype(DataType.DT_FLOAT)
            .setTensorShape(TensorShapeProto.newBuilder()
                .addDim(TensorShapeProto.Dim.newBuilder().setSize(3)))
            .addFloatVal(1.0f)
            .addFloatVal(2.0f)
            .addFloatVal(5.0f)
            .build())
        .build()))
    .to("tensorflow-serving:predict?modelName=half_plus_two&modelVersion=123")
    .log("Result1: ${body.getOutputsOrThrow('y').getFloatVal(0)}")
    .log("Result2: ${body.getOutputsOrThrow('y').getFloatVal(1)}")
    .log("Result3: ${body.getOutputsOrThrow('y').getFloatVal(2)}");
```

Specify the model name and version with headers

```java
from("direct:predict-with-headers")
    .setBody(constant(Predict.PredictRequest.newBuilder()
        .putInputs("x", TensorProto.newBuilder()
            .setDtype(DataType.DT_FLOAT)
            .setTensorShape(TensorShapeProto.newBuilder()
                .addDim(TensorShapeProto.Dim.newBuilder().setSize(3)))
            .addFloatVal(1.0f)
            .addFloatVal(2.0f)
            .addFloatVal(5.0f)
            .build())
        .build()))
    .setHeader("CamelTensorFlowServingModelName", constant("half_plus_two"))
    .setHeader("CamelTensorFlowServingModelVersion", constant(123))
    .to("tensorflow-serving:predict")
    .log("Result1: ${body.getOutputsOrThrow('y').getFloatVal(0)}")
    .log("Result2: ${body.getOutputsOrThrow('y').getFloatVal(1)}")
    .log("Result3: ${body.getOutputsOrThrow('y').getFloatVal(2)}");
```

* * *

[1](#_footnoteref_1). `tensorflow.serving.GetModelStatus.GetModelStatusRequest`

[2](#_footnoteref_2). `tensorflow.serving.GetModelStatus.GetModelStatusResponse`

[3](#_footnoteref_3). `tensorflow.serving.GetModelMetadata.GetModelMetadataRequest`

[4](#_footnoteref_4). `tensorflow.serving.GetModelMetadata.GetModelMetadataResponse`

[5](#_footnoteref_5). `tensorflow.serving.Classification.ClassificationRequest`

[6](#_footnoteref_6). `tensorflow.serving.InputOuterClass.Input`

[7](#_footnoteref_7). `tensorflow.serving.Classification.ClassificationResponse`

[8](#_footnoteref_8). `tensorflow.serving.RegressionOuterClass.RegressionRequest`

[9](#_footnoteref_9). `tensorflow.serving.InputOuterClass.Input`

[10](#_footnoteref_10). `tensorflow.serving.RegressionOuterClass.RegressionResponse`

[11](#_footnoteref_11). `tensorflow.serving.Predict.PredictRequest`

[12](#_footnoteref_12). `tensorflow.serving.Predict.PredictResponse`