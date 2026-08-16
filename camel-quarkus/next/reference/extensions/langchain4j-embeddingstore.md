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