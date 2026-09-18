# ![log sink](_images/kamelets/log-sink.svg) Log Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

A sink that logs all data that it receives, useful for debugging purposes.

## Configuration Options

The following table summarizes the configuration options available for the `log-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **level** | Log Level | Logging level to use. Enum values: \* TRACE \* DEBUG \* INFO \* WARN \* ERROR \* OFF | string | INFO |  |
| **logMask** | Log Mask | Mask sensitive information like password or passphrase in the log. | boolean | false |  |
| **loggerName** | Logger Name | Name of the logging category to use. | string | log-sink |  |
| **marker** | Marker | An optional Marker name to use. | string |  |  |
| **multiline** | Multiline | If enabled then each information is outputted on a newline. | boolean | false |  |
| **showAllProperties** | Show All Properties | Show all of the exchange properties (both internal and custom). | boolean | false |  |
| **showBody** | Show Body | Show the message body. | boolean | true |  |
| **showBodyType** | Show Body Type | Show the body Java type. | boolean | true |  |
| **showCachedStreams** | Show Cached Streams | Whether Camel should show cached stream bodies or not. | boolean | true |  |
| **showExchangePattern** | Show Exchange Pattern | Shows the Message Exchange Pattern (or MEP for short). | boolean | true |  |
| **showHeaders** | Show Headers | Show the headers received. | boolean | false |  |
| **showProperties** | Show Properties | Show the exchange properties (only custom). Use showAllProperties to show both internal and custom properties. | boolean | false |  |
| **showStreams** | Show Streams | Show the stream bodies (they may not be available in following steps). | boolean | false |  |

## Dependencies

At runtime, the `log-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:kamelet
    
-   camel:log
    

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
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Log Sink Kamelet Description

### Debugging and Monitoring

This Kamelet is designed for debugging purposes, logging all data it receives to help developers monitor and troubleshoot data flows.

### Log Levels

Supports standard logging levels: TRACE, DEBUG, INFO (default), WARN, ERROR, and OFF.

### Configuration Options

-   **Logger Name**: Custom logging category (defaults to "log-sink")
    
-   **Log Level**: Controls verbosity of logging output
    
-   **Log Mask**: Masks sensitive information like passwords
    
-   **Marker**: Optional marker name for log categorization
    

### Display Options

Extensive customization for what information to display: - **Message Body**: Show/hide message content (default: true) - **Headers**: Display message headers (default: false) - **Properties**: Show exchange properties - **Body Type**: Display Java type information - **Exchange Pattern**: Show Message Exchange Pattern (MEP) - **Streams**: Handle stream body display - **Multiline**: Format output across multiple lines

### Usage

Ideal for development, testing, and production monitoring to understand data flow and diagnose issues in integration pipelines.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/log-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/log-sink.kamelet.yaml)