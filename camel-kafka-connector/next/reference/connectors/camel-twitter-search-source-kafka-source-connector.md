# camel-twitter-search-source-kafka-connector source configuration

Connector Description: Allows to get all tweets on particular keywords from Twitter.

When using camel-twitter-search-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-twitter-search-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.twittersearchsource.CamelTwittersearchsourceSourceConnector
```

The camel-twitter-search-source source connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.twitter-search-source.keywords** | **Required** The keywords to use in the Twitter search (Supports Twitter standard operators) Example: Apache Camel. |  | HIGH |
| **camel.kamelet.twitter-search-source.apiKey** | **Required** The API Key from the Twitter application in the developer portal. |  | HIGH |
| **camel.kamelet.twitter-search-source.apiKeySecret** | **Required** The API Key Secret from the Twitter application in the developer portal. |  | HIGH |
| **camel.kamelet.twitter-search-source.accessToken** | **Required** The Access Token from the Twitter application in the developer portal. |  | HIGH |
| **camel.kamelet.twitter-search-source.accessTokenSecret** | **Required** The Access Token Secret from the Twitter application in the developer portal. |  | HIGH |

The camel-twitter-search-source source connector has no converters out of the box.

The camel-twitter-search-source source connector has no transforms out of the box.

The camel-twitter-search-source source connector has no aggregation strategies out of the box.