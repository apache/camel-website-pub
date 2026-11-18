# ![http sink](_images/kamelets/http-sink.svg) HTTP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends each message to a web service or REST API as an HTTP or HTTPS request, for example a POST of JSON to a webhook.

Use it to push data to any service that accepts HTTP calls, such as a webhook, a REST API or a serverless function.

Input: the body is sent as the request body, as text, bytes or a stream. Turn structured data such as a Map into JSON text first, for example with `json-serialize-action`. The `Content-Type` header is sent as the content type of the request, and the other headers of the message, except the Camel ones, are sent as HTTP headers.

Output: when it is used inside a route, the body afterwards is the response of the service.

Good to know: a response with a status code outside `okStatusCodeRange`, which is `200-299` when it is not set, fails the message. The address and the method come only from the options; headers on the message cannot change where it is sent. Log in either with `authUsername` and `authPassword`, with a static token in `authBearerToken`, or with `oauth2ClientId`, `oauth2ClientSecret` and `oauth2TokenEndpoint`: the Kamelet then gets a token from that URL and sends it as a Bearer token. Without `authenticationPreemptive`, the user and password, or the static token, are sent only after the service asks for them with a 401 response. The certificate of an `https://` service is checked against the certificate authorities that Java trusts. To trust a private one with Camel JBang or Camel Main, set the application properties `camel.ssl.enabled=true`, `camel.ssl.trustStore`, `camel.ssl.trustStorePassword` and `camel.component.https.useGlobalSslContextParameters=true`: that trust store then replaces the one of Java for every `https://` call of the application.

## Configuration Options

The following table summarizes the configuration options available for the `http-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The address to send each message to, with the path and any query parameters. It must start with `http://` or `https://`. | string |  | https://my-service/path |
| **authBearerToken** | Bearer Token | A static token, such as an API key, sent in the `Authorization` header as `Bearer` followed by the token. Set `authMethod` to `Bearer` with it. Also set `authenticationPreemptive` to true, unless the service first answers 401 with a `WWW-Authenticate` header that asks for a Bearer token. | string |  |  |
| **authMethod** | Authentication Method | The login method, `Basic`, `Digest`, `NTLM`, or `Bearer` to send `authBearerToken`. Basic and Digest login with `authUsername` and `authPassword` work without it. | string |  | Basic |
| **authPassword** | Authentication Password | The password of `authUsername`. | string |  |  |
| **authUsername** | Authentication Username | The user to log in as, together with `authPassword`. | string |  |  |
| **authenticationPreemptive** | Authentication Preemptive | If true, `authUsername` and `authPassword` are sent with Basic login, or `authBearerToken` as a Bearer token, on the first request. If false, they are sent only after the service answers 401 and asks for them, which takes a second request. | boolean | false |  |
| **method** | Method | The HTTP method of the request. Most APIs expect `POST` to create something and `PUT` to replace it. Enum values: \* GET \* POST \* PUT \* DELETE \* HEAD \* OPTIONS \* TRACE \* PATCH | string | POST |  |
| **oauth2ClientId** | OAuth2 Client ID | The client ID of the application, as registered with the OAuth 2.0 provider. With `oauth2ClientSecret`, it is used to get a token from `oauth2TokenEndpoint` (client credentials grant). | string |  |  |
| **oauth2ClientSecret** | OAuth2 Client Secret | The client secret of the application, as given by the OAuth 2.0 provider. | string |  |  |
| **oauth2Scope** | OAuth2 Scope | The scope to ask for in the token request, when the OAuth 2.0 provider needs one. | string |  | orders.write |
| **oauth2TokenEndpoint** | OAuth2 Token URL | The URL to get the tokens from, as given by the OAuth 2.0 provider. The Kamelet logs in to it with `oauth2ClientId` and `oauth2ClientSecret`. | string |  | https://login.example.com/oauth2/token |
| **okStatusCodeRange** | OK Status Codes | The status codes of a response that do not fail the message, as ranges such as `200-299` and single codes, separated by commas without spaces. When it is not set, it is `200-299`. List the 2xx codes too, for example `200-299,404` to also accept 404. | string |  | 200-299,404 |

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
    

### Logging In

The login options are all optional. Without them, the requests are sent without a login.

  
| Login | Options | When the credentials are sent |
| --- | --- | --- |
| Basic or Digest | `authUsername`, `authPassword` | After the service answers 401 and asks for them. With `authenticationPreemptive: true`, Basic credentials are sent with the first request. |
| Static token, such as an API key | `authMethod: Bearer`, `authBearerToken` | After the service answers 401 with a `WWW-Authenticate: Bearer` header. With `authenticationPreemptive: true`, with the first request, which most APIs need. |
| OAuth 2.0 client credentials | `oauth2ClientId`, `oauth2ClientSecret`, `oauth2TokenEndpoint`, optionally `oauth2Scope` | With every request: the Kamelet gets a token from `oauth2TokenEndpoint` and sends it as a Bearer token. |

For example, to call an API that takes a static token:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        message: '{"status": "ok"}'
      steps:
        - to:
            uri: "kamelet:http-sink"
            parameters:
              url: "https://api.example.com/v1/events"
              authMethod: Bearer
              authBearerToken: "{{api.token}}"
              authenticationPreemptive: true
```

The token is sent as the header `Authorization: Bearer` followed by the token.

### Status Codes That Do Not Fail

A response with a status code outside `okStatusCodeRange` fails the message. When the option is not set, it is `200-299`, so a status code of 300 or higher fails the message. Some APIs answer a normal case with another code, such as 404 when a record does not exist, or 409 when it exists already. List those codes together with the 2xx codes:

```yaml
- to:
    uri: "kamelet:http-sink"
    parameters:
      url: "https://api.example.com/v1/customers"
      okStatusCodeRange: "200-299,409"
```

The response code is then in the `CamelHttpResponseCode` header, and the body is the response of the service. Setting only `409` would make a 200 response fail.

### Trusting a Private Certificate Authority

The certificate of an `https://` service is checked against the certificate authorities that Java trusts. A service whose certificate is signed by a private certificate authority fails with `PKIX path building failed`.

With Camel JBang or Camel Main, put the certificate of the authority in a trust store, for example with `keytool -importcert -file ca.crt -keystore truststore.p12 -storetype PKCS12`, and set these application properties:

```properties
camel.ssl.enabled = true
camel.ssl.trustStore = file:/etc/certs/truststore.p12
camel.ssl.trustStorePassword = changeit
camel.component.https.useGlobalSslContextParameters = true
```

That trust store then replaces the one of Java for every `https://` call of the application, so it must also hold the authorities of any public service the application calls. The `http://` calls are not changed.

### Headers

The Kamelet sets the HTTP method from the `method` option, and removes the headers that could change where the message is sent, such as `CamelHttpUri`. The other headers of the message are sent as HTTP headers.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/http-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/http-sink.kamelet.yaml)