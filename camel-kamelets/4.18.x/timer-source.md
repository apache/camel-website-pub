# ![timer source](_images/kamelets/timer-source.svg) Timer Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Produces periodic messages with a custom payload.

## Configuration Options

The following table summarizes the configuration options available for the `timer-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **message** | Message | **Required** The message to generate. | string |  | hello world |
| **contentType** | Content Type | The content type of the generated message. | string | text/plain |  |
| **period** | Period | The interval (in milliseconds) to wait between producing the next message. | integer | 1000 |  |
| **repeatCount** | Repeat Count | Specifies a maximum limit of number of fires. | integer |  |  |

## Dependencies

At runtime, the `timer-source` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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
      uri: "kamelet:timer-source"
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

## Timer Source Kamelet Description

This Kamelet produces periodic messages with a custom payload at configurable intervals. It’s useful for generating scheduled events or heartbeat messages.

### Output format

The Kamelet outputs the configured message with a specified content type. By default, it produces plain text messages.

### Special headers

The Kamelet sets the following header:

-   `Content-Type`: Configurable content type (default: `text/plain`)
    

### Configuration requirements

This Kamelet requires the following mandatory property:

-   **message**: The text message to generate
    

### Configuration options

-   **period**: Time interval between messages in milliseconds (default: 1000)
    
-   **message**: The message content to send (required)
    
-   **contentType**: MIME type of the message (default: `text/plain`)
    
-   **repeatCount**: Maximum number of messages to send (optional - if not set, runs indefinitely)
    

### Usage examples

Basic periodic message:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "hello world"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Custom interval and content type:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: '{"status": "heartbeat", "timestamp": "${date:now:yyyy-MM-dd HH:mm:ss}"}'
        contentType: "application/json"
        period: 30000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

Limited number of messages:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "Scheduled notification"
        period: 5000
        repeatCount: 10
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/timer-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/timer-source.kamelet.yaml)