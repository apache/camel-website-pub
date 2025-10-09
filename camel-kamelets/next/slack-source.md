# ![slack source](_images/kamelets/slack-source.svg) Slack Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive messages from a Slack channel.

## Configuration Options

The following table summarizes the configuration options available for the `slack-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **channel** | Channel | **Required** The Slack channel to receive messages from. | string |  | #myroom |
| **token** | Token | **Required** The Bot User OAuth Access Token to access Slack. A Slack app that has the following permissions is required: `channels:history`, `groups:history`, `im:history`, `mpim:history`, `channels:read`, `groups:read`, `im:read`, and `mpim:read`. | string |  |  |
| **delay** | Delay | The delay between polls. If no unit provided, milliseconds is the default. | string | 60000 | 60s or 6000 or 1m |
| **naturalOrder** | Natural Order | Create exchanges in natural order (oldest to newest) or not. | boolean | false |  |
| **serverUrl** | Server URL | The Slack API server endpoint URL. | string | [https://slack.com](https://slack.com) | https://slack.com |

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

This Kamelet requires a Slack app token for authentication. You need to create a Slack app and obtain the necessary permissions to access channels and messages.

### Configuration

The Slack Source Kamelet supports the following configurations:

-   **Token**: Slack app token for authentication (required)
    
-   **Channel**: Slack channel to monitor (required)
    
-   **Server URL**: Slack API server URL (optional, defaults to Slack’s API)
    
-   **Delay**: Polling interval in milliseconds for checking new messages
    
-   **Max Results**: Maximum number of messages to retrieve per poll
    

### Output Format

The Kamelet outputs Slack messages as JSON objects containing message content, user information, timestamp, and channel details.

### Setup Requirements

1.  Create a Slack app in your workspace
    
2.  Add necessary OAuth scopes (channels:history, channels:read)
    
3.  Install the app to your workspace
    
4.  Copy the OAuth access token
    

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:slack-source"
      parameters:
        token: "xoxb-your-slack-bot-token"
        channel: "#general"
        delay: 10000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Specific Channel ID

```yaml
- route:
    from:
      uri: "kamelet:slack-source"
      parameters:
        token: "xoxb-your-slack-bot-token"
        channel: "C1234567890"
        delay: 5000
        maxResults: 50
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example Monitoring Multiple Aspects

```yaml
- route:
    from:
      uri: "kamelet:slack-source"
      parameters:
        token: "xoxb-your-slack-bot-token"
        channel: "#alerts"
        delay: 30000
      steps:
        - filter:
            simple: "${body.contains('ERROR')}"
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