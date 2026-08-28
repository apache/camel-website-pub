# ![http secured sink](_images/kamelets/http-secured-sink.svg) Secured HTTP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Forwards an event to a secured HTTP endpoint. Supports Oauth and Basic authentication.

## Configuration Options

The following table summarizes the configuration options available for the `http-secured-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The URL to send data to. | string |  | https://my-service/path |
| **authMethod** | Authentication Method | Authentication methods allowed to use as a comma separated list of values Basic, Digest or NTLM. | string |  |  |
| **authPassword** | Authentication Password | Authentication password. | string |  |  |
| **authUsername** | Authentication Username | Authentication username. | string |  |  |
| **authenticationPreemptive** | Authentication Preemptive | If this option is true, camel-http sends preemptive basic authentication to the server. | boolean | false |  |
| **method** | Method | The HTTP method to use. Enum values: \* GET \* POST \* PUT \* DELETE \* HEAD \* OPTIONS \* TRACE \* PATCH | string | POST |  |
| **oauth2ClientId** | Oauth2 Client Id | Oauth2 Client Id. | string |  |  |
| **oauth2ClientSecret** | Oauth2 Client Secret | Oauth2 Client Secret. | string |  |  |
| **oauth2Scope** | Oauth2 Scope | Oauth2 Scope. | string |  |  |
| **oauth2TokenEndpoint** | Oauth2 Token Endpoint | Oauth2 Token Endpoint. | string |  |  |

## Dependencies

At runtime, the `http-secured-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:http
    
-   camel:kamelet
    
-   camel:core
    

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
            uri: "kamelet:http-secured-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Secured HTTP Sink Kamelet Description

### Authentication Methods

This Kamelet supports multiple authentication methods: - **Basic Authentication**: Username and password - **Digest Authentication**: Enhanced security over basic auth - **NTLM Authentication**: Windows-based authentication - **OAuth 2.0**: Client credentials flow with token endpoint

### HTTP Methods

Supports all standard HTTP methods: GET, POST (default), PUT, DELETE, HEAD, OPTIONS, TRACE, and PATCH.

### OAuth 2.0 Configuration

For OAuth 2.0 authentication, configure: - Client ID and Client Secret - Token Endpoint URL - OAuth Scope (optional)

### Authentication Options

-   **Preemptive Authentication**: Send credentials with the first request (defaults to false)
    
-   **Authentication Methods**: Specify allowed methods as comma-separated values
    

### Required Configuration

-   **URL**: The target HTTP/HTTPS endpoint
    

### Headers

The Kamelet automatically sets the HTTP method header and removes any existing CamelHttpUri header to prevent conflicts.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/http-secured-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/http-secured-sink.kamelet.yaml)