# ![google calendar source](_images/kamelets/google-calendar-source.svg) Google Calendar Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the events of a Google Calendar, such as meetings and appointments, one message per event, by asking the calendar for events at a regular interval.

Use it to act on calendar entries, for example to send a reminder before a meeting, copy new appointments into another system, or notify a team when a booking is made.

Output: the body is the event as JSON text, with the fields of the Google Calendar API such as `id`, `summary`, `start` and `attendees`. The `CamelGoogleCalendarEventId` header gives the ID of the event.

Good to know: by default it only receives the events that have not ended yet at the time of the poll (`consumeFromNow`). Each poll asks for one page of up to `maxResults` events (10 by default), the events that changed least recently first, so the same events can come again on every poll. With `considerLastUpdate` set to true, each poll reads all the pages, and after the first poll only the events that changed since the last one received. With `syncFlow` set to true, each poll after the first asks only for the events that are new or changed since the previous one; do not combine it with `query` or `considerLastUpdate`. It logs in to Google either with OAuth (an OAuth client of a Google Cloud project, and an access token and a refresh token of a Google account that may read the calendar), or with the key of a service account in `serviceAccountKey`, which reads the calendars shared with it, or the calendar of the user in `delegate`.

## Configuration Options

The following table summarizes the configuration options available for the `google-calendar-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **applicationName** | Application Name | **Required** A name for your application, sent to Google with each call, such as `my-company-calendar/1.0`. | string |  | my-company-calendar/1.0 |
| **calendarId** | Calendar ID | **Required** The ID of the calendar to read, `primary` for the main calendar of the Google account, or the ID shown in the settings of the calendar under Integrate calendar, which looks like an email address. | string |  | primary |
| **index** | Index | **Required** Any name for this reader of the calendar, such as `events`. It is not sent to Google. | string |  | events |
| **accessToken** | Access Token | An OAuth 2 access token of the Google account, with access to Google Calendar. It expires after about an hour; the Kamelet then gets a new one with `refreshToken`. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **clientId** | Client ID | The client ID of an OAuth client, created in the Google Cloud console under APIs & Services > Credentials, in a project where the Google Calendar API is enabled. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **clientSecret** | Client Secret | The client secret of the OAuth client of `clientId`. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **considerLastUpdate** | Only Changed Events | If true, each poll reads all the pages, and each poll after the first asks only for the events that changed since the last one received, so an event comes again only when it changes. When it is not set, it is false. Do not combine it with `syncFlow`. | boolean |  |  |
| **consumeFromNow** | Consume from Now | If true, only the events that have not ended yet at the time of each poll are read. If false, past events are read too. | boolean | true |  |
| **delay** | Delay | How long to wait between two polls of the calendar, in milliseconds. For example, 60000 is one minute. | integer | 500 | 60000 |
| **delegate** | Delegate User | The email address of a user of your Google Workspace, whose calendar the service account of `serviceAccountKey` reads on their behalf. A Workspace administrator must first allow the client ID of the service account, with the scope of `scopes`, under Security > Access and data control > API controls > Domain-wide delegation. Only used with `serviceAccountKey`. | string |  | alice@example.com// |
| **maxResults** | Max Results | The most events to ask Google for at once, in one page. Each poll reads one page, or all the pages when `considerLastUpdate` is true. When it is not set, 10 is used. | integer |  | 50 |
| **query** | Search Text | Only read the events that contain this text, as the search box of Google Calendar finds them, for example in their title, description, location or attendees. Do not combine it with `syncFlow`. | string |  | standup |
| **refreshToken** | Refresh Token | An OAuth 2 refresh token of the Google account, which the Kamelet uses to get a new access token when the current one expires. You get it together with the access token, for example from the Google OAuth 2.0 Playground. Not needed when logging in with `serviceAccountKey`. | string |  |  |
| **scopes** | Scopes | The permissions to ask Google for when logging in with `serviceAccountKey`, as URLs separated by commas, such as `[https://www.googleapis.com/auth/calendar.readonly](https://www.googleapis.com/auth/calendar.readonly)` to only read. When it is not set, `[https://www.googleapis.com/auth/calendar](https://www.googleapis.com/auth/calendar)` is used. Only used with `serviceAccountKey`. | string |  | https://www.googleapis.com/auth/calendar.readonly |
| **serviceAccountKey** | Service Account Key | The JSON key of a Google service account, to log in with instead of OAuth: `file:` followed by the path of the key file, `classpath:` followed by a resource of the application, or `base64:` followed by the Base64 encoding of the key. Create the key in the Google Cloud console under IAM & Admin > Service Accounts > Keys. The service account reads the calendars that are shared with its email address, or the calendar of the user in `delegate`. Only used when `clientId` and `clientSecret` are not set. | string |  | file:/etc/google/service-account.json |
| **syncFlow** | Sync Flow | If true, each poll after the first asks Google only for the events that were created, changed or cancelled since the previous poll. | boolean | false |  |

## Dependencies

At runtime, the `google-calendar-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson3
    
-   camel:google-calendar
    
-   camel:kamelet
    

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
      uri: "kamelet:google-calendar-source"
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

## Google Calendar Source Kamelet Description

### Authentication methods

The Kamelet logs in to Google in one of two ways:

-   With OAuth 2.0: `clientId` and `clientSecret` of an OAuth client from your Google Cloud Console application, an `accessToken` for immediate access (it expires after about an hour) and a `refreshToken` to get new ones.
    
-   With a service account: its JSON key in `serviceAccountKey`, as `file:<path>`, `classpath:<resource>` or `base64:<Base64 of the key file>`. The service account reads the calendars shared with its email address. To read the calendar of a user of your Google Workspace, set `delegate` to the email address of the user; a Workspace administrator must first allow the client ID of the service account under Security > Access and data control > API controls > Domain-wide delegation, with the scope `[https://www.googleapis.com/auth/calendar](https://www.googleapis.com/auth/calendar)`, or the one set in `scopes`. The service account key is only used when `clientId` and `clientSecret` are not set.
    

An application name of your choice is sent to Google with each call.

### Output format

The Kamelet produces calendar event data in JSON format. It supports two output data types:

-   **json**: Json representation of a Google Calendar event object
    
-   **cloudevents**: Output data as CloudEvent V1 format with specific headers
    

### Headers

When processing calendar events, the following headers are set:

-   `CamelGoogleCalendarEventId`: The calendar event id
    

For CloudEvents output format, additional headers are set: - `CamelCloudEventID`: The Camel exchange id set as event id - `CamelCloudEventType`: The event type (default: "org.apache.camel.event.google.calendar.stream.consume") - `CamelCloudEventSource`: The event source (Calendar Event Id with prefix "google.calendar.stream.") - `CamelCloudEventSubject`: The event subject (Calendar event type) - `CamelCloudEventTime`: The exchange creation timestamp as event time

### Configuration

The Kamelet requires the following parameters:

-   `index`: An index for the Google Calendar endpoint
    
-   `calendarId`: The calendar ID to use as the source of event data
    
-   `applicationName`: The Google Calendar application name
    

To log in with OAuth:

-   `clientId`: The Client ID of the Google Calendar application
    
-   `clientSecret`: The Client secret of the Google Calendar application
    
-   `accessToken`: The OAuth 2 access token
    
-   `refreshToken`: The OAuth 2 refresh token for long term usage
    

To log in with a service account:

-   `serviceAccountKey`: The JSON key of the service account, such as `file:/etc/google/service-account.json`
    
-   `delegate`: The email address of the user whose calendar to read, with domain-wide delegation
    
-   `scopes`: The permissions to ask for, such as `[https://www.googleapis.com/auth/calendar.readonly](https://www.googleapis.com/auth/calendar.readonly)` (default: `[https://www.googleapis.com/auth/calendar](https://www.googleapis.com/auth/calendar)`)
    

Optional parameters: - `delay`: The number of milliseconds before the next poll (default: 500) - `syncFlow`: Specifies to sync events for incremental synchronization (default: false); do not combine it with `query` or `considerLastUpdate` - `consumeFromNow`: Specifies to consume events in the calendar from now on (default: true) - `maxResults`: The most events in one page; each poll reads one page, or all the pages with `considerLastUpdate` (default: 10) - `query`: Only read the events that contain this text, such as `standup` - `considerLastUpdate`: Each poll reads all the pages, and after the first only the events changed since the last one received (default: false)

Each poll asks for the events that changed least recently first. Without `syncFlow` or `considerLastUpdate`, it reads the first page again on every poll, so the same events can come again.

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: google-calendar-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: google-calendar-source
    properties:
      index: "events"
      calendarId: "primary"
      clientId: "{{client-id}}"
      clientSecret: "{{client-secret}}"
      accessToken: "{{access-token}}"
      refreshToken: "{{refresh-token}}"
      applicationName: "My Calendar App"
      delay: 1000
      syncFlow: true
      consumeFromNow: true
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

### Example with a Service Account

Reads the events of the calendar of `alice@example.com` that mention `standup`, with the key of a service account that has domain-wide delegation for the read-only scope. With `considerLastUpdate`, an event comes again only when it changes.

```yaml
- route:
    from:
      uri: "kamelet:google-calendar-source"
      parameters:
        index: "standups"
        calendarId: "primary"
        applicationName: "my-company-calendar/1.0"
        serviceAccountKey: "file:/etc/google/service-account.json"
        delegate: "alice@example.com"
        scopes: "https://www.googleapis.com/auth/calendar.readonly"
        query: "standup"
        maxResults: 50
        considerLastUpdate: true
        delay: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-calendar-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-calendar-source.kamelet.yaml)