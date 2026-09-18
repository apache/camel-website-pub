# ![insert header action](_images/kamelets/insert-header-action.svg) Insert Header Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Adds an header with a simple language parsed expression to the message in transit.

## Configuration Options

The following table summarizes the configuration options available for the `insert-header-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **name** | Name | **Required** The name of the header to be added. For Knative only, the name of the header requires a CloudEvent (ce-) prefix. | string |  | headername |
| **value** | Value | **Required** The value of the header to be added. | string |  |  |

## Dependencies

At runtime, the `insert-header-action` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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
            uri: "kamelet:insert-header-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/insert-header-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/insert-header-action.kamelet.yaml)