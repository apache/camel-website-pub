# ![ibm watson language sink](_images/kamelets/ibm-watson-language-sink.svg) IBM Watson Natural Language Understanding Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Analyzes the text of each message with IBM Watson Natural Language Understanding and replaces the body with the results, such as the sentiment, the entities and the keywords.

Use it to find out what people write about and how they feel, for example to flag angry customer emails, tag support tickets with the products they mention, or measure the tone of reviews.

Input: the body is the text to analyze, as text. With `operation` set to `analyzeUrl`, the body is instead the address of a web page for Watson to fetch and analyze. The optional `CamelIBMWatsonLanguageText` or `CamelIBMWatsonLanguageUrl` header gives the text or the address instead of the body. An empty body fails.

Output: when it is used inside a route, the body afterwards is the results as JSON text (bytes), with the `Content-Type` header set to `application/json`. The `CamelIBMWatsonLanguageSentimentLabel` and `CamelIBMWatsonLanguageSentimentScore` headers give the sentiment of the whole text, and `CamelIBMWatsonLanguageLanguage` its language.

Good to know: it logs in with the API key of a Natural Language Understanding instance in IBM Cloud; set `serviceUrl` when the instance is not in the US South region. Headers that start with `CamelIBMWatsonLanguage`, except `CamelIBMWatsonLanguageText` and `CamelIBMWatsonLanguageUrl`, are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `ibm-watson-language-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apiKey** | API Key | **Required** The API key of the Natural Language Understanding instance, the `apikey` value of its service credentials in the IBM Cloud console. | string |  |  |
| **analyzeCategories** | Analyze Categories | If true, the results place the text in a hierarchy of topics, such as `/technology and computing/software`. | boolean | false |  |
| **analyzeConcepts** | Analyze Concepts | If true, the results list general concepts that the text is about, even when it does not name them. | boolean | false |  |
| **analyzeEmotion** | Analyze Emotion | If true, the results give the emotions of the text, such as joy, anger, sadness, fear and disgust. | boolean | false |  |
| **analyzeEntities** | Analyze Entities | If true, the results list the people, companies, organizations, places and other named things in the text. | boolean | true |  |
| **analyzeKeywords** | Analyze Keywords | If true, the results list the important words and phrases of the text. | boolean | true |  |
| **analyzeSentiment** | Analyze Sentiment | If true, the results say whether the text is positive, negative or neutral, with a score from -1 to 1. | boolean | true |  |
| **operation** | Operation | `analyzeText` analyzes the text of the body; `analyzeUrl` takes the body as the address of a web page that Watson fetches and analyzes. Enum values: \* analyzeText \* analyzeUrl | string | analyzeText |  |
| **serviceUrl** | Service URL | The address of the Natural Language Understanding instance, the `url` value of its service credentials, which depends on the region of the instance. When it is not set, the address of the US South region is used. | string |  | https://api.us-south.natural-language-understanding.watson.cloud.ibm.com |

## Dependencies

At runtime, the `ibm-watson-language-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:ibm-watson-language
    
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
            uri: "kamelet:ibm-watson-language-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## IBM Watson Natural Language Understanding Sink Kamelet Description

### Authentication

This Kamelet uses IBM Cloud IAM (Identity and Access Management) for authentication. You need to provide:

-   **apiKey**: Your IBM Cloud API key with access to Watson Natural Language Understanding service
    
-   **serviceUrl** (optional): The Watson NLU service endpoint URL for your region
    

### Getting your credentials

1.  Log in to the [IBM Cloud Console](https://cloud.ibm.com)
    
2.  Navigate to your Watson Natural Language Understanding service instance
    
3.  Go to **Service credentials** section
    
4.  Create new credentials or use existing ones
    
5.  Copy the **apikey** value
    

### Regional endpoints

Watson Natural Language Understanding provides different endpoints for different regions:

-   **US South**: `[https://api.us-south.natural-language-understanding.watson.cloud.ibm.com](https://api.us-south.natural-language-understanding.watson.cloud.ibm.com)`
    
-   **US East**: `[https://api.us-east.natural-language-understanding.watson.cloud.ibm.com](https://api.us-east.natural-language-understanding.watson.cloud.ibm.com)`
    
-   **EU GB (London)**: `[https://api.eu-gb.natural-language-understanding.watson.cloud.ibm.com](https://api.eu-gb.natural-language-understanding.watson.cloud.ibm.com)`
    
-   **EU DE (Frankfurt)**: `[https://api.eu-de.natural-language-understanding.watson.cloud.ibm.com](https://api.eu-de.natural-language-understanding.watson.cloud.ibm.com)`
    
-   **Tokyo**: `[https://api.jp-tok.natural-language-understanding.watson.cloud.ibm.com](https://api.jp-tok.natural-language-understanding.watson.cloud.ibm.com)`
    
-   **Sydney**: `[https://api.au-syd.natural-language-understanding.watson.cloud.ibm.com](https://api.au-syd.natural-language-understanding.watson.cloud.ibm.com)`
    

If not specified, the kamelet uses the default US South endpoint.

For more information, see the [Watson Natural Language Understanding API documentation](https://cloud.ibm.com/apidocs/natural-language-understanding).

### Analysis features

Watson NLU can analyze text for:

-   **Sentiment** - Detect positive, negative, or neutral sentiment (enabled by default)
    
-   **Emotions** - Identify joy, anger, sadness, fear, disgust
    
-   **Entities** - Extract people, companies, organizations, cities (enabled by default)
    
-   **Keywords** - Extract important keywords and phrases (enabled by default)
    
-   **Concepts** - Identify high-level concepts not explicitly mentioned
    
-   **Categories** - Classify content into hierarchical categories
    

You can enable or disable each feature using the kamelet properties.

### Operations

This kamelet supports two operations:

-   **analyzeText** (default) - Analyze text provided in the message body
    
-   **analyzeUrl** - Analyze content from a URL specified in the `CamelIBMWatsonLanguageUrl` header
    

### Pricing

Watson Natural Language Understanding offers a free tier:

-   **Lite Plan**: 30,000 NLU items per month (free)
    
-   Additional items are charged per item
    

For current pricing details, visit the [Watson NLU Pricing page](https://www.ibm.com/cloud/watson-natural-language-understanding/pricing).

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/ibm-watson-language-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/ibm-watson-language-sink.kamelet.yaml)