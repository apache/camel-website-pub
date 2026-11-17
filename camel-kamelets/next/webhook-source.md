# ![webhook source](_images/kamelets/webhook-source.svg) Webhook Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Receives HTTP requests on a path of its own, such as `/webhook`, and sends each request on as a message, with its body and headers.

Use it to receive the webhook calls of an online service, such as a payment, form or code hosting service, or to let another system push data with a simple HTTP POST. To fetch a URL at a regular interval instead, use `http-source`.

Output: the body is the body of the request, as a stream, and is empty for a request without a body, such as a GET. The HTTP headers of the request become headers of the message, and so does each query parameter. `CamelHttpMethod` gives the method (such as `POST`), `CamelHttpPath` the path and `CamelHttpQuery` the query string. A form (`application/x-www-form-urlencoded`) arrives as a Map of its fields instead.

Good to know: there is no login, so anyone who can reach the address can send messages; protect it with network rules or a gateway in front, and treat the content as untrusted. It accepts every HTTP method, on the exact path only. It listens on the HTTP port of the application, 8080 by default with Camel JBang. The caller gets back the message as it is at the end of the flow: by default the body it sent, with status 200, or status 204 when there is no body.

## Configuration Options

The following table summarizes the configuration options available for the `webhook-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **subpath** | Subpath | The path to receive the requests on, without a leading `/`. For example, `hooks/orders` receives the requests sent to `[http://<host>:<port>/hooks/orders](http://\<host\>:\<port\>/hooks/orders)`. | string | webhook | hooks/orders |

## Dependencies

At runtime, the `webhook-source` Kamelet relies upon the presence of the following dependencies:

-   camel:platform-http
    
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
      uri: "kamelet:webhook-source"
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

## Webhook Source Kamelet Description

This Kamelet creates an HTTP endpoint that can receive webhook calls and forward the received data to the sink. It’s designed to act as a bridge for incoming HTTP requests, making it ideal for integrating with external systems that send data via webhooks.

### HTTP endpoint configuration

The Kamelet creates an HTTP endpoint accessible at a configurable subpath. By default, it listens on `/webhook`, but this can be customized using the `subpath` parameter.

### Request handling

The webhook accepts HTTP requests of any method (GET, POST, PUT, etc.) and forwards the complete request (including headers, body, and parameters) to the configured sink.

### Data forwarding

All incoming HTTP requests are forwarded as-is to the sink, preserving:

-   Request body content
    
-   HTTP headers
    
-   Query parameters
    
-   HTTP method information
    

### Configuration options

-   **subpath**: The URL subpath where the webhook listens (default: "webhook")
    

### Usage examples

Basic webhook listener:

```yaml
- route:
    from:
      uri: "kamelet:webhook-source"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This creates an endpoint at `/webhook` that logs all incoming requests.

Custom webhook path:

```yaml
- route:
    from:
      uri: "kamelet:webhook-source"
      parameters:
        subpath: "api/notifications"
      steps:
        - to:
            uri: "kamelet:log-sink"
```

This creates an endpoint at `/api/notifications`.

Processing webhook data:

```yaml
- route:
    from:
      uri: "kamelet:webhook-source"
      parameters:
        subpath: "github-webhook"
      steps:
        - filter:
            expression:
              simple:
                expression: "${header.X-GitHub-Event} == 'push'"
            steps:
              - to:
                  uri: "kamelet:log-sink"
```

This example filters for GitHub push events before processing.

### Integration scenarios

The webhook source is commonly used for:

-   Receiving notifications from external services
    
-   Creating API endpoints for data ingestion
    
-   Building event-driven integrations
    
-   Implementing serverless function triggers
    

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/webhook-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/webhook-source.kamelet.yaml)