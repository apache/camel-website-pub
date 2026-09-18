# ![telegram source](_images/kamelets/telegram-source.svg) Telegram Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive all messages that people send to your Telegram bot.

## Configuration Options

The following table summarizes the configuration options available for the `telegram-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **authorizationToken** | Token | **Required** The token to access your bot on Telegram. You can obtain it from the Telegram @botfather. | string |  |  |

## Dependencies

At runtime, the `telegram-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:telegram
    
-   camel:core
    

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
      uri: "kamelet:telegram-source"
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

## Telegram Source Kamelet Description

### Authentication

This Kamelet requires a Telegram Bot token for authentication. You need to create a Telegram bot through @BotFather and obtain the bot token.

### Configuration

The Telegram Source Kamelet supports the following configurations:

-   **Authorization Token**: Telegram bot token (required)
    
-   **Chat ID**: Telegram chat ID to monitor (optional, can monitor all chats if not specified)
    

### Output Format

The Kamelet outputs Telegram messages as JSON objects containing message content, sender information, chat details, and timestamp.

### Bot Setup

1.  Contact @BotFather on Telegram
    
2.  Create a new bot with /newbot command
    
3.  Follow the instructions to set bot name and username
    
4.  Copy the provided bot token
    
5.  Add the bot to your chat or channel
    

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:telegram-source"
      parameters:
        authorizationToken: "your-bot-token-here"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Specific Chat

```yaml
- route:
    from:
      uri: "kamelet:telegram-source"
      parameters:
        authorizationToken: "your-bot-token-here"
        chatId: "-1001234567890"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Message Processing

The kamelet receives all types of Telegram messages including text, photos, documents, and other media. Message metadata includes sender information, chat details, and message type.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/telegram-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/telegram-source.kamelet.yaml)