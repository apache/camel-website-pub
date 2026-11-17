# ![twitter search source](_images/kamelets/twitter-search-source.svg) Twitter Search Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the new tweets that match a search, such as a word, a hashtag or a mention, by asking Twitter (X) at a regular interval, one message per tweet.

Use it to follow what people say about a brand, a product or an event, for example to collect mentions for analysis or to alert a team. To follow the tweets of one account, use `twitter-timeline-source`.

Output: the body is the tweet as JSON text, with its `text`, its `id`, its `lang`, the time it was created and the `user` who wrote it. The `CamelTwitterEventType` header is `STATUS`.

Good to know: it searches every 30 seconds. The first search sends up to 5 matching tweets, and each later search sends at most 5 tweets newer than the last one it saw, so on a busy search some tweets are missed. It does not remember what it read: after a restart, it starts over as on the first search. It uses the standard search of version 1.1 of the Twitter API.

## Configuration Options

The following table summarizes the configuration options available for the `twitter-search-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** The access token of the account to read with, generated on the Keys and Tokens page of the app in the developer portal. The Kamelet acts as that account. Used together with `accessTokenSecret`. | string |  |  |
| **accessTokenSecret** | Access Token Secret | **Required** The access token secret, shown with the access token on the Keys and Tokens page of the app in the developer portal. | string |  |  |
| **apiKey** | API Key | **Required** The API key (consumer key) of your app, from the Keys and Tokens page of the app in the Twitter (X) developer portal at developer.x.com. Used together with `apiKeySecret`. | string |  |  |
| **apiKeySecret** | API Key Secret | **Required** The API key secret (consumer secret) of your app, shown with the API key on the Keys and Tokens page of the app in the developer portal. | string |  |  |
| **keywords** | Keywords | **Required** What to search for, as you would type it in the Twitter search box. Words must all appear, and the standard search operators work, such as `OR`, `#hashtag`, `from:user` and `-word` to exclude a word. | string |  | #ApacheCamel OR "Apache Camel" |

## Dependencies

At runtime, the `twitter-search-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:twitter-search-source"
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

## Twitter Search Source Kamelet Description

### Authentication methods

This Kamelet connects to version 1.1 of the Twitter (X) API with the four keys of an app of the Twitter developer portal (OAuth 1.0a):

-   `apiKey` and `apiKeySecret`: the API key and secret of the app.
    
-   `accessToken` and `accessTokenSecret`: the access token and secret of the account the Kamelet reads with.
    

All four are on the **Keys and Tokens** page of the app in the developer portal.

### Output format

Each matching tweet becomes one message. The body is the tweet as JSON text, with its `text`, its `id`, its `lang`, the time it was created and the `user` who wrote it. The `CamelTwitterEventType` header is `STATUS`.

### Configuration

The `keywords` option is the search, as you would type it in the Twitter search box. It supports the standard search operators, such as `OR`, `#hashtag`, `from:user` and `-word`.

The Kamelet searches every 30 seconds. The first search sends up to 5 matching tweets; each later search sends at most 5 tweets newer than the last one it saw.

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:twitter-search-source"
      parameters:
        keywords: "#ApacheCamel"
        apiKey: "{{twitter.apiKey}}"
        apiKeySecret: "{{twitter.apiKeySecret}}"
        accessToken: "{{twitter.accessToken}}"
        accessTokenSecret: "{{twitter.accessTokenSecret}}"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/twitter-search-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/twitter-search-source.kamelet.yaml)