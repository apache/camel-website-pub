# ![throttle action](_images/kamelets/throttle-action.svg) Throttle Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Lets through at most a set number of messages per period of time, such as 10 per second, and holds back the rest for a later period.

Use it to protect a sink or a service that cannot take more than a certain rate, for example an API that allows 100 calls per minute. To hold every message for a fixed time instead, use `delay-action`.

Input: any message.

Output: the same message, unchanged. The messages over the limit are not dropped: they wait, and are passed on in a later period.

## Configuration Options

The following table summarizes the configuration options available for the `throttle-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **messages** | Message Limit | **Required** How many messages may pass in each `timePeriod`. For example, 10 with a `timePeriod` of 1000 lets 10 messages through per second. | integer |  | 10 |
| **timePeriod** | Time Period | The length of the period that `messages` counts in, in milliseconds. For example, 60000 is one minute. | string | 1000 | 60000 |

## Dependencies

At runtime, the `throttle-action` Kamelet relies upon the presence of the following dependencies:

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