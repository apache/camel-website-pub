# ![google sheets source](_images/kamelets/google-sheets-source.svg) Google Sheets Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the cells of a Google Sheets spreadsheet again and again, at a regular interval, and sends each row of the range as a message.

Use it to feed the content of a spreadsheet that people maintain, such as a price list, a contact list or a list of tasks, to another system on a schedule. To write rows to a spreadsheet, use `google-sheets-sink`.

Output: with `range` set, the body is one row as JSON text, a JSON array of the values of the row (or of one column, with `majorDimension` set to `COLUMNS`), such as `["Alice","3"]`; with `splitResults` set to false, it is the whole range as JSON text, with the rows in its `values` field. Without `range`, the body is the description of the spreadsheet (its sheets and properties) as JSON text, not its cells. The `CamelGoogleSheets.spreadsheetId` and `CamelGoogleSheets.range` headers repeat the options.

Good to know: every poll reads the whole range again, by default every 500 milliseconds, so the same rows come again and again until `repeatCount` is reached; it does not track which rows are new. It logs in to Google with OAuth: an OAuth client of a Google Cloud project, and an access token and a refresh token of a Google account that may read the spreadsheet.

## Configuration Options

The following table summarizes the configuration options available for the `google-sheets-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** An OAuth 2 access token of the Google account, with access to Google Sheets. It expires after about an hour; the Kamelet then gets a new one with `refreshToken`. | string |  |  |
| **clientId** | Client ID | **Required** The client ID of an OAuth client, created in the Google Cloud console under APIs & Services > Credentials, in a project where the Google Sheets API is enabled. | string |  |  |
| **clientSecret** | Client Secret | **Required** The client secret of the OAuth client of `clientId`. | string |  |  |
| **refreshToken** | Refresh Token | **Required** An OAuth 2 refresh token of the Google account, which the Kamelet uses to get a new access token when the current one expires. You get it together with the access token, for example from the Google OAuth 2.0 Playground. | string |  |  |
| **spreadsheetId** | Spreadsheet ID | **Required** The ID of the spreadsheet, the long part of its address between `/d/` and `/edit`, as in `[https://docs.google.com/spreadsheets/d/<ID>/edit](https://docs.google.com/spreadsheets/d/\<ID\>/edit)`. | string |  | 1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms |
| **applicationName** | Application Name | A name for your application, sent to Google with each call, such as `my-company-sheets/1.0`. | string |  | my-company-sheets/1.0 |
| **columnNames** | Column Names | Sets the `CamelGoogleSheets.columnNames` header, for a later step that turns the rows into JSON objects with these names as keys instead of the column letters. Names separated by commas, in the order of the columns. | string | A | name,qty |
| **delay** | Delay | How long to wait between two reads of the spreadsheet, in milliseconds. For example, 60000 is one minute. | integer | 500 | 60000 |
| **majorDimension** | Major Dimension | Whether the cells are read by rows (`ROWS`) or by columns (`COLUMNS`). With `COLUMNS`, each message holds one column instead of one row. It is also set as the `CamelGoogleSheets.majorDimension` header. Enum values: \* COLUMNS \* ROWS | string | ROWS | ROWS |
| **range** | Cells Range | The cells to read, in A1 notation, optionally with the name of the sheet, such as `Sheet1!A2:C100`. Several ranges can be given, separated by commas. When it is not set, the description of the spreadsheet is read instead of its cells. | string |  | Sheet1!A2:C100 |
| **repeatCount** | Repeat Count | How many times to read the spreadsheet in total, such as 1 to read it once. When it is not set, it is read again every `delay` until the integration is stopped. | integer |  | 1 |
| **splitResults** | Split Results | If true, each row of `range` is sent as a message of its own. If false, the whole range is sent as one message. Only used when `range` is set. | boolean | true |  |

## Dependencies

At runtime, the `google-sheets-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:google-sheets-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Google Sheets Source Kamelet Description

### Authentication methods

This Kamelet uses OAuth 2.0 authentication to connect to Google Sheets. You need to provide:

-   Client ID and Client Secret from your Google Cloud Console application
    
-   Access Token for immediate access (typically expires after an hour)
    
-   Refresh Token for long-term usage (allows automatic token renewal)
    
-   The Spreadsheet ID from which to read data
    

### Output format

The Kamelet produces spreadsheet data in JSON format from the specified Google Sheets document.

### Configuration

The Kamelet requires the following parameters:

-   `spreadsheetId`: The Spreadsheet ID to be used as events source
    
-   `clientId`: Client ID of the sheets application
    
-   `clientSecret`: Client Secret of the sheets application
    
-   `accessToken`: OAuth 2 access token
    
-   `refreshToken`: OAuth 2 refresh token for long term usage
    

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: google-sheets-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: google-sheets-source
    properties:
      spreadsheetId: "1BxEBc3z8Zm4x7_5uW9QdQpVmW8QFvOoE"
      clientId: "{{client-id}}"
      clientSecret: "{{client-secret}}"
      accessToken: "{{access-token}}"
      refreshToken: "{{refresh-token}}"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-sheets-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-sheets-source.kamelet.yaml)