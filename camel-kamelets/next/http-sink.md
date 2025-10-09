# ![http sink](_images/kamelets/http-sink.svg) HTTP Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Forward data to a HTTP or HTTPS endpoint.

## Configuration Options

The following table summarizes the configuration options available for the `http-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The URL to which you want to send data. | string |  | https://my-service/path |
| **method** | Method | The HTTP method to use. Enum values: \* GET \* POST \* PUT \* DELETE \* HEAD \* OPTIONS \* TRACE \* PATCH | string | POST |  |

## Dependencies

At runtime, the `http-sink` Kamelet relies upon the presence of the following dependencies:

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