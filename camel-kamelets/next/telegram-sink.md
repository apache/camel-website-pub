# ![telegram sink](_images/kamelets/telegram-sink.svg) Telegram Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message as a text message, or as a photo, from your Telegram bot to a Telegram chat, group or channel.

Use it to notify a person or a group on Telegram, for example with an alert, an order update or a daily report, or to answer the messages your bot receives with `telegram-source`.

Input: the body is the text of the message, as text; another kind of body is turned into text first, and the text is sent as it is, without Markdown or HTML formatting. When the `Content-Type` header is `image/png` or `image/jpeg`, the body is sent as a photo instead, as bytes, and the `text` or `ce-text` header is its caption. The `chat-id` or `ce-chatid` header chooses the chat, instead of the `chatId` option; `telegram-source` sets both, so a reply goes back to the chat a message came from.

Output: when it is used inside a route, the body afterwards is the answer of Telegram as JSON text, with the message that was sent.

Good to know: a message fails when no chat is given, neither in a header nor in `chatId`, and when Telegram refuses it, for example because the bot is not a member of the group or the person never started a chat with the bot.

## Configuration Options

The following table summarizes the configuration options available for the `telegram-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **authorizationToken** | Token | **Required** The token of your Telegram bot, such as `123456789:AAH…​`. Telegram gives it when you create the bot by talking to @BotFather in Telegram, with the command `/newbot`. | string |  |  |
| **chatId** | Chat ID | The chat to send to when the message has no `chat-id` or `ce-chatid` header. The ID of a person or group is a number (negative for a group); a public channel can also be given as `@` and its name. To learn the ID, send a message to the bot and read the `chat-id` header that `telegram-source` sets. | string |  | \-1001234567890 |

## Dependencies

At runtime, the `telegram-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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

This Kamelet integrates with Telegram’s Bot API, enabling automated message sending through a Telegram bot to users, groups, or channels.

### Bot Setup

1.  Contact @BotFather on Telegram
    
2.  Create a new bot with the `/newbot` command
    
3.  Follow the instructions to set the bot name and username
    
4.  Copy the bot token into `authorizationToken`
    
5.  Add the bot to the group or channel to send to. To send to a person, that person must first start a chat with the bot: a bot cannot start a conversation.
    

### What It Sends

The Kamelet sends two kinds of messages:

-   **Text messages**: by default, the body is sent as the text of the message, as it is. Markdown and HTML are not interpreted.
    
-   **Photos**: when the `Content-Type` header is `image/png` or `image/jpeg`, the body is sent as a photo, and the `text` (or `ce-text`) header becomes its caption.
    

### Choosing the Chat

The chat is taken, in this order, from the `chat-id` header, the `ce-chatid` header, and the `chatId` option. A message with none of them fails. The ID of a person or a group is a number, negative for a group; a public channel can also be written as `@channelname`.

To learn the ID of a chat, send a message to the bot and run `telegram-source`: it sets the `chat-id` header of each message it receives. For the same reason, a route from `telegram-source` to `telegram-sink` answers in the chat the message came from.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "Order 1234 has shipped."
        repeatCount: 1
      steps:
        - to:
            uri: "kamelet:telegram-sink"
            parameters:
              authorizationToken: "{{telegram.token}}"
              chatId: "123456789"
```

### Notification Use Cases

Common applications include:

-   System alerts and monitoring notifications
    
-   Customer support and engagement
    
-   News and content distribution
    
-   E-commerce order updates
    
-   IoT device status reporting
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/telegram-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/telegram-sink.kamelet.yaml)