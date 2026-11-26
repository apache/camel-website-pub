# ![google mail source](_images/kamelets/google-mail-source.svg) Google Mail Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the emails of a Gmail mailbox that match a search, by default the unread ones, one message per email, and marks each email as read once it has been processed.

Use it to act on incoming email, for example to open a ticket for each email sent to a support address, or to collect orders or invoices that arrive by mail.

Output: the body is the text of the email (its first part with content, such as the plain text part) as JSON text, that is the text in double quotes with JSON escapes. The headers give the subject (`CamelGoogleMailStreamSubject`), the sender (`CamelGoogleMailStreamFrom`), the recipients (`CamelGoogleMailStreamTo`, `CamelGoogleMailStreamCc`, `CamelGoogleMailStreamBcc`) and the Gmail ID of the email (`CamelGoogleMailId`). With `raw` set to true, the body is the whole email instead, with its attachments, encoded in base64url, as JSON text, and only the Gmail ID is set as a header.

Good to know: it reads the emails that match `query`, by default the unread ones. With `markAsRead` set to false and the default query, the same emails are read again on every poll. An email whose processing fails is marked as unread again. Each poll reads up to `maxResults` emails, 10 by default. It logs in to Google either with OAuth (an OAuth client of a Google Cloud project, and an access token and a refresh token of the Gmail account), or with the key of a service account in `serviceAccountKey` together with `scopes`, which reads the mailbox of the user in `delegate`.

## Configuration Options

