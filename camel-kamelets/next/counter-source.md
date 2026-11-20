# ![counter source](_images/kamelets/counter-source.svg) Counter Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends a message with a number that counts up by one, such as 1, 2, 3, at a regular interval.

Use it to try out a sink or an action with messages that are each different and easy to follow, or to make ordered test data. For the same fixed message every time use `timer-source`, and for a calendar schedule such as "every weekday at 9:00" use `cron-source`.

Output: the body is the number, as text, such as `42`. The `Content-Type` header is `text/plain`.

Good to know: it keeps sending until the integration is stopped, unless `numbers` is set. The count starts again from `start` when the integration restarts.

## Configuration Options

The following table summarizes the configuration options available for the `counter-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **numbers** | Number of Messages | How many messages to send in total. When it is not set, a message is sent every `period` until the integration is stopped. | integer |  | 10 |
| **period** | Period | How long to wait between two messages, in milliseconds. For example, 60000 is one minute. | integer | 1000 | 60000 |
| **start** | Start | The number in the first message. Each next message has a number one higher. | integer | 1 | 100 |

## Dependencies

At runtime, the `counter-source` Kamelet relies upon the presence of the following dependencies:

-   camel:timer
    
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
      uri: "kamelet:counter-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Counter Source Kamelet Description

This Kamelet provides a simple counting source that generates sequential numbers at configurable intervals. It starts from a specified number and counts upward (1, 2, 3, …​) with each timer tick.

### Output format

The Kamelet outputs each number as an `Integer` body (a whole number, not text), even though the `Content-Type` header is `text/plain`. Each message contains a single number that increments by one from the starting value.

### Special headers

The Kamelet sets the following header:

-   `Content-Type`: `text/plain`
    

### Configuration options

The Kamelet allows you to configure:

-   **period**: Time interval between numbers (default: 1000ms)
    
-   **start**: Starting number (default: 1)
    
-   **numbers**: Total count of numbers to generate (optional - if not set, runs indefinitely)
    

### Usage examples

Basic counter starting from 1:

```yaml
- route:
    from:
      uri: "kamelet:counter-source"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Counter with custom starting point and interval:

```yaml
- route:
    from:
      uri: "kamelet:counter-source"
      parameters:
        start: 100
        period: 500
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Generate exactly 10 numbers:

```yaml
- route:
    from:
      uri: "kamelet:counter-source"
      parameters:
        start: 1
        numbers: 10
        period: 2000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/counter-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/counter-source.kamelet.yaml)