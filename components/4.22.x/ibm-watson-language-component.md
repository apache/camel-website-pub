# IBM Watson Language

**Since Camel 4.16**

**Only producer is supported**

The IBM Watson Language component provides natural language understanding capabilities using [IBM Watson Natural Language Understanding](https://www.ibm.com/cloud/watson-natural-language-understanding).

Prerequisites

You must have a valid IBM Cloud account and have provisioned a Watson Natural Language Understanding service instance.

## URI Format

ibm-watson-language:label\[?options\]

Where `label` is a logical name for the endpoint.

You can append query options to the URI in the following format:

`?option1=value&option2=value&…​`

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The IBM Watson Language component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceUrl** (common) | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **analyzeCategories** (producer) | Enable category classification. | false | boolean |
| **analyzeConcepts** (producer) | Enable concept extraction. | false | boolean |
| **analyzeEmotion** (producer) | Enable emotion analysis. | false | boolean |
| **analyzeEntities** (producer) | Enable entity extraction. | true | boolean |
| **analyzeKeywords** (producer) | Enable keyword extraction. | true | boolean |
| **analyzeSentiment** (producer) | Enable sentiment analysis. | true | boolean |
| **configuration** (producer) | Component configuration. |  | WatsonLanguageConfiguration |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   analyzeText
    
-   analyzeUrl
    





 |  | WatsonLanguageOperations |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **healthCheckConsumerEnabled** (health) | Used for enabling or disabling all consumer based health checks from this component. | true | boolean |
| **healthCheckProducerEnabled** (health) | Used for enabling or disabling all producer based health checks from this component. Notice: Camel has by default disabled all producer based health-checks. You can turn on producer checks globally by setting camel.health.producersEnabled=true. | true | boolean |
| **apiKey** (security) | **Required** The IBM Cloud API key for authentication. |  | String |

## Endpoint Options

The IBM Watson Language endpoint is configured using URI syntax:

ibm-watson-language:label

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **label** (producer) | **Required** Logical name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **serviceUrl** (common) | The service endpoint URL. If not specified, the default URL will be used. |  | String |
| **analyzeCategories** (producer) | Enable category classification. | false | boolean |
| **analyzeConcepts** (producer) | Enable concept extraction. | false | boolean |
| **analyzeEmotion** (producer) | Enable emotion analysis. | false | boolean |
| **analyzeEntities** (producer) | Enable entity extraction. | true | boolean |
| **analyzeKeywords** (producer) | Enable keyword extraction. | true | boolean |
| **analyzeSentiment** (producer) | Enable sentiment analysis. | true | boolean |
| **operation** (producer) | 
The operation to perform.

Enum values:

-   analyzeText
    
-   analyzeUrl
    





 |  | WatsonLanguageOperations |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **apiKey** (security) | **Required** The IBM Cloud API key for authentication. |  | String |

## Message Headers

The IBM Watson Language component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelIBMWatsonLanguageOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#OPERATION) | The operation to perform. |  | String |
| **CamelIBMWatsonLanguageText** (producer) Constant: [`TEXT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#TEXT) | The text to analyze. |  | String |
| **CamelIBMWatsonLanguageUrl** (producer) Constant: [`URL`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#URL) | The URL to analyze. |  | String |
| **CamelIBMWatsonLanguageAnalyzeSentiment** (producer) Constant: [`ANALYZE_SENTIMENT`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#ANALYZE_SENTIMENT) | Enable sentiment analysis. |  | Boolean |
| **CamelIBMWatsonLanguageAnalyzeEmotion** (producer) Constant: [`ANALYZE_EMOTION`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#ANALYZE_EMOTION) | Enable emotion analysis. |  | Boolean |
| **CamelIBMWatsonLanguageAnalyzeEntities** (producer) Constant: [`ANALYZE_ENTITIES`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#ANALYZE_ENTITIES) | Enable entity extraction. |  | Boolean |
| **CamelIBMWatsonLanguageAnalyzeKeywords** (producer) Constant: [`ANALYZE_KEYWORDS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#ANALYZE_KEYWORDS) | Enable keyword extraction. |  | Boolean |
| **CamelIBMWatsonLanguageAnalyzeConcepts** (producer) Constant: [`ANALYZE_CONCEPTS`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#ANALYZE_CONCEPTS) | Enable concept extraction. |  | Boolean |
| **CamelIBMWatsonLanguageAnalyzeCategories** (producer) Constant: [`ANALYZE_CATEGORIES`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#ANALYZE_CATEGORIES) | Enable category classification. |  | Boolean |
| **CamelIBMWatsonLanguageLanguage** (producer) Constant: [`LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#LANGUAGE) | The language of the text. |  | String |
| **CamelIBMWatsonLanguageSentimentScore** (producer) Constant: [`SENTIMENT_SCORE`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#SENTIMENT_SCORE) | The sentiment score. |  | Double |
| **CamelIBMWatsonLanguageSentimentLabel** (producer) Constant: [`SENTIMENT_LABEL`](https://javadoc.io/doc/org.apache.camel/camel-ibm-watson-language/latest/org/apache/camel/component/ibm/watson/language/WatsonLanguageConstants.html#SENTIMENT_LABEL) | The sentiment label (positive, negative, neutral). |  | String |

Required IBM Watson Language component options

You must provide the `apiKey` for authentication and optionally the `serviceUrl` for your Watson service instance.

## Usage

### IBM Watson Natural Language Understanding

This component integrates with IBM Watson Natural Language Understanding service to analyze text and extract metadata like sentiment, entities, keywords, concepts, categories, and emotions.

### Authentication

IBM Watson services use IBM Cloud IAM (Identity and Access Management) for authentication. You need to provide:

-   `apiKey`: Your IBM Cloud API key
    
-   `serviceUrl`: The endpoint URL for your Watson service instance (optional, defaults to the public endpoint)
    

You can find your service credentials in the IBM Cloud console.

### Operations

1.  `analyzeText` - Analyze text content provided in the message body or header
    
2.  `analyzeUrl` - Analyze content from a URL
    

### Analysis Features

You can enable/disable various analysis features:

-   `analyzeSentiment` - Detect positive, negative, or neutral sentiment (default: true)
    
-   `analyzeEntities` - Extract people, companies, organizations, cities, etc. (default: true)
    
-   `analyzeKeywords` - Extract important keywords (default: true)
    
-   `analyzeEmotion` - Detect emotions like joy, anger, sadness (default: false)
    
-   `analyzeConcepts` - Identify high-level concepts (default: false)
    
-   `analyzeCategories` - Classify content into categories (default: false)
    

## Examples

### Sentiment Analysis Example

Analyze sentiment of text:

-   Java
    
-   YAML
    

```java
from("direct:sentiment")
    .setBody(constant("I love this product! It's amazing!"))
    .to("ibm-watson-language:default?apiKey=RAW(yourApiKey)&operation=analyzeText&analyzeSentiment=true&analyzeEntities=false&analyzeKeywords=false")
    .process(exchange -> {
        AnalysisResults results = exchange.getIn().getBody(AnalysisResults.class);
        String sentiment = results.getSentiment().getDocument().getLabel();
        Double score = results.getSentiment().getDocument().getScore();
        // Or use convenience headers:
        String sentimentLabel = exchange.getIn().getHeader("CamelIBMWatsonLanguageSentimentLabel", String.class);
        Double sentimentScore = exchange.getIn().getHeader("CamelIBMWatsonLanguageSentimentScore", Double.class);
    });
```

```yaml
- from:
    uri: direct:sentiment
    steps:
      - setBody:
          constant: "I love this product! It's amazing!"
      - to:
          uri: ibm-watson-language:default
          parameters:
            apiKey: RAW(yourApiKey)
            operation: analyzeText
            analyzeSentiment: true
            analyzeEntities: false
            analyzeKeywords: false
      - log: "Sentiment: ${header.CamelIBMWatsonLanguageSentimentLabel} (${header.CamelIBMWatsonLanguageSentimentScore})"
```

The full `AnalysisResults` object is returned in the body, containing all requested analyses (sentiment, entities, keywords, etc.). Common values like sentiment score and label are also available as headers for convenience.

### Extract Entities and Keywords

Analyze text to extract entities and keywords:

-   Java
    
-   YAML
    

```java
from("direct:analyze")
    .setBody(constant("IBM Watson is an AI platform developed by IBM in Armonk, New York."))
    .to("ibm-watson-language:default?apiKey=RAW(yourApiKey)&operation=analyzeText&analyzeSentiment=false&analyzeEntities=true&analyzeKeywords=true")
    .process(exchange -> {
        AnalysisResults results = exchange.getIn().getBody(AnalysisResults.class);
        results.getEntities().forEach(entity ->
            System.out.println("Entity: " + entity.getText() + " (" + entity.getType() + ")")
        );
        results.getKeywords().forEach(keyword ->
            System.out.println("Keyword: " + keyword.getText() + " (relevance: " + keyword.getRelevance() + ")")
        );
    });
```

```yaml
- from:
    uri: direct:analyze
    steps:
      - setBody:
          constant: "IBM Watson is an AI platform developed by IBM in Armonk, New York."
      - to:
          uri: ibm-watson-language:default
          parameters:
            apiKey: RAW(yourApiKey)
            operation: analyzeText
            analyzeSentiment: false
            analyzeEntities: true
            analyzeKeywords: true
      - log: "Analysis complete: ${body}"
```

### Comprehensive Analysis

Analyze text with multiple features enabled:

-   Java
    
-   YAML
    

```java
from("direct:comprehensive")
    .setBody(constant("Apple Inc. announced record profits. The CEO praised the team's innovation."))
    .to("ibm-watson-language:default?apiKey=RAW(yourApiKey)&operation=analyzeText&analyzeSentiment=true&analyzeEntities=true&analyzeKeywords=true&analyzeEmotion=true")
    .process(exchange -> {
        AnalysisResults results = exchange.getIn().getBody(AnalysisResults.class);
        System.out.println("Sentiment: " + results.getSentiment().getDocument().getLabel());
        System.out.println("Entities: " + results.getEntities().size());
        System.out.println("Keywords: " + results.getKeywords().size());
        if (results.getEmotion() != null) {
            System.out.println("Emotions: " + results.getEmotion().getDocument().getEmotion());
        }
    });
```

```yaml
- from:
    uri: direct:comprehensive
    steps:
      - setBody:
          constant: "Apple Inc. announced record profits. The CEO praised the team's innovation."
      - to:
          uri: ibm-watson-language:default
          parameters:
            apiKey: RAW(yourApiKey)
            operation: analyzeText
            analyzeSentiment: true
            analyzeEntities: true
            analyzeKeywords: true
            analyzeEmotion: true
```

### Analyze URL

Analyze content from a webpage:

-   Java
    
-   YAML
    

```java
from("direct:url")
    .setHeader("CamelIBMWatsonLanguageUrl", constant("https://www.ibm.com/watson"))
    .to("ibm-watson-language:default?apiKey=RAW(yourApiKey)&operation=analyzeUrl&analyzeSentiment=true&analyzeKeywords=true")
    .process(exchange -> {
        AnalysisResults results = exchange.getIn().getBody(AnalysisResults.class);
        System.out.println("Page language: " + results.getLanguage());
        System.out.println("Page sentiment: " + results.getSentiment().getDocument().getLabel());
    });
```

```yaml
- from:
    uri: direct:url
    steps:
      - setHeader:
          name: CamelIBMWatsonLanguageUrl
          constant: "https://www.ibm.com/watson"
      - to:
          uri: ibm-watson-language:default
          parameters:
            apiKey: RAW(yourApiKey)
            operation: analyzeUrl
            analyzeSentiment: true
            analyzeKeywords: true
      - log: "Page sentiment: ${header.CamelIBMWatsonLanguageSentimentLabel}"
```

### Dynamic Feature Selection

Use headers to dynamically enable/disable analysis features:

-   Java
    
-   YAML
    

```java
from("direct:dynamic")
    .setBody(constant("This is great news for the company!"))
    .setHeader(WatsonLanguageConstants.ANALYZE_SENTIMENT, constant(true))
    .setHeader(WatsonLanguageConstants.ANALYZE_EMOTION, constant(true))
    .setHeader(WatsonLanguageConstants.ANALYZE_KEYWORDS, constant(false))
    .to("ibm-watson-language:default?apiKey=RAW(yourApiKey)&operation=analyzeText");
```

```yaml
- from:
    uri: direct:dynamic
    steps:
      - setBody:
          constant: "This is great news for the company!"
      - setHeader:
          name: CamelIBMWatsonLanguageAnalyzeSentiment
          constant: true
      - setHeader:
          name: CamelIBMWatsonLanguageAnalyzeEmotion
          constant: true
      - setHeader:
          name: CamelIBMWatsonLanguageAnalyzeKeywords
          constant: false
      - to:
          uri: ibm-watson-language:default
          parameters:
            apiKey: RAW(yourApiKey)
            operation: analyzeText
```

### Custom Service URL

If your Watson service is in a specific region, specify the service URL:

-   Java
    
-   YAML
    

```java
from("direct:regional")
    .to("ibm-watson-language:default?apiKey=RAW(yourApiKey)&serviceUrl=https://api.us-south.natural-language-understanding.watson.cloud.ibm.com&operation=analyzeText");
```

```yaml
- from:
    uri: direct:regional
    steps:
      - to:
          uri: ibm-watson-language:default
          parameters:
            apiKey: RAW(yourApiKey)
            serviceUrl: "https://api.us-south.natural-language-understanding.watson.cloud.ibm.com"
            operation: analyzeText
```

## Dependencies

Maven users will need to add the following dependency to their `pom.xml`.

**pom.xml**

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-ibm-watson-language</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

where `x.x.x` is the version number of Camel.