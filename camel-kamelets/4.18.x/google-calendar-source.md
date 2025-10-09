# ![google calendar source](_images/kamelets/google-calendar-source.svg) Google Calendar Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive event data from Google Calendar.

## Configuration Options

The following table summarizes the configuration options available for the `google-calendar-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** The OAuth 2 access token for the Google Calendar application. This token typically expires after an hour. For long term usage, set the `refreshToken` property. | string |  |  |
| **applicationName** | Application name | **Required** The Google Calendar application name. | string |  |  |
| **calendarId** | Calendar ID | **Required** The calendar ID to use as the source of event data. | string |  |  |
| **clientId** | Client Id | **Required** The Client ID of the Google Calendar application. | string |  |  |
| **clientSecret** | Client Secret | **Required** The Client secret of the Google Calendar application. | string |  |  |
| **index** | Index | **Required** An index for the Google Calendar endpoint. | string |  |  |
| **refreshToken** | Refresh Token | **Required** The OAuth 2 refresh token for the Google Calendar application. The Google Calendar component can obtain a new `accessToken` whenever the current one expires. Set this value for long term usage. | string |  |  |
| **consumeFromNow** | Consume from now | Specfies to consume events in the calendar from now on. | boolean | true |  |
| **delay** | Delay | The number of milliseconds before the next poll. | integer | 500 |  |
| **syncFlow** | Sync Flow | Specifies to sync events for incremental synchronization. | boolean | false |  |

## Dependencies

At runtime, the `google-calendar-source` Kamelet relies upon the presence of the following dependencies:

-   camel:jackson
    
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
    
-   Application Name registered in Google Cloud Console
    

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