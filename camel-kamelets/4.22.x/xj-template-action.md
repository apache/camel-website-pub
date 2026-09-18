# ![xj template action](_images/kamelets/xj-template-action.svg) XJ Template Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Apply the XJ Template Transformation to transform JSON to XML and XML to JSON.

## Configuration Options

The following table summarizes the configuration options available for the `xj-template-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **direction** | Direction | **Required** The transform direction. Enum values: \* XML2JSON \* JSON2XML | string |  |  |
| **template** | Template | **Required** The inline template to apply a transformation through template. | string |  | file:////template.vm |

## Dependencies

At runtime, the `xj-template-action` Kamelet relies upon the presence of the following dependencies:

-   camel:xj
    
-   camel:kamelet
    

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
            uri: "kamelet:xj-template-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/xj-template-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/xj-template-action.kamelet.yaml)