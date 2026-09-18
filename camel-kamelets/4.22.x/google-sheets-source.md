# ![google sheets source](_images/kamelets/google-sheets-source.svg) Google Sheets Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from Google Sheets.

## Configuration Options

The following table summarizes the configuration options available for the `google-sheets-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** OAuth 2 access token for google sheets application. This typically expires after an hour so refreshToken is recommended for long term usage. | string |  |  |
| **clientId** | Client Id | **Required** Client ID of the sheets application. | string |  |  |
| **clientSecret** | Client Secret | **Required** Client Secret of the sheets application. | string |  |  |
| **refreshToken** | Refresh Token | **Required** OAuth 2 refresh token for google sheets application. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. | string |  |  |
| **spreadsheetId** | Spreadsheet ID | **Required** The Spreadsheet ID to be used as events source. | string |  |  |
| **applicationName** | Application name | Google Sheets application name. | string |  |  |
| **columnNames** | Column Names | Optional custom column names that map to cell coordinates based on their position. | string | A |  |
| **delay** | Delay | The number of milliseconds before the next poll. | integer | 500 |  |
| **majorDimension** | Major Dimension | Specifies the major dimension that the given values should use (ROWS or COLUMNS). Enum values: \* COLUMNS \* ROWS | string | ROWS | ROWS |
| **range** | Cells Range | The range of rows and columns in a sheet to get data from. | string |  | A1:B3 |
| **repeatCount** | Repeat Count | Specifies a maximum limit of number of fires. | integer |  |  |
| **splitResults** | Split Results | True if value range result should be split into rows or columns to process each of them individually. | boolean | true |  |

## Dependencies

At runtime, the `google-sheets-source` Kamelet relies upon the presence of the following dependencies:

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