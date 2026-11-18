# ![slack sink](_images/kamelets/slack-sink.svg) Slack Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Posts each message as a text message to a Slack channel, through an incoming webhook of a Slack app.

Use it to tell a team in Slack when something happens, such as a monitoring alert, a failed build, a new order or a daily report. To read the messages of a channel instead, use `slack-source`.

Input: the body is the text of the Slack message, as text; another kind of body is turned into text first. JSON text is posted as it is, as the text of the message, not as a Slack message structure. The text can use Slack’s own formatting, such as `**bold**`. Headers are not read.

Output: the message is unchanged.

Good to know: the webhook decides where the message goes. The webhook of a Slack app posts only to the channel chosen when the webhook was created, whatever `channel` says. When Slack does not answer with a success status, the message fails.

## Configuration Options

The following table summarizes the configuration options available for the `slack-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **channel** | Channel | **Required** The channel to post to, with a leading `#`. It is sent along with each message, but the webhook of a Slack app always posts to the channel it was created for, so set the same channel here. | string |  | #alerts |
| **webhookUrl** | Webhook URL | **Required** The incoming webhook URL of your Slack app, which starts with `[https://hooks.slack.com/services/](https://hooks.slack.com/services/)`. Create it on the Incoming Webhooks page of your app at api.slack.com/apps, with Add New Webhook to Workspace, and choose the channel there. Anyone who has it can post to that channel. | string |  |  |

## Dependencies

At runtime, the `slack-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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

This Kamelet integrates with Slack, a popular team collaboration and messaging platform. It posts each message as a text message to a Slack channel, through an incoming webhook.

### Setup Requirements

1.  Create a Slack app in your workspace at [https://api.slack.com/apps](https://api.slack.com/apps).
    
2.  On the **Incoming Webhooks** page of the app, turn incoming webhooks on.
    
3.  Click **Add New Webhook to Workspace** and choose the channel to post to.
    
4.  Copy the webhook URL, which starts with `[https://hooks.slack.com/services/](https://hooks.slack.com/services/)`, into `webhookUrl`, and the name of the same channel into `channel`.
    

The webhook of a Slack app always posts to the channel it was created for. To post to several channels, create one webhook per channel and one Kamelet per webhook.

### Message Formatting

The body of the message becomes the text of the Slack message. The text can use Slack formatting, such as `**bold**`, `_italic_` and `` `code` `` , and emoji such as `:tada:`. JSON in the body is posted as text, not as a Slack message structure, so attachments, blocks and interactive elements are not available through this Kamelet.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: "The nightly build *failed*."
        repeatCount: 1
      steps:
        - to:
            uri: "kamelet:slack-sink"
            parameters:
              channel: "#alerts"
              webhookUrl: "{{slack.webhookUrl}}"
```

### Notification Patterns

Common use cases include:

-   System alerts and monitoring notifications
    
-   CI/CD pipeline status updates
    
-   Business process notifications
    
-   Customer support escalations
    
-   Automated reporting and metrics
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/slack-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/slack-sink.kamelet.yaml)