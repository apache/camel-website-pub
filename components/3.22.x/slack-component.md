# Slack

**Since Camel 2.16**

**Both producer and consumer are supported**

The Slack component allows you to connect to an instance of [Slack](http://www.slack.com/) and to send and receive the messages.

To send a message contained in the message body a pre established [Slack incoming webhook](https://api.slack.com/incoming-webhooks) must be configured in Slack.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-slack</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

To send a message to a channel.

slack:#channel\[?options\]

To send a direct message to a slack user.

slack:@userID\[?options\]

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

The component level is the highest level which holds general and common configurations that are inherited by the endpoints. For example a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

Configuring components can be done with the [Component DSL](../../manual/component-dsl.md), in a configuration file (application.properties|yaml), or directly with Java code.

### Configuring Endpoint Options

Where you find yourself configuring the most is on endpoints, as endpoints often have many options, which allows you to configure what you need the endpoint to do. The options are also categorized into whether the endpoint is used as consumer (from) or as a producer (to), or used for both.

Configuring endpoints is most often done directly in the endpoint URI as path and query parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md), which allows to not hardcode urls, port numbers, sensitive information, and other settings. In other words placeholders allows to externalize the configuration from your code, and gives more flexibility and reuse.

The following two sections lists all the options, firstly for the component followed by the endpoint.

## Component Options

The Slack component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **bridgeErrorHandler** (consumer) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **token** (token) | The token to access Slack. This app needs to have channels:history, groups:history, im:history, mpim:history, channels:read, groups:read, im:read and mpim:read permissions. The User OAuth Token is the kind of token needed. |  | String |
| **webhookUrl** (webhook) | The incoming webhook URL. |  | String |

## Endpoint Options

The Slack endpoint is configured using URI syntax:

slack:channel

with the following path and query parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **channel** (common) | **Required** The channel name (syntax #name) or slack user (syntax userName) to send a message directly to an user. |  | String |

### Query Parameters (29 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **token** (common) | The token to access Slack. This app needs to have channels:history, groups:history, im:history, mpim:history, channels:read, groups:read, im:read and mpim:read permissions. The User OAuth Token is the kind of token needed. |  | String |
| **conversationType** (consumer) | 
Type of conversation.

Enum values:

-   PUBLIC\_CHANNEL
    
-   PRIVATE\_CHANNEL
    
-   MPIM
    
-   IM
    





 | PUBLIC\_CHANNEL | ConversationType |
| **maxResults** (consumer) | The Max Result for the poll. | 10 | String |
| **naturalOrder** (consumer) | Create exchanges in natural order (oldest to newest) or not. | false | boolean |
| **sendEmptyMessageWhenIdle** (consumer) | If the polling consumer did not poll any files, you can enable this option to send an empty message (no body) instead. | false | boolean |
| **serverUrl** (consumer) | The Server URL of the Slack instance. | [https://slack.com](https://slack.com) | String |
| **bridgeErrorHandler** (consumer (advanced)) | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | boolean |
| **exceptionHandler** (consumer (advanced)) | To let the consumer use a custom ExceptionHandler. Notice if the option bridgeErrorHandler is enabled then this option is not in use. By default the consumer will deal with exceptions, that will be logged at WARN or ERROR level and ignored. |  | ExceptionHandler |
| **exchangePattern** (consumer (advanced)) | 

Sets the exchange pattern when the consumer creates an exchange.

Enum values:

-   InOnly
    
-   InOut
    
-   InOptionalOut
    





 |  | ExchangePattern |
| **pollStrategy** (consumer (advanced)) | A pluggable org.apache.camel.PollingConsumerPollingStrategy allowing you to provide your custom implementation to control error handling usually occurred during the poll operation before an Exchange have been created and being routed in Camel. |  | PollingConsumerPollStrategy |
| **iconEmoji** (producer) | **Deprecated** Use a Slack emoji as an avatar. |  | String |
| **iconUrl** (producer) | **Deprecated** The avatar that the component will use when sending message to a channel or user. |  | String |
| **username** (producer) | **Deprecated** This is the username that the bot will have when sending messages to a channel or user. |  | String |
| **webhookUrl** (producer) | The incoming webhook URL. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
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
| **schedulerProperties** (scheduler) | To configure additional properties when using a custom scheduler or any of the Quartz, Spring based scheduler. |  | Map |
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

## Configuring in Spring XML

The SlackComponent with XML must be configured as a Spring or Blueprint bean that contains the incoming webhook url or the app token for the integration as a parameter.

```xml
<bean id="slack" class="org.apache.camel.component.slack.SlackComponent">
    <property name="webhookUrl" value="https://hooks.slack.com/services/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"/>
    <property name="token" value="xoxb-12345678901-1234567890123-xxxxxxxxxxxxxxxxxxxxxxxx"/>
</bean>
```

For Java you can configure this using Java code.

## Example

A CamelContext with Blueprint could be as:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<blueprint xmlns="http://www.osgi.org/xmlns/blueprint/v1.0.0" default-activation="lazy">

    <bean id="slack" class="org.apache.camel.component.slack.SlackComponent">
        <property name="webhookUrl" value="https://hooks.slack.com/services/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"/>
    </bean>

    <camelContext xmlns="http://camel.apache.org/schema/blueprint">
        <route>
            <from uri="direct:test"/>
            <to uri="slack:#channel?iconEmoji=:camel:&amp;username=CamelTest"/>
        </route>
    </camelContext>

</blueprint>
```

## Producer

You can now use a token to send a message instead of WebhookUrl

```java
from("direct:test")
    .to("slack:#random?token=RAW(<YOUR_TOKEN>)");
```

You can now use the Slack API model to create blocks. You can read more about it here [https://api.slack.com/block-kit](https://api.slack.com/block-kit)

```java
    public void testSlackAPIModelMessage() {
        Message message = new Message();
        message.setBlocks(Collections.singletonList(SectionBlock
                .builder()
                .text(MarkdownTextObject
                        .builder()
                        .text("*Hello from Camel!*")
                        .build())
                .build()));

        template.sendBody(test, message);
    }
```

You’ll need to create a Slack app and use it on your workspace.

For token usage, set the 'OAuth Token'.

> **Important**
> Add the corresponding (`channels:history`, `chat:write`) user token scopes to your app to grant it permission to write messages in the corresponding channel. You’ll also need to invite the Bot or User to the corresponding channel.

For Bot tokens you’ll need the following permissions:

-   channels:history
    
-   chat:write
    

For User tokens you’ll need the following permissions:

-   channels:history
    
-   chat:write
    

## Consumer

You can also use a consumer for messages in a channel

```java
from("slack://general?token=RAW(<YOUR_TOKEN>)&maxResults=1")
    .to("mock:result");
```

This way you’ll get the last message from `general` channel. The consumer will track the timestamp of the last message consumed and in the next poll it will consume only newer messages in the channel.

You’ll need to create a Slack app and use it in your workspace.

Use the 'User OAuth Token' as token for the consumer endpoint.

> **Important**
> Add the corresponding history (`channels:history`, `groups:history`, `mpim:history` and `im:history`) and read (`channels:read`, `groups:read`, `mpim:read` and `im:read`) user token scope to your app to grant it permission to view messages in the corresponding channel.

For Bot tokens you’ll need the following permissions:

-   channels:history
    
-   groups:history
    
-   im:history
    
-   mpim:history
    
-   channels:read
    
-   groups:read
    
-   im:read
    
-   mpim:read
    

For User tokens you’ll need the following permissions:

-   channels:history
    
-   groups:history
    
-   im:history
    
-   mpim:history
    
-   channels:read
    
-   groups:read
    
-   im:read
    
-   mpim:read
    

The naturalOrder option allows consuming messages from the oldest to the newest. Originally you would get the newest first and consume backward (message 3 ⇒ message 2 ⇒ message 1)

> **Important**
> The channel / conversation doesn’t need to be public to read the history and messages. Use the `conversationType` option to specify the type of the conversation (PUBLIC\_CHANNEL,PRIVATE\_CHANNEL, MPIM, IM).

## Spring Boot Auto-Configuration

When using slack with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-slack-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.slack.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.slack.bridge-error-handler** | Allows for bridging the consumer to the Camel routing Error Handler, which mean any exceptions occurred while the consumer is trying to pickup incoming messages, or the likes, will now be processed as a message and handled by the routing Error Handler. By default the consumer will use the org.apache.camel.spi.ExceptionHandler to deal with exceptions, that will be logged at WARN or ERROR level and ignored. | false | Boolean |
| **camel.component.slack.enabled** | Whether to enable auto configuration of the slack component. This is enabled by default. |  | Boolean |
| **camel.component.slack.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.slack.token** | The token to access Slack. This app needs to have channels:history, groups:history, im:history, mpim:history, channels:read, groups:read, im:read and mpim:read permissions. The User OAuth Token is the kind of token needed. |  | String |
| **camel.component.slack.webhook-url** | The incoming webhook URL. |  | String |