# ![djl image to text action](_images/kamelets/djl-image-to-text-action.svg) Image-to-Text Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Detect and classify objects in an image into texts using the SSD and ResNet models and the ImageNet dataset.

## Configuration Options

The `djl-image-to-text-action` Kamelet does not specify any configuration options.

## Dependencies

At runtime, the `djl-image-to-text-action` Kamelet relies upon the presence of the following dependencies:

-   mvn:ai.djl.pytorch:pytorch-engine:0.29.0
    
-   mvn:ai.djl.pytorch:pytorch-model-zoo:0.29.0
    
-   camel:core
    
-   camel:kamelet
    
-   camel:jackson
    
-   camel:djl
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:djl-image-to-text-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/djl-image-to-text-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/djl-image-to-text-action.kamelet.yaml)