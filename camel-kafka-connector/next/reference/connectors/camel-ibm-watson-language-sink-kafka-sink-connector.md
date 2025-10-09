# camel-ibm-watson-language-sink-kafka-connector sink configuration

Connector Description: Analyze text using IBM Watson Natural Language Understanding to extract sentiment, entities, keywords, concepts, categories, and emotions.

When using camel-ibm-watson-language-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-ibm-watson-language-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.ibmwatsonlanguagesink.CamelIbmwatsonlanguagesinkSinkConnector
```

The camel-ibm-watson-language-sink sink connector supports 9 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.ibm-watson-language-sink.apiKey** | **Required** The IBM Cloud API key for Watson Natural Language Understanding. |  | HIGH |
| **camel.kamelet.ibm-watson-language-sink.serviceUrl** | The Watson Natural Language Understanding service endpoint URL. If not specified, the default URL will be used. Example: [https://api.us-south.natural-language-understanding.watson.cloud.ibm.com](https://api.us-south.natural-language-understanding.watson.cloud.ibm.com). |  | MEDIUM |
| **camel.kamelet.ibm-watson-language-sink.operation** | The operation to perform. | "analyzeText" | MEDIUM |
| **camel.kamelet.ibm-watson-language-sink.analyzeSentiment** | Enable sentiment analysis to detect positive, negative, or neutral sentiment. | true | MEDIUM |
| **camel.kamelet.ibm-watson-language-sink.analyzeEmotion** | Enable emotion analysis to detect emotions like joy, anger, sadness, fear, and disgust. | false | MEDIUM |
| **camel.kamelet.ibm-watson-language-sink.analyzeEntities** | Enable entity extraction to identify people, companies, organizations, cities, and more. | true | MEDIUM |
| **camel.kamelet.ibm-watson-language-sink.analyzeKeywords** | Enable keyword extraction to identify important keywords and phrases. | true | MEDIUM |
| **camel.kamelet.ibm-watson-language-sink.analyzeConcepts** | Enable concept extraction to identify high-level concepts that aren’t necessarily mentioned in the text. | false | MEDIUM |
| **camel.kamelet.ibm-watson-language-sink.analyzeCategories** | Enable category classification to classify content into a hierarchy of categories. | false | MEDIUM |

The camel-ibm-watson-language-sink sink connector has no converters out of the box.

The camel-ibm-watson-language-sink sink connector has no transforms out of the box.

The camel-ibm-watson-language-sink sink connector has no aggregation strategies out of the box.