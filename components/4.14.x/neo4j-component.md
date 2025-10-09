# Neo4j

**Since Camel 4.10**

**Only producer is supported**

The Neo4j component provides support for Neo4j graph database.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-neo4j</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## URI format

neo4j:name\[?options\]

Where **name** is the database name.

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

The Neo4j component supports 19 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **alias** (producer) | Node alias. |  | String |
| **configuration** (producer) | The configuration;. |  | Neo4jConfiguration |
| **databaseUrl** (producer) | Url for connecting to Neo database. |  | String |
| **detachRelationship** (producer) | Detach a relationship - set true if want to delete a node and detach its relationships to other nodes at same time. | false | boolean |
| **dimension** (producer) | Dimension of Vector Index. |  | Integer |
| **label** (producer) | Node Label. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxResults** (producer) | Maximum results for Vector Similarity search. | 3 | int |
| **minScore** (producer) | Minimum score for Vector Similarity search. | 0 | double |
| **query** (producer) | Cypher Query. |  | String |
| **similarityFunction** (producer) | 
Similarity Function of Vector Index.

Enum values:

-   cosine
    
-   euclidean
    





 | cosine | Neo4jSimilarityFunction |
| **vectorIndexName** (producer) | Vector Index Name. |  | String |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **driver** (advanced) | **Autowired** Advanced - Driver. |  | Driver |
| **kerberosAuthTicket** (security) | Kerberos Authentication encoded base64 ticket. |  | String |
| **password** (security) | Basic authentication database password. |  | String |
| **realm** (security) | Basic authentication database realm. |  | String |
| **token** (security) | Bearer authentication database realm. |  | String |
| **username** (security) | Basic authentication database user. |  | String |

## Endpoint Options

The Neo4j endpoint is configured using URI syntax:

neo4j:name

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **name** (producer) | **Required** The database name. |  | String |

### Query Parameters (17 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **alias** (producer) | Node alias. |  | String |
| **databaseUrl** (producer) | Url for connecting to Neo database. |  | String |
| **detachRelationship** (producer) | Detach a relationship - set true if want to delete a node and detach its relationships to other nodes at same time. | false | boolean |
| **dimension** (producer) | Dimension of Vector Index. |  | Integer |
| **label** (producer) | Node Label. |  | String |
| **maxResults** (producer) | Maximum results for Vector Similarity search. | 3 | int |
| **minScore** (producer) | Minimum score for Vector Similarity search. | 0 | double |
| **query** (producer) | Cypher Query. |  | String |
| **similarityFunction** (producer) | 
Similarity Function of Vector Index.

Enum values:

-   cosine
    
-   euclidean
    





 | cosine | Neo4jSimilarityFunction |
| **vectorIndexName** (producer) | Vector Index Name. |  | String |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **driver** (advanced) | **Autowired** Advanced - Driver. |  | Driver |
| **kerberosAuthTicket** (security) | Kerberos Authentication encoded base64 ticket. |  | String |
| **password** (security) | Basic authentication database password. |  | String |
| **realm** (security) | Basic authentication database realm. |  | String |
| **token** (security) | Bearer authentication database realm. |  | String |
| **username** (security) | Basic authentication database user. |  | String |

## Message Headers

The Neo4j component supports 12 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelNeo4jOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#OPERATION) | 
The operation to be performed.

Enum values:

-   CREATE\_NODE
    
-   DELETE\_NODE
    
-   RETRIEVE\_NODES
    
-   RETRIEVE\_NODES\_AND\_UPDATE\_WITH\_CYPHER\_QUERY
    
-   ADD\_OR\_DELETE\_NODE\_WITH\_CYPHER\_QUERY
    
-   CREATE\_VECTOR\_INDEX
    
-   DROP\_VECTOR\_INDEX
    
-   CREATE\_VECTOR
    
-   VECTOR\_SIMILARITY\_SEARCH
    





 |  | String |
