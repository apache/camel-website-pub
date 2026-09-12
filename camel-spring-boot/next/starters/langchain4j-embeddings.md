Camel Spring Boot

# LangChain4j Embeddings

LangChain4j Embeddings

## What’s inside

-   [LangChain4j Embeddings component](../../../components/next/langchain4j-embeddings-component.md), URI syntax: `langchain4j-embeddings:embeddingId`
    

Please refer to the above links for usage and configuration details.

## Maven coordinates

```xml
<dependency>
    <groupId>org.apache.camel.springboot</groupId>
    <artifactId>camel-langchain4j-embeddings-starter</artifactId>
</dependency>
```

## Spring Boot Auto-Configuration

### Providing an `EmbeddingModel`

The Camel starter configures the component but does not create an `EmbeddingModel`. Add a LangChain4j provider starter and configure its embedding-model properties. Use the `-spring-boot-starter` variant with Spring Boot 3 or the `-spring-boot4-starter` variant with Spring Boot 4. For example, the Ollama starter creates an `ollamaEmbeddingModel` bean, which can be referenced with `embeddingModel=#ollamaEmbeddingModel`.

When exactly one `EmbeddingModel` is available, Camel autowires it and the `embeddingModel` endpoint option can be omitted. See the [LangChain4j Spring Boot integration documentation](https://docs.langchain4j.dev/tutorials/spring-boot-integration) for provider starters, properties, and compatible versions.

The starter supports 5 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| camel.component.langchain4j-embeddings.autowired-enabled | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| camel.component.langchain4j-embeddings.configuration | The configuration. The option is a org.apache.camel.component.langchain4j.embeddings.LangChain4jEmbeddingsConfiguration type. |  | LangChain4jEmbeddingsConfiguration |
| camel.component.langchain4j-embeddings.embedding-model | The EmbeddingModel engine to use. The option is a dev.langchain4j.model.embedding.EmbeddingModel type. |  | EmbeddingModel |
| camel.component.langchain4j-embeddings.enabled | Whether to enable auto configuration of the langchain4j-embeddings component. This is enabled by default. |  | Boolean |
| camel.component.langchain4j-embeddings.lazy-start-producer | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |