# ![webhook source](_images/kamelets/webhook-source.svg) Webhook Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Creates an HTTP endpoint that can be used as a bridge to forward data to the Kamelet sink.

## Configuration Options

The following table summarizes the configuration options available for the `webhook-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **subpath** | Subpath | The subpath where the webhook is registered . | string | webhook |  |

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
            header:
              name: "X-GitHub-Event"
              value: "push"
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