| **CamelNeo4jMatchProperties** (producer) Constant: [`MATCH_PROPERTIES`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#MATCH_PROPERTIES) | MATCH properties for the generated MATCH query. Needed only if we are matching properties and values. Example: \\{name: 'Alice'}. |  | String |
| **CamelNeo4jQueryResult** (producer) Constant: [`QUERY_RESULT`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#QUERY_RESULT) | Query Result. |  | String |
| **CamelNeo4jQueryResultNodesCreated** (producer) Constant: [`QUERY_RESULT_NODES_CREATED`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#QUERY_RESULT_NODES_CREATED) | Query Number of nodes created. |  | Long |
| **CamelNeo4jQueryResultNodesDeleted** (producer) Constant: [`QUERY_RESULT_NODES_DELETED`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#QUERY_RESULT_NODES_DELETED) | Query Number of nodes deleted. |  | Long |
| **CamelNeo4jQueryResultContainsUpdates** (producer) Constant: [`QUERY_RESULT_CONTAINS_UPDATES`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#QUERY_RESULT_CONTAINS_UPDATES) | Query executed contains update. |  | Boolean |
| **CamelNeo4jQueryResultRelationshipsCreated** (producer) Constant: [`QUERY_RESULT_RELATIONSHIPS_CREATED`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#QUERY_RESULT_RELATIONSHIPS_CREATED) | Query executed number of relationships created. |  | Long |
| **CamelNeo4jQueryResultRelationshipsDeleted** (producer) Constant: [`QUERY_RESULT_RELATIONSHIPS_DELETED`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#QUERY_RESULT_RELATIONSHIPS_DELETED) | Query executed number of relationships deleted. |  | Long |
| **CamelNeo4jQueryResultRetrieveSize** (producer) Constant: [`QUERY_RETRIEVE_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#QUERY_RETRIEVE_SIZE) | Number of nodes retrieved. |  | Long |
| **CamelNeo4jQueryResultListNeo4jNodes** (producer) Constant: [`QUERY_RETRIEVE_LIST_NEO4J_NODES`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#QUERY_RETRIEVE_LIST_NEO4J_NODES) | Query execution time in Milliseconds. |  | Long |
| **CamelNeo4jVectorEmbeddingId** (producer) Constant: [`VECTOR_ID`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#VECTOR_ID) | Vector Id for the embedding. |  | String |
| **CamelNeo4jLabel** (producer) Constant: [`LABEL`](https://javadoc.io/doc/org.apache.camel/camel-neo4j/latest/org/apache/camel/component/neo4j/Neo4jConstants$Headers.html#LABEL) | Label for the Node - used when inserting from Embeddings. |  | String |

## Spring Boot Auto-Configuration

When using neo4j with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-neo4j-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 20 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.neo4j.alias** | Node alias. |  | String |
| **camel.component.neo4j.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.neo4j.configuration** | The configuration;. The option is a org.apache.camel.component.neo4j.Neo4jConfiguration type. |  | Neo4jConfiguration |
| **camel.component.neo4j.database-url** | Url for connecting to Neo database. |  | String |
| **camel.component.neo4j.detach-relationship** | Detach a relationship - set true if want to delete a node and detach its relationships to other nodes at same time. | false | Boolean |
| **camel.component.neo4j.dimension** | Dimension of Vector Index. |  | Integer |
| **camel.component.neo4j.driver** | Advanced - Driver. The option is a org.neo4j.driver.Driver type. |  | Driver |
| **camel.component.neo4j.enabled** | Whether to enable auto configuration of the neo4j component. This is enabled by default. |  | Boolean |
| **camel.component.neo4j.kerberos-auth-ticket** | Kerberos Authentication encoded base64 ticket. |  | String |
| **camel.component.neo4j.label** | Node Label. |  | String |
| **camel.component.neo4j.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.neo4j.max-results** | Maximum results for Vector Similarity search. | 3 | Integer |
| **camel.component.neo4j.min-score** | Minimum score for Vector Similarity search. |  | Double |
| **camel.component.neo4j.password** | Basic authentication database password. |  | String |
| **camel.component.neo4j.query** | Cypher Query. |  | String |
| **camel.component.neo4j.realm** | Basic authentication database realm. |  | String |
| **camel.component.neo4j.similarity-function** | Similarity Function of Vector Index. | cosine | Neo4jSimilarityFunction |
| **camel.component.neo4j.token** | Bearer authentication database realm. |  | String |
| **camel.component.neo4j.username** | Basic authentication database user. |  | String |
| **camel.component.neo4j.vector-index-name** | Vector Index Name. |  | String |

## Graph database usage - simple operations

### Create a Node

To create a node in a database named `test`, define the body as a string containing the JSON body. Use the operation `CREATE_NODE`. The URI endpoint should contain also specify the label and the alias.

Example:

```java
        var body = "{name: 'Alice', email: 'alice@example.com', age: 30}";

        Exchange result = fluentTemplate.to("neo4j:test?alias=u1&label=User")
                .withBodyAs(body, String.class)
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.CREATE_NODE)
                .request(Exchange.class);
```

### Create a Node with properties

To create a node in a database named `test` with properties, define the body as a Map containing the properties and values. Use the operation `CREATE_NODE`. The URI endpoint should contain also specify the label and the alias.

Example:

```java
        Map<String, Object> params = Map.of(
                "name", "Bob",
                "email", "bob@example.com",
                "age", 25);

        Exchange result = fluentTemplate.to("neo4j:test?alias=u2&label=User")
                .withBodyAs(params, Map.class)
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.CREATE_NODE)
                .request(Exchange.class);
```

### Retrieve Node

To retrieve a node in a database named `test`. Define the header `MATCH_PROPERTIES` as a string containing the match query. Use the operation `RETRIEVE_NODES`. The URI endpoint should also specify the label and the alias. The response is a List of Map<String, Object>. Each map represents the list of properties of a single node.

Example:

```java
        Exchange result = fluentTemplate.to("neo4j:test?alias=u&label=User")
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.RETRIEVE_NODES)
                .withHeader(Neo4j.Headers.MATCH_PROPERTIES, "{name: 'Alice'}")
                .request(Exchange.class);
```

To retrieve all nodes with label=`User`, use the same request without specifying any `MATCH_PROPERTIES`.

Example:

```java
        Exchange result = fluentTemplate.to("neo4j:test?alias=u&label=User")
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.RETRIEVE_NODES)
                .request(Exchange.class);
```

### Delete Node

To delete a node in a database named `test`. Define the header `MATCH_PROPERTIES` as a string containing the match query. Use the operation `DELETE_NODE`. The URI endpoint should also specify the label and the alias.

Example:

```java
        Exchange result = fluentTemplate.to("neo4j:test?alias=u&label=User")
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.DELETE_NODE)
                .withHeader(Neo4j.Headers.MATCH_PROPERTIES, "{name: 'Alice'}")
                .request(Exchange.class);
```

### Delete Node with relationships

If a node has relationships, it won’t be deleted unless we either delete the relationships or delete it with detached relationships. To delete a node with detached relationships, set the option `detachRelationship` to `true`.

Example:

```java
        Exchange result = fluentTemplate.to("neo4j:test?alias=u&label=User&detachRelationship=true")
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.DELETE_NODE)
                .withHeader(Neo4j.Headers.MATCH_PROPERTIES, "{name: 'Alice'}")
                .request(Exchange.class);
```

## Graph database usage - use Cypher Queries

### Create / Delete Nodes with a Cypher query

To create or delete nodes with a Cypher query in a database named `test`, set the Cypher query in the body. Use the operation `ADD_OR_DELETE_NODE_WITH_CYPHER_QUERY`. The operation can be used too to create multiple nodes and relationships between nodes.

Example creating a node:

```java
        var cypherQuery = "CREATE (u3:User {name: 'Charlie', email: 'charlie@example.com', age: 35})";
        Exchange result = fluentTemplate.to("neo4j:test")
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.ADD_OR_DELETE_NODE_WITH_CYPHER_QUERY)
                .withBodyAs(cypherQuery, String.class)
                .request(Exchange.class);
```

Example deleting a node:

```java
        var cypherQuery = "MATCH (u:User {name: 'Bob'}) DELETE u";
        Exchange result = fluentTemplate.to("neo4j:test")
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.ADD_OR_DELETE_NODE_WITH_CYPHER_QUERY)
                .withBodyAs(cypherQuery, String.class)
                .request(Exchange.class);
