# ![simple filter action](_images/kamelets/simple-filter-action.svg) Simple Filter Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Filter based on simple expression.

## Configuration Options

The following table summarizes the configuration options available for the `simple-filter-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **expression** | Simple Expression | **Required** A simple expression to apply on the exchange to filter out some exchange. | string |  |  |

## Dependencies

At runtime, the `simple-filter-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:simple-filter-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/simple-filter-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/simple-filter-action.kamelet.yaml)