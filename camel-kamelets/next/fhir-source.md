# ![fhir source](_images/kamelets/fhir-source.svg) FHIR Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Runs the same search on a FHIR server of healthcare data over and over, by default for all the Patient resources, and sends each search result, a FHIR Bundle, as one message.

Use it to copy healthcare records, such as patients or observations, from a FHIR server into another system, or to check a FHIR server on a schedule. To create or update resources on a FHIR server, use `fhir-sink`.

Output: the body is a FHIR Bundle of type `searchset`, as JSON text, with the number of resources found (`total`) and the resources themselves under `entry`. The `Content-Type` header is `application/fhir+json`.

Good to know: a new search starts about every half second unless `delay` is set, and every search returns all the matching resources again, not only the new ones; add a filter such as `_lastUpdated` to `url` to narrow it. Log in with `username` and `password`, or with `accessToken`, or leave them out for a server without login; when both kinds are set, both are sent.

## Configuration Options

The following table summarizes the configuration options available for the `fhir-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **serverUrl** | Server URL | **Required** The base address of the FHIR API of the server, the part before the resource type, starting with `http://` or `https://`. | string |  | https://fhir.example.com/fhir |
| **accessToken** | Access Token | An OAuth access token, sent as a Bearer token, for a server that uses OAuth, such as SMART on FHIR. Use it instead of `username` and `password`. | string |  |  |
| **delay** | Delay | How long to wait after a search before the next one starts, in milliseconds. For example, 60000 is one minute. When it is not set, it is 500 (half a second). | integer |  | 60000 |
| **encoding** | Encoding | How the server is asked to answer, `JSON` or `XML`. The body that comes out is JSON in both cases. Enum values: \* JSON \* XML | string | JSON |  |
| **fhirVersion** | FHIR Version | The version of the FHIR standard that the server uses. Most servers today use `R4`. Enum values: \* DSTU2 \* DSTU2\_HL7ORG \* DSTU2\_1 \* DSTU3 \* R4 \* R5 | string | R4 |  |
| **password** | Password | The password of `username`, for Basic authentication. | string |  |  |
| **prettyPrint** | Json Pretty Print | If true, the JSON in the body is indented over several lines; if false, it is on one line. | boolean | true |  |
| **proxyHost** | Proxy Host | The host name of an HTTP proxy to reach the server through. Use it with `proxyPort`. | string |  | proxy.example.com |
| **proxyPassword** | Proxy Password | The password of `proxyUser` for the HTTP proxy. | string |  |  |
| **proxyPort** | Proxy Port | The port of the HTTP proxy in `proxyHost`. | integer |  | 3128 |
| **proxyUser** | Proxy User | The user to log in to the HTTP proxy as, when the proxy needs a login. | string |  |  |
| **url** | URL | The search to run, as the part of a FHIR search URL after `serverUrl`, starting with the resource type, and optionally followed by search parameters. | string | /Patient | /Observation?subject=Patient/123 |
| **username** | Username | The user to log in to the server as, with Basic authentication. Leave it out for a server without login. | string |  |  |

## Dependencies

At runtime, the `fhir-source` Kamelet relies upon the presence of the following dependencies:

-   camel:fhir
    
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
      uri: "kamelet:fhir-source"
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

## FHIR Source Kamelet Description

### Authentication

Log in to the FHIR server with Basic authentication, through the `username` and `password` properties, or with an OAuth access token in `accessToken`. Leave them out for a server without login. When both are set, both are sent.

To reach the server through an HTTP proxy, set `proxyHost` and `proxyPort`, and `proxyUser` and `proxyPassword` for a proxy that needs a login.

### Configuration

The FHIR Source Kamelet supports the following configurations:

-   **Server URL**: The FHIR server URL endpoint (required)
    
-   **Resource URL**: The FHIR resource type URL (default: "/Patient")
    
-   **Encoding**: Response encoding format - JSON or XML (default: "JSON")
    
-   **FHIR Version**: The FHIR specification version to use (default: "R4")
    
-   **Pretty Print**: Whether to format JSON responses for readability (default: true)
    
-   **Delay**: How long to wait between two searches, in milliseconds (default: 500)
    

### Output Format

The Kamelet outputs data in JSON format, marshalling FHIR resources according to the specified FHIR version and pretty print settings.

### Usage Example

```yaml
- route:
    from:
      uri: "kamelet:fhir-source"
      parameters:
        serverUrl: "https://hapi.fhir.org/baseR4"
        username: "your-username"
        password: "your-password"
        url: "/Patient"
        fhirVersion: "R4"
        encoding: "JSON"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

### Example with Different Resource Type

```yaml
- route:
    from:
      uri: "kamelet:fhir-source"
      parameters:
        serverUrl: "https://hapi.fhir.org/baseR4"
        username: "your-username"
        password: "your-password"
        url: "/Observation"
        fhirVersion: "R4"
        encoding: "JSON"
        prettyPrint: false
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This example searches for Observation resources from the FHIR server with compact JSON output.

### Example with an Access Token, a Proxy and a Delay

```yaml
- route:
    from:
      uri: "kamelet:fhir-source"
      parameters:
        serverUrl: "https://fhir.example.com/fhir"
        accessToken: "my-oauth-token"
        url: "/Observation?_lastUpdated=gt2026-01-01"
        delay: 60000
        proxyHost: "proxy.example.com"
        proxyPort: 3128
        proxyUser: "proxy-user"
        proxyPassword: "proxy-password"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This example runs the search once a minute, through an HTTP proxy, with an OAuth access token.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/fhir-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/fhir-source.kamelet.yaml)