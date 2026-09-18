# ![delay action](_images/kamelets/delay-action.svg) Delay Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Delay the processing using a specific amount of time

## Configuration Options

The following table summarizes the configuration options available for the `delay-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **milliseconds** | Milliseconds | **Required** The number of milliseconds of delay. | integer |  | 1000 |

## Dependencies

At runtime, the `delay-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:delay-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/delay-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/delay-action.kamelet.yaml)