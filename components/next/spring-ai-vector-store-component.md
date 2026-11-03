# Spring AI Vector Store

**Since Camel 4.17**

**Only producer is supported**

The Spring AI Vector Store component provides support for storing and retrieving documents in vector databases using [Spring AI](https://docs.spring.io/spring-ai/reference/api/vectordbs.md) vector store capabilities.

Vector stores enable:

-   Storage of documents with embeddings
    
-   Similarity search based on vector distance
    
-   Metadata-based filtering
    
-   Document management (add, delete)
    

## URI format

spring-ai-vector-store:storeId\[?options\]

Where **storeId** can be any string to uniquely identify the endpoint

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

The Spring AI Vector Store component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration. |  | SpringAiVectorStoreConfiguration |
| **filterExpression** (producer) | Filter expression for metadata-based filtering in searches. |  | String |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **operation** (producer) | 
The operation to perform on the vector store (ADD, DELETE, SIMILARITY\_SEARCH).

Enum values:

-   ADD
    
-   DELETE
    
-   SIMILARITY\_SEARCH
    





 | ADD | SpringAiVectorStoreOperation |
| **similarityThreshold** (producer) | The minimum similarity score threshold (0-1) for similarity search. | 0 | double |
| **topK** (producer) | The maximum number of similar documents to return for similarity search. | 5 | int |
| **vectorStore** (producer) | **Autowired** **Required** The VectorStore to use for vector operations. |  | VectorStore |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Spring AI Vector Store endpoint is configured using URI syntax:

spring-ai-vector-store:storeId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **storeId** (producer) | **Required** The id. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **filterExpression** (producer) | Filter expression for metadata-based filtering in searches. |  | String |
| **operation** (producer) | 
The operation to perform on the vector store (ADD, DELETE, SIMILARITY\_SEARCH).

Enum values:

-   ADD
    
-   DELETE
    
-   SIMILARITY\_SEARCH
    





 | ADD | SpringAiVectorStoreOperation |
| **similarityThreshold** (producer) | The minimum similarity score threshold (0-1) for similarity search. | 0 | double |
| **topK** (producer) | The maximum number of similar documents to return for similarity search. | 5 | int |
| **vectorStore** (producer) | **Autowired** **Required** The VectorStore to use for vector operations. |  | VectorStore |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Spring AI Vector Store component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSpringAiVectorStoreOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-vector-store/latest/org/apache/camel/component/springai/vectorstore/SpringAiVectorStoreHeaders.html#OPERATION) | 
The operation to perform (ADD, DELETE, SIMILARITY\_SEARCH).

Enum values:

-   ADD
    
-   DELETE
    
-   SIMILARITY\_SEARCH
    





 |  | SpringAiVectorStoreOperation |
| **CamelSpringAiVectorStoreTopK** (producer) Constant: [`TOP_K`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-vector-store/latest/org/apache/camel/component/springai/vectorstore/SpringAiVectorStoreHeaders.html#TOP_K) | The maximum number of similar documents to return (topK). |  | Integer |
| **CamelSpringAiVectorStoreSimilarityThreshold** (producer) Constant: [`SIMILARITY_THRESHOLD`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-vector-store/latest/org/apache/camel/component/springai/vectorstore/SpringAiVectorStoreHeaders.html#SIMILARITY_THRESHOLD) | The similarity threshold (0-1). |  | Double |
| **CamelSpringAiVectorStoreFilterExpression** (producer) Constant: [`FILTER_EXPRESSION`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-vector-store/latest/org/apache/camel/component/springai/vectorstore/SpringAiVectorStoreHeaders.html#FILTER_EXPRESSION) | Filter expression for metadata-based filtering. |  | String |
| **CamelSpringAiVectorStoreDocumentIds** (producer) Constant: [`DOCUMENT_IDS`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-vector-store/latest/org/apache/camel/component/springai/vectorstore/SpringAiVectorStoreHeaders.html#DOCUMENT_IDS) | List of document IDs (output of ADD and SIMILARITY\_SEARCH, and input of DELETE when the message has no body). |  | List |
| **CamelSpringAiVectorStoreSimilarDocuments** (producer) Constant: [`SIMILAR_DOCUMENTS`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-vector-store/latest/org/apache/camel/component/springai/vectorstore/SpringAiVectorStoreHeaders.html#SIMILAR_DOCUMENTS) | List of similar documents found. |  | List |
| **CamelSpringAiVectorStoreDocumentsAdded** (producer) Constant: [`DOCUMENTS_ADDED`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-vector-store/latest/org/apache/camel/component/springai/vectorstore/SpringAiVectorStoreHeaders.html#DOCUMENTS_ADDED) | Number of documents added. |  | Integer |
| **CamelSpringAiVectorStoreDocumentsDeleted** (producer) Constant: [`DOCUMENTS_DELETED`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-vector-store/latest/org/apache/camel/component/springai/vectorstore/SpringAiVectorStoreHeaders.html#DOCUMENTS_DELETED) | Number of document IDs that DELETE gave to the vector store, as the vector store does not tell how many of them existed. |  | Integer |

## Message Body

The message body at each side of the Spring AI Vector Store component: _Consumer_ is the body of the messages the consumer creates, _Consumer reply_ the bodies a consumer that answers its caller can reply with, _Producer input_ the bodies the producer can send or write, and _Producer output_ the body after the producer.

  
| Side | Body | Description |
| --- | --- | --- |
| **Producer input** | `any` | 
ADD takes a Document, a List of Document or of texts, or text (another body is added as its text); a List with another element fails. After spring-ai-embeddings it adds the float\[\] (or List of float\[\]) body with the text of the CamelSpringAiEmbeddingInputText(s) header, and a vector without its text fails. DELETE takes the id, a Document, or a List of ids or Documents (such as the result of SIMILARITY\_SEARCH); the CamelSpringAiVectorStoreDocumentIds header is used only without a body. SIMILARITY\_SEARCH takes the query text, or after spring-ai-embeddings the float\[\] body with the CamelSpringAiEmbeddingInputText header. Otherwise no body fails. The CamelSpringAiVectorStoreOperation header overrides operation.

-   With `operation=DELETE`: `text`, `list`, `pojo` or `null`
    
-   With `operation=SIMILARITY_SEARCH`: `text` or `list`
    





 |
| **Producer output** | `unchanged` | 

SIMILARITY\_SEARCH gives the List of Document found. ADD and DELETE keep the body, with the ids and the count in headers.

-   With `operation=SIMILARITY_SEARCH`: `list`
    





 |

The bodies are the ones with the default options. A side that is not listed is not known, and tooling does not guess it. The carriers, the sides and the tools that use them are described in [Message Body Types](../../manual/body-types.md).

## Operations

The component supports three main operations:

### ADD Operation

Stores documents in the vector store. Can accept:

-   String text (embeddings will be generated automatically)
    
-   Document objects
    
-   List of Documents or of String texts (an element of another type fails)
    
-   Output from the spring-ai-embeddings component (semi-automatic integration, this depends on the underlying Spring AI Vectore Store implementation): a `float[]` body with the `CamelSpringAiEmbeddingInputText` header, or a List of `float[]` body with the `CamelSpringAiEmbeddingInputTexts` header with one text per vector. A vector without its text fails.
    

The `CamelSpringAiEmbeddingInputText(s)` headers are only used together with a vector body, so a header left over from an earlier spring-ai-embeddings call does not replace a Document or text body.

After documents are added, the component sets the `CamelSpringAiVectorStoreDocumentIds` header containing a list of the IDs of the added documents. This allows you to reference or track the stored documents in subsequent processing steps.

> **Note**
> **Best Practice:** Use the ADD operation directly with the vector store component when working with text. The component will automatically handle embedding generation internally if the vector store is configured with an embedding model. This is the recommended approach as it simplifies your routes and reduces the number of steps.

### DELETE Operation

Removes documents from the vector store by their IDs. The body has the documents to delete: an ID, a Document, or a List of IDs or of Documents (such as the result of SIMILARITY\_SEARCH). Only when there is no body, the IDs are taken from the `CamelSpringAiVectorStoreDocumentIds` header. The body comes first because ADD and SIMILARITY\_SEARCH set this header to their own output IDs.

The `CamelSpringAiVectorStoreDocumentsDeleted` header is the number of IDs given to the vector store. The Spring AI `VectorStore` API does not tell how many of them existed, so IDs that are not in the store are counted too.

### SIMILARITY\_SEARCH Operation

Searches for documents similar to a query text. After the spring-ai-embeddings component, where the body is the `float[]` vector of the text, the query is the text in the `CamelSpringAiEmbeddingInputText` header (the vector store embeds the query itself).

The component returns matching documents in the message body and sets the following headers:

-   `CamelSpringAiVectorStoreSimilarDocuments` - List of Document objects found
    
-   `CamelSpringAiVectorStoreDocumentIds` - List of IDs of the found documents
    

## Usage Examples

### Add Documents from Text (Recommended)

This is the **recommended best practice** for adding documents. The vector store component handles embedding generation internally:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:store")
    .to("spring-ai-vector-store:myStore?operation=ADD&vectorStore=#vectorStore");
```

```xml
<route>
  <from uri="direct:store"/>
  <to uri="spring-ai-vector-store:myStore?operation=ADD&amp;vectorStore=#vectorStore"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:store
      steps:
        - to:
            uri: spring-ai-vector-store:myStore
            parameters:
              operation: ADD
              vectorStore: "#vectorStore"
```

When you send plain text to this route, the component automatically: 1. Generates embeddings using the embedding model configured in the vector store 2. Creates a Document object 3. Stores it in the vector store

This single-step approach is simpler and more efficient than manually chaining the embeddings component.

### Add from Embeddings Component (Alternative)

If you need explicit control over the embedding process or want to manipulate embeddings before storing, you can chain the components:

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:embedAndStore")
    .to("spring-ai-embeddings:test?embeddingModel=#embeddingModel")
    .to("spring-ai-vector-store:test?vectorStore=#vectorStore");
```

```xml
<route>
  <from uri="direct:embedAndStore"/>
  <to uri="spring-ai-embeddings:test?embeddingModel=#embeddingModel"/>
  <to uri="spring-ai-vector-store:test?vectorStore=#vectorStore"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:embedAndStore
      steps:
        - to:
            uri: spring-ai-embeddings:test
            parameters:
              embeddingModel: "#embeddingModel"
        - to:
            uri: spring-ai-vector-store:test
            parameters:
              vectorStore: "#vectorStore"
```

> **Note**
> This approach is only necessary when you need to access or modify the embeddings between generation and storage. For most use cases, the direct ADD operation (shown above) is preferred.

### Similarity Search

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:search")
    .setBody(constant("What is AI?"))
    .to("spring-ai-vector-store:myStore?operation=SIMILARITY_SEARCH&topK=5&similarityThreshold=0.7")
    .log("Found ${header.CamelSpringAiVectorStoreSimilarDocuments.size()} similar documents")
    .log("Document IDs: ${header.CamelSpringAiVectorStoreDocumentIds}");
```

```xml
<route>
  <from uri="direct:search"/>
  <setBody><constant>What is AI?</constant></setBody>
  <to uri="spring-ai-vector-store:myStore?operation=SIMILARITY_SEARCH&amp;topK=5&amp;similarityThreshold=0.7"/>
  <log message="Found ${header.CamelSpringAiVectorStoreSimilarDocuments.size()} similar documents"/>
  <log message="Document IDs: ${header.CamelSpringAiVectorStoreDocumentIds}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:search
      steps:
        - setBody:
            constant: "What is AI?"
        - to:
            uri: spring-ai-vector-store:myStore
            parameters:
              operation: SIMILARITY_SEARCH
              topK: 5
              similarityThreshold: 0.7
        - log:
            message: "Found ${header.CamelSpringAiVectorStoreSimilarDocuments.size()} similar documents"
        - log:
            message: "Document IDs: ${header.CamelSpringAiVectorStoreDocumentIds}"
```

### Delete Documents

Delete documents by specifying their IDs in the body:

_Java-only: Arrays.asList()_

```java
from("direct:delete")
    .setBody(constant(Arrays.asList("doc1", "doc2")))
    .to("spring-ai-vector-store:myStore?operation=DELETE");
```

You can also chain operations to search for documents and then delete the documents found:

_Java-only: Java constants and enum values_

```java
from("direct:searchAndDelete")
    .setBody(constant("outdated content"))
    .to("spring-ai-vector-store:myStore?operation=SIMILARITY_SEARCH&topK=10")
    .log("Found ${header.CamelSpringAiVectorStoreDocumentIds.size()} documents to delete")
    // DELETE deletes the List of Document that SIMILARITY_SEARCH gives in the body
    .setHeader(SpringAiVectorStoreHeaders.OPERATION, constant(SpringAiVectorStoreOperation.DELETE))
    .to("spring-ai-vector-store:myStore");
```

### Dynamic Operation

_Java-only: Java constants and enum values_

```java
from("direct:dynamic")
    .setHeader(SpringAiVectorStoreHeaders.OPERATION, constant(SpringAiVectorStoreOperation.ADD))
    .to("spring-ai-vector-store:myStore");
```

## Configuration

### Configuring the Vector Store

To use the ADD operation with automatic embedding generation (recommended), configure your vector store with an embedding model:

_Java-only: Java Spring AI SDK configuration_

```java
// Create a Qdrant Client
QdrantClient qdrantClient
                = new QdrantClient(QdrantGrpcClient.newBuilder(QDRANT.getGrpcHost(), QDRANT.getGrpcPort(), false).build());

// Create an embedding model
EmbeddingModel embeddingModel = new OllamaEmbeddingModel(ollamaApi, options);

// Create a vector store with the embedding model
// Example with Qdrant
VectorStore vectorStore = QdrantVectorStore.builder(qdrantClient, embeddingModel)
    .collectionName("my_collection")
    .initializeSchema(true)
    .build();

// Or with Simple Vector Store
VectorStore vectorStore = new SimpleVectorStore(embeddingModel);

// Register in Camel context
context.getRegistry().bind("vectorStore", vectorStore);

// Use in route - the component will use the configured embedding model
from("direct:start")
    .to("spring-ai-vector-store:test?vectorStore=#vectorStore&operation=ADD");
```

> **Important**
> Make sure your vector store is configured with an embedding model to enable automatic embedding generation when using the ADD operation with text input.

### Search Parameters

-   `topK` - Maximum number of results (default: 5)
    
-   `similarityThreshold` - Minimum similarity score 0-1 (default: 0.0)
    
-   `filterExpression` - Metadata-based filter expression