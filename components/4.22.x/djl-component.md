# Deep Java Library

**Since Camel 3.3**

**Only producer is supported**

The **Deep Java Library** component is used to infer deep learning models from message exchanges data. This component uses the [Deep Java Library](https://djl.ai/) as the underlying library.

To use the DJL component, Maven users will need to add the following dependency to their `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-djl</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

djl:application

Where `application` represents the [application](https://javadoc.io/doc/ai.djl/api/latest/ai/djl/Application.md) in the context of DJL, the common functional signature for a group of deep learning models.

### Supported applications

Currently, the component supports the following applications.

  
| Application | Input types | Output type |
| --- | --- | --- |
| `cv/image_classification` | `ai.djl.modality.cv.Image   byte[]   InputStream   File` | `ai.djl.modality.Classifications` |
| `cv/object_detection` | `ai.djl.modality.cv.Image   byte[]   InputStream   File` | `ai.djl.modality.cv.output.DetectedObjects` |
| `cv/semantic_segmentation` | `ai.djl.modality.cv.Image   byte[]   InputStream   File` | `ai.djl.modality.cv.output.CategoryMask` |
| `cv/instance_segmentation` | `ai.djl.modality.cv.Image   byte[]   InputStream   File` | `ai.djl.modality.cv.output.DetectedObjects` |
| `cv/pose_estimation` | `ai.djl.modality.cv.Image   byte[]   InputStream   File` | `ai.djl.modality.cv.output.Joints` |
| `cv/action_recognition` | `ai.djl.modality.cv.Image   byte[]   InputStream   File` | `ai.djl.modality.Classifications` |
| `cv/word_recognition` | `ai.djl.modality.cv.Image   byte[]   InputStream   File` | `String` |
| `cv/image_generation` | `int[]` | `ai.djl.modality.cv.Image[]` |
| `cv/image_enhancement` | `ai.djl.modality.cv.Image   byte[]   InputStream   File` | `ai.djl.modality.cv.Image` |
| `nlp/fill_mask` | `String` | `String[]` |
| `nlp/question_answer` | `ai.djl.modality.nlp.qa.QAInput   String[]` | `String` |
| `nlp/text_classification` | `String` | `ai.djl.modality.Classifications` |
| `nlp/sentiment_analysis` | `String` | `ai.djl.modality.Classifications` |
| `nlp/token_classification` | `String` | `ai.djl.modality.Classifications` |
| `nlp/text_generation` | `String` | `String` |
| `nlp/machine_translation` | `String` | `String` |
| `nlp/multiple_choice` | `String` | `String` |
| `nlp/text_embedding` | `String` | `ai.djl.ndarray.NDArray` |
| `audio` | `ai.djl.modality.audio.Audio   byte[]   InputStream   File` | `String` |
| `timeseries/forecasting` | `ai.djl.timeseries.TimeSeriesData` | `ai.djl.timeseries.Forecast` |

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

The Deep Java Library component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Deep Java Library endpoint is configured using URI syntax:

djl:application

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **application** (producer) | **Required** Application name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **artifactId** (producer) | Model Artifact. |  | String |
| **model** (producer) | Model. |  | String |
| **showProgress** (producer) | Show progress while loading zoo models. This parameter takes effect only with zoo models. | false | boolean |
| **translator** (producer) | Translator. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Deep Java Library component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDjlInput** (producer) Constant: [`INPUT`](https://javadoc.io/doc/org.apache.camel/camel-djl/latest/org/apache/camel/component/djl/DJLConstants.html#INPUT) | The input data used for prediction. |  |  |
| **CamelDjlFileType** (producer) Constant: [`FILE_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-djl/latest/org/apache/camel/component/djl/DJLConstants.html#FILE_TYPE) | The file type of the message body data. It is used when the body is converted to bytes. |  |  |

## Usage

### Model Zoo

The following tables contain supported models in the model zoos per application.

> **Note**
> Those applications without a table mean that there are no pre-trained models found for them from the basic, PyTorch, TensorFlow or MXNet DJL model zoos. You may still find more models for an application from other model zoos such as Hugging Face, ONNX, etc.

#### CV - Image Classification

Application: `cv/image_classification`

  
| Model family | Artifact ID | Options |
| --- | --- | --- |
| MLP | `ai.djl.zoo:mlp:0.0.3` | {dataset=mnist} |
| MLP | `ai.djl.mxnet:mlp:0.0.1` | {dataset=mnist} |
| ResNet | `ai.djl.zoo:resnet:0.0.2` | {layers=50, flavor=v1, dataset=cifar10} |
| ResNet | `ai.djl.pytorch:resnet:0.0.1` | {layers=50, dataset=imagenet}  
{layers=18, dataset=imagenet}  
{layers=101, dataset=imagenet} |
| ResNet | `ai.djl.tensorflow:resnet:0.0.1` | {flavor=v1, layers=50, dataset=imagenet} |
| ResNet | `ai.djl.mxnet:resnet:0.0.1` | {layers=18, flavor=v1, dataset=imagenet}  
{layers=50, flavor=v2, dataset=imagenet}  
{layers=101, dataset=imagenet}  
{layers=152, flavor=v1d, dataset=imagenet}  
{layers=50, flavor=v1, dataset=cifar10} |
| ResNet-18 | `ai.djl.pytorch:resnet18_embedding:0.0.1` | {} |
| SENet | `ai.djl.mxnet:senet:0.0.1` | {layers=154, dataset=imagenet} |
| SE-ResNeXt | `ai.djl.mxnet:se_resnext:0.0.1` | {layers=101, flavor=32x4d, dataset=imagenet}  
{layers=101, flavor=64x4d, dataset=imagenet} |
| ResNeSt | `ai.djl.mxnet:resnest:0.0.1` | {layers=14, dataset=imagenet}  
{layers=26, dataset=imagenet}  
{layers=50, dataset=imagenet}  
{layers=101, dataset=imagenet}  
{layers=200, dataset=imagenet}  
{layers=269, dataset=imagenet} |
| SqueezeNet | `ai.djl.mxnet:squeezenet:0.0.1` | {flavor=1.0, dataset=imagenet} |
| MobileNet | `ai.djl.tensorflow:mobilenet:0.0.1` | {flavor=v2, dataset=imagenet} |
| MobileNet | `ai.djl.mxnet:mobilenet:0.0.1` | {flavor=v1, multiplier=0.25, dataset=imagenet}  
{flavor=v1, multiplier=0.5, dataset=imagenet}  
{flavor=v1, multiplier=0.75, dataset=imagenet}  
{flavor=v1, multiplier=1.0, dataset=imagenet}  
{flavor=v2, multiplier=0.25, dataset=imagenet}  
{flavor=v2, multiplier=0.5, dataset=imagenet}  
{flavor=v2, multiplier=0.75, dataset=imagenet}  
{flavor=v2, multiplier=1.0, dataset=imagenet}  
{flavor=v3\_small, multiplier=1.0, dataset=imagenet}  
{flavor=v3\_large, multiplier=1.0, dataset=imagenet} |
| GoogLeNet | `ai.djl.mxnet:googlenet:0.0.1` | {dataset=imagenet} |
| Darknet | `ai.djl.mxnet:darknet:0.0.1` | {layers=53, flavor=v3, dataset=imagenet} |
| Inception v3 | `ai.djl.mxnet:inceptionv3:0.0.1` | {dataset=imagenet} |
| AlexNet | `ai.djl.mxnet:alexnet:0.0.1` | {dataset=imagenet} |
| VGGNet | `ai.djl.mxnet:vgg:0.0.1` | {layers=11, dataset=imagenet}  
{layers=13, dataset=imagenet}  
{layers=16, dataset=imagenet}  
{layers=19, dataset=imagenet}  
{flavor=batch\_norm, layers=11, dataset=imagenet}  
{flavor=batch\_norm, layers=13, dataset=imagenet}  
{flavor=batch\_norm, layers=16, dataset=imagenet}  
{flavor=batch\_norm, layers=19, dataset=imagenet} |
| DenseNet | `ai.djl.mxnet:densenet:0.0.1` | {layers=121, dataset=imagenet}  
{layers=161, dataset=imagenet}  
{layers=169, dataset=imagenet}  
{layers=201, dataset=imagenet} |
| Xception | `ai.djl.mxnet:xception:0.0.1` | {flavor=65, dataset=imagenet} |

#### CV - Object Detection

Application: `cv/object_detection`

  
| Model family | Artifact ID | Options |
| --- | --- | --- |
| SSD | `ai.djl.zoo:ssd:0.0.2` | {flavor=tiny, dataset=pikachu} |
| SSD | `ai.djl.pytorch:ssd:0.0.1` | {size=300, backbone=resnet50, dataset=coco} |
| SSD | `ai.djl.tensorflow:ssd:0.0.1` | {backbone=mobilenet\_v2, dataset=openimages\_v4} |
| SSD | `ai.djl.mxnet:ssd:0.0.1` | {size=512, backbone=resnet50, flavor=v1, dataset=voc}  
{size=512, backbone=vgg16, flavor=atrous, dataset=coco}  
{size=512, backbone=mobilenet1.0, dataset=voc}  
{size=300, backbone=vgg16, flavor=atrous, dataset=voc} |
| YOLO | `ai.djl.mxnet:yolo:0.0.1` | {dataset=voc, version=3, backbone=darknet53, imageSize=320}  
{dataset=voc, version=3, backbone=darknet53, imageSize=416}  
{dataset=voc, version=3, backbone=mobilenet1.0, imageSize=320}  
{dataset=voc, version=3, backbone=mobilenet1.0, imageSize=416}  
{dataset=coco, version=3, backbone=darknet53, imageSize=320}  
{dataset=coco, version=3, backbone=darknet53, imageSize=416}  
{dataset=coco, version=3, backbone=darknet53, imageSize=608}  
{dataset=coco, version=3, backbone=mobilenet1.0, imageSize=320}  
{dataset=coco, version=3, backbone=mobilenet1.0, imageSize=416}  
{dataset=coco, version=3, backbone=mobilenet1.0, imageSize=608} |
| YOLOv5 | `ai.djl.pytorch:yolo5s:0.0.1` | {} |
| YOLOv8 | `ai.djl.pytorch:yolov8n:0.0.1` | {} |

#### CV - Semantic Segmentation

Application: `cv/semantic_segmentation`

  
| Model family | Artifact ID | Options |
| --- | --- | --- |
| DeepLabV3 | `ai.djl.pytorch:deeplabv3:0.0.1` | {backbone=resnet50, flavor=v1b, dataset=coco} |

#### CV - Instance Segmentation

Application: `cv/instance_segmentation`

  
| Model family | Artifact ID | Options |
| --- | --- | --- |
| Mask R-CNN | `ai.djl.mxnet:mask_rcnn:0.0.1` | {backbone=resnet18, flavor=v1b, dataset=coco}  
{backbone=resnet101, flavor=v1d, dataset=coco} |

#### CV - Pose Estimation

Application: `cv/pose_estimation`

  
| Model family | Artifact ID | Options |
| --- | --- | --- |
| Simple Pose | `ai.djl.mxnet:simple_pose:0.0.1` | {backbone=resnet18, flavor=v1b, dataset=imagenet}  
{backbone=resnet50, flavor=v1b, dataset=imagenet}  
{backbone=resnet101, flavor=v1d, dataset=imagenet}  
{backbone=resnet152, flavor=v1b, dataset=imagenet}  
{backbone=resnet152, flavor=v1d, dataset=imagenet} |

#### CV - Action Recognition

Application: `cv/action_recognition`

  
| Model family | Artifact ID | Options |
| --- | --- | --- |
| Action Recognition | `ai.djl.mxnet:action_recognition:0.0.1` | {backbone=vgg16, dataset=ucf101}  
{backbone=inceptionv3, dataset=ucf101} |

#### CV - Image Generation

Application: `cv/image_generation`

  
| Model family | Artifact ID | Options |
| --- | --- | --- |
| CycleGAN | `ai.djl.pytorch:cyclegan:0.0.1` | {artist=cezanne}  
{artist=monet}  
{artist=ukiyoe}  
{artist=vangogh} |
| BigGAN | `ai.djl.pytorch:biggan-deep:0.0.1` | {layers=12, size=128, dataset=imagenet}  
{layers=24, size=256, dataset=imagenet}  
{layers=12, size=512, dataset=imagenet} |

#### NLP - Question Answer

Application: `nlp/question_answer`

  
| Model family | Artifact ID | Options |
| --- | --- | --- |
| BertQA | `ai.djl.pytorch:bertqa:0.0.1` | {modelType=distilbert, size=base, cased=false, dataset=SQuAD}  
{modelType=distilbert, size=base, cased=true, dataset=SQuAD}  
{backbone=bert, cased=false, dataset=SQuAD}  
{backbone=bert, cased=true, dataset=SQuAD}  
{backbone=distilbert, cased=true, dataset=SQuAD} |
| BertQA | `ai.djl.mxnet:bertqa:0.0.1` | {backbone=bert, dataset=book\_corpus\_wiki\_en\_uncased} |

#### NLP - Sentiment Analysis

Application: `nlp/sentiment_analysis`

  
| Model family | Artifact ID | Options |
| --- | --- | --- |
| DistilBERT | `ai.djl.pytorch:distilbert:0.0.1` | {backbone=distilbert, dataset=sst} |

#### Time Series - Forecasting

Application: `timeseries/forecasting`

  
| Model family | Artifact ID | Options |
| --- | --- | --- |
| DeepAR | `ai.djl.pytorch:deepar:0.0.1` | {dataset=m5forecast} |
| DeepAR | `ai.djl.mxnet:deepar:0.0.1` | {dataset=airpassengers}  
{dataset=m5forecast} |

### DJL Engine implementation

Because DJL is deep learning framework-agnostic, you don’t have to make a choice between frameworks when creating your projects. You can switch frameworks at any point. To ensure the best performance, DJL also provides automatic CPU/GPU choice based on hardware configuration.

#### PyTorch engine

You can pull the PyTorch engine from the central Maven repository by including the following dependency:

```xml
<dependency>
    <groupId>ai.djl.pytorch</groupId>
    <artifactId>pytorch-engine</artifactId>
    <version>x.x.x</version>
    <scope>runtime</scope>
</dependency>
```

By default, DJL will download the PyTorch native libraries into the [cache folder](https://docs.djl.ai/docs/development/cache_management.md) the first time you run DJL. It will automatically determine the appropriate jars for your system based on the platform and GPU support.

More information about [PyTorch engine installation](https://docs.djl.ai/engines/pytorch/index.md)

#### TensorFlow engine

You can pull the TensorFlow engine from the central Maven repository by including the following dependency:

```xml
<dependency>
    <groupId>ai.djl.tensorflow</groupId>
    <artifactId>tensorflow-engine</artifactId>
    <version>x.x.x</version>
    <scope>runtime</scope>
</dependency>
```

By default, DJL will download the TensorFlow native libraries into [cache folder](https://docs.djl.ai/docs/development/cache_management.md) the first time you run DJL. It will automatically determine the appropriate jars for your system based on the platform and GPU support.

More information about [TensorFlow engine installation](https://docs.djl.ai/engines/tensorflow/index.md)

#### MXNet engine

You can pull the MXNet engine from the central Maven repository by including the following dependency:

```xml
<dependency>
    <groupId>ai.djl.mxnet</groupId>
    <artifactId>mxnet-engine</artifactId>
    <version>x.x.x</version>
    <scope>runtime</scope>
</dependency>
```

By default, DJL will download the Apache MXNet native libraries into [cache folder](https://docs.djl.ai/docs/development/cache_management.md) the first time you run DJL. It will automatically determine the appropriate jars for your system based on the platform and GPU support.

More information about [MXNet engine installation](https://docs.djl.ai/engines/mxnet/index.md)

## Examples

MNIST image classification from file

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:/data/mnist/0/10.png")
    .to("djl:cv/image_classification?artifactId=ai.djl.mxnet:mlp:0.0.1");
```

```xml
<route>
  <from uri="file:/data/mnist/0/10.png"/>
  <to uri="djl:cv/image_classification?artifactId=ai.djl.mxnet:mlp:0.0.1"/>
</route>
```

```yaml
- route:
    from:
      uri: "file:/data/mnist/0/10.png"
      steps:
        - to:
            uri: djl:cv/image_classification
            parameters:
              artifactId: "ai.djl.mxnet:mlp:0.0.1"
```

Object detection

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:/data/mnist/0/10.png")
    .to("djl:cv/image_classification?artifactId=ai.djl.mxnet:mlp:0.0.1");
```

```xml
<route>
  <from uri="file:/data/mnist/0/10.png"/>
  <to uri="djl:cv/image_classification?artifactId=ai.djl.mxnet:mlp:0.0.1"/>
</route>
```

```yaml
- route:
    from:
      uri: "file:/data/mnist/0/10.png"
      steps:
        - to:
            uri: djl:cv/image_classification
            parameters:
              artifactId: "ai.djl.mxnet:mlp:0.0.1"
```

_Java-only: creating a custom DJL model with translator and binding to the registry_

```java
// create a deep learning model
Model model = Model.newInstance();
model.setBlock(new Mlp(28 * 28, 10, new int[]{128, 64}));
model.load(Paths.get(MODEL_DIR), MODEL_NAME);

// create translator for pre-processing and postprocessing
ImageClassificationTranslator.Builder builder = ImageClassificationTranslator.builder();
builder.setSynsetArtifactName("synset.txt");
builder.setPipeline(new Pipeline(new ToTensor()));
builder.optApplySoftmax(true);
ImageClassificationTranslator translator = new ImageClassificationTranslator(builder);

// Bind model and translator beans
context.getRegistry().bind("MyModel", model);
context.getRegistry().bind("MyTranslator", translator);

from("file:/data/mnist/0/10.png")
    .to("djl:cv/image_classification?model=MyModel&translator=MyTranslator");
```