# ![cron source](_images/kamelets/cron-source.svg) Cron Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends the same fixed message on a calendar schedule, written as a cron expression, such as every weekday at 9:00.

Use it to start a flow at set times, such as a report every morning or a clean-up every night. For a message every few seconds or minutes, `timer-source` is simpler, and for a message that counts up use `counter-source`.

Output: the body is the `message` option as text, the same on every message. The `Content-Type` header is `text/plain`, also when the message is JSON or XML. Headers about the schedule are set too, such as `fireTime` (the time of this message) and `nextFireTime`.

Good to know: the times are in the time zone of the machine it runs on. It keeps sending until the integration is stopped.

## Configuration Options

The following table summarizes the configuration options available for the `cron-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **message** | Message | **Required** The body of every message, sent as text exactly as written. | string |  | hello world |
| **schedule** | Cron Schedule | **Required** When to send a message, as a Quartz cron expression of six or seven fields: seconds, minutes, hours, day of month, month, day of week, and an optional year. For example, `0 0 9 ? * MON-FRI` is 9:00 every weekday, and `0 */5 * * * ?` is every five minutes. A Unix cron expression of five fields, without the seconds, works too. | string |  | 0 0 9 ? \* MON-FRI |

## Dependencies

At runtime, the `cron-source` Kamelet relies upon the presence of the following dependencies:

-   camel:quartz
    
-   camel:cron
    
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
      uri: "kamelet:cron-source"
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

## Cron Source Kamelet Description

This Kamelet provides a cron-based scheduler that sends events at specific times defined by a cron expression. It allows you to generate custom messages according to a cron schedule.

### Output format

The Kamelet outputs the configured message as plain text content at the times specified by the cron expression.

### Configuration requirements

This Kamelet requires the following mandatory properties:

-   **schedule**: A cron expression that defines when events should be triggered
    
-   **message**: The text message to send when the schedule triggers
    

### Cron expression format

The cron expression follows the Quartz format, with the seconds first (a Unix cron expression of five fields, without the seconds, works too):

```none
<seconds> <minutes> <hours> <day-of-month> <month> <day-of-week> [year]
```

### Usage examples

Send a message every 3 seconds during minute 10 of every hour:

```yaml
- route:
    from:
      uri: "kamelet:cron-source"
      parameters:
        schedule: "0/3 10 * * * ?"
        message: "hello world"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Send a daily reminder at 9 AM:

```yaml
- route:
    from:
      uri: "kamelet:cron-source"
      parameters:
        schedule: "0 0 9 * * ?"
        message: "Daily reminder: Check your tasks!"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Send a message every Monday at 8:30 AM:

```yaml
- route:
    from:
      uri: "kamelet:cron-source"
      parameters:
        schedule: "0 30 8 ? * MON"
        message: "Weekly team meeting reminder"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/cron-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/cron-source.kamelet.yaml)