```

### Retrieve / Update nodes with a Cypher query

To retrieve or update nodes with Cypher Query in a database named `test`, set the Cypher query in the body. Use the operation `RETRIEVE_NODES_AND_UPDATE_WITH_CYPHER_QUERY`.

The operation is the same as `ADD_OR_DELETE_NODE_WITH_CYPHER_QUERY`, except that it returns a list of retrieved or updated nodes represented as `Map<String, Object>`.

Example updating a node:

```java
         var cypherQuery = "MATCH " +
                          "(u:User {name: 'Ethan'})" +
                          "SET u.age=41 " +
                          "RETURN u";

         Exchange result = fluentTemplate.to("neo4j:test")
                .withBodyAs(cypherQuery, String.class)
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.RETRIEVE_NODES_AND_UPDATE_WITH_CYPHER_QUERY)
                .request(Exchange.class);
```

## Vector database embeddings usage

### Create a vector index

To use Neo4j as a Vector database, we must create first a vector index for a label.

To create a vector index in a database named `test`, use the operation `CREATE_VECTOR_INDEX`. The URI endpoint should also specify the label, the alias, the vector index name and the dimension of embeddings.

Example:

```java
         Exchange result = fluentTemplate.to("neo4j:test?vectorIndexName=movieIdx&alias=m&label=Movie&dimension=2")
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.CREATE_VECTOR_INDEX)
                .request(Exchange.class);
