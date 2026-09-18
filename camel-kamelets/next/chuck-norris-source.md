# ![chuck norris source](_images/kamelets/chuck-norris-source.svg) Chuck Norris Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Gets periodically Chuck Norris jokes

## Configuration Options

The following table summarizes the configuration options available for the `chuck-norris-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **period** | Period | The interval (msec) to wait before getting the next joke. | integer | 10000 |  |

## Dependencies

At runtime, the `chuck-norris-source` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:timer
    
-   camel:http
    
-   camel:jsonpath
    

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
      uri: "kamelet:chuck-norris-source"
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

## Chuck Norris Source Kamelet Description

This Kamelet provides a periodic source of Chuck Norris jokes from the Chuck Norris API. It fetches random jokes at configurable intervals and outputs them as plain text.

### Output format

The Kamelet outputs Chuck Norris jokes as plain text strings, one joke per message. The jokes are extracted from the JSON response using JSONPath to get the `value` field from the API response.

### Usage examples

Basic usage with default 10-second interval:

```yaml
- route:
    from:
      uri: "kamelet:chuck-norris-source"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Custom interval of 30 seconds:

```yaml
- route:
    from:
      uri: "kamelet:chuck-norris-source"
      parameters:
        period: 30000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/chuck-norris-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/chuck-norris-source.kamelet.yaml)