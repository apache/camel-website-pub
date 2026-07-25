# Specialized tokenizer for AI applications

The Tokenizer EIP provides support to tokenize (chunk) larger blocks of text into text segments that can be used when interacting with LLMs. Tokenization is particularly helpful when used with [vector databases](https://en.wikipedia.org/wiki/Vector_database) to provide better and more contextual search results for [retrieval-augmented generation (RAG)](https://en.wikipedia.org/wiki/Retrieval-augmented_generation).

This EIP uses the [LangChain4j document splitter](https://docs.langchain4j.dev/tutorials/rag/#document-splitter) to handle chunking.

## EIP options

The Specialized tokenizer for AI applications eip supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **note** | The note for this node. |  | String |
| **description** | The description for this node. |  | String |
| **disabled** | Whether to disable this EIP from the route during build time. Once an EIP has been disabled then it cannot be enabled later at runtime. | false | Boolean |
| **tokenizerImplementation** | The tokenizer implementation to use, such as LangChain4j character, line, paragraph, sentence, or word tokenizers. |  | TokenizerImplementationDefinition |

## Supported Splitters

The following type of splitters is supported:

-   By paragraph: using the DSL `tokenizer().byParagraph()`
    
-   By sentence: using the DSL `tokenizer().bySentence()`
    
-   By word: using the DSL `tokenizer().byWord()`
    
-   By line: using the DSL `tokenizer().byLine()`
    
-   By character: using the DSL `tokenizer().byCharacter()`
    

## Supported Tokenizers

The following tokenizers are supported:

-   OpenAI: using `LangChain4jTokenizerDefinition.TokenizerType.OPEN_AI`
    
-   Azure: using `LangChain4jTokenizerDefinition.TokenizerType.AZURE`
    
-   Qwen: using `LangChain4jTokenizerDefinition.TokenizerType.QWEN`
    

## Example

The tokenization creates a composite message (an array of Strings). This composite message can be split using the [Split EIP](split-eip.md) so that each text segment is sent separately to an endpoint.

-   Java
    

```java
from("direct:start")
    .tokenize(tokenizer()
            .byParagraph()
                .maxSegmentSize(1024)
                .maxOverlap(10)
                .using(LangChain4jTokenizerDefinition.TokenizerType.OPEN_AI)
                .end())
    .split().body()
    .to("mock:result");
```

### Tokenize by tokens

Starting with Camel 4.12, the code defaults to using segment sizes for determining the maximum amount of data to tokenize. To tokenize by tokens, you must specify the underlying model:

-   Java
    

```java
from("direct:start")
    .tokenize(tokenizer()
            .byParagraph()
                .maxTokens(1024, "gpt-4o-mini")
                .maxOverlap(10)
                .using(LangChain4jTokenizerDefinition.TokenizerType.OPEN_AI)
                .end())
    .split().body()
    .to("mock:result");
```

## Dependencies

Maven users will need to add the following dependency:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-langchain4j-tokenizer</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

The application must also provide the specific tokenizer implementation from LangChain4j:

-   OpenAI: `dev.langchain4j:langchain4j-open-ai`
    
-   Azure: `dev.langchain4j:langchain4j-azure-open-ai`
    
-   Qwen: `dev.langchain4j:langchain4j-dashscope`
    

## See Also

-   [Split EIP](split-eip.md)