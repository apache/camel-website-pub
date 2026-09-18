# ![http source](_images/kamelets/http-source.svg) HTTP Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Periodically fetches an HTTP resource and provides the content as output.

## Configuration Options

The following table summarizes the configuration options available for the `http-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | URL | **Required** The URL to fetch for data. | string |  | https://gist.githubusercontent.com/nicolaferraro/e3c72ace3c751f9f88273896611ce5fe/raw/3b6f54060bacb56b6719b7386a4645cb59ad6cc1/quote.json |
| **contentType** | Content Type | The content type accepted for the resource. | string | application/json |  |
| **period** | Period between Updates | The interval between fetches in milliseconds. | integer | 10000 |  |

## Dependencies

At runtime, the `http-source` Kamelet relies upon the presence of the following dependencies:

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
    

### Authentication

This is the basic HTTP source kamelet without authentication. For secured HTTP endpoints requiring authentication, use the HTTP Secured Source kamelet instead.

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

### Scheduling Behavior

The kamelet uses a timer to periodically fetch data from the specified URL. The timer starts immediately when the route starts and repeats at the configured interval. Each request includes the specified Accept header to indicate the expected content type.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/http-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/http-source.kamelet.yaml)