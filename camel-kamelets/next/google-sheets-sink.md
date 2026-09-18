# ![google sheets sink](_images/kamelets/google-sheets-sink.svg) Google Sheets Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Send data to Google Sheets and update/append values on a spreadsheet.

## Configuration Options

The following table summarizes the configuration options available for the `google-sheets-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** OAuth 2 access token for google sheets application. This typically expires after an hour so refreshToken is recommended for long term usage. | string |  |  |
| **clientId** | Client Id | **Required** Client ID of the sheets application. | string |  |  |
| **clientSecret** | Client Secret | **Required** Client Secret of the sheets application. | string |  |  |
| **refreshToken** | Refresh Token | **Required** OAuth 2 refresh token for google sheets application. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. | string |  |  |
| **spreadsheetId** | Spreadsheet ID | **Required** The Spreadsheet ID to be used as identifier. | string |  |  |
| **applicationName** | Application Name | Google Sheets application name. | string |  |  |
| **columnNames** | Column Names | Optional custom column names that map to cell coordinates based on their position. | string | A |  |
| **majorDimension** | Major Dimension | Specifies the major dimension that the given values should use (ROWS or COLUMNS). Enum values: \* COLUMNS \* ROWS | string | ROWS | ROWS |
| **operation** | Operation Mode | Operation to execute (update or append). Enum values: \* update \* append | string | append | append |
| **range** | Cells Range | The cell range of rows and columns to write data to. | string |  | A1:B3 |
| **valueInputOption** | Value Input Option | Controls how the entered values should be be interpreted when adding them. Enum values: \* USER\_ENTERED \* RAW | string | USER\_ENTERED | USER\_ENTERED |

## Dependencies

At runtime, the `google-sheets-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:core
    
-   camel:jackson
    
-   camel:kamelet
    
-   camel:google-sheets
    

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
            uri: "kamelet:google-sheets-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Google Sheets Sink Kamelet Description

### Authentication

This Kamelet uses OAuth 2.0 authentication with Google Sheets API. You need to provide: - Client ID and Client Secret from your Google Cloud Console application - Access Token (typically expires after an hour) - Refresh Token for long-term usage (recommended)

### Input Format

This Kamelet expects JSON data that will be transformed into Google Sheets ValueRange format.

### Operation Modes

-   **Update**: Updates existing data in specified cells
    
-   **Append**: Appends new data to the spreadsheet (default)
    

### Configuration Options

-   **Spreadsheet ID**: The unique identifier for your Google Sheets spreadsheet
    
-   **Range**: Cell range specification (e.g., "A1:B3")
    
-   **Major Dimension**: ROWS (default) or COLUMNS
    
-   **Column Names**: Custom column mappings
    
-   **Value Input Option**: USER\_ENTERED (default) or RAW
    

### Headers Support

The Kamelet supports various headers to override configuration: - `CamelGoogleSheets.range`: Override the cell range - `CamelGoogleSheets.spreadsheetId`: Override spreadsheet ID - `CamelGoogleSheets.majorDimension`: Override major dimension - `CamelGoogleSheets.columnNames`: Override column names - `CamelGoogleSheets.valueInputOption`: Override value input option

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-sheets-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-sheets-sink.kamelet.yaml)