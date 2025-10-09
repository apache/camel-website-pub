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

### Schema Validation

OpenAPI specifications include schema definitions that can be used for request and response validation, ensuring data integrity and API compliance.

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