# camel-google-sheets-sink-kafka-connector sink configuration

Connector Description: Send data to Google Sheets and update/append values on a spreadsheet.

When using camel-google-sheets-sink-kafka-connector as sink make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-sheets-sink-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this sink connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlesheetssink.CamelGooglesheetssinkSinkConnector
```

The camel-google-sheets-sink sink connector supports 11 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-sheets-sink.spreadsheetId** | **Required** The Spreadsheet ID to be used as identifier. |  | HIGH |
| **camel.kamelet.google-sheets-sink.clientId** | **Required** Client ID of the sheets application. |  | HIGH |
| **camel.kamelet.google-sheets-sink.clientSecret** | **Required** Client Secret of the sheets application. |  | HIGH |
| **camel.kamelet.google-sheets-sink.accessToken** | **Required** OAuth 2 access token for google sheets application. This typically expires after an hour so refreshToken is recommended for long term usage. |  | HIGH |
| **camel.kamelet.google-sheets-sink.refreshToken** | **Required** OAuth 2 refresh token for google sheets application. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | HIGH |
| **camel.kamelet.google-sheets-sink.applicationName** | Google Sheets application name. |  | MEDIUM |
| **camel.kamelet.google-sheets-sink.operation** | Operation to execute (update or append) Example: append. | "append" | MEDIUM |
| **camel.kamelet.google-sheets-sink.range** | The cell range of rows and columns to write data to. Example: A1:B3. |  | MEDIUM |
| **camel.kamelet.google-sheets-sink.majorDimension** | Specifies the major dimension that the given values should use (ROWS or COLUMNS). Example: ROWS. | "ROWS" | MEDIUM |
| **camel.kamelet.google-sheets-sink.columnNames** | Optional custom column names that map to cell coordinates based on their position. | "A" | MEDIUM |
| **camel.kamelet.google-sheets-sink.valueInputOption** | Controls how the entered values should be be interpreted when adding them. Example: USER\_ENTERED. | "USER\_ENTERED" | MEDIUM |

The camel-google-sheets-sink sink connector has no converters out of the box.

The camel-google-sheets-sink sink connector has no transforms out of the box.

The camel-google-sheets-sink sink connector has no aggregation strategies out of the box.