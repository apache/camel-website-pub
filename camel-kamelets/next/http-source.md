# ![http source](_images/kamelets/http-source.svg) HTTP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Fetches a web address with an HTTP request, a GET unless `method` says otherwise, at a regular interval, and sends each response as a message.

Use it to poll a REST API, a feed or a status page for its current data, for example fetch the state of the orders every minute. To receive the requests that other systems send instead, use `webhook-source`.

Output: the body is the body of the response, as bytes. The headers of the response, such as `Content-Type`, are copied to the message, and `CamelHttpResponseCode` holds the status code.

Good to know: it fetches the address every `period` and sends a message for each response, even when the data has not changed. A response with a status code outside `okStatusCodeRange`, which is `200-299` when it is not set, sends no message: the error is logged, and the address is fetched again at the next period. Log in either with `authUsername` and `authPassword`, with a static token in `authBearerToken`, or with `oauth2ClientId`, `oauth2ClientSecret` and `oauth2TokenEndpoint`: the Kamelet then gets a token from that URL and sends it as a Bearer token. To go through an HTTP proxy, set `proxyHost` and `proxyPort`, and `proxyUser` and `proxyPassword` when the proxy asks for a login; an `https://` address goes through the proxy too. The certificate of an `https://` service is checked against the certificate authorities that Java trusts. To trust a private one with Camel JBang or Camel Main, set the application properties `camel.ssl.enabled=true`, `camel.ssl.trustStore`, `camel.ssl.trustStorePassword` and `camel.component.https.useGlobalSslContextParameters=true`: that trust store then replaces the one of Java for every `https://` call of the application. It keeps the cookies that the service sets, as a browser does, and sends them back on the next calls. To turn that off, set the application property `camel.component.http.cookie-management-disabled=true`, or `camel.component.https.cookie-management-disabled=true` for an `https://` address: it then applies to every call of the application to such addresses.

## Configuration Options

The following table summarizes the configuration options available for the `http-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The address to fetch, with the path and any query parameters. It must start with `http://` or `https://`. | string |  | https://api.example.com/v1/orders/status |
| **authBearerToken** | Bearer Token | A static token, such as an API key, sent in the `Authorization` header as `Bearer` followed by the token. Set `authMethod` to `Bearer` with it. Also set `authenticationPreemptive` to true, unless the service first answers 401 with a `WWW-Authenticate` header that asks for a Bearer token. | string |  |  |
| **authMethod** | Authentication Method | The login method, `Basic`, `Digest`, `NTLM`, or `Bearer` to send `authBearerToken`. Basic and Digest login with `authUsername` and `authPassword` work without it. | string |  | Basic |
| **authPassword** | Authentication Password | The password of `authUsername`. | string |  |  |
| **authUsername** | Authentication Username | The user to log in as, together with `authPassword`. | string |  |  |
| **authenticationPreemptive** | Authentication Preemptive | If true, `authUsername` and `authPassword` are sent with Basic login, or `authBearerToken` as a Bearer token, on the first request. If false, they are sent only after the service answers 401 and asks for them, which takes a second request. | boolean | false |  |
| **contentType** | Content Type | The value of the `Accept` header of the request, which tells the service the kind of response you want, such as `application/json` or `text/csv`. | string | application/json | text/csv |
| **followRedirects** | Follow Redirects | If true, a redirect, a response with a status code such as 301, 302 or 307, is followed to the address in its `Location` header, and the response from there is sent as the message. When it is not set, the redirect is not followed, so it sends no message unless its status code is in `okStatusCodeRange`. | boolean |  |  |
| **method** | Method | The HTTP method of the request, such as `POST` for an API that expects one to return data. When it is not set, it is `GET`. The request has no body. Enum values: \* GET \* POST \* PUT \* DELETE \* HEAD \* OPTIONS \* TRACE \* PATCH | string |  | POST |
| **oauth2ClientId** | OAuth2 Client ID | The client ID of the application, as registered with the OAuth 2.0 provider. With `oauth2ClientSecret`, it is used to get a token from `oauth2TokenEndpoint` (client credentials grant). | string |  |  |
| **oauth2ClientSecret** | OAuth2 Client Secret | The client secret of the application, as given by the OAuth 2.0 provider. | string |  |  |
| **oauth2Scope** | OAuth2 Scope | The scope to ask for in the token request, when the OAuth 2.0 provider needs one. | string |  | orders.write |
| **oauth2TokenEndpoint** | OAuth2 Token URL | The URL to get the tokens from, as given by the OAuth 2.0 provider. The Kamelet logs in to it with `oauth2ClientId` and `oauth2ClientSecret`. | string |  | https://login.example.com/oauth2/token |
| **okStatusCodeRange** | OK Status Codes | The status codes of a response that is sent as a message, as ranges such as `200-299` and single codes, separated by commas without spaces. When it is not set, it is `200-299`. List the 2xx codes too, for example `200-299,404` to also send the 404 responses. | string |  | 200-299,404 |
| **period** | Period between Updates | How long to wait between two requests, in milliseconds. The default, 10000, is ten seconds. | integer | 10000 | 60000 |
| **proxyHost** | Proxy Host | The host name or IP address of an HTTP proxy to send the requests through, without the port. Use it with `proxyPort`; the proxy is used only when both are set. | string |  | proxy.example.com |
| **proxyPassword** | Proxy Password | The password of `proxyUser` for the HTTP proxy. | string |  |  |
| **proxyPort** | Proxy Port | The port of the HTTP proxy in `proxyHost`. | integer |  | 3128 |
| **proxyUser** | Proxy User | The user to log in to the HTTP proxy as, when the proxy asks for a login. Use it with `proxyPassword`. | string |  |  |

