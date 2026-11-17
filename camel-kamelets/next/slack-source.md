# ![slack source](_images/kamelets/slack-source.svg) Slack Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the new messages posted in a public Slack channel, by asking Slack at a regular interval, one message per Slack message.

Use it to react to what people write in a channel, for example to turn a message in `#support` into a ticket, to archive a channel, or to start a job when someone posts a command. To post to Slack instead, use `slack-sink`.

Output: the body is the Slack message as JSON text, with fields such as `text` (what was written), `user` (the ID of the author) and `ts` (the time stamp that identifies the message). The `Content-Type` header is `application/json`.

Good to know: when it starts, it also sends the most recent message already in the channel, then only the messages posted after it. It does not remember where it stopped: after a restart it starts again from the most recent message. It reads public channels only, by their name, and needs a token of a Slack app, see `token`.

## Configuration Options

The following table summarizes the configuration options available for the `slack-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **channel** | Channel | **Required** The name of the public channel to read, without the leading `#`, as Slack shows it in the channel list. Not the channel ID. When no public channel has this name, the Kamelet does not start. | string |  | support |
| **token** | Token | **Required** The OAuth token of your Slack app, which starts with `xoxb-` (bot token) or `xoxp-` (user token). Copy it from the OAuth & Permissions page of your app at api.slack.com/apps, after you install the app in your workspace. The app needs the scopes `channels:history`, `groups:history`, `im:history`, `mpim:history`, `channels:read`, `groups:read`, `im:read`, and `mpim:read`. | string |  |  |
| **delay** | Delay | How long to wait between two checks for new messages. A number is in milliseconds; a unit can be added, such as `30s` or `1m`. | string | 60000 | 30s |
| **naturalOrder** | Natural Order | If true, the new messages found at a check are sent oldest first. If false, they are sent newest first. | boolean | false |  |
| **serverUrl** | Server URL | The address of the Slack API. Change it only to use a test server or a proxy that stands in for Slack. | string | [https://slack.com](https://slack.com) | https://slack.com |

## Dependencies

At runtime, the `slack-source` Kamelet relies upon the presence of the following dependencies:

-   camel:gson
    
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
      uri: "kamelet:slack-source"
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

## Slack Source Kamelet Description

### Authentication

This Kamelet requires the OAuth token of a Slack app. You need to create a Slack app and give it the permissions (scopes) to read channels and their messages.

### Configuration

The Slack Source Kamelet supports the following configurations:

-   **Token**: OAuth token of the Slack app (required)
    
-   **Channel**: the name of the public channel to read, without the leading `#` (required)
    
-   **Server URL**: Slack API server URL (optional, defaults to `[https://slack.com](https://slack.com)`)
    
-   **Delay**: how long to wait between two checks for new messages, in milliseconds or with a unit such as `30s`
    
-   **Natural Order**: whether the new messages of a check are sent oldest first
    

### Output Format

The Kamelet outputs each Slack message as JSON text, with fields such as `text` (the content), `user` (the ID of the author) and `ts` (the time stamp of the message). The message does not say in which channel it was posted.

When it starts, the Kamelet also sends the most recent message already in the channel. After that it sends only the messages posted since the last check.

### Setup Requirements

1.  Create a Slack app in your workspace at [https://api.slack.com/apps](https://api.slack.com/apps)
    
2.  Add the necessary OAuth scopes (`channels:history`, `channels:read`, and the others listed for the `token` option)
    
3.  Install the app to your workspace
    
4.  Copy the OAuth token from the **OAuth & Permissions** page of the app
    

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:slack-source"
      parameters:
        token: "{{slack.token}}"
        channel: "general"
        delay: 10000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example Filtering the Messages

```yaml
- route:
    from:
      uri: "kamelet:slack-source"
      parameters:
        token: "{{slack.token}}"
        channel: "alerts"
        delay: 30000
      steps:
        - filter:
            simple: "${body} contains 'ERROR'"
            steps:
              - to:
                  uri: "kamelet:log-sink"
```

### Security Considerations

-   Store the Slack token securely as a secret
    
-   Use appropriate OAuth scopes to limit access
    
-   Monitor token usage and rotate tokens periodically
    
-   Consider using Slack’s real-time messaging API for high-frequency scenarios
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/slack-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/slack-source.kamelet.yaml)