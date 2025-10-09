# ![counter source](_images/kamelets/counter-source.svg) Counter Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Generates sequential number events starting from a configurable value, incrementing by a specified step. Useful for testing, scheduled tasks, or creating ordered event sequences.

## Configuration Options

The following table summarizes the configuration options available for the `counter-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **numbers** | Numbers | How many numbers to generate. | integer |  |  |
| **period** | Period | The time interval between two numbers. | integer | 1000 |  |
| **start** | Starting Number | The starting number. | integer | 1 |  |

## Dependencies

At runtime, the `counter-source` Kamelet relies upon the presence of the following dependencies:

-   camel:timer
    
-   camel:core
    
-   camel:bean
    
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

The Kamelet outputs each number as a plain text integer. Each message contains a single number that increments from the starting value.

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