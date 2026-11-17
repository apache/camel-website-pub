# ![delay action](_images/kamelets/delay-action.svg) Delay Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Holds each message for a fixed time, such as one second, before passing it on.

Use it to slow down a flow, for example to give another system time to finish its work before the next step, or to space out the calls of a test. To limit how many messages pass per second or per minute, rather than holding each one, use `throttle-action`.

Input: any message.

Output: the same message, unchanged, after the wait.

## Configuration Options

The following table summarizes the configuration options available for the `delay-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **milliseconds** | Delay in Milliseconds | **Required** How long to hold each message, in milliseconds. For example, 1000 is one second. | integer |  | 1000 |

## Dependencies

At runtime, the `delay-action` Kamelet relies upon the presence of the following dependencies:

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