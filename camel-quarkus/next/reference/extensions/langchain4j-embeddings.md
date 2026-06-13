# LangChain4j Embeddings

JVM since3.10.0 Native since3.29.0

LangChain4j Embeddings

## What’s inside

-   [LangChain4j Embeddings component](../../../../components/next/langchain4j-embeddings-component.md), URI syntax: `langchain4j-embeddings:embeddingId`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-langchain4j-embeddings)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-langchain4j-embeddings</artifactId>
</dependency>
```

Check the [User guide](../../user-guide/index.md) for more information about writing Camel Quarkus applications.

## LangChain4j usage

### Dependency management

In order to ensure alignment across all Quarkus and LangChain4j related dependencies, it is recommended to import the LangChain4j BOM as below:

```xml
<dependencyManagement>
  <dependencies>
    <dependency>
      <groupId>dev.langchain4j</groupId>
      <artifactId>langchain4j-bom</artifactId>
      <version>1.16.2</version>
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