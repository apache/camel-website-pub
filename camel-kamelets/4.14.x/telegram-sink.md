# ![telegram sink](_images/kamelets/telegram-sink.svg) Telegram Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send a message to a Telegram chat by using your Telegram bot as sender.

## Configuration Options

The following table summarizes the configuration options available for the `telegram-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **authorizationToken** | Token | **Required** The token to access your bot on Telegram. You you can obtain it from the Telegram @botfather. | string |  |  |
| **chatId** | Chat ID | The Chat ID to where you want to send messages by default. | string |  |  |

## Dependencies

At runtime, the `telegram-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:jackson
    
-   camel:kamelet
    
-   camel:telegram
    

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
            uri: "kamelet:telegram-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Telegram Sink Kamelet Description

### Telegram Bot Integration

This Kamelet integrates with Telegram’s Bot API, enabling automated message sending through Telegram bots to users, groups, or channels.

### Bot API Features

Telegram Bot API provides comprehensive messaging capabilities:

-   Text messages with rich formatting
    
-   Media sharing (photos, videos, documents)
    
-   Inline keyboards and custom keyboards
    
-   Location and contact sharing
    
-   Polls and quizzes
    

### Message Formatting

Supports Telegram’s message formatting options:

-   Markdown and HTML parsing
    
-   Bold, italic, and code formatting
    
-   Links and mentions
    
-   Emoji and stickers
    
-   Message threading and replies
    

### Delivery Options

Provides flexible message delivery:

-   Direct messages to users
    
-   Group chat messaging
    
-   Channel broadcasting
    
-   Silent notifications
    
-   Message scheduling and editing
    

### Bot Authentication

Uses Telegram bot tokens for authentication, providing secure API access while maintaining user privacy and platform security.

### Notification Use Cases

Common applications include:

-   System alerts and monitoring notifications
    
-   Customer support and engagement
    
-   News and content distribution
    
-   E-commerce order updates
    
-   IoT device status reporting
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/telegram-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/telegram-sink.kamelet.yaml)