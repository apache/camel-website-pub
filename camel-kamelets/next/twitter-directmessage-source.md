# ![twitter directmessage source](_images/kamelets/twitter-directmessage-source.svg) Twitter Direct Message Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the direct messages of a Twitter (X) account, by asking Twitter at a regular interval, one message per direct message.

Use it to react to private messages sent to your company account, for example to open a support case or to forward them to a team chat. To read public tweets, use `twitter-search-source` or `twitter-timeline-source`.

Output: the body is the direct message as JSON text, with its `text`, its `id`, the `senderId` and the `recipientId`. The `CamelTwitterEventType` header is `DIRECT_MESSAGE`.

Good to know: it reads the messages of the account that owns `accessToken`, both the ones it received and the ones it sent; compare `senderId` to tell them apart. At the first check, every direct message that Twitter still lists (the last 30 days) is sent, then only new ones, every 30 seconds. It does not remember what it read: after a restart, it sends them all again. It uses version 1.1 of the Twitter API, and the app needs the permission to read direct messages.

## Configuration Options

The following table summarizes the configuration options available for the `twitter-directmessage-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** The access token of the account to read with, generated on the Keys and Tokens page of the app in the developer portal. The Kamelet acts as that account. Used together with `accessTokenSecret`. | string |  |  |
| **accessTokenSecret** | Access Token Secret | **Required** The access token secret, shown with the access token on the Keys and Tokens page of the app in the developer portal. | string |  |  |
| **apiKey** | API Key | **Required** The API key (consumer key) of your app, from the Keys and Tokens page of the app in the Twitter (X) developer portal at developer.x.com. Used together with `apiKeySecret`. | string |  |  |
| **apiKeySecret** | API Key Secret | **Required** The API key secret (consumer secret) of your app, shown with the API key on the Keys and Tokens page of the app in the developer portal. | string |  |  |
| **user** | User | **Required** The user name of the account, without the `@`. It is required, but it does not choose whose messages are read; that is always the account of `accessToken`. | string |  | ApacheCamel |

## Dependencies

At runtime, the `twitter-directmessage-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:twitter-directmessage-source"
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

## Twitter Directmessage Source Kamelet Description

### Authentication methods

This Kamelet connects to version 1.1 of the Twitter (X) API with the four keys of an app of the Twitter developer portal (OAuth 1.0a):

-   `apiKey` and `apiKeySecret`: the API key and secret of the app.
    
-   `accessToken` and `accessTokenSecret`: the access token and secret of the account whose direct messages are read.
    

All four are on the **Keys and Tokens** page of the app in the developer portal. The app needs the permission to read direct messages; generate the access token again after you change the permissions of the app.

### Output format

Each direct message becomes one message. The body is the direct message as JSON text, with its `text`, its `id`, the `senderId` and the `recipientId`. The `CamelTwitterEventType` header is `DIRECT_MESSAGE`.

### Configuration

The Kamelet reads the direct messages of the account that owns the access token, the ones it received and the ones it sent. The `user` option is required, but it does not change which messages are read.

The Kamelet checks every 30 seconds. The first check sends every direct message that Twitter still lists, then each later check sends only the new ones.

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:twitter-directmessage-source"
      parameters:
        user: "MyCompany"
        apiKey: "{{twitter.apiKey}}"
        apiKeySecret: "{{twitter.apiKeySecret}}"
        accessToken: "{{twitter.accessToken}}"
        accessTokenSecret: "{{twitter.accessTokenSecret}}"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/twitter-directmessage-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/twitter-directmessage-source.kamelet.yaml)