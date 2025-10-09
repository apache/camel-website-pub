# camel-google-calendar-source-kafka-connector source configuration

Connector Description: Receive event data from Google Calendar.

When using camel-google-calendar-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-calendar-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlecalendarsource.CamelGooglecalendarsourceSourceConnector
```

The camel-google-calendar-source source connector supports 10 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-calendar-source.index** | **Required** An index for the Google Calendar endpoint. |  | HIGH |
| **camel.kamelet.google-calendar-source.calendarId** | **Required** The calendar ID to use as the source of event data. |  | HIGH |
| **camel.kamelet.google-calendar-source.clientId** | **Required** The Client ID of the Google Calendar application. |  | HIGH |
| **camel.kamelet.google-calendar-source.clientSecret** | **Required** The Client secret of the Google Calendar application. |  | HIGH |
| **camel.kamelet.google-calendar-source.accessToken** | **Required** The OAuth 2 access token for the Google Calendar application. This token typically expires after an hour. For long term usage, set the `refreshToken` property. |  | HIGH |
| **camel.kamelet.google-calendar-source.refreshToken** | **Required** The OAuth 2 refresh token for the Google Calendar application. The Google Calendar component can obtain a new `accessToken` whenever the current one expires. Set this value for long term usage. |  | HIGH |
| **camel.kamelet.google-calendar-source.delay** | The number of milliseconds before the next poll. | 500 | MEDIUM |
| **camel.kamelet.google-calendar-source.applicationName** | **Required** The Google Calendar application name. |  | HIGH |
| **camel.kamelet.google-calendar-source.syncFlow** | Specifies to sync events for incremental synchronization. | false | MEDIUM |
| **camel.kamelet.google-calendar-source.consumeFromNow** | Specfies to consume events in the calendar from now on. | true | MEDIUM |

The camel-google-calendar-source source connector has no converters out of the box.

The camel-google-calendar-source source connector has no transforms out of the box.

The camel-google-calendar-source source connector has no aggregation strategies out of the box.