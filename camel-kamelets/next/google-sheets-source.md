# ![google sheets source](_images/kamelets/google-sheets-source.svg) Google Sheets Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Reads the cells of a Google Sheets spreadsheet again and again, at a regular interval, and sends each row of the range as a message.

Use it to feed the content of a spreadsheet that people maintain, such as a price list, a contact list or a list of tasks, to another system on a schedule. To write rows to a spreadsheet, use `google-sheets-sink`.

Output: with `range` set, the body is one row as JSON text, a JSON array of the values of the row (or of one column, with `majorDimension` set to `COLUMNS`), such as `["Alice","3"]`; with `splitResults` set to false, it is the whole range as JSON text, with the rows in its `values` field. Without `range`, the body is the description of the spreadsheet (its sheets and properties) as JSON text, not its cells. The JSON text is in bytes, and the `Content-Type` header is `application/json`. The `CamelGoogleSheets.spreadsheetId` and `CamelGoogleSheets.range` headers repeat the options.

Good to know: every poll reads the whole range again, by default every 500 milliseconds, so the same rows come again and again until `repeatCount` is reached; it does not track which rows are new. It logs in to Google either with OAuth (an OAuth client of a Google Cloud project, and an access token and a refresh token of a Google account that may read the spreadsheet), or with the key of a service account in `serviceAccountKey` together with `scopes`; share the spreadsheet with the email address of the service account, or set `delegate`.

## Configuration Options

