# ![data type action](_images/kamelets/data-type-action.svg) Data Type Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Applies a given data type with respective data transformation.

## Configuration Options

The following table summarizes the configuration options available for the `data-type-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **format** | Data Type Format | **Required** Defines the data type that is applied by this action. Apache Camel and the Kamelet catalog support different data types and performs automatic message conversion according to the given type. | string |  |  |
| **scheme** | Component Scheme | The data type component scheme enables users to apply Camel component specific data type conversions. | string |  |  |

## Dependencies

At runtime, the `data-type-action` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:core
    

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
            uri: "kamelet:data-type-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/data-type-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/data-type-action.kamelet.yaml)