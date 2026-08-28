# ![rest openapi sink](_images/kamelets/rest-openapi-sink.svg) REST OpenAPI Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Load an OpenAPI specification from a URI and call an operation on a HTTP service. The request that is generated respects the rules given in the OpenAPI specification (for example, path parameters and Content-Type).

## Configuration Options

The following table summarizes the configuration options available for the `rest-openapi-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **operation** | Operation ID | **Required** The operation to call. | string |  |  |
| **specification** | Specification URI | **Required** The URI to the OpenApi specification file. | string |  | https://api.example.com/openapi.json |
| **basePath** | Base Path | The API base path. Overrides the value present in the OpenAPI specification. | string |  | /v3 |
| **clientRequestValidation** | Client Request Validation | Whether to enable validation of the client request to check if the incoming request is valid according to the OpenAPI specification. | boolean | false |  |
| **host** | Host | The host to use for calling the REST service. Overrides the value found in the OpenAPI specification. The format is [https://hostname:port](https://hostname:port). | string |  | https://api.example.com:443 |

## Dependencies

At runtime, the `rest-openapi-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:rest-openapi
    
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

Uses OpenAPI specifications to understand API endpoints, request/response formats, and authentication requirements, ensuring consistent and documented API interactions.

### HTTP Operations

Supports various HTTP operations (GET, POST, PUT, DELETE, etc.) as defined in the OpenAPI specification, providing comprehensive REST API integration capabilities.

### Host and Base Path Configuration

The host and base path for the REST service can be configured to override the default values found in the OpenAPI specification. This is useful for production environments where the specification may contain default values like localhost:8080 that need to be replaced with the actual service endpoint.

### Schema Validation

OpenAPI specifications include schema definitions that can be used for request and response validation, ensuring data integrity and API compliance. Client request validation can be enabled to check if outgoing requests conform to the OpenAPI specification before they are sent.

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