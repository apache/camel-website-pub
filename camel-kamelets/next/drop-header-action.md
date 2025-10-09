# ![drop header action](_images/kamelets/drop-header-action.svg) Drop Header Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Remove an header from the message in transit.

## Configuration Options

The following table summarizes the configuration options available for the `drop-header-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **name** | Name | **Required** The name of the header to be removed. | string |  | headername |

## Dependencies

At runtime, the `drop-header-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:drop-header-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/drop-header-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/drop-header-action.kamelet.yaml)