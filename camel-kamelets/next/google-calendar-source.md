# ![google calendar source](_images/kamelets/google-calendar-source.svg) Google Calendar Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives the events of a Google Calendar, such as meetings and appointments, one message per event, by asking the calendar for events at a regular interval.

Use it to act on calendar entries, for example to send a reminder before a meeting, copy new appointments into another system, or notify a team when a booking is made.

Output: the body is the event as JSON text, with the fields of the Google Calendar API such as `id`, `summary`, `start` and `attendees`. The `CamelGoogleCalendarEventId` header gives the ID of the event.

Good to know: by default it only receives the events that have not ended yet at the time of the poll (`consumeFromNow`). With `syncFlow` set to true, each poll after the first asks only for the events that are new or changed since the previous one. It logs in to Google with OAuth: an OAuth client of a Google Cloud project, and an access token and a refresh token of a Google account that may read the calendar.

## Configuration Options

The following table summarizes the configuration options available for the `google-calendar-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** An OAuth 2 access token of the Google account, with access to Google Calendar. It expires after about an hour; the Kamelet then gets a new one with `refreshToken`. | string |  |  |
| **applicationName** | Application Name | **Required** A name for your application, sent to Google with each call, such as `my-company-calendar/1.0`. | string |  | my-company-calendar/1.0 |
| **calendarId** | Calendar ID | **Required** The ID of the calendar to read, `primary` for the main calendar of the Google account, or the ID shown in the settings of the calendar under Integrate calendar, which looks like an email address. | string |  | primary |
| **clientId** | Client ID | **Required** The client ID of an OAuth client, created in the Google Cloud console under APIs & Services > Credentials, in a project where the Google Calendar API is enabled. | string |  |  |
| **clientSecret** | Client Secret | **Required** The client secret of the OAuth client of `clientId`. | string |  |  |
| **index** | Index | **Required** Any name for this reader of the calendar, such as `events`. It is not sent to Google. | string |  | events |
| **refreshToken** | Refresh Token | **Required** An OAuth 2 refresh token of the Google account, which the Kamelet uses to get a new access token when the current one expires. You get it together with the access token, for example from the Google OAuth 2.0 Playground. | string |  |  |
| **consumeFromNow** | Consume from Now | If true, only the events that have not ended yet at the time of each poll are read. If false, past events are read too. | boolean | true |  |
| **delay** | Delay | How long to wait between two polls of the calendar, in milliseconds. For example, 60000 is one minute. | integer | 500 | 60000 |
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

This Kamelet uses OAuth 2.0 authentication to connect to Google Calendar. You need to provide:

-   Client ID and Client Secret from your Google Cloud Console application
    
-   Access Token for immediate access (typically expires after an hour)
    
-   Refresh Token for long-term usage (allows automatic token renewal)
    
-   An application name of your choice, sent to Google with each call
    

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
    
-   `clientId`: The Client ID of the Google Calendar application
    
-   `clientSecret`: The Client secret of the Google Calendar application
    
-   `accessToken`: The OAuth 2 access token
    
-   `refreshToken`: The OAuth 2 refresh token for long term usage
    
-   `applicationName`: The Google Calendar application name
    

Optional parameters: - `delay`: The number of milliseconds before the next poll (default: 500) - `syncFlow`: Specifies to sync events for incremental synchronization (default: false) - `consumeFromNow`: Specifies to consume events in the calendar from now on (default: true)

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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/google-calendar-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/google-calendar-source.kamelet.yaml)