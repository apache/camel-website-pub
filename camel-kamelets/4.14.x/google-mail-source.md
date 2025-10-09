# ![google mail source](_images/kamelets/google-mail-source.svg) Google Mail Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receive data from Google Mail.

## Configuration Options

The following table summarizes the configuration options available for the `google-mail-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **accessToken** | Access Token | **Required** OAuth 2 access token for google mail application. This typically expires after an hour so refreshToken is recommended for long term usage. | string |  |  |
| **applicationName** | Application name | **Required** Google Mail application name. | string |  |  |
| **clientId** | Client ID | **Required** Client ID of the gmail application. | string |  |  |
| **clientSecret** | Client Secret | **Required** Client Secret of the gmail application. | string |  |  |
| **index** | Index | **Required** An index for the google mail endpoint. | string |  |  |
| **refreshToken** | Refresh Token | **Required** OAuth 2 refresh token for google mail application. Using this, the Google Calendar component can obtain a new accessToken whenever the current one expires - a necessity if the application is long-lived. | string |  |  |
| **delay** | Delay | The number of milliseconds before the next poll. | integer | 500 |  |
| **labels** | Gmail Labels | Comma separated list of labels to take into account. | string |  | inbox |
| **markAsRead** | Mark as Read | Mark the message as read once it has been consumed. | boolean | true |  |
| **query** | Gmail Query | The query to execute on gmail box. | string | is:unread | is:unread -category:(promotions OR social) |

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
    
-   Application Name registered in Google Cloud Console
    

### Output format

The Kamelet produces mail data in JSON format. It supports two output data types:

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
    

Optional parameters: - `delay`: The number of milliseconds before the next poll (default: 500) - `markAsRead`: Mark the message as read once it has been consumed (default: true) - `labels`: Comma separated list of labels to take into account (example: "inbox") - `query`: The query to execute on gmail box (default: "is:unread", example: "is:unread -category:(promotions OR social)")

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