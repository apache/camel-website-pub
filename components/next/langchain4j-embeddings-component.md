# LangChain4j Embeddings

**Since Camel 4.5**

**Only producer is supported**

The LangChain4j embeddings component provides support for compute embeddings using [LangChain4j](https://docs.langchain4j.dev/) embeddings.

## URI format

langchain4j-embeddings:embeddingId\[?options\]

Where **embeddingId** can be any string to uniquely identify the endpoint

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

The LangChain4j Embeddings component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration. |  | LangChain4jEmbeddingsConfiguration |
| **embeddingModel** (producer) | **Autowired** **Required** The EmbeddingModel engine to use. |  | EmbeddingModel |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The LangChain4j Embeddings endpoint is configured using URI syntax:

langchain4j-embeddings:embeddingId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **embeddingId** (producer) | **Required** The id. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **embeddingModel** (producer) | **Autowired** **Required** The EmbeddingModel engine to use. |  | EmbeddingModel |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The LangChain4j Embeddings component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelLangChain4jEmbeddingsFinishReason** (producer) Constant: [`FINISH_REASON`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#FINISH_REASON) | 
The Finish Reason.

Enum values:

-   STOP
    
-   LENGTH
    
-   TOOL\_EXECUTION
    
-   CONTENT\_FILTER
    
-   OTHER
    





 |  | FinishReason |
| **CamelLangChain4jEmbeddingsInputTokenCount** (producer) Constant: [`INPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#INPUT_TOKEN_COUNT) | The Input Token Count. |  | int |
| **CamelLangChain4jEmbeddingsOutputTokenCount** (producer) Constant: [`OUTPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#OUTPUT_TOKEN_COUNT) | The Output Token Count. |  | int |
| **CamelLangChain4jEmbeddingsTotalTokenCount** (producer) Constant: [`TOTAL_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#TOTAL_TOKEN_COUNT) | The Total Token Count. |  | int |
| **CamelLangChain4jEmbeddingsRequestModel** (producer) Constant: [`REQUEST_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#REQUEST_MODEL) | The request model name. |  | String |
| **CamelLangChain4jEmbeddingsResponseModel** (producer) Constant: [`RESPONSE_MODEL`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#RESPONSE_MODEL) | The response model name. |  | String |
| **CamelLangChain4jEmbeddingsEmbedding** (producer) Constant: [`EMBEDDING`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#EMBEDDING) | Embedding representation of a text. |  | Embedding |
| **CamelLangChain4jEmbeddingsEmbeddings** (producer) Constant: [`EMBEDDINGS`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#EMBEDDINGS) | List of embeddings from a batch embedAll operation. |  | List |
| **CamelLangChain4jEmbeddingsVector** (producer) Constant: [`VECTOR`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#VECTOR) | A dense vector embedding of a text. |  | float\[\] |
| **CamelLangChain4jEmbeddingsTextSegment** (producer) Constant: [`TEXT_SEGMENT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#TEXT_SEGMENT) | A TextSegment representation of the vector embedding input text. |  | TextSegment |
| **CamelLangChain4jEmbeddingsTextSegments** (producer) Constant: [`TEXT_SEGMENTS`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddingsHeaders.html#TEXT_SEGMENTS) | List of text segments from a batch embedAll operation. |  | List |

## Usage

### Using Embedding Models

The Camel LangChain4j embeddings component provides support for generating embeddings using various embedding models supported by [LangChain4j](https://docs.langchain4j.dev/).

#### Integrating with specific Embedding Model

##### Using LangChain4j Spring Boot Starters (Recommended for Spring Boot)

When using Camel with Spring Boot, you can leverage LangChain4j’s Spring Boot starters for automatic configuration of embedding models.

Add the dependency for LangChain4j OpenAI Spring Boot starter:

pom.xml

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-open-ai-spring-boot-starter</artifactId>
    <version>1.10.0</version>
    <!-- use the same version as your LangChain4j version -->
</dependency>
```

Configure the OpenAI Embedding Model in `application.properties` or `application.yml`:

application.properties

```properties
langchain4j.open-ai.embedding-model.api-key=${OPENAI_API_KEY}
langchain4j.open-ai.embedding-model.model-name=text-embedding-ada-002
```

application.yml

```yaml
langchain4j:
  open-ai:
    embedding-model:
      api-key: ${OPENAI_API_KEY}
      model-name: text-embedding-ada-002
```

The `EmbeddingModel` bean will be automatically configured and available in the Spring context. Use it in your Camel routes:

-   Java
    
-   YAML
    
-   XML
    

```java
from("direct:embeddings")
    .to("langchain4j-embeddings:test?embeddingModel=#embeddingModel");
```

```yaml
- route:
    from:
      uri: direct:embeddings
    steps:
      - to:
          uri: langchain4j-embeddings:test
          parameters:
            embeddingModel: "#embeddingModel"
```

```xml
<route>
  <from uri="direct:embeddings"/>
  <to uri="langchain4j-embeddings:test?embeddingModel=#embeddingModel"/>
</route>
```

> **Note**
> LangChain4j Spring Boot starters provide auto-configuration for various embedding model providers including:
>
> -   `langchain4j-open-ai-spring-boot-starter` - OpenAI embeddings
>     
> -   `langchain4j-azure-open-ai-spring-boot-starter` - Azure OpenAI embeddings
>     
> -   `langchain4j-ollama-spring-boot-starter` - Ollama embeddings
>     
> -   `langchain4j-hugging-face-spring-boot-starter` - Hugging Face embeddings
>     
> -   `langchain4j-vertex-ai-spring-boot-starter` - Google Vertex AI embeddings
>     
>
> For a complete list of available starters and their configuration options, refer to the [LangChain4j Spring Boot Integration documentation](https://docs.langchain4j.dev/tutorials/spring-boot-integration).

##### Manual Configuration (Alternative)

Alternatively, you can manually initialize the Embedding Model and add it to the Camel Registry:

Add the dependency for LangChain4j OpenAI support:

pom.xml

```xml
<dependency>
    <groupId>dev.langchain4j</groupId>
    <artifactId>langchain4j-open-ai</artifactId>
    <version>1.10.0</version>
    <!-- use the same version as your LangChain4j version -->
</dependency>
```

Initialize the OpenAI Embedding Model:

_Java-only: programmatic EmbeddingModel initialization and registry binding_

```java
EmbeddingModel embeddingModel = OpenAiEmbeddingModel.builder()
    .apiKey(openApiKey)
    .modelName("text-embedding-ada-002")
    .build();
context.getRegistry().bind("myEmbeddingModel", embeddingModel);
```

Use the model in the Camel LangChain4j Embeddings Producer:

-   Java
    
-   YAML
    

```java
from("direct:embeddings")
    .to("langchain4j-embeddings:test?embeddingModel=#myEmbeddingModel");
```

```yaml
- route:
    from:
      uri: direct:embeddings
    steps:
      - to:
          uri: langchain4j-embeddings:test
          parameters:
            embeddingModel: "#myEmbeddingModel"
```

### Integration with Vector Stores

The LangChain4j Embeddings component works seamlessly with vector databases for RAG (Retrieval-Augmented Generation) workflows.

#### Using with Qdrant

This example shows how to embed text and store it in Qdrant vector database:

-   Java
    
-   YAML
    

```java
from("direct:store")
    .to("langchain4j-embeddings:embed")
    .setHeader(QdrantHeaders.ACTION).constant(QdrantAction.UPSERT)
    .setHeader(QdrantHeaders.POINT_ID).constant(1)
    .transformDataType(new DataType("qdrant:embeddings"))
    .to("qdrant:myCollection");
```

```yaml
- route:
    from:
      uri: direct:store
    steps:
      - to:
          uri: langchain4j-embeddings:embed
      - setHeader:
          name: CamelQdrantAction
          constant: UPSERT
      - setHeader:
          name: CamelQdrantPointId
          constant: 1
      - transform:
          dataType: "qdrant:embeddings"
      - to:
          uri: qdrant:myCollection
```

#### Similarity Search for RAG

Retrieve relevant content using similarity search:

-   Java
    
-   YAML
    

```java
from("direct:search")
    .to("langchain4j-embeddings:embed")
    .transformDataType(new DataType("qdrant:embeddings"))
    .setHeader(QdrantHeaders.ACTION, constant(QdrantAction.SIMILARITY_SEARCH))
    .setHeader(QdrantHeaders.INCLUDE_PAYLOAD, constant(true))
    .to("qdrant:myCollection")
    .transformDataType(new DataType("qdrant:rag"));
```

```yaml
- route:
    from:
      uri: direct:search
    steps:
      - to:
          uri: langchain4j-embeddings:embed
      - transform:
          dataType: "qdrant:embeddings"
      - setHeader:
          name: CamelQdrantAction
          constant: SIMILARITY_SEARCH
      - setHeader:
          name: CamelQdrantIncludePayload
          constant: true
      - to:
          uri: qdrant:myCollection
      - transform:
          dataType: "qdrant:rag"
```

#### Using with PGVector

This example shows how to embed text and store it in PostgreSQL with pgvector:

-   Java
    
-   YAML
    

```java
from("direct:store")
    .to("langchain4j-embeddings:embed")
    .setHeader(PgVectorHeaders.ACTION).constant(PgVectorAction.UPSERT)
    .transformDataType(new DataType("pgvector:embeddings"))
    .to("pgvector:myCollection");
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
```

Similarity search with PGVector and RAG:

-   Java
    
-   YAML
    

```java
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

#### Using with LangChain4j Embedding Store Component

For a simpler integration, use the `langchain4j-embeddingstore` component which provides a unified interface:

-   Java
    
-   YAML
    

```java
from("direct:store")
    .to("langchain4j-embeddings:embed")
    .to("langchain4j-embeddingstore:myStore?action=ADD");

from("direct:search")
    .to("langchain4j-embeddings:embed")
    .to("langchain4j-embeddingstore:myStore?action=SEARCH&maxResults=5&returnTextContent=true");
```

```yaml
- route:
    from:
      uri: direct:store
    steps:
      - to:
          uri: langchain4j-embeddings:embed
      - to:
          uri: langchain4j-embeddingstore:myStore
          parameters:
            action: ADD

- route:
    from:
      uri: direct:search
    steps:
      - to:
          uri: langchain4j-embeddings:embed
      - to:
          uri: langchain4j-embeddingstore:myStore
          parameters:
            action: SEARCH
            maxResults: 5
            returnTextContent: true
```

### Structured error exchange properties

When a LangChain4j embeddings call fails, Camel sets structured metadata on the exchange **before** the model exception propagates. This works even when GenAI observability is disabled.

 
| Exchange property | Meaning |
| --- | --- |
| `CamelAiErrorCategory` | Coarse category derived from the LangChain4j exception: `RATE_LIMIT`, `SERVER_ERROR`, `VALIDATION`, `AUTH`, or `UNKNOWN` |
| `CamelAiRetryAfterMillis` | Not populated for LangChain4j providers (OpenAI-only today) |

Use categories when a route should branch on failure type without matching every LangChain4j exception class. See [LangChain4j Chat structured error properties](langchain4j-chat-component.html#_structured_error_exchange_properties) and [AI LLM integration guide](ai-llm-integration-guide.html#_structured_error_exchange_properties) for related detail.