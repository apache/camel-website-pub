# ![http secured source](_images/kamelets/http-secured-source.svg) HTTP Secured Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Deprecated"**

Deprecated, use `http-source` instead, which has the same login options: fetches a web address at a regular interval with a login, one message per response.

Use it to poll a protected REST API or feed for its current data, for example fetch the state of the orders every minute. This Kamelet will be removed in a later release: `http-source` now takes the same options, so change only the name of the Kamelet. To receive the requests that other systems send instead, use `webhook-source`.

Output: the body is the body of the response, as bytes. The headers of the response, such as `Content-Type`, are copied to the message, and `CamelHttpResponseCode` holds the status code.

Good to know: it fetches the address every `period` and sends a message for each response, even when the data has not changed. A response with a status code of 300 or higher sends no message: the error is logged, and the address is fetched again at the next period. Log in either with `authUsername` and `authPassword`, or with `oauth2ClientId`, `oauth2ClientSecret` and `oauth2TokenEndpoint`: the Kamelet then gets a token from that URL and sends it as a Bearer token.

## Configuration Options

The following table summarizes the configuration options available for the `http-secured-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The address to fetch, with the path and any query parameters. It must start with `http://` or `https://`. | string |  | https://api.example.com/v1/orders/status |
| **authMethod** | Authentication Method | The login methods to allow when the service asks for a login, as a comma-separated list of `Basic`, `Digest` and `NTLM`. Basic login with `authUsername` and `authPassword` works without it. | string |  | Basic |
| **authPassword** | Authentication Password | The password of `authUsername`. | string |  |  |
| **authUsername** | Authentication Username | The user to log in as, together with `authPassword`. | string |  |  |
| **authenticationPreemptive** | Authentication Preemptive | If true, `authUsername` and `authPassword` are sent with Basic login on the first request. If false, they are sent only after the service answers 401 and asks for them, which takes a second request. | boolean | false |  |
| **contentType** | Content Type | The value of the `Accept` header of the request, which tells the service the kind of response you want, such as `application/json` or `text/csv`. | string | application/json | text/csv |
| **oauth2ClientId** | OAuth2 Client ID | The client ID of the application, as registered with the OAuth 2.0 provider. With `oauth2ClientSecret`, it is used to get a token from `oauth2TokenEndpoint` (client credentials grant). | string |  |  |
| **oauth2ClientSecret** | OAuth2 Client Secret | The client secret of the application, as given by the OAuth 2.0 provider. | string |  |  |
| **oauth2Scope** | OAuth2 Scope | The scope to ask for in the token request, when the OAuth 2.0 provider needs one. | string |  | orders.write |
| **oauth2TokenEndpoint** | OAuth2 Token URL | The URL to get the tokens from, as given by the OAuth 2.0 provider. The Kamelet logs in to it with `oauth2ClientId` and `oauth2ClientSecret`. | string |  | https://login.example.com/oauth2/token |
| **period** | Period between Updates | How long to wait between two requests, in milliseconds. The default, 10000, is ten seconds. | integer | 10000 | 60000 |

## Dependencies

At runtime, the `http-secured-source` Kamelet relies upon the presence of the following dependencies:

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
      uri: "kamelet:http-secured-source"
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

## HTTP Secured Source Kamelet Description

### Authentication methods

This Kamelet supports multiple authentication methods:

-   OAuth 2.0 client credentials (`oauth2ClientId`, `oauth2ClientSecret`, `oauth2TokenEndpoint`, `oauth2Scope`)
    
-   Basic, Digest or NTLM authentication using username and password (`authUsername`, `authPassword`, `authMethod`)
    
-   No authentication (if not specified)
    

### Output format

The Kamelet periodically fetches a secured HTTP resource with a GET request and provides the body of the response, as bytes, as output. The `contentType` option sets the `Accept` header of the request (default: application/json). The headers of the response are copied to the message, with the status code in `CamelHttpResponseCode`. A response with a status code of 300 or higher sends no message; the error is logged.

### Configuration

The Kamelet requires the following parameters:

-   `url`: The URL to fetch for data
    

Optional parameters: - `period`: The interval between fetches in milliseconds (default: 10000) - `contentType`: The value of the `Accept` header of the request (default: "application/json") - Authentication parameters (oauth or basic auth credentials)

### Usage example

```yaml
apiVersion: camel.apache.org/v1alpha1
kind: KameletBinding
metadata:
  name: http-secured-source-binding
spec:
  source:
    ref:
      kind: Kamelet
      apiVersion: camel.apache.org/v1alpha1
      name: http-secured-source
    properties:
      url: "https://api.example.com/data"
      period: 30000
      contentType: "application/json"
  sink:
    ref:
      kind: Service
      apiVersion: v1
      name: my-service
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/http-secured-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/http-secured-source.kamelet.yaml)