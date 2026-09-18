# LangChain4j Embedding Store

**Since Camel 4.14**

**Only producer is supported**

The LangChain4j Embedding Store component provides integration with [LangChain4j](https://github.com/langchain4j/langchain4j) embedding stores for vector database operations. This component enables storing, retrieving, and searching embeddings across multiple vector database implementations through LangChain4j’s unified interface.

## Features

The LangChain4j Embedding Store component offers the following key features:

-   **Vector Operations**: Add, remove, and search embeddings in vector databases
    
-   **Similarity Search**: Perform semantic search with configurable scoring thresholds
    
-   **Metadata Filtering**: Search with metadata-based constraints using filters
    
-   **Multi-Database Support**: Support for various vector databases including Qdrant, Milvus, Weaviate, Neo4j, and others
    
-   **Flexible Configuration**: Configure embedding stores via direct instances or factory patterns
    

## Supported Operations

The component supports three main operations controlled by the `CamelLangchain4jEmbeddingStoreAction` header:

-   **ADD** - Store embeddings with optional text segments and metadata
    
-   **REMOVE** - Delete embeddings by their unique identifier
    
-   **SEARCH** - Perform similarity search with configurable filters and scoring
    

## URI format

```none
langchain4j-embeddingstore:embeddingStoreId[?options]
```

Where **embeddingStoreId** is a unique identifier for the embedding store instance.

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

The LangChain4j Embedding Store component supports 9 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
The operation to perform: ADD, REMOVE, or SEARCH.

Enum values:

-   ADD
    
-   REMOVE
    
-   SEARCH
    





 |  | LangChain4jEmbeddingStoreAction |
| **configuration** (producer) | The configuration;. |  | LangChain4jEmbeddingStoreConfiguration |
| **embeddingStore** (producer) | **Autowired** Direct embedding store instance for vector operations. |  | EmbeddingStore |
| **embeddingStoreFactory** (producer) | **Autowired** The embedding store factory to use for creating embedding stores if no embeddingstore is provided. |  | EmbeddingStoreFactory |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxResults** (producer) | Maximum number of results to return for SEARCH operation. | 5 | Integer |
| **minScore** (producer) | Minimum similarity score threshold for SEARCH operation (0.0 to 1.0). |  | Double |
| **returnTextContent** (producer) | When true, SEARCH returns List with text content instead of List. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The LangChain4j Embedding Store endpoint is configured using URI syntax:

langchain4j-embeddingstore:embeddingStoreId

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **embeddingStoreId** (producer) | **Required** The id of the embedding store. |  | String |

### Query Parameters (7 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **action** (producer) | 
The operation to perform: ADD, REMOVE, or SEARCH.

Enum values:

-   ADD
    
-   REMOVE
    
-   SEARCH
    





 |  | LangChain4jEmbeddingStoreAction |
| **embeddingStore** (producer) | **Autowired** Direct embedding store instance for vector operations. |  | EmbeddingStore |
| **embeddingStoreFactory** (producer) | **Autowired** The embedding store factory to use for creating embedding stores if no embeddingstore is provided. |  | EmbeddingStoreFactory |
| **maxResults** (producer) | Maximum number of results to return for SEARCH operation. | 5 | Integer |
| **minScore** (producer) | Minimum similarity score threshold for SEARCH operation (0.0 to 1.0). |  | Double |
| **returnTextContent** (producer) | When true, SEARCH returns List with text content instead of List. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The LangChain4j Embedding Store component supports 4 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelLangchain4jEmbeddingStoreAction** (producer) Constant: [`ACTION`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddingstore/latest/org/apache/camel/component/langchain4j/embeddingstore/LangChain4jEmbeddingStoreHeaders.html#ACTION) | 
The action to be performed.

Enum values:

-   ADD
    
-   REMOVE
    
-   SEARCH
    





 |  | String |
| **CamelLangchain4jEmbeddingStoreMaxResults** (producer) Constant: [`MAX_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddingstore/latest/org/apache/camel/component/langchain4j/embeddingstore/LangChain4jEmbeddingStoreHeaders.html#MAX_RESULTS) | Maximum number of search results to return. | 5 | Integer |
| **CamelLangchain4jEmbeddingStoreMinScore** (producer) Constant: [`MIN_SCORE`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddingstore/latest/org/apache/camel/component/langchain4j/embeddingstore/LangChain4jEmbeddingStoreHeaders.html#MIN_SCORE) | Minimum similarity score for search results. |  | Double |
| **CamelLangchain4jEmbeddingStoreFilter** (producer) Constant: [`FILTER`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddingstore/latest/org/apache/camel/component/langchain4j/embeddingstore/LangChain4jEmbeddingStoreHeaders.html#FILTER) | Search filter for metadata-based constraints. |  | Filter |

## Spring Boot Auto-Configuration

When using langchain4j-embeddingstore with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-langchain4j-embeddingstore-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 10 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.langchain4j-embeddingstore.action** | The operation to perform: ADD, REMOVE, or SEARCH. |  | LangChain4jEmbeddingStoreAction |
| **camel.component.langchain4j-embeddingstore.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.langchain4j-embeddingstore.configuration** | The configuration;. The option is a org.apache.camel.component.langchain4j.embeddingstore.LangChain4jEmbeddingStoreConfiguration type. |  | LangChain4jEmbeddingStoreConfiguration |
| **camel.component.langchain4j-embeddingstore.embedding-store** | Direct embedding store instance for vector operations. The option is a dev.langchain4j.store.embedding.EmbeddingStore<dev.langchain4j.data.segment.TextSegment> type. |  | EmbeddingStore |
| **camel.component.langchain4j-embeddingstore.embedding-store-factory** | The embedding store factory to use for creating embedding stores if no embeddingstore is provided. The option is a org.apache.camel.component.langchain4j.embeddingstore.EmbeddingStoreFactory type. |  | EmbeddingStoreFactory |
| **camel.component.langchain4j-embeddingstore.enabled** | Whether to enable auto configuration of the langchain4j-embeddingstore component. This is enabled by default. |  | Boolean |
| **camel.component.langchain4j-embeddingstore.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.langchain4j-embeddingstore.max-results** | Maximum number of results to return for SEARCH operation. | 5 | Integer |
| **camel.component.langchain4j-embeddingstore.min-score** | Minimum similarity score threshold for SEARCH operation (0.0 to 1.0). |  | Double |
| **camel.component.langchain4j-embeddingstore.return-text-content** | When true, SEARCH returns List with text content instead of List. | false | Boolean |

## Usage

### Configuring an Embedding Store

The component requires an `EmbeddingStore` instance. Register it in the Camel registry:

```java
EmbeddingStore<TextSegment> embeddingStore = PgVectorEmbeddingStore.builder()
    .host("localhost")
    .port(5432)
    .database("vectordb")
    .user("postgres")
    .password("postgres")
    .table("embeddings")
    .dimension(384)
    .build();

context.getRegistry().bind("myEmbeddingStore", embeddingStore);
```

### Storing Embeddings (ADD Operation)

Store embeddings with optional text segments:

-   Java
    
-   YAML
    

```java
from("direct:store")
    .to("langchain4j-embeddings:embed")
    .to("langchain4j-embeddingstore:myStore?action=ADD");
```

```yaml
- route:
    from:
      uri: "direct:store"
    steps:
      - to: "langchain4j-embeddings:embed"
      - to: "langchain4j-embeddingstore:myStore?action=ADD"
```

The response body contains the generated embedding ID.

### Searching Embeddings (SEARCH Operation)

Perform similarity search to find relevant content:

-   Java
    
-   YAML
    

```java
from("direct:search")
    .to("langchain4j-embeddings:embed")
    .to("langchain4j-embeddingstore:myStore?action=SEARCH&maxResults=5&minScore=0.7");
```

```yaml
- route:
    from:
      uri: "direct:search"
    steps:
      - to: "langchain4j-embeddings:embed"
      - to: "langchain4j-embeddingstore:myStore?action=SEARCH&maxResults=5&minScore=0.7"
```

The response contains a list of `EmbeddingMatch` objects with the matching text segments and scores.

#### Returning Text Content Directly

Use the `returnTextContent` option to get a list of strings instead of `EmbeddingMatch` objects:

-   Java
    
-   YAML
    

```java
from("direct:search")
    .to("langchain4j-embeddings:embed")
    .to("langchain4j-embeddingstore:myStore?action=SEARCH&maxResults=5&returnTextContent=true")
    .log("Found texts: ${body}");
```

```yaml
- route:
    from:
      uri: "direct:search"
    steps:
      - to: "langchain4j-embeddings:embed"
      - to: "langchain4j-embeddingstore:myStore?action=SEARCH&maxResults=5&returnTextContent=true"
      - log: "Found texts: ${body}"
```

### Removing Embeddings (REMOVE Operation)

Delete embeddings by their ID:

-   Java
    
-   YAML
    

```java
from("direct:remove")
    .setBody(simple("${header.embeddingId}"))
    .to("langchain4j-embeddingstore:myStore?action=REMOVE");
```

```yaml
- route:
    from:
      uri: "direct:remove"
    steps:
      - setBody:
          simple: "${header.embeddingId}"
      - to: "langchain4j-embeddingstore:myStore?action=REMOVE"
```

### Complete RAG Pipeline Example

A complete example showing document ingestion and retrieval:

```java
// Ingestion route: chunk, embed, and store documents
from("file:documents?include=.*\\.txt")
    .split().tokenize("\n\n") // Split by paragraphs
    .to("langchain4j-embeddings:embed")
    .to("langchain4j-embeddingstore:ragStore?action=ADD")
    .log("Stored embedding with ID: ${body}");

// Query route: embed query, search, and return text results
from("direct:query")
    .to("langchain4j-embeddings:embed")
    .to("langchain4j-embeddingstore:ragStore?action=SEARCH&maxResults=3&returnTextContent=true");
```

### Supported Vector Databases

The component supports any vector database that LangChain4j provides an `EmbeddingStore` implementation for:

-   **PGVector** - PostgreSQL with pgvector extension
    
-   **Qdrant** - High-performance vector database
    
-   **Milvus** - Cloud-native vector database
    
-   **Weaviate** - Vector search engine
    
-   **Chroma** - Open-source embedding database
    
-   **Pinecone** - Managed vector database
    
-   **Neo4j** - Graph database with vector capabilities
    
-   **InMemoryEmbeddingStore** - For testing purposes
    

Refer to the [LangChain4j Embedding Stores documentation](https://docs.langchain4j.dev/integrations/embedding-stores/) for the complete list and configuration options.