The following table summarizes the configuration options available for the `google-sheets-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **spreadsheetId** | Spreadsheet ID | **Required** The ID of the spreadsheet, the long part of its address between `/d/` and `/edit`, as in `[https://docs.google.com/spreadsheets/d/<ID>/edit](https://docs.google.com/spreadsheets/d/\<ID\>/edit)`. | string |  | 1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms |
| **accessToken** | Access Token | An OAuth 2 access token of the Google account, with access to Google Sheets. It expires after about an hour; the Kamelet then gets a new one with `refreshToken`. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **applicationName** | Application Name | A name for your application, sent to Google with each call, such as `my-company-sheets/1.0`. | string |  | my-company-sheets/1.0 |
| **clientId** | Client ID | The client ID of an OAuth client, created in the Google Cloud console under APIs & Services > Credentials, in a project where the Google Sheets API is enabled. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **clientSecret** | Client Secret | The client secret of the OAuth client of `clientId`. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **columnNames** | Column Names | Sets the `CamelGoogleSheets.columnNames` header, for a later step that turns the rows into JSON objects with these names as keys instead of the column letters. Names separated by commas, in the order of the columns. | string | A | name,qty |
| **delay** | Delay | How long to wait between two reads of the spreadsheet, in milliseconds. For example, 60000 is one minute. | integer | 500 | 60000 |
| **delegate** | Delegate User | The email address of a user of your Google Workspace, whose spreadsheets the service account of `serviceAccountKey` reads on their behalf. A Workspace administrator must first allow the client ID of the service account, with the scopes of `scopes`, under Security > Access and data control > API controls > Domain-wide delegation. Only used with `serviceAccountKey`. | string |  | alice@example.com// |
| **majorDimension** | Major Dimension | Whether the cells are read by rows (`ROWS`) or by columns (`COLUMNS`). With `COLUMNS`, each message holds one column instead of one row. It is also set as the `CamelGoogleSheets.majorDimension` header. Enum values: \* COLUMNS \* ROWS | string | ROWS | ROWS |
| **maxResults** | Max Results | The most rows of each range to send, counted from the first, or the most columns with `majorDimension` set to `COLUMNS`. For example, 1 sends only the first row. Google still returns the whole range, and the other rows are left out. When it is not set, all the rows are sent. | integer |  | 100 |
| **range** | Cells Range | The cells to read, in A1 notation, optionally with the name of the sheet, such as `Sheet1!A2:C100`. Several ranges can be given, separated by commas. When it is not set, the description of the spreadsheet is read instead of its cells. | string |  | Sheet1!A2:C100 |
| **refreshToken** | Refresh Token | An OAuth 2 refresh token of the Google account, which the Kamelet uses to get a new access token when the current one expires. You get it together with the access token, for example from the Google OAuth 2.0 Playground. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **repeatCount** | Repeat Count | How many times to read the spreadsheet in total, such as 1 to read it once. When it is not set, it is read again every `delay` until the integration is stopped. | integer |  | 1 |
| **scopes** | Scopes | The permissions to ask Google for, as URLs separated by commas, such as `[https://www.googleapis.com/auth/spreadsheets.readonly](https://www.googleapis.com/auth/spreadsheets.readonly)`. Needed with `serviceAccountKey` and with the Application Default Credentials: without them, the login asks Google for no permission at all. Leave it unset with `clientId` and `clientSecret`; with them, setting it makes the Kamelet fail. | string |  | https://www.googleapis.com/auth/spreadsheets.readonly |
| **serviceAccountKey** | Service Account Key | The JSON key of a Google service account, to log in with instead of OAuth: `file:` followed by the path of the key file, `classpath:` followed by a resource of the application, or `base64:` followed by the Base64 encoding of the key. Create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys. The service account reads the spreadsheets that are shared with its email address, or those of the user in `delegate`. It needs `scopes`. Only used when `clientId` and `clientSecret` are not set. When none of the three is set, the Application Default Credentials are used: the key file named in the `GOOGLE_APPLICATION_CREDENTIALS` environment variable, or the service account of the Google Cloud machine it runs on. | string |  | file:/etc/google/service-account.json |
| **splitResults** | Split Results | If true, each row of `range` is sent as a message of its own. If false, the whole range is sent as one message. Only used when `range` is set. | boolean | true |  |
| **valueRenderOption** | Value Render Option | How the cells are read: `FORMATTED_VALUE` as the spreadsheet shows them, as text such as `$1.50`; `UNFORMATTED_VALUE` as their values, so a number is a number such as `1.5`; `FORMULA` gives the formula of a cell, such as `=B2*2`, instead of its result. When it is not set, `FORMATTED_VALUE` is used. Enum values: \* FORMATTED\_VALUE \* UNFORMATTED\_VALUE \* FORMULA | string |  | UNFORMATTED\_VALUE |

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

The Kamelet logs in to Google in one of three ways:

-   With OAuth 2.0: `clientId` and `clientSecret` of an OAuth client from your Google Cloud Console application, an `accessToken` (it expires after about an hour) and a `refreshToken` to get new ones. Do not set `scopes` with OAuth.
    
-   With a service account: its JSON key in `serviceAccountKey`, as `file:<path>`, `classpath:<resource>` or `base64:<Base64 of the key file>`, and `scopes`, such as `[https://www.googleapis.com/auth/spreadsheets.readonly](https://www.googleapis.com/auth/spreadsheets.readonly)`. Share the spreadsheet with the email address of the service account, or set `delegate` to the email address of a user of your Google Workspace; a Workspace administrator must first allow the client ID of the service account, with these scopes, under Security > Access and data control > API controls > Domain-wide delegation.
    
-   With none of them set, the Application Default Credentials and `scopes`: the key file named in the `GOOGLE_APPLICATION_CREDENTIALS` environment variable, or the service account of the Google Cloud machine it runs on.
    

### Output format

The Kamelet produces spreadsheet data in JSON format from the specified Google Sheets document.

### Configuration

The Kamelet requires the following parameter:

-   `spreadsheetId`: The Spreadsheet ID to be used as events source
    

To log in with OAuth: `clientId`, `clientSecret`, `accessToken` and `refreshToken`. To log in with a service account: `serviceAccountKey`, `scopes` and optionally `delegate`.

Optional parameters about the cells:

-   `range`: The cells to read, such as `Sheet1!A2:C100`
    
-   `valueRenderOption`: `FORMATTED_VALUE` (as shown, such as `$1.50`, the default), `UNFORMATTED_VALUE` (numbers as numbers, such as `1.5`) or `FORMULA` (the formula, such as `=B2*2`)
    
-   `maxResults`: The most rows of each range to send, counted from the first; Google still returns the whole range
    

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

### Example with a Service Account

Reads the first 100 rows of `Prices!A2:C` once, with numbers as numbers, with the key of a service account the spreadsheet is shared with.

```yaml
- route:
    from:
      uri: "kamelet:google-sheets-source"
      parameters:
        spreadsheetId: "1BxiMVs0XRA5nFMdKvBdBZjgmUUqptlbs74OgvE2upms"
        serviceAccountKey: "file:/etc/google/service-account.json"
        scopes: "https://www.googleapis.com/auth/spreadsheets.readonly"
        range: "Prices!A2:C"
        valueRenderOption: "UNFORMATTED_VALUE"
        maxResults: 100
        repeatCount: 1
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-sheets-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-sheets-source.kamelet.yaml)