# ArangoDb

**Since Camel 3.5**

**Only producer is supported**

The ArangoDb component is client for ArangoDb that uses the [arango java driver](https://github.com/arangodb/arangodb-java-driver) to perform queries on collections and graphs in the ArangoDb database.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-arangodb</artifactId>
    <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

arangodb:database\[?options\]

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

The ArangoDb component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | Component configuration. |  | ArangoDbConfiguration |
| **documentCollection** (producer) | Collection name, when using ArangoDb as a Document Database. Set the documentCollection name when using the CRUD operation on the document database collections (SAVE\_DOCUMENT , FIND\_DOCUMENT\_BY\_KEY, UPDATE\_DOCUMENT, DELETE\_DOCUMENT). |  | String |
| **edgeCollection** (producer) | Collection name of vertices, when using ArangoDb as a Graph Database. Set the edgeCollection name to perform CRUD operation on edges using these operations : SAVE\_VERTEX, FIND\_VERTEX\_BY\_KEY, UPDATE\_VERTEX, DELETE\_VERTEX. The graph attribute is mandatory. |  | String |
| **graph** (producer) | Graph name, when using ArangoDb as a Graph Database. Combine this attribute with one of the two attributes vertexCollection and edgeCollection. |  | String |
| **host** (producer) | ArangoDB host. If host and port are default, this field is Optional. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
Operations to perform on ArangoDb. For the operation AQL\_QUERY, no need to specify a collection or graph.

Enum values:

-   SAVE\_DOCUMENT
    
-   FIND\_DOCUMENT\_BY\_KEY
    
-   UPDATE\_DOCUMENT
    
-   DELETE\_DOCUMENT
    
-   AQL\_QUERY
    
-   SAVE\_VERTEX
    
-   FIND\_VERTEX\_BY\_KEY
    
-   UPDATE\_VERTEX
    
-   DELETE\_VERTEX
    
-   SAVE\_EDGE
    
-   FIND\_EDGE\_BY\_KEY
    
-   UPDATE\_EDGE
    
-   DELETE\_EDGE
    





 |  | ArangoDbOperation |
| **port** (producer) | ArangoDB exposed port. If host and port are default, this field is Optional. |  | int |
| **vertexCollection** (producer) | Collection name of vertices, when using ArangoDb as a Graph Database. Set the vertexCollection name to perform CRUD operation on vertices using these operations : SAVE\_EDGE, FIND\_EDGE\_BY\_KEY, UPDATE\_EDGE, DELETE\_EDGE. The graph attribute is mandatory. |  | String |
| **arangoDB** (advanced) | **Autowired** To use an existing ArangDB client. |  | ArangoDB |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **vertx** (advanced) | **Autowired** To use an existing Vertx in the ArangoDB client. |  | Vertx |
| **password** (security) | ArangoDB password. If user and password are default, this field is Optional. |  | String |
| **user** (security) | ArangoDB user. If user and password are default, this field is Optional. |  | String |

## Endpoint Options

The ArangoDb endpoint is configured using URI syntax:

arangodb:database

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **database** (producer) | **Required** database name. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **documentCollection** (producer) | Collection name, when using ArangoDb as a Document Database. Set the documentCollection name when using the CRUD operation on the document database collections (SAVE\_DOCUMENT , FIND\_DOCUMENT\_BY\_KEY, UPDATE\_DOCUMENT, DELETE\_DOCUMENT). |  | String |
| **edgeCollection** (producer) | Collection name of vertices, when using ArangoDb as a Graph Database. Set the edgeCollection name to perform CRUD operation on edges using these operations : SAVE\_VERTEX, FIND\_VERTEX\_BY\_KEY, UPDATE\_VERTEX, DELETE\_VERTEX. The graph attribute is mandatory. |  | String |
| **graph** (producer) | Graph name, when using ArangoDb as a Graph Database. Combine this attribute with one of the two attributes vertexCollection and edgeCollection. |  | String |
| **host** (producer) | ArangoDB host. If host and port are default, this field is Optional. |  | String |
| **operation** (producer) | 
Operations to perform on ArangoDb. For the operation AQL\_QUERY, no need to specify a collection or graph.

Enum values:

-   SAVE\_DOCUMENT
    
-   FIND\_DOCUMENT\_BY\_KEY
    
-   UPDATE\_DOCUMENT
    
-   DELETE\_DOCUMENT
    
-   AQL\_QUERY
    
-   SAVE\_VERTEX
    
-   FIND\_VERTEX\_BY\_KEY
    
-   UPDATE\_VERTEX
    
-   DELETE\_VERTEX
    
-   SAVE\_EDGE
    
-   FIND\_EDGE\_BY\_KEY
    
-   UPDATE\_EDGE
    
-   DELETE\_EDGE
    





 |  | ArangoDbOperation |
| **port** (producer) | ArangoDB exposed port. If host and port are default, this field is Optional. |  | int |
| **vertexCollection** (producer) | Collection name of vertices, when using ArangoDb as a Graph Database. Set the vertexCollection name to perform CRUD operation on vertices using these operations : SAVE\_EDGE, FIND\_EDGE\_BY\_KEY, UPDATE\_EDGE, DELETE\_EDGE. The graph attribute is mandatory. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **arangoDB** (advanced) | To use an existing ArangDB client. |  | ArangoDB |
| **vertx** (advanced) | To use an existing Vertx instance in the ArangoDB client. |  | Vertx |
| **password** (security) | ArangoDB password. If user and password are default, this field is Optional. |  | String |
| **user** (security) | ArangoDB user. If user and password are default, this field is Optional. |  | String |

## Message Headers

The ArangoDb component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelArangoDbMultiUpdate** (producer) Constant: [`MULTI_UPDATE`](https://javadoc.io/doc/org.apache.camel/camel-arangodb/latest/org/apache/camel/component/arangodb/ArangoDbConstants.html#MULTI_UPDATE) | Indicates if there are multiple documents to update. If set to true, the body of the message must be a Collection of documents to update. | false | Boolean |
| **CamelArangoDbMultiInsert** (producer) Constant: [`MULTI_INSERT`](https://javadoc.io/doc/org.apache.camel/camel-arangodb/latest/org/apache/camel/component/arangodb/ArangoDbConstants.html#MULTI_INSERT) | Indicates if there are multiple documents to insert. If set to true, the body of the message must be a Collection of documents to insert. | false | Boolean |
| **CamelArangoDbMultiDelete** (producer) Constant: [`MULTI_DELETE`](https://javadoc.io/doc/org.apache.camel/camel-arangodb/latest/org/apache/camel/component/arangodb/ArangoDbConstants.html#MULTI_DELETE) | Indicates if there are multiple documents to delete. If set to true, the body of the message must be a Collection of key of documents to delete. | false | Boolean |
| **CamelArangoDbKey** (producer) Constant: [`ARANGO_KEY`](https://javadoc.io/doc/org.apache.camel/camel-arangodb/latest/org/apache/camel/component/arangodb/ArangoDbConstants.html#ARANGO_KEY) | The Arango key to use for the operation. |  | String |
| **CamelArangoDbResultClassType** (producer) Constant: [`RESULT_CLASS_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-arangodb/latest/org/apache/camel/component/arangodb/ArangoDbConstants.html#RESULT_CLASS_TYPE) | The type of the result of the operation. | BaseDocument.class or BaseEdgeDocument.class | Class |
| **CamelArangoDbAqlQuery** (producer) Constant: [`AQL_QUERY`](https://javadoc.io/doc/org.apache.camel/camel-arangodb/latest/org/apache/camel/component/arangodb/ArangoDbConstants.html#AQL_QUERY) | The AQL query to execute. |  | String |
| **CamelArangoDbAqlParameters** (producer) Constant: [`AQL_QUERY_BIND_PARAMETERS`](https://javadoc.io/doc/org.apache.camel/camel-arangodb/latest/org/apache/camel/component/arangodb/ArangoDbConstants.html#AQL_QUERY_BIND_PARAMETERS) | The key/value pairs defining the variables to bind the query to. |  | Map |
| **CamelArangoDbAqlOptions** (advanced) Constant: [`AQL_QUERY_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-arangodb/latest/org/apache/camel/component/arangodb/ArangoDbConstants.html#AQL_QUERY_OPTIONS) | The additional options that will be passed to the query API. |  | AqlQueryOptions |

## Message Body

The message body at each side of the ArangoDb component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `map`, `pojo` or `list` | 
By the operation: the document to save or update as a Map or a POJO (a List of them with the CamelArangoDbMultiInsert or CamelArangoDbMultiUpdate header), the key as text to find or delete (a List of keys with CamelArangoDbMultiDelete), and the AQL query as text unless the CamelArangoDbAqlQuery header has it. JSON text, bytes or a stream is not a document: unmarshal it to a Map first. The key of an update is the CamelArangoDbKey header.

-   With `operation=FIND_DOCUMENT_BY_KEY`: `text`
    
-   With `operation=DELETE_DOCUMENT`: `text` or `list`
    
-   With `operation=AQL_QUERY`: `text`
    
-   With `operation=SAVE_VERTEX`: `map` or `pojo`
    
-   With `operation=UPDATE_VERTEX`: `map` or `pojo`
    
-   With `operation=FIND_VERTEX_BY_KEY`: `text`
    
-   With `operation=DELETE_VERTEX`: `text`
    
-   With `operation=SAVE_EDGE`: `map` or `pojo`
    
-   With `operation=UPDATE_EDGE`: `map` or `pojo`
    
-   With `operation=FIND_EDGE_BY_KEY`: `text`
    
-   With `operation=DELETE_EDGE`: `text`
    





 |
| **Producer output** | `unknown` | 

By the operation, which must be set: the result entity of the ArangoDB driver (DocumentCreateEntity, DocumentUpdateEntity, DocumentDeleteEntity, or a MultiDocumentEntity for the multi headers) for the document writes; the document found as a BaseDocument (or BaseEdgeDocument), or of the class in the CamelArangoDbResultClassType header, or null when there is none; a List of the AQL results, empty for a query that returns nothing; and true for a delete of a vertex or edge.

-   With `operation=SAVE_DOCUMENT`: `pojo`
    
-   With `operation=FIND_DOCUMENT_BY_KEY`: `pojo` or `null`
    
-   With `operation=UPDATE_DOCUMENT`: `pojo`
    
-   With `operation=DELETE_DOCUMENT`: `pojo`
    
-   With `operation=AQL_QUERY`: `list`
    
-   With `operation=SAVE_VERTEX`: `pojo` (`com.arangodb.entity.VertexEntity`)
    
-   With `operation=FIND_VERTEX_BY_KEY`: `pojo` or `null`
    
-   With `operation=UPDATE_VERTEX`: `pojo` (`com.arangodb.entity.VertexUpdateEntity`)
    
-   With `operation=DELETE_VERTEX`: `value` (`java.lang.Boolean`)
    
-   With `operation=SAVE_EDGE`: `pojo` (`com.arangodb.entity.EdgeEntity`)
    
-   With `operation=FIND_EDGE_BY_KEY`: `pojo` or `null`
    
-   With `operation=UPDATE_EDGE`: `pojo` (`com.arangodb.entity.EdgeUpdateEntity`)
    
-   With `operation=DELETE_EDGE`: `value` (`java.lang.Boolean`)
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Examples

### Producer Examples

#### Save document on a collection

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:insert")
    .to("arangodb:testDb?documentCollection=collection&operation=SAVE_DOCUMENT");
```

```xml
<route>
  <from uri="direct:insert"/>
  <to uri="arangodb:testDb?documentCollection=collection&amp;operation=SAVE_DOCUMENT"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:insert
      steps:
        - to:
            uri: arangodb:testDb
            parameters:
              documentCollection: collection
              operation: SAVE_DOCUMENT
```

And you can set as body a BaseDocument class

BaseDocument myObject = new BaseDocument();
myObject.addAttribute("a", "Foo");
myObject.addAttribute("b", 42);

#### Query a collection

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:query")
    .to("arangodb:testDb?operation=AQL_QUERY");
```

```xml
<route>
  <from uri="direct:query"/>
  <to uri="arangodb:testDb?operation=AQL_QUERY"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:query
      steps:
        - to:
            uri: arangodb:testDb
            parameters:
              operation: AQL_QUERY
```

And you can invoke an AQL Query in this way

_Java-only: ProducerTemplate with AQL query parameters and string concatenation_

```java
String query = "FOR t IN " + COLLECTION_NAME + " FILTER t.value == @value";
Map<String, Object> bindVars = new MapBuilder().put("value", "hello")
        .get();

Exchange result = template.request("direct:query", exchange -> {
    exchange.getMessage().setHeader(AQL_QUERY, query);
    exchange.getMessage().setHeader(AQL_QUERY_BIND_PARAMETERS, bindVars);
});
```