# ![graphql sink](_images/kamelets/graphql-sink.svg) GraphQL Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Forward data to a GraphQL endpoint.

## Configuration Options

The following table summarizes the configuration options available for the `graphql-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | GraphQL Server URL | **Required** The URL to which you want to send data. | string |  | http://example.com/graphql |
| **accessToken** | GraphQL Access Token | The access Token to use to access GraphQL server. | string |  |  |

## Dependencies

At runtime, the `graphql-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:graphql
    
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
            uri: "kamelet:graphql-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## GraphQL Sink Kamelet Description

### GraphQL Operations

This Kamelet forwards data to GraphQL endpoints for executing queries, mutations, and subscriptions.

### Required Configuration

-   **URL**: The GraphQL server endpoint URL (must be HTTP or HTTPS)
    

### Authentication

-   **Access Token**: Optional access token for secured GraphQL endpoints
    

### Usage

The Kamelet sends data to the specified GraphQL endpoint, enabling integration with GraphQL APIs for data operations and retrieval.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/graphql-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/graphql-sink.kamelet.yaml)