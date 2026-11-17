# ![graphql sink](_images/kamelets/graphql-sink.svg) GraphQL Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends the GraphQL query or mutation in the body of each message to a GraphQL server, with an HTTP POST, and gives back the answer of the server.

Use it to create or change data through a GraphQL API with a mutation, for example to add a record for each event, or to fetch data with a query.

Input: the body is the GraphQL query or mutation itself, as text, such as `{ books { title } }`. A body that is not text, such as a Map, fails the message. The other headers of the message, except the Camel ones, are sent as HTTP headers.

Output: when it is used inside a route, the body afterwards is the answer of the server, as JSON text with its `data` and `errors`.

Good to know: GraphQL errors in the answer do not fail the message, but an HTTP status outside 200 to 299 does. Since the body is run as a query, only send it messages from a source you trust.

## Configuration Options

The following table summarizes the configuration options available for the `graphql-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | GraphQL Server URL | **Required** The address of the GraphQL API, starting with `http://` or `https://`. | string |  | https://api.example.com/graphql |
| **accessToken** | GraphQL Access Token | A token from the provider of the API, sent as `Authorization` `Bearer` with each request. Leave it out for an API that needs no login. | string |  |  |

## Dependencies

At runtime, the `graphql-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:graphql
    
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
            uri: "kamelet:graphql-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## GraphQL Sink Kamelet Description

### GraphQL Operations

This Kamelet sends the GraphQL query or mutation in the message body to a GraphQL endpoint, with an HTTP POST, and returns the answer of the server.

### Required Configuration

-   **URL**: The GraphQL server endpoint URL (must be HTTP or HTTPS)
    

### Authentication

-   **Access Token**: Optional access token for secured GraphQL endpoints, sent as a Bearer token
    

### Usage

The body of each message must be the text of the query or mutation, such as `{ books { title } }`. The answer of the server, JSON text with `data` and `errors`, becomes the body of the message, for the next steps of a route.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/graphql-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/graphql-sink.kamelet.yaml)