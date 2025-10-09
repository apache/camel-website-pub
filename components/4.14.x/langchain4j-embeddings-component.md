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

The LangChain4j Embeddings component supports 4 options, which are listed below.

   
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

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **embeddingId** (producer) | **Required** The id. |  | String |

### Query Parameters (2 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **embeddingModel** (producer) | **Autowired** **Required** The EmbeddingModel engine to use. |  | EmbeddingModel |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |

## Message Headers

The LangChain4j Embeddings component supports 6 message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelLangChain4jEmbeddingsFinishReason** (producer) Constant: [`FINISH_REASON`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddings$Headers.html#FINISH_REASON) | 
The Finish Reason.

Enum values:

-   STOP
    
-   LENGTH
    
-   TOOL\_EXECUTION
    
-   CONTENT\_FILTER
    
-   OTHER
    





 |  | FinishReason |
| **CamelLangChain4jEmbeddingsInputTokenCount** (producer) Constant: [`INPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddings$Headers.html#INPUT_TOKEN_COUNT) | The Input Token Count. |  | int |
| **CamelLangChain4jEmbeddingsOutputTokenCount** (producer) Constant: [`OUTPUT_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddings$Headers.html#OUTPUT_TOKEN_COUNT) | The Output Token Count. |  | int |
| **CamelLangChain4jEmbeddingsTotalTokenCount** (producer) Constant: [`TOTAL_TOKEN_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddings$Headers.html#TOTAL_TOKEN_COUNT) | The Total Token Count. |  | int |
| **CamelLangChain4jEmbeddingsVector** (producer) Constant: [`VECTOR`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddings$Headers.html#VECTOR) | A dense vector embedding of a text. |  | float\[\] |
| **CamelLangChain4jEmbeddingsTextSegment** (producer) Constant: [`TEXT_SEGMENT`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-embeddings/latest/org/apache/camel/component/langchain4j/embeddings/LangChain4jEmbeddings$Headers.html#TEXT_SEGMENT) | A TextSegment representation of the vector embedding input text. |  | TextSegment |

## Spring Boot Auto-Configuration

When using langchain4j-embeddings with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-langchain4j-embeddings-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.langchain4j-embeddings.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.langchain4j-embeddings.configuration** | The configuration. The option is a org.apache.camel.component.langchain4j.embeddings.LangChain4jEmbeddingsConfiguration type. |  | LangChain4jEmbeddingsConfiguration |
| **camel.component.langchain4j-embeddings.embedding-model** | The EmbeddingModel engine to use. The option is a dev.langchain4j.model.embedding.EmbeddingModel type. |  | EmbeddingModel |
| **camel.component.langchain4j-embeddings.enabled** | Whether to enable auto configuration of the langchain4j-embeddings component. This is enabled by default. |  | Boolean |
| **camel.component.langchain4j-embeddings.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |