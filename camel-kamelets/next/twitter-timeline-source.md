# ![twitter timeline source](_images/kamelets/twitter-timeline-source.svg) Twitter Timeline Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the new tweets that one Twitter (X) account posts, by asking Twitter at a regular interval, one message per tweet.

Use it to follow an account, such as a news feed, a status page or a partner, and pass on what it posts, for example to a chat or a database. To follow a word or a hashtag across all accounts, use `twitter-search-source`.

Output: the body is the tweet as JSON text, with its `text`, its `id`, the time it was created and the `user` who wrote it. The `CamelTwitterEventType` header is `STATUS`.

Good to know: it checks every 30 seconds. The first check sends the 5 most recent tweets of the account, and each later check sends at most 5 tweets newer than the last one it saw. It does not remember what it read: after a restart, it starts again with the most recent tweets. It uses version 1.1 of the Twitter API.

## Configuration Options

The following table summarizes the configuration options available for the `twitter-timeline-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** The access token of the account to read with, generated on the Keys and Tokens page of the app in the developer portal. The Kamelet acts as that account. Used together with `accessTokenSecret`. | string |  |  |
| **accessTokenSecret** | Access Token Secret | **Required** The access token secret, shown with the access token on the Keys and Tokens page of the app in the developer portal. | string |  |  |
| **apiKey** | API Key | **Required** The API key (consumer key) of your app, from the Keys and Tokens page of the app in the Twitter (X) developer portal at developer.x.com. Used together with `apiKeySecret`. | string |  |  |
| **apiKeySecret** | API Key Secret | **Required** The API key secret (consumer secret) of your app, shown with the API key on the Keys and Tokens page of the app in the developer portal. | string |  |  |
| **user** | User | **Required** The user name (handle) of the account whose tweets to read, without the `@`. | string |  | ApacheCamel |

## Dependencies

At runtime, the `twitter-timeline-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:twitter
    
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
      uri: "kamelet:twitter-timeline-source"
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

## Twitter Timeline Source Kamelet Description

### Authentication methods

This Kamelet connects to version 1.1 of the Twitter (X) API with the four keys of an app of the Twitter developer portal (OAuth 1.0a):

-   `apiKey` and `apiKeySecret`: the API key and secret of the app.
    
-   `accessToken` and `accessTokenSecret`: the access token and secret of the account the Kamelet reads with.
    

All four are on the **Keys and Tokens** page of the app in the developer portal.

### Output format

Each tweet of the account becomes one message. The body is the tweet as JSON text, with its `text`, its `id`, the time it was created and the `user` who wrote it. The `CamelTwitterEventType` header is `STATUS`.

### Configuration

The `user` option is the user name (handle) of the account to follow, without the `@`.

The Kamelet checks every 30 seconds. The first check sends the 5 most recent tweets of the account; each later check sends at most 5 tweets newer than the last one it saw.

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:twitter-timeline-source"
      parameters:
        user: "ApacheCamel"
        apiKey: "{{twitter.apiKey}}"
        apiKeySecret: "{{twitter.apiKeySecret}}"
        accessToken: "{{twitter.accessToken}}"
        accessTokenSecret: "{{twitter.accessTokenSecret}}"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/twitter-timeline-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/twitter-timeline-source.kamelet.yaml)