# ![throttle action](_images/kamelets/throttle-action.svg) Throttle Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

The Throttle action allows you to ensure that a specific sink does not get overloaded.

## Configuration Options

The following table summarizes the configuration options available for the `throttle-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **messages** | Messages Number | **Required** The number of messages to send in the time period set. | integer |  | 10 |
| **timePeriod** | Time Period | Sets the time period during which the maximum request count is valid for, in milliseconds. | string | 1000 |  |

## Dependencies

At runtime, the `throttle-action` Kamelet relies upon the presence of the following dependencies:

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
            uri: "kamelet:throttle-action"
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

[https://github.com/apache/camel-kamelets/blob/main/kamelets/throttle-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/throttle-action.kamelet.yaml)