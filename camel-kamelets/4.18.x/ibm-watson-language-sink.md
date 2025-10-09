# ![ibm watson language sink](_images/kamelets/ibm-watson-language-sink.svg) IBM Watson Natural Language Understanding Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Analyze text using IBM Watson Natural Language Understanding to extract sentiment, entities, keywords, concepts, categories, and emotions.

## Configuration Options

The following table summarizes the configuration options available for the `ibm-watson-language-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **apiKey** | API Key | **Required** The IBM Cloud API key for Watson Natural Language Understanding. | string |  |  |
| **analyzeCategories** | Analyze Categories | Enable category classification to classify content into a hierarchy of categories. | boolean | false |  |
| **analyzeConcepts** | Analyze Concepts | Enable concept extraction to identify high-level concepts that aren’t necessarily mentioned in the text. | boolean | false |  |
| **analyzeEmotion** | Analyze Emotion | Enable emotion analysis to detect emotions like joy, anger, sadness, fear, and disgust. | boolean | false |  |
| **analyzeEntities** | Analyze Entities | Enable entity extraction to identify people, companies, organizations, cities, and more. | boolean | true |  |
| **analyzeKeywords** | Analyze Keywords | Enable keyword extraction to identify important keywords and phrases. | boolean | true |  |
| **analyzeSentiment** | Analyze Sentiment | Enable sentiment analysis to detect positive, negative, or neutral sentiment. | boolean | true |  |
| **operation** | Operation | The operation to perform. Enum values: \* analyzeText \* analyzeUrl | string | analyzeText |  |
| **serviceUrl** | Service URL | The Watson Natural Language Understanding service endpoint URL. If not specified, the default URL will be used. | string |  | https://api.us-south.natural-language-understanding.watson.cloud.ibm.com |

## Dependencies

At runtime, the `ibm-watson-language-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
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