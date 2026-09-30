# LangChain4j Chat

JVM since3.11.0 Native since3.12.0

LangChain4j Chat component

## What’s inside

-   [LangChain4j Chat component](../../../../components/4.22.x/langchain4j-chat-component.md), URI syntax: `langchain4j-chat:chatId`
    

Please refer to the above link for usage and configuration details.

## Maven coordinates

[Create a new project with this extension on code.quarkus.io](https://code.quarkus.io/?extension-search=camel-quarkus-langchain4j-chat)

Or add the coordinates to your existing project:

```xml
<dependency>
    <groupId>org.apache.camel.quarkus</groupId>
    <artifactId>camel-quarkus-langchain4j-chat</artifactId>
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
      <version>1.19.3</version>
      <type>pom</type>
      <scope>import</scope>
    </dependency>
  </dependencies>
  ...
</dependencyManagement>
```

Note that the import order is paramount when using maven `dependencyManagement`. As such, one might need to import the `langchain4j-bom` before other related Camel and Quarkus BOMs.

### Quarkus LangChain4j support

This extension is designed and tested to work together with [Quarkus LangChain4j](https://docs.quarkiverse.io/quarkus-langchain4j/dev/index.md).

The `ChatModel` beans produced by Quarkus LangChain4j are regular CDI beans, which the `langchain4j-chat` component resolves from the Camel registry.

The default chat model is requested automatically, so a route needs no `chatModel` option:

```java
from("direct:chat")
    .to("langchain4j-chat:default?chatOperation=CHAT_SINGLE_MESSAGE");
```

Nothing is requested when the application declares its own `ChatModel` bean, or when the provider of the default model cannot be determined. For example, when no Quarkus LangChain4j model provider extension is present, or when several of them are on the classpath and `quarkus.langchain4j.chat-model.provider` is not set.

Models declared under `quarkus.langchain4j.<name>.chat-model.provider` are produced by Quarkus LangChain4j from configuration alone. Select them by name:

```java
from("direct:chat")
    .to("langchain4j-chat:named?chatOperation=CHAT_SINGLE_MESSAGE&chatModel=#custom");
```

Name the model this way whenever named models are in play. Where a default model bean also exists, it takes precedence in the unqualified registry lookup the component performs when `chatModel` is absent.