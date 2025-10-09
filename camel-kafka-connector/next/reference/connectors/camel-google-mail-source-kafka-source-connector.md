# camel-google-mail-source-kafka-connector source configuration

Connector Description: Receive data from Google Mail.

When using camel-google-mail-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-mail-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlemailsource.CamelGooglemailsourceSourceConnector
```

The camel-google-mail-source source connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-mail-source.index** | **Required** An index for the google mail endpoint. |  | HIGH |
| **camel.kamelet.google-mail-source.clientId** | **Required** Client ID of the gmail application. |  | HIGH |
| **camel.kamelet.google-mail-source.clientSecret** | **Required** Client Secret of the gmail application. |  | HIGH |
| **camel.kamelet.google-mail-source.accessToken** | **Required** OAuth 2 access token for google mail application. This typically expires after an hour so refreshToken is recommended for long term usage. |  | HIGH |
| **camel.kamelet.google-mail-source.refreshToken** | **Required** OAuth 2 refresh token for google mail application. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | HIGH |
| **camel.kamelet.google-mail-source.delay** | The number of milliseconds before the next poll. | 500 | MEDIUM |
| **camel.kamelet.google-mail-source.applicationName** | **Required** Google Mail application name. |  | HIGH |
| **camel.kamelet.google-mail-source.markAsRead** | Mark the message as read once it has been consumed. | true | MEDIUM |
| **camel.kamelet.google-mail-source.labels** | Comma separated list of labels to take into account Example: inbox. |  | MEDIUM |
| **camel.kamelet.google-mail-source.query** | The query to execute on gmail box Example: is:unread -category:(promotions OR social). | "is:unread" | MEDIUM |

The camel-google-mail-source source connector has no converters out of the box.

The camel-google-mail-source source connector has no transforms out of the box.

The camel-google-mail-source source connector has no aggregation strategies out of the box.