## Dependencies

At runtime, the `http-source` Kamelet relies upon the presence of the following dependencies:

-   camel:http
    
-   camel:kamelet
    
-   camel:timer
    

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
      uri: "kamelet:http-source"
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

## HTTP Source Kamelet Description

### Configuration

The HTTP Source Kamelet periodically fetches data from an HTTP endpoint. It supports the following configurations:

-   **URL**: The HTTP endpoint to fetch data from (required, must start with http:// or https://)
    
-   **Period**: The interval between fetches in milliseconds (default: 10000)
    
-   **Content Type**: The Accept header content type for the request (default: "application/json")
    
-   **Method**: The HTTP method of the request (default: GET)
    

### Logging In

The login options are all optional. Without them, the requests are sent without a login.

  
| Login | Options | When the credentials are sent |
| --- | --- | --- |
| Basic or Digest | `authUsername`, `authPassword` | After the service answers 401 and asks for them. With `authenticationPreemptive: true`, Basic credentials are sent with the first request. |
| Static token, such as an API key | `authMethod: Bearer`, `authBearerToken` | After the service answers 401 with a `WWW-Authenticate: Bearer` header. With `authenticationPreemptive: true`, with the first request, which most APIs need. |
| OAuth 2.0 client credentials | `oauth2ClientId`, `oauth2ClientSecret`, `oauth2TokenEndpoint`, optionally `oauth2Scope` | With every request: the Kamelet gets a token from `oauth2TokenEndpoint` and sends it as a Bearer token. |

### Output Format

The Kamelet outputs the HTTP response body and preserves any HTTP headers from the response.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:http-source"
      parameters:
        url: "https://api.example.com/data"
        period: 30000
        contentType: "application/json"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with XML Content

```yaml
- route:
    from:
      uri: "kamelet:http-source"
      parameters:
        url: "https://api.example.com/xml-feed"
        period: 60000
        contentType: "application/xml"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with High Frequency Polling

```yaml
- route:
    from:
      uri: "kamelet:http-source"
      parameters:
        url: "https://api.example.com/status"
        period: 5000
        contentType: "text/plain"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This example polls the endpoint every 5 seconds for status updates.

### Example with a Static Token

```yaml
- route:
    from:
      uri: "kamelet:http-source"
      parameters:
        url: "https://api.example.com/v1/orders/status"
        period: 60000
        authMethod: Bearer
        authBearerToken: "{{api.token}}"
        authenticationPreemptive: true
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The token is sent as the header `Authorization: Bearer` followed by the token.

### Status Codes That Send a Message

Only a response with a status code in `okStatusCodeRange` is sent as a message. When the option is not set, it is `200-299`: a response with a status code of 300 or higher sends no message, the error is logged, and the address is fetched again at the next period. To also receive the responses with another code, such as 404 while a resource does not exist yet, list it together with the 2xx codes:

```yaml
- route:
    from:
      uri: "kamelet:http-source"
      parameters:
        url: "https://api.example.com/v1/reports/today"
        okStatusCodeRange: "200-299,404"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

The `CamelHttpResponseCode` header of the message then tells a 404 from a 200. Setting only `404` would stop the 200 responses.

### Method

The request is a `GET` when `method` is not set. Some APIs return data only for a `POST`; set `method: POST` for them. The request has no body.

```yaml
- route:
    from:
      uri: "kamelet:http-source"
      parameters:
        url: "https://api.example.com/v1/reports/search"
        method: POST
        period: 60000
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Going Through a Proxy

To fetch the address through an HTTP proxy, set `proxyHost` and `proxyPort`. The proxy is used only when both are set. When the proxy asks for a login, also set `proxyUser` and `proxyPassword`: they are sent after the proxy answers 407 and asks for them.

```yaml
- route:
    from:
      uri: "kamelet:http-source"
      parameters:
        url: "https://api.example.com/v1/orders/status"
        proxyHost: proxy.example.com
        proxyPort: 3128
        proxyUser: "{{proxy.user}}"
        proxyPassword: "{{proxy.password}}"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

An `https://` address goes through the proxy too, in a tunnel.

### Following Redirects

A redirect, a response with a status code such as 301, 302 or 307, is not followed when `followRedirects` is not set: it sends no message, the error is logged, and the address is fetched again at the next period. With `followRedirects: true`, the address in the `Location` header of the response is fetched, and its response is sent as the message.

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

### Scheduling Behavior

The kamelet uses a timer to periodically fetch data from the specified URL. The timer starts immediately when the route starts and repeats at the configured interval. Each request includes the specified Accept header to indicate the expected content type.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/http-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/http-source.kamelet.yaml)