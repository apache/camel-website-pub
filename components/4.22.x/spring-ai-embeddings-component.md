# Spring AI Embeddings

**Since Camel 4.17**

**Only producer is supported**

The Spring AI Embeddings component provides support for computing embeddings using [Spring AI embedding models](https://docs.spring.io/spring-ai/reference/api/embeddings.md).

Embeddings are numerical vector representations of text that capture semantic relationships between inputs. They are useful for:

-   Semantic similarity search
    
-   Text clustering and classification
    
-   Retrieval-Augmented Generation (RAG)
    
-   Recommendation systems
    

> **Note**
> This is a low-level component for direct embedding computation. For most use cases, you can use the `camel-spring-ai-chat` component with appropriate configuration for RAG scenarios, or the `camel-spring-ai-vector-store` component which can handle embeddings automatically without requiring this component directly.

## URI format

spring-ai-embeddings:embeddingId\[?options\]

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

The Spring AI Embeddings component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration. |  | SpringAiEmbeddingsConfiguration |
| **embeddingModel** (producer) | **Autowired** **Required** The EmbeddingModel to use for generating embeddings. |  | EmbeddingModel |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |

## Endpoint Options

The Spring AI Embeddings endpoint is configured using URI syntax:

spring-ai-embeddings:embeddingId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **embeddingId** (producer) | **Required** The id. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **embeddingModel** (producer) | **Autowired** **Required** The EmbeddingModel to use for generating embeddings. |  | EmbeddingModel |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The Spring AI Embeddings component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelSpringAiEmbeddingMetadata** (producer) Constant: [`EMBEDDING_METADATA`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-embeddings/latest/org/apache/camel/component/springai/embeddings/SpringAiEmbeddingsHeaders.html#EMBEDDING_METADATA) | The embedding response metadata. |  | EmbeddingResponseMetadata |
| **CamelSpringAiEmbeddingIndex** (producer) Constant: [`EMBEDDING_INDEX`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-embeddings/latest/org/apache/camel/component/springai/embeddings/SpringAiEmbeddingsHeaders.html#EMBEDDING_INDEX) | The index of the embedding in the response. |  | Integer |
| **CamelSpringAiEmbedding** (producer) Constant: [`EMBEDDING`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-embeddings/latest/org/apache/camel/component/springai/embeddings/SpringAiEmbeddingsHeaders.html#EMBEDDING) | The Embedding object. |  | Embedding |
| **CamelSpringAiEmbeddingInputText** (producer) Constant: [`INPUT_TEXT`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-embeddings/latest/org/apache/camel/component/springai/embeddings/SpringAiEmbeddingsHeaders.html#INPUT_TEXT) | The input text that was embedded. |  | String |
| **CamelSpringAiEmbeddings** (producer) Constant: [`EMBEDDINGS`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-embeddings/latest/org/apache/camel/component/springai/embeddings/SpringAiEmbeddingsHeaders.html#EMBEDDINGS) | List of Embedding objects. |  | List |
| **CamelSpringAiEmbeddingInputTexts** (producer) Constant: [`INPUT_TEXTS`](https://javadoc.io/doc/org.apache.camel/camel-spring-ai-embeddings/latest/org/apache/camel/component/springai/embeddings/SpringAiEmbeddingsHeaders.html#INPUT_TEXTS) | List of input texts that were embedded. |  | List |

## Usage

The component accepts two types of input:

-   **Single text**: A String containing the text to embed
    
-   **Batch processing**: A List<String> containing multiple texts to embed at once
    

The embedding vectors are returned in the message body, with additional metadata available in headers.

### Single Text Example

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:start")
    .to("spring-ai-embeddings:myEmbedding")
    .log("Embedding vector: ${body}");
```

```xml
<route>
  <from uri="direct:start"/>
  <to uri="spring-ai-embeddings:myEmbedding"/>
  <log message="Embedding vector: ${body}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:start
      steps:
        - to:
            uri: spring-ai-embeddings:myEmbedding
        - log:
            message: "Embedding vector: ${body}"
```

When processing a single String, the component returns:

-   **Message Body**: The embedding vector as `float[]`
    
-   **Headers**:
    
    -   `CamelSpringAiEmbedding` - The Embedding object
        
    -   `CamelSpringAiEmbeddingIndex` - The index (0 for single embeddings)
        
    -   `CamelSpringAiEmbeddingInputText` - The original input text
        
    -   `CamelSpringAiEmbeddingMetadata` - Response metadata
        
    

### Batch Processing Example

-   Java
    
-   XML
    
-   YAML
    

```java
from("direct:batch")
    .setBody(constant(List.of("text 1", "text 2", "text 3")))
    .to("spring-ai-embeddings:myEmbedding")
    .log("Number of embeddings: ${body.size()}");
```

```xml
<route>
  <from uri="direct:batch"/>
  <setBody>
    <constant>["text 1", "text 2", "text 3"]</constant>
  </setBody>
  <to uri="spring-ai-embeddings:myEmbedding"/>
  <log message="Number of embeddings: ${body.size()}"/>
</route>
```

```yaml
- route:
    from:
      uri: direct:batch
      steps:
        - setBody:
            constant: '["text 1", "text 2", "text 3"]'
        - to:
            uri: spring-ai-embeddings:myEmbedding
        - log:
            message: "Number of embeddings: ${body.size()}"
```

When processing a List<String>, the component returns:

-   **Message Body**: List of embedding vectors as `List<float[]>`
    
-   **Headers**:
    
    -   `CamelSpringAiEmbeddings` - List of Embedding objects
        
    -   `CamelSpringAiEmbeddingInputTexts` - The original input texts as List<String>
        
    -   `CamelSpringAiEmbeddingMetadata` - Response metadata