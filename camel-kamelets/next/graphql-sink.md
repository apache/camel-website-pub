# ![graphql sink](_images/kamelets/graphql-sink.svg) GraphQL Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Stable"**

Sends a GraphQL query or mutation, from the body of each message or from a file, to a GraphQL server with an HTTP POST, and gives back the answer of the server.

Use it to create or change data through a GraphQL API with a mutation, for example to add a record for each event, or to fetch data with a query. It can also run a stored query from `queryFile` each time a message arrives.

Input: the body is the GraphQL query or mutation itself, as text, such as `{ books { title } }`. A body that is not text, such as a Map, fails the message. With `queryFile`, the query comes from that file instead, and the body is not sent, except that a Map body is sent as the variables of the query when `variables` is not set. The other headers of the message, except the Camel ones, are sent as HTTP headers.

Output: when it is used inside a route, the body afterwards is the answer of the server, as JSON text with its `data` and `errors`.

Good to know: GraphQL errors in the answer do not fail the message, but an HTTP status outside 200 to 299 does. Without `queryFile`, the body is run as a query, so only send it messages from a source you trust. When the query defines several operations, `operationName` picks the one to run. To go through an HTTP proxy, set `proxyHost` to its host and port; a proxy that asks for a login is not supported. Headers on the message cannot change where the request is sent.

## Configuration Options

The following table summarizes the configuration options available for the `graphql-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **url** | GraphQL Server URL | **Required** The address of the GraphQL API, starting with `http://` or `https://`. | string |  | https://api.example.com/graphql |
| **accessToken** | GraphQL Access Token | A token from the provider of the API, sent as `Authorization` `Bearer` with each request. Leave it out for an API that needs no login. | string |  |  |
| **operationName** | Operation Name | The name of the operation to run, when the query defines more than one, such as `AddBook` for `mutation AddBook \{ …​ }`. | string |  | AddBook |
| **proxyHost** | Proxy | The host name or IP address and the port of an HTTP proxy to send the requests through, as `host:port`, such as `proxy.example.com:3128`. A proxy that asks for a login is not supported. | string |  | proxy.example.com:3128 |
| **queryFile** | Query File | Where to load the GraphQL query or mutation from, in place of the body. `classpath:` followed by a resource in the application, or `file:` followed by the path of a file. The variables then come from `variables`, or from the body when it is a Map. | string |  | file:/etc/graphql/add-book.graphql |
| **variables** | Variables | The values of the variables of the query, as a JSON object, such as `\{"title":"Dune"}` for a query that declares `$title`. When it is set, the body is not used as the variables. | string |  | {"title":"Dune","year":1965} |

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

This Kamelet sends a GraphQL query or mutation, from the message body or from a file, to a GraphQL endpoint, with an HTTP POST, and returns the answer of the server.

### Required Configuration

-   **URL**: The GraphQL server endpoint URL (must be HTTP or HTTPS)
    

### Authentication

-   **Access Token**: Optional access token for secured GraphQL endpoints, sent as a Bearer token
    

### Usage

The body of each message must be the text of the query or mutation, such as `{ books { title } }`. The answer of the server, JSON text with `data` and `errors`, becomes the body of the message, for the next steps of a route.

### Query from a File

With `queryFile`, the query comes from a file, `file:` followed by its path, or `classpath:` followed by a resource in the application, and the body is not sent as the query. The values of the variables of the query come from `variables`, as a JSON object. When the file defines several operations, `operationName` picks the one to run.

```yaml
- to:
    uri: "kamelet:graphql-sink"
    parameters:
      url: "https://api.example.com/graphql"
      queryFile: "file:/etc/graphql/books.graphql"
      operationName: AddBook
      variables: '{"title":"Dune","year":1965}'
```

With this file, `AddBook` runs with `$title` set to `Dune` and `$year` set to 1965:

```graphql
query ListBooks { books { title } }
mutation AddBook($title: String!, $year: Int) { addBook(title: $title, year: $year) { id } }
```

When `variables` is not set, a body that is a Map, such as JSON parsed into a Map, is sent as the variables. Any other body is not sent.

### Proxy

To send the requests through an HTTP proxy, set `proxyHost` to its host and port, such as `proxy.example.com:3128`. A proxy that asks for a login is not supported.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/graphql-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/graphql-sink.kamelet.yaml)