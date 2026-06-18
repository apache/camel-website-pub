# PGVector

**Since Camel 4.19**

**Only producer is supported**

The PGVector Component provides support for interacting with [pgvector](https://github.com/pgvector/pgvector), the open-source vector similarity search extension for PostgreSQL.

## URI format

pgvector:collection\[?options\]

Where **collection** represents the table name used to store vectors in the PostgreSQL database.

## Configuring the DataSource

A `javax.sql.DataSource` must be provided. It is recommended to use a connection pooling DataSource (such as HikariCP) for production deployments. The DataSource can be set on the component or endpoint configuration, or autowired from the registry.

## Actions

The following actions are supported via the `CamelPgVectorAction` header:

-   `CREATE_TABLE` - Creates the pgvector extension and a table with columns: id, text\_content, metadata, embedding
    
-   `CREATE_INDEX` - Creates an HNSW index on the embedding column for faster approximate nearest neighbor search. The index uses the distance type configured on the endpoint (default: COSINE)
    
-   `DROP_TABLE` - Drops the table
    
-   `UPSERT` - Inserts or updates a vector record. The body must be a `List<Float>`. Set `CamelPgVectorRecordId` for the ID (auto-generated UUID if not set), `CamelPgVectorTextContent` for text, and `CamelPgVectorMetadata` for metadata
    
-   `DELETE` - Deletes a record by `CamelPgVectorRecordId`
    
-   `SIMILARITY_SEARCH` - Searches for similar vectors. The body must be a `List<Float>` query vector. Set `CamelPgVectorQueryTopK` for max results (default 3). Optionally set `CamelPgVectorFilter` with a SQL WHERE clause to filter results (e.g., `text_content LIKE '%hello%'`). Returns a `List<Map<String, Object>>` with keys: id, text\_content, metadata, distance
    

## Defaults

-   **dimension**: `384` (matches common embedding models like `all-MiniLM-L6-v2`)
    
-   **distanceType**: `COSINE` (other options: `EUCLIDEAN`, `INNER_PRODUCT`)
    

## Parameterized Filters

When using the `SIMILARITY_SEARCH` action, you can filter results using a SQL WHERE clause via the `CamelPgVectorFilter` header. For safe handling of dynamic values, use parameterized queries with `?` placeholders and provide values via the `CamelPgVectorFilterParams` header:

_Java-only: setting parameterized filter headers programmatically_

```java
from("direct:search")
    .setHeader(PgVectorHeaders.ACTION).constant(PgVectorAction.SIMILARITY_SEARCH)
    .setHeader(PgVectorHeaders.FILTER).constant("text_content LIKE ? AND metadata::jsonb->>'category' = ?")
    .setHeader(PgVectorHeaders.FILTER_PARAMS).constant(List.of("%hello%", "science"))
    .to("pgvector:documents");
```

## Security

The `CamelPgVectorFilter` header value is appended directly as a SQL WHERE clause. When using static, developer-controlled filter expressions this is safe. However, **never pass untrusted user input directly as the filter value** without using parameterized queries (`?` placeholders with `CamelPgVectorFilterParams`), as this could lead to SQL injection.

## OpenAI Integration

The component works directly with the [OpenAI](openai-component.md) component for embedding generation. The OpenAI embeddings endpoint returns a `List<Float>`, which is exactly the body format expected by the pgvector UPSERT and SIMILARITY\_SEARCH actions.

-   Java
    
-   YAML
    

```java
// Index a document
from("direct:index")
    .setVariable("text", body())
    .to("openai:embeddings?embeddingModel=nomic-embed-text")
    .setHeader(PgVectorHeaders.ACTION).constant(PgVectorAction.UPSERT)
    .setHeader(PgVectorHeaders.TEXT_CONTENT).variable("text")
    .to("pgvector:documents");

// Similarity search
from("direct:search")
    .to("openai:embeddings?embeddingModel=nomic-embed-text")
    .setHeader(PgVectorHeaders.ACTION).constant(PgVectorAction.SIMILARITY_SEARCH)
    .setHeader(PgVectorHeaders.QUERY_TOP_K).constant(5)
    .to("pgvector:documents");
```

```yaml
- route:
    from:
      uri: direct:index
    steps:
      - setVariable:
          name: text
          expression:
            simple:
              expression: "${body}"
      - to:
          uri: openai:embeddings
          parameters:
            embeddingModel: nomic-embed-text
      - setHeader:
          name: CamelPgVectorAction
          constant: UPSERT
      - setHeader:
          name: CamelPgVectorTextContent
          expression:
            simple:
              expression: "${variable.text}"
      - to:
          uri: pgvector:documents

- route:
    from:
      uri: direct:search
    steps:
      - to:
          uri: openai:embeddings
          parameters:
            embeddingModel: nomic-embed-text
      - setHeader:
          name: CamelPgVectorAction
          constant: SIMILARITY_SEARCH
      - setHeader:
          name: CamelPgVectorQueryTopK
          constant: 5
      - to:
          uri: pgvector:documents
```

## LangChain4j Integration

This component provides data type transformers for [LangChain4j Embeddings](langchain4j-embeddings-component.md) integration:

-   `pgvector:embeddings` - Transforms LangChain4j embedding output into a format suitable for the PGVector UPSERT action
    
-   `pgvector:rag` - Transforms similarity search results into a `List<String>` for RAG pipelines
    

-   Java
    
-   YAML
    

```java
// Store embeddings
from("direct:store")
    .to("langchain4j-embeddings:embed")
    .setHeader(PgVectorHeaders.ACTION).constant(PgVectorAction.UPSERT)
    .transformDataType(new DataType("pgvector:embeddings"))
    .to("pgvector:myCollection");

// Similarity search for RAG
from("direct:search")
    .to("langchain4j-embeddings:embed")
    .transformDataType(new DataType("pgvector:embeddings"))
    .setHeader(PgVectorHeaders.ACTION, constant(PgVectorAction.SIMILARITY_SEARCH))
    .to("pgvector:myCollection")
    .transformDataType(new DataType("pgvector:rag"));
```

```yaml
- route:
    from:
      uri: direct:store
    steps:
      - to:
          uri: langchain4j-embeddings:embed
      - setHeader:
          name: CamelPgVectorAction
          constant: UPSERT
      - transform:
          dataType: "pgvector:embeddings"
      - to:
          uri: pgvector:myCollection

- route:
    from:
      uri: direct:search
    steps:
      - to:
          uri: langchain4j-embeddings:embed
      - transform:
          dataType: "pgvector:embeddings"
      - setHeader:
          name: CamelPgVectorAction
          constant: SIMILARITY_SEARCH
      - to:
          uri: pgvector:myCollection
      - transform:
          dataType: "pgvector:rag"
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

The PGVector component supports 6 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration;. |  | PgVectorConfiguration |
| **dataSource** (producer) | **Autowired** The DataSource to use for connecting to the PostgreSQL database with pgvector extension. |  | DataSource |
| **dimension** (producer) | The dimension of the vectors to store. | 384 | int |
| **distanceType** (producer) | 
The distance type to use for similarity search.

Enum values:

-   COSINE
    
-   EUCLIDEAN
    
-   INNER\_PRODUCT
    





 | COSINE | PgVectorDistanceType |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The PGVector endpoint is configured using URI syntax:

pgvector:collection

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **collection** (producer) | **Required** The collection (table) name. |  | String |

### Query Parameters (4 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **dataSource** (producer) | **Autowired** The DataSource to use for connecting to the PostgreSQL database with pgvector extension. |  | DataSource |
| **dimension** (producer) | The dimension of the vectors to store. | 384 | int |
| **distanceType** (producer) | 
The distance type to use for similarity search.

Enum values:

-   COSINE
    
-   EUCLIDEAN
    
-   INNER\_PRODUCT
    





 | COSINE | PgVectorDistanceType |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The PGVector component supports 7 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelPgVectorAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-pgvector/latest/org/apache/camel/component/pgvector/PgVectorHeaders.html#ACTION) | 
The action to be performed.

Enum values:

-   CREATE\_TABLE
    
-   CREATE\_INDEX
    
-   DROP\_TABLE
    
-   UPSERT
    
-   DELETE
    
-   SIMILARITY\_SEARCH
    





 |  | String |
| **CamelPgVectorRecordId** (producer) Constant: [`RECORD_ID`](https://javadoc.io/doc/org.apache.camel/camel-pgvector/latest/org/apache/camel/component/pgvector/PgVectorHeaders.html#RECORD_ID) | The id of the vector record. |  | String |
| **CamelPgVectorQueryTopK** (producer) Constant: [`QUERY_TOP_K`](https://javadoc.io/doc/org.apache.camel/camel-pgvector/latest/org/apache/camel/component/pgvector/PgVectorHeaders.html#QUERY_TOP_K) | The maximum number of results to return for similarity search. | 3 | Integer |
| **CamelPgVectorTextContent** (producer) Constant: [`TEXT_CONTENT`](https://javadoc.io/doc/org.apache.camel/camel-pgvector/latest/org/apache/camel/component/pgvector/PgVectorHeaders.html#TEXT_CONTENT) | The text content to store alongside the vector embedding. |  | String |
| **CamelPgVectorMetadata** (producer) Constant: [`METADATA`](https://javadoc.io/doc/org.apache.camel/camel-pgvector/latest/org/apache/camel/component/pgvector/PgVectorHeaders.html#METADATA) | The metadata associated with the vector record, stored as JSON. |  | String |
| **CamelPgVectorFilter** (producer) Constant: [`FILTER`](https://javadoc.io/doc/org.apache.camel/camel-pgvector/latest/org/apache/camel/component/pgvector/PgVectorHeaders.html#FILTER) | Filter condition for similarity search. Applied as a SQL WHERE clause on the text\_content and metadata columns. Supports parameterized queries using placeholders with values provided via the CamelPgVectorFilterParams header. WARNING: When not using parameterized queries, the filter value is appended directly as SQL. Never use untrusted input as the filter value without parameterization, as this could lead to SQL injection. |  | String |
| **CamelPgVectorFilterParams** (producer) Constant: [`FILTER_PARAMS`](https://javadoc.io/doc/org.apache.camel/camel-pgvector/latest/org/apache/camel/component/pgvector/PgVectorHeaders.html#FILTER_PARAMS) | Parameter values for parameterized filter queries. Use with placeholders in the CamelPgVectorFilter header. Example: filter = 'text\_content LIKE AND metadata::jsonb-'category' = ' with filterParams = List.of(%hello%, science). |  | List |