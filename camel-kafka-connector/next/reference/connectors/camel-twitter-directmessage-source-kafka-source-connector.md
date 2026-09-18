# camel-twitter-directmessage-source-kafka-connector source configuration

Connector Description: Allows to get all direct messages for your Twitter account.

When using camel-twitter-directmessage-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-twitter-directmessage-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.twitterdirectmessagesource.CamelTwitterdirectmessagesourceSourceConnector
```

The camel-twitter-directmessage-source source connector supports 5 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.twitter-directmessage-source.user** | **Required** The user we want to read the direct messages Example: ApacheCamel. |  | HIGH |
| **camel.kamelet.twitter-directmessage-source.apiKey** | **Required** The API Key from the Twitter application in the developer portal. |  | HIGH |
| **camel.kamelet.twitter-directmessage-source.apiKeySecret** | **Required** The API Key Secret from the Twitter application in the developer portal. |  | HIGH |
| **camel.kamelet.twitter-directmessage-source.accessToken** | **Required** The Access Token from the Twitter application in the developer portal. |  | HIGH |
| **camel.kamelet.twitter-directmessage-source.accessTokenSecret** | **Required** The Access Token Secret from the Twitter application in the developer portal. |  | HIGH |

The camel-twitter-directmessage-source source connector has no converters out of the box.

The camel-twitter-directmessage-source source connector has no transforms out of the box.

The camel-twitter-directmessage-source source connector has no aggregation strategies out of the box.