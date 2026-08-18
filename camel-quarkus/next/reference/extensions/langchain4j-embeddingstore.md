# LangChain4j Embedding Store

JVM since3.29.0 Native since3.29.0

Perform operations on the LangChain4jEmbeddingStores.

## What’s inside

-   [LangChain4j Embedding Store component](../../../../components/4.22.x/langchain4j-embeddingstore-component.md), URI syntax: `langchain4j-embeddingstore:embeddingStoreId`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-langchain4j-embeddingstore)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-langchain4j-embeddingstore</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## Usage

### Named embedding stores from Quarkus LangChain4j

When the [Quarkus LangChain4j](https://docs.quarkiverse.io/quarkus-langchain4j/dev/index.md) extensions are present, any `EmbeddingStore` CDI bean qualified with `@EmbeddingStoreName` is automatically bound into the Camel registry under its qualifier value. This covers both stores declared through Quarkus LangChain4j named configuration (for example `quarkus.langchain4j.pgvector.products.\*`) and stores produced by your own `@Produces` methods.

Such a store can be referenced from a route by name, with no manual registry binding:

```java
from("direct:ingest-products")
    .to("langchain4j-embeddingstore:products?embeddingStore=#products&embeddingModel=#embeddingModel");
```

A store only referenced from routes does not need to be injected anywhere in Java code; it is retained and instantiated lazily on first use. If the Camel registry already resolves a different `EmbeddingStore` under the same name (for example a `@Named` bean), that existing bean keeps winning lookups and a warning is logged at startup.

### Retrieval augmentors for `@RegisterAiService`

With Quarkus LangChain4j present, a `RetrievalAugmentor` is produced automatically from the `@Default` `EmbeddingStore` and `EmbeddingModel` beans, so an `@RegisterAiService` interface answers from the same store a Camel route ingests into. Nothing is produced when the application declares its own `RetrievalAugmentor`.

Augmentors can also be declared explicitly, one per store:

```properties
quarkus.camel.langchain4j.rag.augmentors.products.embedding-store-name=products
quarkus.camel.langchain4j.rag.augmentors.products.default=true
quarkus.camel.langchain4j.rag.augmentors.support.embedding-store-name=support-docs
```

Each entry produces a `@Named` `RetrievalAugmentor`. With more than one configured, exactly one must be marked `default=true`: that one serves the unqualified lookup `@RegisterAiService` performs, while the others remain selectable by name. Configuring several without marking one fails the build, because an ambiguous unqualified lookup disables RAG for every AI service without reporting anything. A single entry needs no marking.

Selecting one of the others means naming it through a supplier, since `@RegisterAiService` either takes the unqualified augmentor or a `Supplier` class:

```java
public class SupportAugmentorSupplier implements Supplier<RetrievalAugmentor> {
    @Inject
    @Named("support")
    RetrievalAugmentor augmentor;

    @Override
    public RetrievalAugmentor get() {
        return augmentor;
    }
}

@RegisterAiService(retrievalAugmentor = SupportAugmentorSupplier.class)
public interface SupportAssistant {
    String chat(String question);
}
```

### Filtering what retrieval may see

Metadata stored next to a segment — a tenant key, a classification — isolates nothing unless retrieval filters on it. A single `RagRetrievalFilterSupplier` bean, if present, is consulted on every retrieval performed by a produced augmentor:

```java
@ApplicationScoped
public class TenantFilterSupplier implements RagRetrievalFilterSupplier {
    @Inject
    CurrentTenant currentTenant; // request scoped

    @Override
    public Filter filter(Query query, String augmentorName, String embeddingStoreName) {
        if (!"products".equals(embeddingStoreName)) {
            return null; // only this store carries tenant metadata
        }
        String tenant = currentTenant.name();
        if (tenant == null) {
            // fail closed: returning null here would serve every tenant's documents
            throw new IllegalStateException("No tenant in scope");
        }
        return metadataKey("tenant").isEqualTo(tenant);
    }
}
```

The one bean serves every produced augmentor, so it is told which augmentor retrieves and which store is being searched; both are `null` for the auto-produced default augmentor, which is backed by the `@Default` beans. Filtering on a metadata key a store does not carry matches nothing, so return `null` for the stores an implementation does not know about.

Returning `null` means unfiltered retrieval, as it does in LangChain4j itself, so an implementation that cannot determine the caller must throw instead. The tenant may equally come from `query.metadata().chatMemoryId()`, which is the only source that still works when retrieval does not run on the caller’s thread. At most one implementation may exist, and it must not be `@Dependent`; both are build failures.

Two limits are worth knowing before treating this as an access control:

-   The filter reaches only the augmentors this extension produces. Easy RAG, or an application-provided `RetrievalAugmentor`, replaces them, and the filter is then never consulted — the build logs a warning when it detects that combination.
    
-   `EmbeddingStore` implementations are not required to support filtering. One that ignores the filter returns every match, so verify against the store actually in use.
    

## LangChain4j usage

### Dependency management

In order to ensure alignment across all Quarkus and LangChain4j related dependencies, it is recommended to import the LangChain4j BOM as below:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>dev.langchain4j</groupId>
      <artifactId>langchain4j-bom</artifactId>
      <version>1.17.2</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
  ...
</dependencyManagement>
```

Note that the import order is paramount when using maven `dependencyManagement`. As such, one might need to import the `langchain4j-bom` before other related Camel and Quarkus BOMs.

### Quarkus LangChain4j support

> **Warning**
> At present, this extension is neither tested with nor intended to be used in conjunction with any Quarkus LangChain4j extensions. Consequently, both JVM and native modes may exhibit unexpected behaviour or fail to function correctly in such configurations.