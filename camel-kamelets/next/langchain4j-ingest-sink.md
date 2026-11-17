# ![langchain4j ingest sink](_images/kamelets/langchain4j-ingest-sink.svg) LangChain4j Ingest Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Splits each document into small pieces of text, turns each piece into an embedding (a vector of numbers) with an AI embedding model, and writes them to a LangChain4j embedding store.

Use it to load documents into a vector store, so that an AI assistant can later find the pieces that answer a question (RAG). Read PDF or office documents with `tika-extract-text-action` or `docling-convert-action` first, and a directory with `langchain4j-ingest-file-source`.

Input: the document, as text, bytes, a stream or a file, read as text. Every document needs an id, such as its file name, in the `CamelLangChain4jIngestDocumentId` header (or the one named in `documentIdHeader`); an id kept by `tika-extract-text-action` or `docling-convert-action` comes first.

Output: when it is used inside a route, the body afterwards is a result object with the pipeline name, the document id, the number of pieces written, and the outcome: `INGESTED`, `EMPTY` (an empty document, nothing written), `SKIPPED` (an id seen before, with `idempotentRepository`) or `FILTERED` (left out by `includeId`, `excludeId`, `minDocumentSize` or `documentFilter`).

Good to know: the embedding store and the embedding model are objects you define in the application, such as in the `beans` section of a YAML route; when there is one of each, the options can be left out. Writing a document again adds new pieces, and does not replace the ones written before. With `idempotentRepository`, only the first document with a given id is written, so a changed version of a file is skipped. A message without a document id, or larger than `maxDocumentSize`, fails.

## Configuration Options

The following table summarizes the configuration options available for the `langchain4j-ingest-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **contentType** | Content Type | The kind of content of the documents, as a MIME type, handed to the embedding model. Only with `modality` set to `media`. When it is not set, it is guessed from the extension of the document id, such as `.png`. | string |  | image/png |
| **documentFilter** | Document Filter | A filter object defined in the application (a Camel `Predicate`) that decides for each document whether it is written, as `#bean:` followed by its name. A document it refuses gets the outcome `FILTERED`. | string |  | #bean:myFilter |
| **documentIdHeader** | Document ID Header | The name of the header that holds the id of the document, such as its file name or path. Set it to the header your source fills, such as `CamelAwsS3Key` for `aws-s3-source`. An id kept by `tika-extract-text-action` or `docling-convert-action` takes precedence. | string | CamelLangChain4jIngestDocumentId | CamelAwsS3Key |
| **documentSplitter** | Document Splitter | A LangChain4j `DocumentSplitter` defined in the application, to cut the text into pieces your own way, as `#bean:` followed by its name. `maxSegmentSize` and `maxOverlapSize` are then not used. Not allowed with `modality` set to `media`. | string |  | #bean:mySplitter |
| **embeddingBatchSize** | Embedding Batch Size | How many pieces are sent to the embedding model in one request. | integer | 32 |  |
| **embeddingModel** | Embedding Model | The LangChain4j `EmbeddingModel` that turns the text into vectors, defined in the application, as `#bean:` followed by its name. When it is not set, the only embedding model of the application is used. | string |  | #bean:model |
| **embeddingStore** | Embedding Store | The LangChain4j `EmbeddingStore` to write to, defined in the application, as `#bean:` followed by its name. When it is not set, the only embedding store of the application is used. | string |  | #bean:store |
| **excludeId** | Exclude ID | Patterns for the document ids to leave out, separated by commas, in the same form as `includeId`. It wins over `includeId`. | string |  | **\*/draft-** |
| **idempotentRepository** | Idempotent Repository | A Camel `IdempotentRepository` defined in the application, as `#bean:` followed by its name, that remembers the ids of the documents written. A document whose id it has seen before is not written again, and gets the outcome `SKIPPED`, even when its content changed. | string |  | #bean:ingestedIds |
| **includeId** | Include ID | Ant-style patterns that the document id must match to be written, separated by commas, such as `***/**.md` for every Markdown file in any directory. Other documents are left out, with the outcome `FILTERED`. When it is not set, every document is written. | string |  | docs/**\*,**.md |
| **maxDocumentSize** | Max Document Size | The largest document to write, in characters, or in bytes with `modality` set to `media`. A larger document fails the message. When it is not set, there is no limit; the whole document is held in memory. | integer |  | 1000000 |
| **maxOverlapSize** | Max Overlap Size | How many characters at the end of a piece are repeated at the start of the next one, so that a sentence cut in two is still found. | integer | 50 |  |
| **maxSegmentSize** | Max Segment Size | The longest piece of text to embed, in characters. Smaller pieces give more precise search results; larger ones keep more context together. | integer | 500 |  |
| **minDocumentSize** | Min Document Size | The smallest document to write, in characters, or in bytes with `modality` set to `media`. A smaller document is left out, with the outcome `FILTERED`. | integer |  | 100 |
| **modality** | Modality | What the documents are. `text`, used when it is not set, splits the text into pieces. `media` embeds each document whole, as one vector, for an image, audio, video or a PDF; it needs an embedding model that accepts that kind of content, else the integration fails to start, and the splitting options and `embeddingBatchSize` are not used. Enum values: \* text \* media | string |  |  |
| **pipelineName** | Pipeline Name | A name for this ingestion, written on every piece in the store, so that the pieces of several pipelines can be told apart. Letters, digits, dots, underscores and dashes only. | string | ingest | product-manuals |

## Dependencies

At runtime, the `langchain4j-ingest-sink` Kamelet relies upon the presence of the following dependencies:

-   camel:langchain4j-ingest
    
-   camel:kamelet
    

## Camel JBang usage

### **Prerequisites**

-   You’ve installed [JBang](https://www.jbang.dev/).
    
-   You have executed the following command:
    

```shell
jbang app install camel@apache/camel
```

Supposing you have a file named route.yaml with this content:

```yaml
- route:
    from:
      uri: "kamelet:timer-source"
      parameters:
        period: 10000
        message: 'test'
      steps:
        - to:
            uri: "kamelet:langchain4j-ingest-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/langchain4j-ingest-sink.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/langchain4j-ingest-sink.kamelet.yaml)