The following table summarizes the configuration options available for the `google-mail-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **applicationName** | Application Name | **Required** A name for your application, sent to Google with each call, such as `my-company-mail/1.0`. | string |  | my-company-mail/1.0 |
| **index** | Index | **Required** Any name for this reader of the mailbox, such as `support`. It is not sent to Google. | string |  | support |
| **accessToken** | Access Token | An OAuth 2 access token of the Gmail account, with access to read and change its emails. It expires after about an hour; the Kamelet then gets a new one with `refreshToken`. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **clientId** | Client ID | The client ID of an OAuth client, created in the Google Cloud console under APIs & Services > Credentials, in a project where the Gmail API is enabled. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **clientSecret** | Client Secret | The client secret of the OAuth client of `clientId`. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **delay** | Delay | How long to wait between two polls of the mailbox, in milliseconds. For example, 60000 is one minute. | integer | 500 | 60000 |
| **delegate** | Delegate User | The email address of the user of your Google Workspace whose mailbox the service account of `serviceAccountKey` reads on their behalf. A Workspace administrator must first allow the client ID of the service account, with the scopes of `scopes`, under Security > Access and data control > API controls > Domain-wide delegation. Only used with `serviceAccountKey`. | string |  | support@example.com// |
| **labels** | Gmail Labels | The names of the Gmail labels to read the emails of, separated by commas, such as `INBOX` or a label of your own. When it is not set, the emails are not filtered by label. | string |  | INBOX |
| **markAsRead** | Mark as Read | If true, each email is marked as read once it has been processed, so that the default query `is:unread` does not read it again. | boolean | true |  |
| **maxResults** | Max Results | The most emails to read at each poll. When it is not set, 10 is used. | integer |  | 50 |
| **query** | Gmail Query | A Gmail search, written as in the search box of Gmail, that selects the emails to read. | string | is:unread | is:unread -category:(promotions OR social) |
| **raw** | Raw Email | If true, the body is the whole email, with its headers and all its parts, such as attachments, in the format of an `.eml` file (RFC 2822), encoded in base64url, as JSON text, that is in double quotes. Remove the quotes and decode it to get the email. The subject, sender and recipients are then not set as headers. When it is not set, it is false, and the body is the text of the email, without its attachments. | boolean |  |  |
| **refreshToken** | Refresh Token | An OAuth 2 refresh token of the Gmail account, which the Kamelet uses to get a new access token when the current one expires. You get it together with the access token, for example from the Google OAuth 2.0 Playground. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **scopes** | Scopes | The permissions to ask Google for, as URLs separated by commas. Needed with `serviceAccountKey`: without them, the login asks Google for no permission at all. Use `[https://www.googleapis.com/auth/gmail.modify](https://www.googleapis.com/auth/gmail.modify)`, which marking the emails as read needs, or `[https://www.googleapis.com/auth/gmail.readonly](https://www.googleapis.com/auth/gmail.readonly)` with `markAsRead` set to false. Leave it unset with `clientId` and `clientSecret`; with them, setting it makes the Kamelet fail. | string |  | https://www.googleapis.com/auth/gmail.modify |
| **serviceAccountKey** | Service Account Key | The JSON key of a Google service account, to log in with instead of OAuth: `file:` followed by the path of the key file, `classpath:` followed by a resource of the application, or `base64:` followed by the Base64 encoding of the key. Create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys. It reads the mailbox of the user in `delegate`, and needs `scopes`. Only used when `clientSecret` is not set. | string |  | file:/etc/google/service-account.json |

## Dependencies

At runtime, the `google-mail-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
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

The Kamelet logs in to Google in one of two ways:

-   With OAuth 2.0: `clientId` and `clientSecret` of an OAuth client from your Google Cloud Console application, an `accessToken` for immediate access (it expires after about an hour) and a `refreshToken` to get new ones.
    
-   With a service account: its JSON key in `serviceAccountKey`, as `file:<path>`, `classpath:<resource>` or `base64:<Base64 of the key file>`. It reads the mailbox of the user of your Google Workspace in `delegate`, and needs `scopes`, such as `[https://www.googleapis.com/auth/gmail.modify](https://www.googleapis.com/auth/gmail.modify)`, which marking the emails as read needs. A Workspace administrator must first allow the client ID of the service account, with these scopes, under Security > Access and data control > API controls > Domain-wide delegation. The service account key is only used when `clientSecret` is not set; do not set `scopes` with OAuth.
    

An application name of your choice is sent to Google with each call.

### Output format

The body is the text of the mail (its first part with content, such as the plain text part) as JSON text, that is the text in double quotes with JSON escapes. With `raw` set to true, the body is instead the whole email, with its attachments, in the format of an `.eml` file (RFC 2822), encoded in base64url, as JSON text; the subject, sender and recipient headers are then not set.

It supports two output data types:

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
    
-   `applicationName`: Google Mail application name
    

To log in with OAuth:

-   `clientId`: Client ID of the gmail application
    
-   `clientSecret`: Client Secret of the gmail application
    
-   `accessToken`: OAuth 2 access token
    
-   `refreshToken`: OAuth 2 refresh token for long term usage
    

To log in with a service account:

-   `serviceAccountKey`: The JSON key of the service account, such as `file:/etc/google/service-account.json`
    
-   `delegate`: The email address of the user whose mailbox to read
    
-   `scopes`: The permissions to ask for, such as `[https://www.googleapis.com/auth/gmail.modify](https://www.googleapis.com/auth/gmail.modify)`
    

Optional parameters: - `delay`: The number of milliseconds before the next poll (default: 500) - `markAsRead`: Mark the message as read once it has been consumed (default: true) - `query`: The query to execute on gmail box (default: "is:unread", example: "is:unread -category:(promotions OR social)") - `labels`: Comma separated list of labels to take into account (example: "INBOX"); when it is not set, the emails are not filtered by label - `maxResults`: The most emails to read at each poll (default: 10) - `raw`: The body is the whole email with its attachments, encoded in base64url (default: false)

### Usage example

```yaml
- route:
    from:
      uri: "kamelet:google-mail-source"
      parameters:
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
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with a Service Account and Attachments

Reads the unread emails of `support@example.com`, at most 20 at each poll, as whole emails with their attachments. Each body is a JSON string; remove the quotes and decode it as base64url to get the `.eml` content.

```yaml
- route:
    from:
      uri: "kamelet:google-mail-source"
      parameters:
        index: "support"
        applicationName: "my-company-mail/1.0"
        serviceAccountKey: "file:/etc/google/service-account.json"
        delegate: "support@example.com"
        scopes: "https://www.googleapis.com/auth/gmail.modify"
        maxResults: 20
        raw: true
        delay: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-mail-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-mail-source.kamelet.yaml)