# Deep Java Library

**Since Camel 3.3**

**Only producer is supported**

The **Deep Java Library** component is used to infer Deep Learning models from message exchanges data. This component uses [Deep Java Library](https://djl.ai/) as underlying library.

In order to use the DJL component, Maven users will need to add the following dependency to their `pom.xml`:

**pom.xml**

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

The Deep Java Library component supports 2 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Deep Java Library endpoint is configured using URI syntax:

djl:application

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **application** (producer) | **Required** Application name. |  | String |

### Query Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **artifactId** (producer) | Model Artifact. |  | String |
| **model** (producer) | Model. |  | String |
| **translator** (producer) | Translator. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Model Zoo

The following table contains supported models in the model zoo:

     
| CV | Image Classification | Resnet image classification | `cv/image_classification` | `ai.djl.zoo:resnet:0.0.1` | {layers=50, flavor=v1, dataset=cifar10} |
| --- | --- | --- | --- | --- | --- |
| CV | Image Classification | MLP image classification | `cv/image_classification` | `ai.djl.zoo:mlp:0.0.2` | {dataset=mnist} |
| CV | Image Classification | MLP image classification | `cv/image_classification` | `ai.djl.mxnet:mlp:0.0.1` | {dataset=mnist} |
| CV | Image Classification | Resnet image classification | `cv/image_classification` | `ai.djl.mxnet:resnet:0.0.1` | {layers=18, flavor=v1, dataset=imagenet} |
| CV | Image Classification | Resnet image classification | `cv/image_classification` | `ai.djl.mxnet:resnet:0.0.1` | {layers=50, flavor=v2, dataset=imagenet} |
| CV | Image Classification | Resnet image classification | `cv/image_classification` | `ai.djl.mxnet:resnet:0.0.1` | {layers=152, flavor=v1d, dataset=imagenet} |
| CV | Image Classification | Resnet image classification | `cv/image_classification` | `ai.djl.mxnet:resnet:0.0.1` | {layers=50, flavor=v1, dataset=cifar10} |
| CV | Image Classification | Resnext image classification | `cv/image_classification` | `ai.djl.mxnet:resnext:0.0.1` | {layers=101, flavor=64x4d, dataset=imagenet} |
| CV | Image Classification | Senet image classification | `cv/image_classification` | `ai.djl.mxnet:senet:0.0.1` | {layers=154, dataset=imagenet} |
| CV | Image Classification | Senet and Resnext image classification | `cv/image_classification` | `ai.djl.mxnet:se_resnext:0.0.1` | {layers=101, flavor=32x4d, dataset=imagenet} |
| CV | Image Classification | Senet and Resnext image classification | `cv/image_classification` | `ai.djl.mxnet:se_resnext:0.0.1` | {layers=101, flavor=64x4d, dataset=imagenet} |
| CV | Image Classification | Squeezenet image classification | `cv/image_classification` | `ai.djl.mxnet:squeezenet:0.0.1` | {flavor=1.0, dataset=imagenet} |
| CV | Object Detection | Single Shot Detection for Object Detection | `cv/object_detection` | `ai.djl.zoo:ssd:0.0.1` | {flavor=tiny, dataset=pikachu} |
| CV | Object Detection | Single-shot object detection | `cv/object_detection` | `ai.djl.mxnet:ssd:0.0.1` | {size=512, backbone=resnet50, flavor=v1, dataset=voc} |
| CV | Object Detection | Single-shot object detection | `cv/object_detection` | `ai.djl.mxnet:ssd:0.0.1` | {size=512, backbone=vgg16, flavor=atrous, dataset=coco} |
| CV | Object Detection | Single-shot object detection | `cv/object_detection` | `ai.djl.mxnet:ssd:0.0.1` | {size=512, backbone=mobilenet1.0, dataset=voc} |
| CV | Object Detection | Single-shot object detection | `cv/object_detection` | `ai.djl.mxnet:ssd:0.0.1` | {size=300, backbone=vgg16, flavor=atrous, dataset=voc} |

## DJL Engine implementation

Because DJL is deep learning framework agnostic, you don’t have to make a choice between frameworks when creating your projects. You can switch frameworks at any point. To ensure the best performance, DJL also provides automatic CPU/GPU choice based on hardware configuration.

### MxNet engine

You can pull the MXNet engine from the central Maven repository by including the following dependency:

```xml
<dependency>
    <groupId>ai.djl.mxnet</groupId>
    <artifactId>mxnet-engine</artifactId>
    <version>x.x.x</version>
    <scope>runtime</scope>
</dependency>
```

DJL offers an automatic option that will download the jars the first time you run DJL. It will automatically determine the appropriate jars for your system based on the platform and GPU support.

```xml
    <dependency>
      <groupId>ai.djl.mxnet</groupId>
      <artifactId>mxnet-native-auto</artifactId>
      <version>1.7.0-a</version>
      <scope>runtime</scope>
    </dependency>
```

More information about [MxNet engine installation](https://docs.djl.ai/engines/mxnet/index.md)

### PyTorch engine

You can pull the PyTorch engine from the central Maven repository by including the following dependency:

```xml
<dependency>
    <groupId>ai.djl.pytorch</groupId>
    <artifactId>pytorch-engine</artifactId>
    <version>x.x.x</version>
    <scope>runtime</scope>
</dependency>
```

DJL offers an automatic option that will download the jars the first time you run DJL. It will automatically determine the appropriate jars for your system based on the platform and GPU support.

```xml
    <dependency>
      <groupId>ai.djl.pytorch</groupId>
      <artifactId>pytorch-native-auto</artifactId>
      <version>1.5.0</version>
      <scope>runtime</scope>
    </dependency>
```

More information about [PyTorch engine installation](https://docs.djl.ai/engines/pytorch/index.md)

### Tensorflow engine

You can pull the Tensorflow engine from the central Maven repository by including the following dependency:

```xml
<dependency>
    <groupId>ai.djl.tensorflow</groupId>
    <artifactId>tensorflow-engine</artifactId>
    <version>x.x.x</version>
    <scope>runtime</scope>
</dependency>
```

DJL offers an automatic option that will download the jars the first time you run DJL. It will automatically determine the appropriate jars for your system based on the platform and GPU support.

```xml
    <dependency>
      <groupId>ai.djl.tensorflow</groupId>
      <artifactId>tensorflow-native-auto</artifactId>
      <version>2.1.0</version>
      <scope>runtime</scope>
    </dependency>
```

More information about [Tensorflow engine installation](https://docs.djl.ai/engines/tensorflow/index.md)

## Examples

### MNIST image classification from file

```java
from("file:/data/mnist/0/10.png")
    .to("djl:cv/image_classification?artifactId=ai.djl.mxnet:mlp:0.0.1");
```

### Object detection

```java
from("file:/data/mnist/0/10.png")
    .to("djl:cv/image_classification?artifactId=ai.djl.mxnet:mlp:0.0.1");
```

### Custom deep learning model

```java
// create deep learning model
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

## Spring Boot Auto-Configuration

When using djl with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-djl-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 3 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.djl.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.djl.enabled** | Whether to enable auto configuration of the djl component. This is enabled by default. |  | Boolean |
| **camel.component.djl.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |