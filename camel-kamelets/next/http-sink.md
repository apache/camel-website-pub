# ![http sink](_images/kamelets/http-sink.svg) HTTP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a web service or REST API as an HTTP or HTTPS request, for example a POST of JSON to a webhook.

Use it to push data to any service that accepts HTTP calls, such as a webhook, a REST API or a serverless function.

Input: the body is sent as the request body, as text, bytes or a stream. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The `Content-Type` header is sent as the content type of the request, and the other headers of the message, except the Camel ones, are sent as HTTP headers.

Output: when it is used inside a route, the body afterwards is the response of the service.

Good to know: a response with a status code of 300 or higher fails the message. The address and the method come only from the options; headers on the message cannot change where it is sent. Log in either with `authUsername` and `authPassword`, or with `oauth2ClientId`, `oauth2ClientSecret` and `oauth2TokenEndpoint`: the Kamelet then gets a token from that URL and sends it as a Bearer token. Without `authenticationPreemptive`, the user and password are sent only after the service asks for them with a 401 response.

## Configuration Options

The following table summarizes the configuration options available for the `http-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The address to send each message to, with the path and any query parameters. It must start with `http://` or `https://`. | string |  | https://my-service/path |
| **authMethod** | Authentication Method | The login methods to allow when the service asks for a login, as a comma-separated list of `Basic`, `Digest` and `NTLM`. Basic login with `authUsername` and `authPassword` works without it. | string |  | Basic |
| **authPassword** | Authentication Password | The password of `authUsername`. | string |  |  |
| **authUsername** | Authentication Username | The user to log in as, together with `authPassword`. | string |  |  |
| **authenticationPreemptive** | Authentication Preemptive | If true, `authUsername` and `authPassword` are sent with Basic login on the first request. If false, they are sent only after the service answers 401 and asks for them, which takes a second request. | boolean | false |  |
| **method** | Method | The HTTP method of the request. Most APIs expect `POST` to create something and `PUT` to replace it. Enum values: \* GET \* POST \* PUT \* DELETE \* HEAD \* OPTIONS \* TRACE \* PATCH | string | POST |  |
| **oauth2ClientId** | OAuth2 Client ID | The client ID of the application, as registered with the OAuth 2.0 provider. With `oauth2ClientSecret`, it is used to get a token from `oauth2TokenEndpoint` (client credentials grant). | string |  |  |
| **oauth2ClientSecret** | OAuth2 Client Secret | The client secret of the application, as given by the OAuth 2.0 provider. | string |  |  |
| **oauth2Scope** | OAuth2 Scope | The scope to ask for in the token request, when the OAuth 2.0 provider needs one. | string |  | orders.write |
| **oauth2TokenEndpoint** | OAuth2 Token URL | The URL to get the tokens from, as given by the OAuth 2.0 provider. The Kamelet logs in to it with `oauth2ClientId` and `oauth2ClientSecret`. | string |  | https://login.example.com/oauth2/token |

## Dependencies

At runtime, the `http-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:http
    
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
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:http-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## HTTP Sink Kamelet Description

### HTTP Methods

Supports all standard HTTP methods: GET, POST (default), PUT, DELETE, HEAD, OPTIONS, TRACE, and PATCH.

### Required Configuration

-   **URL**: The target HTTP or HTTPS endpoint where data will be sent
    

### Usage

This Kamelet forwards data to HTTP or HTTPS endpoints without authentication. For secured endpoints requiring authentication, use the HTTP Secured Sink Kamelet instead.

### Headers

The Kamelet automatically sets the HTTP method header and removes any existing CamelHttpUri header to prevent conflicts.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/http-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/http-sink.kamelet.yaml)