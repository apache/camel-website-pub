# ![log sink](_images/kamelets/log-sink.svg) Log Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Writes each message it receives to the log, with its body and optionally its headers.

Use it to see what a source sends while you build or try out an integration, or to end a flow during a test without a real system behind it. To log in the middle of a flow and pass the message on, use `log-action`.

Input: any message, with any kind of body.

Output: the message is unchanged.

Good to know: by default the log line shows the body and its Java type, but not the headers. The body is logged as it is, secrets included, unless `logMask` is true.

## Configuration Options

The following table summarizes the configuration options available for the `log-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **level** | Log Level | The level to log at. Lines at a level below the one the logging is set to, such as `DEBUG` when the logging shows `INFO`, are not shown. `OFF` logs nothing. Enum values: \* TRACE \* DEBUG \* INFO \* WARN \* ERROR \* OFF | string | INFO |  |
| **logMask** | Log Mask | If true, values that look like secrets, such as what follows `password=` or a header named `token`, are replaced by `xxxxx` in the log. | boolean | false |  |
| **loggerName** | Logger Name | The name of the logger, shown on each log line. Use it to tell these log lines apart from others, or to set their level in the logging configuration. | string | log-sink | orders |
| **marker** | Marker | A logging marker to add to each log line, for logging setups that filter or send log lines by marker. When it is not set, no marker is added. | string |  | AUDIT |
| **multiline** | Multiline | If true, each part of the log line, such as the headers, the body type and the body, is written on a line of its own, which is easier to read for large messages. | boolean | false |  |
| **showAllProperties** | Show All Properties | If true, also logs all the properties Camel keeps with the message, including its internal ones. Mostly useful to Camel developers. | boolean | false |  |
| **showBody** | Show Body | If true, the body is logged. Set it to false for large bodies, or bodies that must not appear in the log. | boolean | true |  |
| **showBodyType** | Show Body Type | If true, the Java type of the body is logged, such as `String`, `byte[]` or `java.util.LinkedHashMap`, which shows what kind of body the next step receives. | boolean | true |  |
| **showCachedStreams** | Show Cached Streams | If true, a body that is a stream cached by Camel, which can be read again, is logged. Camel caches stream bodies by default, so this is the usual case. | boolean | true |  |
| **showExchangePattern** | Show Exchange Pattern | If true, the message pattern is logged: `InOnly` for a one-way message, `InOut` when a reply is expected. | boolean | true |  |
| **showHeaders** | Show Headers | If true, the headers of the message are logged too. | boolean | false |  |
| **showProperties** | Show Properties | If true, also logs the properties that the steps of the integration set on the message, but not Camel’s internal ones. Use `showAllProperties` to see those too. | boolean | false |  |
| **showStreams** | Show Streams | If true, a body that is a stream not cached by Camel is logged too. Logging reads such a stream, so the next step may then get an empty body. | boolean | false |  |

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