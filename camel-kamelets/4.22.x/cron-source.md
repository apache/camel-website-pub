# ![cron source](_images/kamelets/cron-source.svg) Cron Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send events at specific time.

## Configuration Options

The following table summarizes the configuration options available for the `cron-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **message** | Message | **Required** The message to generate. | string |  | hello world |
| **schedule** | Cron Schedule | **Required** A cron expression that is used to trigger events generation. | string |  | 0/3 10 \* \* \* ? |

## Dependencies

At runtime, the `cron-source` Kamelet relies upon the presence of the following dependencies:

-   camel:quartz
    
-   camel:core
    
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

The cron expression follows the standard format:

```none
<seconds> <minutes> <hours> <day-of-month> <month> <day-of-week> [year]
```

### Usage examples

Send a message every 3 seconds during the 10th hour:

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