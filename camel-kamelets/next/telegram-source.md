# ![telegram source](_images/kamelets/telegram-source.svg) Telegram Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the messages that people send to your Telegram bot, in private chats and in the groups the bot is in, one message per Telegram message.

Use it to build a chat bot, for example to answer questions, take orders or run commands sent on Telegram; send the answers with `telegram-sink`.

Output: the body is the Telegram message as JSON text, with fields such as `text` (what was written), `chat` (with the `id` of the chat), `from` (the sender) and `message_id`. A photo or a document comes without `text`. The `chat-id` and `ce-chatid` headers hold the ID of the chat, so that `telegram-sink` can answer in the same chat.

Good to know: it asks Telegram for new messages all the time, and each message is received once. Telegram keeps the messages that arrive while the Kamelet is stopped for up to 24 hours. It does not work while a webhook is set for the bot, and only one application at a time can read the messages of a bot. In a group, Telegram gives a bot only the commands and the replies to the bot, unless its privacy mode is turned off with @BotFather.

## Configuration Options

The following table summarizes the configuration options available for the `telegram-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **authorizationToken** | Token | **Required** The token of your Telegram bot, such as `123456789:AAH…​`. Telegram gives it when you create the bot by talking to @BotFather in Telegram, with the command `/newbot`. | string |  |  |

## Dependencies

At runtime, the `telegram-source` Kamelet relies upon the presence of the following dependencies:

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

The Telegram Source Kamelet has one option:

-   **Authorization Token**: Telegram bot token (required)
    

It receives the messages of every chat the bot is in. To keep only the messages of one chat, filter on the `chat-id` header.

### Output Format

The Kamelet outputs each Telegram message as JSON text, with the content of the message (`text`), the sender (`from`), the chat (`chat`) and the time (`date`). The `chat-id` and `ce-chatid` headers hold the ID of the chat.

### Bot Setup

1.  Contact @BotFather on Telegram
    
2.  Create a new bot with the `/newbot` command
    
3.  Follow the instructions to set bot name and username
    
4.  Copy the provided bot token
    
5.  Add the bot to your chat or channel. In a group, the bot receives only commands and replies to it, unless you turn its privacy mode off with the `/setprivacy` command of @BotFather.
    

The Kamelet asks Telegram for new messages with long polling. It does not work while a webhook is set for the bot, and only one application at a time can read the messages of a bot.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:telegram-source"
      parameters:
        authorizationToken: "{{telegram.token}}"
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
        authorizationToken: "{{telegram.token}}"
      steps:
        - filter:
            simple: "${header[chat-id]} == '-1001234567890'"
            steps:
              - to:
                  uri: "kamelet:log-sink"
```

### Message Processing

The kamelet receives all types of Telegram messages including text, photos, documents, and other media. A message without text, such as a photo, has no `text` field.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/telegram-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/telegram-source.kamelet.yaml)