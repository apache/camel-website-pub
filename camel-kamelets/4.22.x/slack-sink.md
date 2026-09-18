# ![slack sink](_images/kamelets/slack-sink.svg) Slack Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send messages to a Slack channel.

## Configuration Options

The following table summarizes the configuration options available for the `slack-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **channel** | Channel | **Required** The Slack channel to send messages to. | string |  | #myroom |
| **webhookUrl** | Webhook URL | **Required** The webhook URL used by the Slack channel to handle incoming messages. | string |  |  |

## Dependencies

At runtime, the `slack-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:slack
    
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
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:slack-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Slack Sink Kamelet Description

### Team Communication Integration

This Kamelet integrates with Slack, a popular team collaboration and messaging platform. It enables automated message posting to Slack channels, users, or groups.

### Channel and Direct Messaging

Supports posting messages to:

-   Public and private channels
    
-   Direct messages to users
    
-   Group conversations
    
-   Thread replies for organized discussions
    

### Rich Message Formatting

Slack supports rich message formatting including:

-   Text formatting (bold, italic, code blocks)
    
-   Mentions (@user, @channel, @here)
    
-   Emoji and reactions
    
-   Attachments and interactive elements
    

### Bot Integration

Often used with Slack bots and applications to provide automated notifications, alerts, and system status updates to team members.

### API Authentication

Uses Slack’s API authentication mechanisms including bot tokens, OAuth tokens, and webhook URLs for secure message posting.

### Notification Patterns

Common use cases include:

-   System alerts and monitoring notifications
    
-   CI/CD pipeline status updates
    
-   Business process notifications
    
-   Customer support escalations
    
-   Automated reporting and metrics
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/slack-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/slack-sink.kamelet.yaml)