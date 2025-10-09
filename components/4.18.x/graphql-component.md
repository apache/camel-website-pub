# GraphQL

**Since Camel 3.0**

**Only producer is supported**

The GraphQL component is a GraphQL client that communicates over HTTP and supports queries and mutations, but not subscriptions. It uses the [Apache HttpClient](https://hc.apache.org/httpcomponents-client-4.5.x/index.md) library.

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

The GraphQL component supports 5 options, which are listed below.

   
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

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **httpUri** (producer) | **Required** The GraphQL server URI. |  | URI |

### Query Parameters (15 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **headerFilterStrategy** (common (advanced)) | To use a custom HeaderFilterStrategy to filter header to and from Camel message. |  | HeaderFilterStrategy |
| **operationName** (producer) | The query or mutation name. |  | String |
| **proxyHost** (producer) | The proxy host in the format hostname:port. |  | String |
| **query** (producer) | The query text. |  | String |
| **queryFile** (producer) | The query file name located in the classpath (or use file: to load from file system). |  | String |
| **queryHeader** (producer) | The name of a header containing the GraphQL query. |  | String |
| **throwExceptionOnFailure** (producer) | Option to disable throwing the HttpOperationFailedException in case of failed responses from the remote server. This allows you to get all responses regardless of the HTTP status code. | true | boolean |
| **variables** (producer) | The JsonObject instance containing the operation variables. |  | JsonObject |
| **variablesHeader** (producer) | The name of a header containing a JsonObject instance containing the operation variables. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **httpClient** (advanced) | To use a custom pre-existing Http Client. Beware that when using this, then other configurations such as proxy, access token, is not applied and all this must be pre-configured on the Http Client. |  | HttpClient |
| **accessToken** (security) | The access token sent in the Authorization header. |  | String |
| **jwtAuthorizationType** (security) | The JWT Authorization type. Default is Bearer. | Bearer | String |
| **password** (security) | The password for Basic authentication. |  | String |
| **username** (security) | The username for Basic authentication. |  | String |

## Message Body

If the `variables` and `variablesHeader` parameters are not set and the IN body is a JsonObject instance, Camel will use it for the operation’s variables. If the `query` and `queryFile` parameters are not set and the IN body is a String, Camel will use it as the query. Camel will store the GraphQL response from the external server on the OUT message body. All headers from the IN message will be copied to the OUT message, so headers are preserved during routing. Additionally, Camel will add the HTTP response headers as well to the OUT message headers.

## Examples

### Queries

Simple queries can be defined directly in the URI:

```java
from("direct:start")
    .to("graphql://http://example.com/graphql?query={books{id name}}")
```

The body can also be used for the query:

```java
from("direct:start")
    .setBody(constant("{books{id name}}"))
    .to("graphql://http://example.com/graphql")
```

The query can come from a header also:

```java
from("direct:start")
    .setHeader("myQuery", constant("{books{id name}}"))
    .to("graphql://http://example.com/graphql?queryHeader=myQuery")
```

More complex queries can be stored in a file and referenced in the URI:

booksQuery.graphql file:

query Books {
  books {
    id
    name
  }
}

```java
from("direct:start")
    .to("graphql://http://example.com/graphql?queryFile=booksQuery.graphql")
```

When the query file defines multiple operations, it’s required to specify which one should be executed:

```java
from("direct:start")
    .to("graphql://http://example.com/graphql?queryFile=multipleQueries.graphql&operationName=Books")
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

## Spring Boot Auto-Configuration

When using graphql with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-graphql-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.graphql.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.graphql.enabled** | Whether to enable auto configuration of the graphql component. This is enabled by default. |  | Boolean |
| **camel.component.graphql.header-filter-strategy** | To use a custom org.apache.camel.spi.HeaderFilterStrategy to filter header to and from Camel message. The option is a org.apache.camel.spi.HeaderFilterStrategy type. |  | HeaderFilterStrategy |
| **camel.component.graphql.http-client** | To use a custom pre-existing Http Client. Beware that when using this, then other configurations such as proxy, access token, is not applied and all this must be pre-configured on the Http Client. The option is a org.apache.hc.client5.http.classic.HttpClient type. |  | HttpClient |
| **camel.component.graphql.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.graphql.throw-exception-on-failure** | Option to disable throwing the HttpOperationFailedException in case of failed responses from the remote server. This allows you to get all responses regardless of the HTTP status code. | true | Boolean |