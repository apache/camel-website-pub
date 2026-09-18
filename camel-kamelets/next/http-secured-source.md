# ![http secured source](_images/kamelets/http-secured-source.svg) HTTP Secured Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Periodically fetches a secured HTTP resource and provides the content as output. Supports Oauth and Basic authentication.

## Configuration Options

The following table summarizes the configuration options available for the `http-secured-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The URL to fetch for data. | string |  | https://gist.githubusercontent.com/nicolaferraro/e3c72ace3c751f9f88273896611ce5fe/raw/3b6f54060bacb56b6719b7386a4645cb59ad6cc1/quote.json |
| **authMethod** | Authentication Method | Authentication methods allowed to use as a comma separated list of values Basic, Digest or NTLM. | string |  |  |
| **authPassword** | Authentication Password | Authentication password. | string |  |  |
| **authUsername** | Authentication Username | Authentication username. | string |  |  |
| **authenticationPreemptive** | Authentication Preemptive | If this option is true, camel-http sends preemptive basic authentication to the server. | boolean | false |  |
| **contentType** | Content Type | The content type accepted for the resource. | string | application/json |  |
| **oauth2ClientId** | Oauth2 Client Id | Oauth2 Client Id. | string |  |  |
| **oauth2ClientSecret** | Oauth2 Client Secret | Oauth2 Client Secret. | string |  |  |
| **oauth2Scope** | Oauth2 Scope | Oauth2 Scope. | string |  |  |
| **oauth2TokenEndpoint** | Oauth2 Token Endpoint | Oauth2 Token Endpoint. | string |  |  |
| **period** | Period between Updates | The interval between fetches in milliseconds. | integer | 10000 |  |

## Dependencies

At runtime, the `http-secured-source` Kamelet relies upon the presence of the following dependencies:

-   camel:http
    
-   camel:kamelet
    
-   camel:core
    
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

-   OAuth authentication
    
-   Basic authentication using username and password
    
-   No authentication (if not specified)
    

### Output format

The Kamelet periodically fetches a secured HTTP resource and provides the content as output. The content type is configurable and defaults to application/json.

### Configuration

The Kamelet requires the following parameters:

-   `url`: The URL to fetch for data
    

Optional parameters: - `period`: The interval between fetches in milliseconds (default: 10000) - `contentType`: The content type accepted for the resource (default: "application/json") - Authentication parameters (oauth or basic auth credentials)

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