```

### Drop a vector index

To drop a vector index in a database named `test`, use the operation `DROP_VECTOR_INDEX`. The URI endpoint should contain also specify the vector index name.

Example:

```java
         Exchange result = fluentTemplate.to("neo4j:test?vectorIndexName=movieIdx")
                .withHeader(Neo4j.Headers.OPERATION, Neo4Operation.DROP_VECTOR_INDEX)
                .request(Exchange.class);
```

### Create a vector

To create a vector in a database named `test`, use the operation `CREATE_VECTOR`. The URI endpoint should also specify the label, the alias and the vector index name. Put the vector array in the `CamelLangChain4jEmbeddingsVector` header, and the corresponding text in the body. The `id` can be generated by Camel Neo4j.

Camel Neo4j will create the node and store the vector as an `embedding` property, the text as `text` property and the ``id`as `id`` property.

Example:

```java
            Exchange result = fluentTemplate.to("neo4j:test?vectorIndexName=myIndex&label=Test&alias=t")
                .withHeader(Neo4jConstants.Headers.OPERATION, Neo4Operation.CREATE_VECTOR)
                .withHeader(Neo4jConstants.Headers.VECTOR_ID, "1")
                .withHeader("CamelLangChain4jEmbeddingsVector", new float[] { 10.8f, 10.6f })
                .withBody("Hello World!")
                .request(Exchange.class);
```

### Similarity search

To perform a similarity search using vectors in a database named `test`, use the operation `VECTOR_SIMILARITY_SEARCH`. The URI endpoint should also specify the label, the alias and the vector index name.

Example:

```java
         Exchange result = fluentTemplate.to("neo4j:test?vectorIndexName=myIndex&label=Test&alias=t")
                .withHeader(Neo4jConstants.Headers.OPERATION, Neo4Operation.VECTOR_SIMILARITY_SEARCH)
                .withBody(List.of(0.75f, 0.65f))
                .request(Exchange.class);
```

## Generate Embeddings with Langchain4j-embeddings

You can generate embeddings with an Embedding Models using the camel Lancghain4j Embeddings components. Camel Neo4j introduces a DataType `neo4j:embeddings` that automates the transformations of the Lancghain4j embeddings to Neo4j vectors.

Example of a camel Route that create embeddings with Camel Langchain4j Embeddings, and ingest them into Neo4j database.

```java
         from("direct:in")
            .to("langchain4j-embeddings:test")
            .setHeader(Neo4j.Headers.OPERATION).constant(Neo4Operation.CREATE_VECTOR)
            .setHeader(Neo4j.Headers.LABEL).constant("Test")
            .transform(new DataType("neo4j:embeddings"))
            .to("neo4j:neo4j?vectorIndexName=myIndex&label=Test");
```

## Similarity Search for LangChain4j RAG

You can enhance the Camel LangChain4j chat RAG experience by integrating Neo4j similarity search with Camel Neo4j DataTypes.

To achieve this, use the `neo4j:embeddings` DataType to generate embeddings from the prompt. These embeddings will then be utilized for the similarity search operation.

Next, use the `neo4j:rag` DataType to convert the retrieved embeddings into a List<String> for RAG. This list can be directly used with the `LangChain4jRagAggregatorStrategy` from the LangChain4j chat component.

> **Note**
> The retrieved embeddings must be ingested in Neo4j as LangChain4j embeddings.

Example of a camel Route that performs a similarity search in the Vector index, using a string and returning a list of strings

```java
         from("direct:search")
                        .to("langchain4j-embeddings:test")
                        // transform prompt into embeddings for search
                        .transform(
                                new DataType("neo4j:embeddings"))
                        .setHeader(Neo4jConstants.Headers.OPERATION, constant(Neo4Operation.VECTOR_SIMILARITY_SEARCH))
                        .to("neo4j:neo4j?vectorIndexName=myIndex&label=Test")
                        // decode retrieved embeddings for RAG
                        .transform(
                                new DataType("neo4j:rag"));
```