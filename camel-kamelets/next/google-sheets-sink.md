# ![google sheets sink](_images/kamelets/google-sheets-sink.svg) Google Sheets Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Writes each message as one or more rows to a Google Sheets spreadsheet, either appended after the last row or written over a given range of cells.

Use it to collect data in a spreadsheet that people can read and share, such as form submissions, orders or daily figures. To read the rows of a spreadsheet, use `google-sheets-source`.

Input: the body is JSON text: a JSON object for one row, or a JSON array of objects for several rows. The keys are the column letters of the cells to write, such as `{"A": "Alice", "B": 3}`, or the names set in `columnNames`. Only the columns of `range` are written, so set `range` to cover them, such as `A:B`.

Output: when it is used inside a route, the body afterwards is the response of Google Sheets, which says which cells were written.

Good to know: without `range`, only column `A` is written. With the default `operation` of `append`, the rows are added after the last row of the table found in `range`; with `update`, they overwrite the cells of `range`. It logs in to Google with OAuth: an OAuth client of a Google Cloud project, and an access token and a refresh token of the Google account that owns or may edit the spreadsheet.

## Configuration Options

The following table summarizes the configuration options available for the `google-sheets-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** An OAuth 2 access token of the Google account, with access to Google Sheets. It expires after about an hour; the Kamelet then gets a new one with `refreshToken`. | string |  |  |
| **clientId** | Client ID | **Required** The client ID of an OAuth client, created in the Google Cloud console under APIs & Services > Credentials, in a project where the Google Sheets API is enabled. | string |  |  |
| **clientSecret** | Client Secret | **Required** The client secret of the OAuth client of `clientId`. | string |  |  |
| **refreshToken** | Refresh Token | **Required** An OAuth 2 refresh token of the Google account, which the Kamelet uses to get a new access token when the current one expires. You get it together with the access token, for example from the Google OAuth 2.0 Playground. | string |  |  |
| **spreadsheetId** | Spreadsheet ID | **Required** The ID of the spreadsheet, the long part of its address between `/d/` and `/edit`, as in `[https://docs.google.com/spreadsheets/d/<ID>/edit](https://docs.google.com/spreadsheets/d/\<ID\>/edit)`. | string |  | 1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms |
| **applicationName** | Application Name | A name for your application, sent to Google with each call, such as `my-company-sheets/1.0`. | string |  | my-company-sheets/1.0 |
| **columnNames** | Column Names | Names to use as keys in the JSON objects instead of the column letters, separated by commas, in the order of the columns of `range`. For example, with `range` `A:B`, `name,qty` reads the key `name` into column A and `qty` into column B. | string | A | name,qty |
| **majorDimension** | Major Dimension | `ROWS` writes each JSON object as a row; `COLUMNS` writes each JSON object as a column, with the keys `#1`, `#2` and so on for the row numbers. Enum values: \* COLUMNS \* ROWS | string | ROWS | ROWS |
| **operation** | Operation Mode | `append` adds the rows after the last row of the table found in `range`; `update` writes them over the cells of `range`. Enum values: \* update \* append | string | append | append |
| **range** | Cells Range | The cells to write to, in A1 notation, optionally with the name of the sheet, such as `Sheet1!A:C` or `A1:B3`. Its columns decide which keys of each JSON object are written. | string |  | Sheet1!A:C |
| **valueInputOption** | Value Input Option | `USER_ENTERED` reads each value as if a person typed it, so `=SUM(A1:A3)` becomes a formula and `3` a number; `RAW` stores each value as it is. Enum values: \* USER\_ENTERED \* RAW | string | USER\_ENTERED | USER\_ENTERED |

## Dependencies

At runtime, the `google-sheets-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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

This Kamelet expects JSON text: a JSON object for one row, or a JSON array of objects for several rows. The keys are the column letters, such as `{"A": "Alice", "B": 3}`, or the names set in `columnNames`. Only the columns of `range` are written, so set `range` to cover them, such as `A:B`; without it, only column A is written.

### Operation Modes

-   **Update**: Updates existing data in specified cells
    
-   **Append**: Appends new data to the spreadsheet (default)
    

### Configuration Options

-   **Spreadsheet ID**: The unique identifier for your Google Sheets spreadsheet
    
-   **Range**: Cell range specification (e.g., "A1:B3")
    
-   **Major Dimension**: ROWS (default) or COLUMNS
    
-   **Column Names**: Custom column mappings
    
-   **Value Input Option**: USER\_ENTERED (default) or RAW
    

### Headers

The Kamelet sets these headers from its options before it writes, so headers that the message already has are replaced:

-   `CamelGoogleSheets.range`: the `range` option
    
-   `CamelGoogleSheets.spreadsheetId`: the `spreadsheetId` option
    
-   `CamelGoogleSheets.majorDimension`: the `majorDimension` option
    
-   `CamelGoogleSheets.columnNames`: the `columnNames` option
    
-   `CamelGoogleSheets.valueInputOption`: the `valueInputOption` option
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-sheets-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-sheets-sink.kamelet.yaml)