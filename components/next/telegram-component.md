# Telegram

**Since Camel 2.18**

**Both producer and consumer are supported**

The Telegram component provides access to the [Telegram Bot API](https://core.telegram.org/bots/api). It allows a Camel-based application to send and receive messages by acting as a Bot, participating in direct conversations with normal users, private and public groups or channels.

A Telegram Bot must be created before using this component, following the instructions at the [Telegram Bot developers home](https://core.telegram.org/bots#3-how-do-i-create-a-bot). When a new Bot is created, the [BotFather](https://telegram.me/botfather) provides an **authorization token** corresponding to the Bot. The authorization token is a mandatory parameter for the camel-telegram endpoint.

> **Note**
> To allow the Bot to receive all messages exchanged within a group or channel (not just the ones starting with a '/' character), ask the BotFather to **disable the privacy mode**, using the **/setprivacy** command.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-telegram</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

telegram:type\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The Telegram component supports 8 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **baseUri** (advanced) | Can be used to set an alternative base URI, e.g. when you want to test the component against a mock Telegram API. | [https://api.telegram.org](https://api.telegram.org) | String |
| **client** (advanced) | To use a custom java.net.http.HttpClient. |  | HttpClient |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **authorizationToken** (security) | The default Telegram authorization token to be used when the information is not provided in the endpoints. |  | String |

## Endpoint Options

The Telegram endpoint is configured using URI syntax:

telegram:type

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **type** (common) | 
**Required** The endpoint type. Currently, only the 'bots' type is supported.

Enum values:

-   bots
    





 |  | String |

### Query Parameters (30 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **limit** (consumer) | Limit on the number of updates that can be received in a single polling request. | 100 | Integer |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **timeout** (consumer) | Timeout in seconds for long polling. Put 0 for short polling or a bigger number for long polling. Long polling produces shorter response time. | 30 | Integer |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 
Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **chatId** (producer) | The identifier of the chat that will receive the produced messages. Chat ids can be first obtained from incoming messages (eg. when a telegram user starts a conversation with a bot, its client sends automatically a '/start' message containing the chat id). It is an optional parameter, as the chat id can be set dynamically for each outgoing message (using body or headers). |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **baseUri** (advanced) | Can be used to set an alternative base URI, e.g. when you want to test the component against a mock Telegram API. |  | String |
| **bufferSize** (advanced) | The initial in-memory buffer size used when transferring data between Camel and AHC Client. | 1048576 | int |
| **client** (advanced) | To use a custom HttpClient. |  | HttpClient |
| **proxyHost** (proxy) | HTTP proxy host which could be used when sending out the message. |  | String |
| **proxyPort** (proxy) | HTTP proxy port which could be used when sending out the message. |  | Integer |
| **proxyType** (proxy) | 

HTTP proxy type which could be used when sending out the message.

Enum values:

-   HTTP
    
-   SOCKS4
    
-   SOCKS5
    





 | HTTP | TelegramProxyType |
| **backoffErrorThreshold** (scheduler) | The number of subsequent error polls (failed due some error) that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffIdleThreshold** (scheduler) | The number of subsequent idle polls that should happen before the backoffMultipler should kick-in. |  | int |
| **backoffMultiplier** (scheduler) | To let the scheduled polling consumer backoff if there has been a number of subsequent idles/errors in a row. The multiplier is then the number of polls that will be skipped before the next actual attempt is happening again. When this option is in use then backoffIdleThreshold and/or backoffErrorThreshold must also be configured. |  | int |
| **delay** (scheduler) | Milliseconds before the next poll. | 500 | long |
| **greedy** (scheduler) | If greedy is enabled, then the ScheduledPollConsumer will run immediately again, if the previous run polled 1 or more messages. | false | boolean |
| **initialDelay** (scheduler) | Milliseconds before the first poll starts. | 1000 | long |
| **repeatCount** (scheduler) | Specifies a maximum limit of number of fires. So if you set it to 1, the scheduler will only fire once. If you set it to 5, it will only fire five times. A value of zero or negative means fire forever. | 0 | long |
| **runLoggingLevel** (scheduler) | 

The consumer logs a start/complete log line when it polls. This option allows you to configure the logging level for that.

Enum values:

-   TRACE
    
-   DEBUG
    
-   INFO
    
-   WARN
    
-   ERROR
    
-   OFF
    





 | TRACE | LoggingLevel |
| **scheduledExecutorService** (scheduler) | Allows for configuring a custom/shared thread pool to use for the consumer. By default each consumer has its own single threaded thread pool. |  | ScheduledExecutorService |
| **scheduler** (scheduler) | To use a cron scheduler from either camel-spring or camel-quartz component. Use value spring or quartz for built in scheduler. | none | Object |
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. This is a multi-value option with prefix: scheduler. |  | Map |
| **startScheduler** (scheduler) | Whether the scheduler should be auto started. | true | boolean |
| **timeUnit** (scheduler) | 

Time unit for initialDelay and delay options.

Enum values:

-   NANOSECONDS
    
-   MICROSECONDS
    
-   MILLISECONDS
    
-   SECONDS
    
-   MINUTES
    
-   HOURS
    
-   DAYS
    





 | MILLISECONDS | TimeUnit |
| **useFixedDelay** (scheduler) | Controls if fixed delay or fixed rate is used. See ScheduledExecutorService in JDK for details. | true | boolean |
| **authorizationToken** (security) | **Required** The authorization token for using the bot (ask the BotFather). |  | String |

## Message Headers

The Telegram component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelTelegramChatId** (producer) Constant: [`TELEGRAM_CHAT_ID`](https://javadoc.io/doc/org.apache.camel/camel-telegram/latest/org/apache/camel/component/telegram/TelegramConstants.html#TELEGRAM_CHAT_ID) | This header is used by the producer endpoint in order to resolve the chat id that will receive the message. The recipient chat id can be placed (in order of priority) in message body, in the CamelTelegramChatId header or in the endpoint configuration (chatId option). This header is also present in all incoming messages. |  | Object |
| **CamelTelegramMediaType** (common) Constant: [`TELEGRAM_MEDIA_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-telegram/latest/org/apache/camel/component/telegram/TelegramConstants.html#TELEGRAM_MEDIA_TYPE) | This header is used to identify the media type when the outgoing message is composed of pure binary data. Possible values are strings or enum values belonging to the org.apache.camel.component.telegram.TelegramMediaType enumeration. |  | TelegramMediaType or String |
| **CamelTelegramMediaTitleCaption** (common) Constant: [`TELEGRAM_MEDIA_TITLE_CAPTION`](https://javadoc.io/doc/org.apache.camel/camel-telegram/latest/org/apache/camel/component/telegram/TelegramConstants.html#TELEGRAM_MEDIA_TITLE_CAPTION) | This header is used to provide a caption or title for outgoing binary messages. |  | String |
| **CamelTelegramMediaMarkup** (common) Constant: [`TELEGRAM_MEDIA_MARKUP`](https://javadoc.io/doc/org.apache.camel/camel-telegram/latest/org/apache/camel/component/telegram/TelegramConstants.html#TELEGRAM_MEDIA_MARKUP) | The reply markup. |  | ReplyMarkup |
| **CamelTelegramParseMode** (common) Constant: [`TELEGRAM_PARSE_MODE`](https://javadoc.io/doc/org.apache.camel/camel-telegram/latest/org/apache/camel/component/telegram/TelegramConstants.html#TELEGRAM_PARSE_MODE) | 
This header is used to format text messages using HTML or Markdown.

Enum values:

-   HTML
    
-   MARKDOWN
    





 |  | TelegramParseMode |
| **CamelMessageTimestamp** (common) Constant: [`MESSAGE_TIMESTAMP`](https://javadoc.io/doc/org.apache.camel/camel-telegram/latest/org/apache/camel/component/telegram/TelegramConstants.html#MESSAGE_TIMESTAMP) | The message timestamp. |  | long |

## Usage

The Telegram component supports both consumer and producer endpoints. It can also be used in **reactive chatbot mode** (to consume, then produce messages).

### Producer

The following is a basic example of how to send a message to a Telegram chat through the Telegram Bot API.

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: telegram:bots
            parameters:
              authorizationToken: "123456789:insertYourAuthorizationTokenHere"
```

The code `123456789:insertYourAuthorizationTokenHere` is the **authorization token** corresponding to the Bot.

When using the producer endpoint without specifying the **chat id** option, the target chat will be identified using information contained in the body or headers of the message. The following message bodies are allowed for a producer endpoint (messages of type `OutgoingXXXMessage` belong to the package `org.apache.camel.component.telegram.model`)

 
| Java Type | Description |
| --- | --- |
| `OutgoingTextMessage` | To send a text message to a chat |
| `OutgoingPhotoMessage` | To send a photo (JPG, PNG) to a chat |
| `OutgoingAudioMessage` | To send a mp3 audio to a chat |
| `OutgoingVideoMessage` | To send a mp4 video to a chat |
| `OutgoingDocumentMessage` | To send a file to a chat (any media type) |
| `OutgoingStickerMessage` | To send a sticker to a chat (WEBP) |
| `OutgoingAnswerInlineQuery` | To send answers to an inline query |
| `EditMessageTextMessage` | To edit text and game messages (editMessageText) |
| `EditMessageCaptionMessage` | To edit captions of messages (editMessageCaption) |
| `EditMessageMediaMessage` | To edit animation, audio, document, photo, or video messages. (editMessageMedia) |
| `EditMessageReplyMarkupMessage` | To edit only the reply markup of a message. (editMessageReplyMarkup) |
| `EditMessageDelete` | To delete a message, including service messages. (deleteMessage) |
| `SendLocationMessage` | To send a location (setSendLocation) |
| `EditMessageLiveLocationMessage` | To send changes to a live location (editMessageLiveLocation) |
| `StopMessageLiveLocationMessage` | To stop updating a live location message sent by the bot or via the bot (for inline bots) before live\_period expires (stopMessageLiveLocation) |
| `SendVenueMessage` | To send information about a venue (sendVenue) |
| `SendInvoiceMessage` | To send an invoice for payment (sendInvoice) |
| `CreateInvoiceLinkMessage` | To create a link for an invoice (createInvoiceLink) |
| `AnswerShippingQueryMessage` | To reply to shipping queries (answerShippingQuery) |
| `AnswerPreCheckoutQueryMessage` | To respond to a pre-checkout query from a payment (answerPreCheckoutQuery) |
| `SendChatActionMessage` | To send a chat action status like typing, uploading, etc. (sendChatAction) |
| `GetMyStarBalanceMessage` | To get the bot’s current Telegram Star balance (getMyStarBalance) |
| `GetStarTransactionsMessage` | To get the list of bot’s Telegram Star transactions (getStarTransactions) |
| `RefundStarPaymentMessage` | To refund a successful payment in Telegram Stars (refundStarPayment) |
| `EditUserStarSubscriptionMessage` | To cancel or re-enable extension of a subscription paid in Telegram Stars (editUserStarSubscription) |
| `byte[]` | To send any media type supported. It requires the `CamelTelegramMediaType` header to be set to the appropriate media type |
| `String` | To send a text message to a chat. It gets converted automatically into a `OutgoingTextMessage` |

### Consumer

The following is a basic example of how to receive all messages that telegram users are sending to the configured Bot.

-   Java
    
-   XML
    
-   YAML
    

```java
from("telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere")
    .bean(ProcessorBean.class);
```

```xml
<route>
  <from uri="telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere"/>
  <bean ref="myBean"/>
</route>
```

```yaml
- route:
    from:
      uri: telegram:bots
      parameters:
        authorizationToken: "123456789:insertYourAuthorizationTokenHere"
      steps:
        - bean:
            ref: myBean
```

The `MyBean` is a simple bean that will receive the messages

_Java-only: bean class definition_

```java
public class MyBean {

    public void process(String message) {
        // or Exchange, or org.apache.camel.component.telegram.model.IncomingMessage (or both)

        // do process
    }

}
```

Supported types for incoming messages are

 
| Java Type | Description |
| --- | --- |
| `IncomingMessage` | The full object representation of an incoming message |
| `String` | The content of the message, for text messages only |

### Reactive Chat-Bot Example

The reactive chatbot mode is a simple way of using the Camel component to build a simple chatbot that replies directly to chat messages received from the Telegram users.

The following is a basic configuration of the chatbot:

-   Java
    
-   XML
    
-   YAML
    

```java
from("telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere")
    .bean(ChatBotLogic.class)
    .to("telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere");
```

```xml
<route>
  <from uri="telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere"/>
  <bean ref="chatBotLogic"/>
  <to uri="telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere"/>
</route>
```

```yaml
- route:
    from:
      uri: telegram:bots
      parameters:
        authorizationToken: "123456789:insertYourAuthorizationTokenHere"
      steps:
        - bean:
            ref: chatBotLogic
        - to:
            uri: telegram:bots
            parameters:
              authorizationToken: "123456789:insertYourAuthorizationTokenHere"
```

The `ChatBotLogic` is a simple bean that implements a generic String-to-String method.

_Java-only: bean class definition_

```java
public class ChatBotLogic {

    public String chatBotProcess(String message) {
        if( "do-not-reply".equals(message) ) {
            return null; // no response in the chat
        }

        return "echo from the bot: " + message; // echoes the message
    }

}
```

Every non-null string returned by the `chatBotProcess` method is automatically routed to the chat that originated the request (as the `CamelTelegramChatId` header is used to route the message).

### Getting the Chat ID

If you want to push messages to a specific Telegram chat when an event occurs, you need to retrieve the corresponding chat ID. The chat ID is not currently shown in the telegram client, but you can obtain it using a simple route.

First, add the bot to the chat where you want to push messages, then run a route like the following one.

-   Java
    
-   XML
    
-   YAML
    

```java
from("telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere")
    .to("log:INFO?showHeaders=true");
```

```xml
<route>
  <from uri="telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere"/>
  <to uri="log:INFO?showHeaders=true"/>
</route>
```

```yaml
- route:
    from:
      uri: telegram:bots
      parameters:
        authorizationToken: "123456789:insertYourAuthorizationTokenHere"
      steps:
        - to:
            uri: log:INFO
            parameters:
              showHeaders: true
```

Any message received by the bot will be dumped to your log together with information about the chat (`CamelTelegramChatId` header).

Once you get the chat ID, you can use the following sample route to push a message to it.

-   Java
    
-   XML
    
-   YAML
    

```java
from("timer:tick")
    .setBody().constant("Hello")
    .to("telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere&chatId=123456");
```

```xml
<route>
    <from uri="timer:tick"/>
    <setBody>
        <constant>Hello</constant>
    </setBody>
    <to uri="telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere&amp;chatId=123456"/>
</route>
```

```yaml
- route:
    from:
      uri: timer:tick
    steps:
      - setBody:
          constant: Hello
      - to:
          uri: telegram:bots
          parameters:
            authorizationToken: "123456789:insertYourAuthorizationTokenHere"
            chatId: "123456"
```

Note that the corresponding URI parameter is simply `chatId`.

### Customizing keyboard

You can customize the user keyboard instead of asking him to write an option. `OutgoingTextMessage` has the property `ReplyMarkup` which can be used for such a thing.

_Java-only: inline Processor with keyboard builder API_

```java
from("telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere")
    .process(exchange -> {

        OutgoingTextMessage msg = new OutgoingTextMessage();
        msg.setText("Choose one option!");

        InlineKeyboardButton buttonOptionOneI = InlineKeyboardButton.builder()
                .text("Option One - I").build();

        InlineKeyboardButton buttonOptionOneII = InlineKeyboardButton.builder()
                .text("Option One - II").build();

        InlineKeyboardButton buttonOptionTwoI = InlineKeyboardButton.builder()
                .text("Option Two - I").build();

        ReplyKeyboardMarkup replyMarkup = ReplyKeyboardMarkup.builder()
                .keyboard()
                    .addRow(Arrays.asList(buttonOptionOneI, buttonOptionOneII))
                    .addRow(Arrays.asList(buttonOptionTwoI))
                    .close()
                .oneTimeKeyboard(true)
                .build();

        msg.setReplyMarkup(replyMarkup);

        exchange.getIn().setBody(msg);
    })
    .to("telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere");
```

If you want to disable it, the next message must have the property `removeKeyboard` set on `ReplyKeyboardMarkup` object.

_Java-only: inline Processor with keyboard removal_

```java
from("telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere")
    .process(exchange -> {

        OutgoingTextMessage msg = new OutgoingTextMessage();
        msg.setText("Your answer was accepted!");

        ReplyKeyboardMarkup replyMarkup = ReplyKeyboardMarkup.builder()
                .removeKeyboard(true)
                .build();

        msg.setReplyKeyboardMarkup(replyMarkup);

        exchange.getIn().setBody(msg);
    })
    .to("telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere");
```

### Webhook Mode

The Telegram component supports usage in the **webhook mode** using the **camel-webhook** component.

To enable webhook mode, users need first to add a REST implementation to their application. Maven users, for example, can add **netty-http** to their `pom.xml` file:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-netty-http</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

Once done, you need to prepend the webhook URI to the telegram URI you want to use.

In the route below:

-   Java
    
-   XML
    
-   YAML
    

```java
from("webhook:telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere")
    .to("log:info");
```

```xml
<route>
    <from uri="webhook:telegram:bots?authorizationToken=123456789:insertYourAuthorizationTokenHere"/>
    <to uri="log:info"/>
</route>
```

```yaml
- route:
    from:
      uri: webhook:telegram:bots
      parameters:
        authorizationToken: "123456789:insertYourAuthorizationTokenHere"
    steps:
      - to:
          uri: log:info
```

Some endpoints will be exposed by your application and Telegram will be configured to send messages to them. You need to ensure that your server is exposed to the internet and to pass the right value of the **camel.component.webhook.configuration.webhook-external-url** property.

Refer to the **camel-webhook** component documentation for instructions on how to set it.

## Spring Boot Auto-Configuration

When using telegram with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-telegram-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.telegram.authorization-token** | The default Telegram authorization token to be used when the information is not provided in the endpoints. |  | String |
| **camel.component.telegram.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.telegram.base-uri** | Can be used to set an alternative base URI, e.g. when you want to test the component against a mock Telegram API. | [https://api.telegram.org](https://api.telegram.org) | String |
| **camel.component.telegram.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions (if possible) occurred while the Camel consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. Important: This is only possible if the 3rd party component allows Camel to be alerted if an exception was thrown. Some components handle this internally only, and therefore bridgeErrorHandler is not possible. In other situations we may improve the Camel component to hook into the 3rd party component and make this possible for future releases. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.telegram.client** | To use a custom java.net.http.HttpClient. The option is a java.net.http.HttpClient type. |  | HttpClient |
| **camel.component.telegram.enabled** | Whether to enable auto configuration of the telegram component. This is enabled by default. |  | Boolean |
| **camel.component.telegram.health-check-consumer-enabled** | Used for enabling or disabling all consumer based health checks from this component. | true | Boolean |
| **camel.component.telegram.health-check-producer-enabled** | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | Boolean |
| **camel.component.telegram.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |