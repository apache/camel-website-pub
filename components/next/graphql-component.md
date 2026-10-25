# GraphQL

**Since Camel 3.0**

**Only producer is supported**

The GraphQL component is a GraphQL client that communicates over HTTP and supports queries and mutations, but not subscriptions. It sends the requests with the [HTTP](http-component.md) component, which uses the Apache HttpClient 5 library.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-graphql</artifactId>
    <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## Configuring Options

Camel components are configured on two separate levels:

-   component level
    
-   endpoint level
    

### Configuring Component Options

At the component level, you set general and shared configurations that are, then, inherited by the endpoints. It is the highest configuration level.

For example, a component may have security settings, credentials for authentication, urls for network connection and so forth.

Some components only have a few options, and others may have many. Because components typically have pre-configured defaults that are commonly used, then you may often only need to configure a few options on a component; or none at all.

You can configure components using:

-   the [Component DSL](../../manual/component-dsl.md).
    
-   in a configuration file (`application.properties`, `*.yaml` files, etc).
    
-   directly in the Java code.
    

### Configuring Endpoint Options

You usually spend more time setting up endpoints because they have many options. These options help you customize what you want the endpoint to do. The options are also categorized into whether the endpoint is used as a consumer (_from_), as a producer (_to_), or both.

Configuring endpoints is most often done directly in the endpoint URI as _path_ and _query_ parameters. You can also use the [Endpoint DSL](../../manual/Endpoint-dsl.md) and [DataFormat DSL](../../manual/dataformat-dsl.md) as a _type safe_ way of configuring endpoints and data formats in Java.

A good practice when configuring options is to use [Property Placeholders](../../manual/using-propertyplaceholder.md).

Property placeholders provide a few benefits:

-   They help prevent using hardcoded urls, port numbers, sensitive information, and other settings.
    
-   They allow externalizing the configuration from the code.
    
-   They help the code to become more flexible and reusable.
    

The following two sections list all the options, firstly for the component followed by the endpoint.

## Component Options

The GraphQL component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **throwExceptionOnFailure** (producer) | Option to disable throwing the HttpOperationFailedException in case of failed responses from the remote server. This allows you to get all responses regardless of the HTTP status code. | true | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **httpClient** (advanced) | To use a custom pre-existing Http Client. Beware that when using this, then other configurations such as proxy, access token, is not applied and all this must be pre-configured on the Http Client. |  | HttpClient |
| **headerFilterStrategy** (filter) | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |

## Endpoint Options

The GraphQL endpoint is configured using URI syntax:

graphql:httpUri

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **httpUri** (producer) | **Required** The GraphQL server URI. |  | URI |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **headerFilterStrategy** (common (advanced)) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **operationName** (producer) | The query or mutation name. |  | String |
| **proxyHost** (producer) | The proxy host in the format hostname:port. |  | String |
| **query** (producer) | The query text. |  | String |
| **queryFile** (producer) | The query file name located in the classpath (or use file: to load from file system). |  | String |
| **queryHeader** (producer) | The name of a header containing the GraphQL query. The header is not sent as an HTTP header. |  | String |
| **throwExceptionOnFailure** (producer) | Option to disable throwing the HttpOperationFailedException in case of failed responses from the remote server. This allows you to get all responses regardless of the HTTP status code. | true | boolean |
| **variables** (producer) | The JsonObject instance containing the operation variables. |  | JsonObject |
| **variablesHeader** (producer) | The name of a header containing the operation variables, as a JsonObject or a Map. The header is not sent as an HTTP header. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **httpClient** (advanced) | To use a custom pre-existing Http Client. Beware that when using this, then other configurations such as proxy, access token, is not applied and all this must be pre-configured on the Http Client. |  | HttpClient |
| **accessToken** (security) | The access token sent in the Authorization header. |  | String |
| **jwtAuthorizationType** (security) | The JWT Authorization type. Default is Bearer. | Bearer | String |
| **password** (security) | The password for Basic authentication. |  | String |
| **username** (security) | The username for Basic authentication. |  | String |

## Message Body

The message body at each side of the GraphQL component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `text`, `bytes`, `stream` or `file` | The query, when none of query, queryFile and queryHeader is set: text, or bytes, a stream or a file of it; another body, such as a Map, fails. With one of them the body is not sent, except that a Map body, such as an org.apache.camel.util.json.JsonObject, is the variables when neither variables nor variablesHeader is set.
Not known when `query` or `queryFile` or `queryHeader` is set.

 |
| **Producer output** | `text` or `null` | The response as text, the JSON with the data and errors of GraphQL: unmarshal it to read them. Errors in the response do not fail the exchange; a status outside 2xx does, unless throwExceptionOnFailure=false, which keeps the response as text. null for a response without a body. |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers are described in the [Camel Catalog](../../manual/camel-catalog.md).

## Message Body

If the `query`, `queryFile` and `queryHeader` parameters are not set, the body is the query: it must be text, bytes, a stream or a file, and another body (such as a `Map`) fails with an `InvalidPayloadException`. Otherwise, if the `variables` and `variablesHeader` parameters are not set and the body is a `Map` (such as a `JsonObject`), Camel will use it for the operation’s variables. Camel will store the GraphQL response from the external server on the message body, as a `String` of the JSON response, with the `data` and `errors` of GraphQL: errors in the response do not fail the exchange.

## HTTP Headers

The headers of the message are sent as HTTP request headers (filtered by the `headerFilterStrategy`), except:

-   the headers named by the `queryHeader` and `variablesHeader` parameters, as the query and the variables are sent in the JSON body of the request;
    
-   a `Content-Encoding` header, as the request is not compressed.
    

The producer always sends the request with `Content-Type: application/json`, `Accept: application/json` and `Accept-Encoding: gzip`, whatever the headers of the message are.

After the call, the message keeps its own headers, and Camel adds the HTTP response headers (such as `CamelHttpResponseCode` and the `Content-Type` of the response). The headers the producer set for the request (`CamelHttpMethod`, `Accept` and `Accept-Encoding`) do not stay on the message: a header of the message with the same name keeps its value.

## Examples

### Queries

Simple queries can be defined directly in the URI:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("graphql://http://example.com/graphql?query={books{id name}}");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="graphql://http://example.com/graphql?query={books{id name}}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: graphql://http://example.com/graphql
            parameters:
              query: "{books{id name}}"
```

The body can also be used for the query:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setBody(constant("{books{id name}}"))
    .to("graphql://http://example.com/graphql");
```

```xml
<route>
  <from uri="direct:start"/>
  <setBody>
    <constant>{books{id name}}</constant>
  </setBody>
  <to uri="graphql://http://example.com/graphql"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setBody:
            constant: "{books{id name}}"
        - to:
            uri: graphql://http://example.com/graphql
```

The query can come from a header also:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .setHeader("myQuery", constant("{books{id name}}"))
    .to("graphql://http://example.com/graphql?queryHeader=myQuery");
```

```xml
<route>
  <from uri="direct:start"/>
  <setHeader name="myQuery">
    <constant>{books{id name}}</constant>
  </setHeader>
  <to uri="graphql://http://example.com/graphql?queryHeader=myQuery"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - setHeader:
            name: myQuery
            constant: "{books{id name}}"
        - to:
            uri: graphql://http://example.com/graphql
            parameters:
              queryHeader: myQuery
```

More complex queries can be stored in a file and referenced in the URI:

booksQuery.graphql file:

query Books {
  books {
    id
    name
  }
}

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("graphql://http://example.com/graphql?queryFile=booksQuery.graphql");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="graphql://http://example.com/graphql?queryFile=booksQuery.graphql"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: graphql://http://example.com/graphql
            parameters:
              queryFile: booksQuery.graphql
```

When the query file defines multiple operations, it’s required to specify which one should be executed:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("graphql://http://example.com/graphql?queryFile=multipleQueries.graphql&operationName=Books");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="graphql://http://example.com/graphql?queryFile=multipleQueries.graphql&amp;operationName=Books"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: graphql://http://example.com/graphql
            parameters:
              queryFile: multipleQueries.graphql
              operationName: Books
```

Queries with variables need to reference a JsonObject instance from the registry:

bookByIdQuery.graphql file:

query BookById($id: Int!) {
  bookById(id: $id) {
    id
    name
    author
  }
}

_Java-only: registering query variables and referencing them in the endpoint_

```java
@BindToRegistry("bookByIdQueryVariables")
public JsonObject bookByIdQueryVariables() {
    JsonObject variables = new JsonObject();
    variables.put("id", "book-1");
    return variables;
}

from("direct:start")
    .to("graphql://http://example.com/graphql?queryFile=bookByIdQuery.graphql&variables=#bookByIdQueryVariables")
```

A query that accesses variables via the variablesHeader parameter:

_Java-only: setting variables via a header with a lambda supplier_

```java
from("direct:start")
    .setHeader("myVariables", () -> {
        JsonObject variables = new JsonObject();
        variables.put("id", "book-1");
        return variables;
    })
    .to("graphql://http://example.com/graphql?queryFile=bookByIdQuery.graphql&variablesHeader=myVariables")
```

### Mutations

Mutations are like queries with variables. They specify a query and a reference to a variables' bean:

addBookMutation.graphql file:

mutation AddBook($bookInput: BookInput) {
  addBook(bookInput: $bookInput) {
    id
    name
    author {
      name
    }
  }
}

_Java-only: registering mutation variables and referencing them in the endpoint_

```java
@BindToRegistry("addBookMutationVariables")
public JsonObject addBookMutationVariables() {
    JsonObject bookInput = new JsonObject();
    bookInput.put("name", "Typee");
    bookInput.put("authorId", "author-2");
    JsonObject variables = new JsonObject();
    variables.put("bookInput", bookInput);
    return variables;
}

from("direct:start")
    .to("graphql://http://example.com/graphql?queryFile=addBookMutation.graphql&variables=#addBookMutationVariables")
```