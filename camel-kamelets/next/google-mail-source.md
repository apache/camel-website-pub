# ![google mail source](_images/kamelets/google-mail-source.svg) Google Mail Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the emails of a Gmail mailbox that match a search, by default the unread ones, one message per email, and marks each email as read once it has been processed.

Use it to act on incoming email, for example to open a ticket for each email sent to a support address, or to collect orders or invoices that arrive by mail.

Output: the body is the text of the email (its first part with content, such as the plain text part) as JSON text, that is the text in double quotes with JSON escapes. The headers give the subject (`CamelGoogleMailStreamSubject`), the sender (`CamelGoogleMailStreamFrom`), the recipients (`CamelGoogleMailStreamTo`, `CamelGoogleMailStreamCc`, `CamelGoogleMailStreamBcc`) and the Gmail ID of the email (`CamelGoogleMailId`).

Good to know: it reads the emails that match `query`, by default the unread ones. With `markAsRead` set to false and the default query, the same emails are read again on every poll. An email whose processing fails is marked as unread again. It logs in to Google with OAuth: an OAuth client of a Google Cloud project, and an access token and a refresh token of the Gmail account.

## Configuration Options

The following table summarizes the configuration options available for the `google-mail-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** An OAuth 2 access token of the Gmail account, with access to read and change its emails. It expires after about an hour; the Kamelet then gets a new one with `refreshToken`. | string |  |  |
| **applicationName** | Application Name | **Required** A name for your application, sent to Google with each call, such as `my-company-mail/1.0`. | string |  | my-company-mail/1.0 |
| **clientId** | Client ID | **Required** The client ID of an OAuth client, created in the Google Cloud console under APIs & Services > Credentials, in a project where the Gmail API is enabled. | string |  |  |
| **clientSecret** | Client Secret | **Required** The client secret of the OAuth client of `clientId`. | string |  |  |
| **index** | Index | **Required** Any name for this reader of the mailbox, such as `support`. It is not sent to Google. | string |  | support |
| **refreshToken** | Refresh Token | **Required** An OAuth 2 refresh token of the Gmail account, which the Kamelet uses to get a new access token when the current one expires. You get it together with the access token, for example from the Google OAuth 2.0 Playground. | string |  |  |
| **delay** | Delay | How long to wait between two polls of the mailbox, in milliseconds. For example, 60000 is one minute. | integer | 500 | 60000 |
| **labels** | Gmail Labels | The names of the Gmail labels to read the emails of, separated by commas, such as `INBOX` or a label of your own. When it is not set, the emails are not filtered by label. | string |  | INBOX |
| **markAsRead** | Mark as Read | If true, each email is marked as read once it has been processed, so that the default query `is:unread` does not read it again. | boolean | true |  |
| **query** | Gmail Query | A Gmail search, written as in the search box of Gmail, that selects the emails to read. | string | is:unread | is:unread -category:(promotions OR social) |

## Dependencies

At runtime, the `google-mail-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
-   camel:kamelet
    
-   camel:google-mail
    

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
      uri: "kamelet:google-mail-source"
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

## Google Mail Source Kamelet Description

### Authentication methods

This Kamelet uses OAuth 2.0 authentication to connect to Google Mail. You need to provide:

-   Client ID and Client Secret from your Google Cloud Console application
    
-   Access Token for immediate access (typically expires after an hour)
    
-   Refresh Token for long-term usage (allows automatic token renewal)
    
-   An application name of your choice, sent to Google with each call
    

### Output format

The body is the text of the mail (its first part with content, such as the plain text part) as JSON text, that is the text in double quotes with JSON escapes. It supports two output data types:

-   **json**: Json representation of a Google Mail event object
    
-   **cloudevents**: Output data as CloudEvent V1 format with specific headers
    

### Headers

When processing mail messages, the following headers are set:

-   `CamelGoogleMailId`: The ID of the message
    
-   `CamelGoogleMailStreamTo`: The recipient of the message
    
-   `CamelGoogleMailStreamFrom`: The emitter of the message
    
-   `CamelGoogleMailStreamCc`: The carbon copy of the message
    
-   `CamelGoogleMailStreamBcc`: The blind carbon copy of the message
    
-   `CamelGoogleMailStreamSubject`: The subject of the message
    

For CloudEvents output format, additional headers are set: - `CamelCloudEventID`: The Camel exchange id set as event id - `CamelCloudEventType`: The event type (default: "org.apache.camel.event.google.mail.stream.consume") - `CamelCloudEventSource`: The event source (Mail From with prefix "google.mail.stream.") - `CamelCloudEventSubject`: The event subject - `CamelCloudEventTime`: The exchange creation timestamp as event time

### Configuration

The Kamelet requires the following parameters:

-   `index`: An index for the google mail endpoint
    
-   `clientId`: Client ID of the gmail application
    
-   `clientSecret`: Client Secret of the gmail application
    
-   `accessToken`: OAuth 2 access token
    
-   `refreshToken`: OAuth 2 refresh token for long term usage
    
-   `applicationName`: Google Mail application name
    
-   `labels`: Comma separated list of labels to take into account (example: "INBOX"); when it is not set, the emails are not filtered by label
    

Optional parameters: - `delay`: The number of milliseconds before the next poll (default: 500) - `markAsRead`: Mark the message as read once it has been consumed (default: true) - `query`: The query to execute on gmail box (default: "is:unread", example: "is:unread -category:(promotions OR social)")

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: google-mail-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: google-mail-source
    properties:
      index: "messages"
      clientId: "{{client-id}}"
      clientSecret: "{{client-secret}}"
      accessToken: "{{access-token}}"
      refreshToken: "{{refresh-token}}"
      applicationName: "My Mail App"
      delay: 1000
      markAsRead: true
      labels: "inbox"
      query: "is:unread -category:(promotions OR social)"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-mail-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-mail-source.kamelet.yaml)