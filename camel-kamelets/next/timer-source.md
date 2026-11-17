# ![timer source](_images/kamelets/timer-source.svg) Timer Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends the same fixed message again and again at a regular interval, such as once every second.

Use it to try out a sink or an action without a real system behind it, to trigger a flow on a schedule (for example, call an HTTP service every minute), or to send a heartbeat. For a calendar schedule such as "every weekday at 9:00" use `cron-source` instead, and for a message that counts up use `counter-source`.

Output: the body is the `message` option as text, the same on every message. The `Content-Type` header is set to the `contentType` option.

Good to know: it keeps sending until the integration is stopped, unless `repeatCount` is set.

## Configuration Options

The following table summarizes the configuration options available for the `timer-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **message** | Message | **Required** The body of every message, sent as text exactly as written. To send JSON, write the JSON here and set `contentType` to `application/json`. | string |  | hello world |
| **contentType** | Content Type | The value of the `Content-Type` header on every message, which tells the next step what kind of text the body is. | string | text/plain | application/json |
| **period** | Period | How long to wait between two messages, in milliseconds. For example, 60000 is one minute. | integer | 1000 | 60000 |
| **repeatCount** | Repeat Count | How many messages to send in total. When it is not set, a message is sent every `period` until the integration is stopped. | integer |  | 10 |

## Dependencies

At runtime, the `timer-source` Kamelet relies upon the presence of the following dependencies:

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