# Docling - Using Docling-Serve API

[Back to Docling Component](../docling-component.md)

## Basic usage with docling-serve

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?useDoclingServe=true&doclingServeUrl=http://localhost:5001&contentInBody=true")
    .process(exchange -> {
        String markdown = exchange.getIn().getBody(String.class);
        log.info("Converted content: {}", markdown);
    });
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            useDoclingServe: true
            doclingServeUrl: "http://localhost:5001"
            contentInBody: true
      - process:
          ref: "markdownProcessor"
```

## Converting documents from URLs using docling-serve

When using docling-serve API mode, you can also process documents from URLs:

-   Java
    
-   YAML
    

```java
from("timer:convert?repeatCount=1")
    .setBody(constant("https://arxiv.org/pdf/2501.17887"))
    .to("docling:CONVERT_TO_MARKDOWN?useDoclingServe=true&contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: timer:convert
      parameters:
        repeatCount: 1
    steps:
      - setBody:
          constant: "https://arxiv.org/pdf/2501.17887"
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            useDoclingServe: true
            contentInBody: true
      - to:
          uri: file:///data/output
```

## Batch processing with docling-serve

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.(pdf|docx)")
    .to("docling:CONVERT_TO_HTML?useDoclingServe=true&doclingServeUrl=http://localhost:5001&contentInBody=true")
    .to("file:///data/converted?fileName=${file:name.noext}.html");
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.(pdf|docx)"
    steps:
      - to:
          uri: docling:CONVERT_TO_HTML
          parameters:
            useDoclingServe: true
            doclingServeUrl: "http://localhost:5001"
            contentInBody: true
      - to:
          uri: file:///data/converted
          parameters:
            fileName: "${file:name.noext}.html"
```

## Authentication with docling-serve

The component supports multiple authentication mechanisms for secured docling-serve instances.

### Bearer Token Authentication

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "doclingServeUrl=http://localhost:5001&" +
        "authenticationScheme=BEARER&" +
        "authenticationToken=your-bearer-token-here&" +
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            useDoclingServe: true
            doclingServeUrl: "http://localhost:5001"
            authenticationScheme: "BEARER"
            authenticationToken: "your-bearer-token-here"
            contentInBody: true
      - to:
          uri: file:///data/output
```

### API Key Authentication

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "doclingServeUrl=http://localhost:5001&" +
        "authenticationScheme=API_KEY&" +
        "authenticationToken=your-api-key-here&" +
        "apiKeyHeader=X-API-Key&" +
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            useDoclingServe: true
            doclingServeUrl: "http://localhost:5001"
            authenticationScheme: "API_KEY"
            authenticationToken: "your-api-key-here"
            apiKeyHeader: "X-API-Key"
            contentInBody: true
      - to:
          uri: file:///data/output
```

### Using Custom API Key Header

If your docling-serve instance uses a custom header name for API keys:

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "doclingServeUrl=http://localhost:5001&" +
        "authenticationScheme=API_KEY&" +
        "authenticationToken=your-api-key-here&" +
        "apiKeyHeader=X-Custom-API-Key&" +
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            useDoclingServe: true
            doclingServeUrl: "http://localhost:5001"
            authenticationScheme: "API_KEY"
            authenticationToken: "your-api-key-here"
            apiKeyHeader: "X-Custom-API-Key"
            contentInBody: true
      - to:
          uri: file:///data/output
```

### Using Authentication Token from Properties

For better security, store authentication tokens in properties or environment variables:

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "doclingServeUrl={{docling.serve.url}}&" +
        "authenticationScheme=BEARER&" +
        "authenticationToken={{docling.serve.token}}&" +
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            useDoclingServe: true
            doclingServeUrl: "{{docling.serve.url}}"
            authenticationScheme: "BEARER"
            authenticationToken: "{{docling.serve.token}}"
            contentInBody: true
      - to:
          uri: file:///data/output
```

Then define in `application.properties`:

```properties
docling.serve.url=http://localhost:5001
docling.serve.token=your-bearer-token-here
```

### OAuth Authentication

When the docling-serve instance is protected by an OAuth identity provider, set the `oauthProfile` parameter to acquire an access token via the OAuth 2.0 Client Credentials grant. The token is used as the `authenticationToken` and the `authenticationScheme` is automatically set to `BEARER`. This requires `camel-oauth` on the classpath.

```properties
camel.oauth.docling.client-id=my-client
camel.oauth.docling.client-secret=my-secret
camel.oauth.docling.token-endpoint=https://idp.example.com/token
```

-   Java
    
-   XML
    
-   YAML
    

```java
from("file:///data/input")
    .to("docling:CONVERT_TO_MARKDOWN?useDoclingServe=true&doclingServeUrl=http://localhost:5001&oauthProfile=docling&contentInBody=true")
    .log("${body}");
```

```xml
<route>
  <from uri="file:///data/input"/>
  <to uri="docling:CONVERT_TO_MARKDOWN?useDoclingServe=true&amp;doclingServeUrl=http://localhost:5001&amp;oauthProfile=docling&amp;contentInBody=true"/>
  <log message="${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: file:///data/input
      steps:
        - to:
            uri: docling:CONVERT_TO_MARKDOWN
            parameters:
              useDoclingServe: true
              doclingServeUrl: "http://localhost:5001"
              oauthProfile: docling
              contentInBody: true
        - log:
            message: "${body}"
```