# ![rest openapi sink](_images/kamelets/rest-openapi-sink.svg) REST OpenAPI Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Calls one operation of a REST API for each message, building the request (method, path, parameters and content type) from the OpenAPI specification of the API.

Use it to call an API that publishes an OpenAPI (Swagger) document without writing its URLs by hand, for example to create a customer or look up an order in a service of your company. For a call to a fixed URL, use `http-sink`.

Input: the body is the request body, such as JSON text, and is sent with the content type the specification gives for the operation, or the one in `produces`. The path and query parameters of the operation come from headers of the same name: for `/pets/{petId}`, set the `petId` header. The other headers of the message, except the Camel ones, are sent as HTTP headers.

Output: when it is used inside a route, the body afterwards is the response of the API, as bytes, with the headers of the response and its status code in `CamelHttpResponseCode`.

Good to know: a missing path parameter is not an error; the request is sent with `{petId}` in the path, unless `clientRequestValidation` is true. The address of the API is taken from the `servers` of the specification, unless `host` or `basePath` is set. The login comes only from the options: an `Authorization` or `Proxy-Authorization` header on the message is removed, so a credential that came with the message is not sent on. Log in either with `authUsername` and `authPassword`, sent with Basic login after the service answers 401, or with a static token in `authBearerToken`, sent as a Bearer token on every request. The Kamelet does not start when the specification has no operation with the ID in `operation`. Headers that start with `CamelHttp` or `CamelRestHttp` are removed from the message first, so they cannot change what the Kamelet does.

## Configuration Options

The following table summarizes the configuration options available for the `rest-openapi-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **operation** | Operation ID | **Required** The `operationId` of the operation to call, exactly as it is written in the specification. | string |  | getOrderById |
| **specification** | Specification URI | **Required** Where to load the OpenAPI document of the API from. It starts with `https://` or `http://` for a URL, `file://` for a file, or `classpath://` for a resource in the application. | string |  | https://api.example.com/openapi.json |
| **authBearerToken** | Bearer Token | A static token, such as an API key, sent on every request in the `Authorization` header as `Bearer` followed by the token. The header is removed from the message after the call. | string |  |  |
| **authPassword** | Authentication Password | The password of `authUsername`. | string |  |  |
| **authUsername** | Authentication Username | The user to log in as with Basic login, together with `authPassword`. They are sent only after the service answers 401 and asks for them, which takes a second request. | string |  |  |
| **basePath** | Base Path | The path that comes before the paths of the operations, in place of the one in the specification. | string |  | /v3 |
| **clientRequestValidation** | Client Request Validation | If true, each request is checked against the specification before it is sent. A request that does not match it, such as one without a required parameter, fails the message and is not sent. | boolean | false |  |
| **consumes** | Accepted Response Types | The content types of the response to ask the API for, sent as the `Accept` header, in place of the ones the specification lists for the responses of the operation. Separate several types with commas, without spaces, such as `application/json,text/csv`. An `Accept` header on the message is sent instead. | string |  | application/json |
| **host** | Host | The scheme, host and port of the API, in place of the address in the `servers` of the specification. Use it when the specification points to another server, such as a test server or `localhost`. | string |  | https://api.example.com:443 |
| **produces** | Request Content Type | The content type of the request body, sent as the `Content-Type` header, such as `application/json`, in place of the one the specification gives for the request body of the operation. A `Content-Type` header on the message is sent instead. | string |  | application/merge-patch+json |

## Dependencies

At runtime, the `rest-openapi-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:rest-openapi
    
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
            uri: "kamelet:rest-openapi-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## REST OpenAPI Sink Kamelet Description

### RESTful API Integration

This Kamelet provides integration with RESTful APIs that are documented using OpenAPI specifications. It enables standardized API communication based on OpenAPI/Swagger definitions.

### OpenAPI Specification

Uses the OpenAPI specification to find the method, the path, the parameters and the content type of the operation given in `operation`. The path and query parameters come from headers with the same names as the parameters: for `/pets/{petId}`, set the `petId` header. A missing path parameter is not an error: the request is sent with `{petId}` in the path. The Kamelet has no authentication options.

### Content Types

The `Accept` and `Content-Type` headers of the request come from the specification: the content types of the responses of the operation, and the content type of its request body. `consumes` replaces the `Accept` header, and `produces` the `Content-Type` header, for an API whose specification lists other types than the ones it should be called with:

```yaml
- to:
    uri: "kamelet:rest-openapi-sink"
    parameters:
      specification: "https://api.example.com/openapi.json"
      operation: updateCustomer
      produces: "application/merge-patch+json"
      consumes: "application/json"
```

Separate several types in `consumes` with commas, without spaces, such as `application/json,text/csv`. An `Accept` or `Content-Type` header on the message is sent instead of these options.

### HTTP Operations

Supports various HTTP operations (GET, POST, PUT, DELETE, etc.) as defined in the OpenAPI specification, providing comprehensive REST API integration capabilities.

### Host and Base Path Configuration

The host and base path for the REST service can be configured to override the default values found in the OpenAPI specification. This is useful for production environments where the specification may contain default values like localhost:8080 that need to be replaced with the actual service endpoint.

### Schema Validation

OpenAPI specifications include schema definitions that can be used for request and response validation. With `clientRequestValidation` set to true, a request that does not conform to the specification fails the message and is not sent.

### Documentation-Driven Development

Enables documentation-driven API development where the API specification serves as the contract between API providers and consumers.

### Standards Compliance

Follows REST architectural principles and OpenAPI standards for:

-   Consistent API design patterns
    
-   Standardized error handling
    
-   Clear documentation and discoverability
    
-   Interoperability across platforms
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/rest-openapi-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/rest-openapi-sink.kamelet.yaml)