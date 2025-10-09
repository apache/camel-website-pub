# Apache Camel 4.x Upgrade Guide

This document is for helping you upgrade your Apache Camel application from Camel 4.x to 4.y. For example, if you are upgrading Camel 4.0 to 4.2, then you should follow the guides from both 4.0 to 4.1 and 4.1 to 4.2.

> **Note**
> [The Camel Upgrade Recipes project](https://github.com/apache/camel-upgrade-recipes/) provides automated assistance for some common migration tasks. Note that manual migration is still required. See the [documentation](camel-upgrade-recipes-tool.md) page for details.

> **Important**
> In this 4.15.0 release the Camel Spring Boot does not support running with JDK 17. This has been fixed for the next 4.16.0 release.

## Upgrading Camel 4.14 to 4.15

### Data Formats

The data formats has been refactored to ensure their options are consistent and can be mapped from the DSL to their implementation using reflection-free configurers. A few data formats has therefore changed some option names:

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top"><strong>Data Format</strong></td><td class="tableblock halign-left valign-top"><strong>Old Name</strong></td><td class="tableblock halign-left valign-top"><strong>New Name</strong></td></tr><tr><td class="tableblock halign-left valign-top">crypto</td><td class="tableblock halign-left valign-top">algorithmParameterRef</td><td class="tableblock halign-left valign-top">algorithmParameterSpec</td></tr><tr><td class="tableblock halign-left valign-top">crypto</td><td class="tableblock halign-left valign-top">keyRef</td><td class="tableblock halign-left valign-top">key</td></tr><tr><td class="tableblock halign-left valign-top">crypto</td><td class="tableblock halign-left valign-top">initVectorRef</td><td class="tableblock halign-left valign-top">initVector</td></tr><tr><td class="tableblock halign-left valign-top">csv</td><td class="tableblock halign-left valign-top">formatRef</td><td class="tableblock halign-left valign-top">format</td></tr><tr><td class="tableblock halign-left valign-top">csv</td><td class="tableblock halign-left valign-top">formatName</td><td class="tableblock halign-left valign-top">format</td></tr><tr><td class="tableblock halign-left valign-top">flatpack</td><td class="tableblock halign-left valign-top">parserFactoryRef</td><td class="tableblock halign-left valign-top">parserFactory</td></tr><tr><td class="tableblock halign-left valign-top">jaxb</td><td class="tableblock halign-left valign-top">namespacePrefixRef</td><td class="tableblock halign-left valign-top">namespacePrefix</td></tr><tr><td class="tableblock halign-left valign-top">soap</td><td class="tableblock halign-left valign-top">namespacePrefixRef</td><td class="tableblock halign-left valign-top">namespacePrefix</td></tr><tr><td class="tableblock halign-left valign-top">soap</td><td class="tableblock halign-left valign-top">elementNameStrategyRef</td><td class="tableblock halign-left valign-top">elementNameStrategy</td></tr><tr><td class="tableblock halign-left valign-top">swiftMx</td><td class="tableblock halign-left valign-top">readConfigRef</td><td class="tableblock halign-left valign-top">readConfig</td></tr><tr><td class="tableblock halign-left valign-top">swiftMx</td><td class="tableblock halign-left valign-top">writeConfigRef</td><td class="tableblock halign-left valign-top">writeConfig</td></tr><tr><td class="tableblock halign-left valign-top">xmlSecurity</td><td class="tableblock halign-left valign-top">keyOrTrustStoreParametersRef</td><td class="tableblock halign-left valign-top">keyOrTrustStoreParameters</td></tr></tbody></table>

And in XML DSL the csv dataformat have changed `header` from a `List<String>` to be a single `String` where the header values are separated by comma. This is more tooling friendly and also how other components and dataformats are configured.

For example:

```xml
<csv format="EXCEL" delimiter="|" skipHeaderRecord="true">
  <header>orderId</header>
  <header>amount</header>
</csv>
```

Should be changed to:

```xml
<csv format="EXCEL" delimiter="|" skipHeaderRecord="true" header="orderId,amount"/>
```

Likewise in XML DSL the YAML data format has changed `typeFilter` from a `List`\> to be a single `String` where the types values are separated by comma. This is more tooling friendly and also how other components and dataformats are configured.

```xml
<yaml id="yaml-type-constructor-strdef" library="SnakeYAML">
    <typeFilter value="org.apache.camel.component.snakeyaml.model.TestPojo"/>
    <typeFilter value="org.apache.camel.component.snakeyaml.model.Rex.*" type="regexp"/>
</yaml>
```

Should be changed to:

```xml
<yaml id="yaml-type-constructor-strdef" library="SnakeYAML"
      typeFilter="org.apache.camel.component.snakeyaml.model.TestPojo,org.apache.camel.component.snakeyaml.model.Rex.*"/>
```

Removed the `tidyMarkup` DataFormat in the DSL as the implementation has been removed in earlier version, but we forgot to remove it from the DSL model.

### camel-netty / camel-netty-http

Removed deprecated options `keyStoreFile` and `trustStoreFile`. Use `keyStoreResource` and `trustStoreResources` instead, and prefix the value with `file:` as documented.

### Camel AI Nested Headers classes

There were a number of nested headers classes in the camel-ai components that have been separated into a standalone Headers class. The original class and the corresponding new class are listed below. For more information, the related issue is CAMEL-22334.

<table class="tableblock frame-all grid-all stretch"><colgroup><col> <col></colgroup><tbody><tr><td class="tableblock halign-left valign-top"><strong>Original Class</strong></td><td class="tableblock halign-left valign-top"><strong>New Class</strong></td></tr><tr><td class="tableblock halign-left valign-top">org.apache.camel.component.langchain4j.chat.LangChain4jChat.Headers</td><td class="tableblock halign-left valign-top">org.apache.camel.component.langchain4j.chat.LangChain4jChatHeaders</td></tr><tr><td class="tableblock halign-left valign-top">org.apache.camel.component.langchain4j.embeddings.LangChain4jEmbeddings.Headers</td><td class="tableblock halign-left valign-top">org.apache.camel.component.langchain4j.embeddings.LangChain4jEmbeddingsHeaders</td></tr><tr><td class="tableblock halign-left valign-top">org.apache.camel.component.langchain4j.embeddingstore.LangChain4jEmbeddingStore.Headers</td><td class="tableblock halign-left valign-top">org.apache.camel.component.langchain4j.embeddingstore.LangChain4jEmbeddingStoreHeaders</td></tr><tr><td class="tableblock halign-left valign-top">org.apache.camel.component.milvus.Milvus.Headers</td><td class="tableblock halign-left valign-top">org.apache.camel.component.milvus.MilvusHeaders</td></tr><tr><td class="tableblock halign-left valign-top">org.apache.camel.component.neo4j.Neo4jConstants.Headers</td><td class="tableblock halign-left valign-top">org.apache.camel.component.neo4j.Neo4jHeaders</td></tr><tr><td class="tableblock halign-left valign-top">org.apache.camel.component.qdrant.Qdrant.Headers</td><td class="tableblock halign-left valign-top">org.apache.camel.component.qdrant.QdrantHeaders</td></tr><tr><td class="tableblock halign-left valign-top">org.apache.camel.component.pinecone.PineconeVectorDb.Headers</td><td class="tableblock halign-left valign-top">org.apache.camel.component.pinecone.PineconeVectorDbHeaders</td></tr><tr><td class="tableblock halign-left valign-top">org.apache.camel.component.weaviate.WeaviateVectorDb.Headers</td><td class="tableblock halign-left valign-top">org.apache.camel.component.weaviate.WeaviateVectorDbHeaders</td></tr></tbody></table>

org.apache.camel.component.langchain4j.web.search.LangChain4jWebSearchEngine.Headers was empty and has been removed

### camel-mdc

We have introduced a new component, `camel-mdc`, whose goal is to simplify the usage of logging MDC (Mapped Diagnostic Context) by allowing the user to configure the Exchange headers and properties to use to trace in MDC logging format.