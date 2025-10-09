# camel-google-sheets-source-kafka-connector source configuration

Connector Description: Receive data from Google Sheets.

When using camel-google-sheets-source-kafka-connector as source make sure to use the following Maven dependency to have support for the connector:

```xml
<dependency>
  <groupId>org.apache.camel.kafkaconnector</groupId>
  <artifactId>camel-google-sheets-source-kafka-connector</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel Kafka connector version -->
</dependency>
```

To use this source connector in Kafka connect you’ll need to set the following connector.class

```java
connector.class=org.apache.camel.kafkaconnector.googlesheetssource.CamelGooglesheetssourceSourceConnector
```

The camel-google-sheets-source source connector supports 12 options, which are listed below.

   
| Name | Description | Default | Priority |
| --- | --- | --- | --- |
| **camel.kamelet.google-sheets-source.spreadsheetId** | **Required** The Spreadsheet ID to be used as events source. |  | HIGH |
| **camel.kamelet.google-sheets-source.clientId** | **Required** Client ID of the sheets application. |  | HIGH |
| **camel.kamelet.google-sheets-source.clientSecret** | **Required** Client Secret of the sheets application. |  | HIGH |
| **camel.kamelet.google-sheets-source.accessToken** | **Required** OAuth 2 access token for google sheets application. This typically expires after an hour so refreshToken is recommended for long term usage. |  | HIGH |
| **camel.kamelet.google-sheets-source.refreshToken** | **Required** OAuth 2 refresh token for google sheets application. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. |  | HIGH |
| **camel.kamelet.google-sheets-source.delay** | The number of milliseconds before the next poll. | 500 | MEDIUM |
| **camel.kamelet.google-sheets-source.repeatCount** | Specifies a maximum limit of number of fires. |  | MEDIUM |
| **camel.kamelet.google-sheets-source.applicationName** | Google Sheets application name. |  | MEDIUM |
| **camel.kamelet.google-sheets-source.splitResults** | True if value range result should be split into rows or columns to process each of them individually. | true | MEDIUM |
| **camel.kamelet.google-sheets-source.range** | The range of rows and columns in a sheet to get data from. Example: A1:B3. |  | MEDIUM |
| **camel.kamelet.google-sheets-source.majorDimension** | Specifies the major dimension that the given values should use (ROWS or COLUMNS). Example: ROWS. | "ROWS" | MEDIUM |
| **camel.kamelet.google-sheets-source.columnNames** | Optional custom column names that map to cell coordinates based on their position. | "A" | MEDIUM |

The camel-google-sheets-source source connector has no converters out of the box.

The camel-google-sheets-source source connector has no transforms out of the box.

The camel-google-sheets-source source connector has no aggregation strategies out of the box.