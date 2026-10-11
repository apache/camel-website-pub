# ![langchain4j ingest sink](_images/kamelets/langchain4j-ingest-sink.svg) LangChain4j Ingest Sink

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Ingest documents into a LangChain4j EmbeddingStore: the payload is split into overlapping segments, embedded in batches and written to the store, each segment stamped with the pipeline name and the document id.

The document id is read from the `CamelLangChain4jIngestDocumentId` exchange property when a prior step captured it (the parser actions do, before the parse), else from the header named by `documentIdHeader` - the property always wins, so a parsed document cannot forge its own identity. Bean references are `#bean:name` values; when `embeddingStore` or `embeddingModel` is not set, the single registry bean of that type is used. With `idempotentRepository` set, the first write per document id wins - a re-delivered edited document is skipped, so streams that carry updates need a version-aware id. The filter options (`includeId`, `excludeId`, `minDocumentSize`, `documentFilter`) answer rejected deliveries with a filtered outcome that never keeps a dedup claim.

With `modality` set to `media` the payload (audio, an image, video or a PDF) is embedded whole, as one vector; the source must deliver raw bytes. A file source re-polls any document that fails the exchange on every run, so restrict the ids with `includeId` or the source’s `include`.

## Configuration Options

The following table summarizes the configuration options available for the `langchain4j-ingest-sink` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **contentType** | Content Type | MIME type of a media payload, such as audio/wav or image/png, handed to the embedding model. When unset, it is derived from the document id’s file extension (Camel’s MIME table); a document whose type cannot be determined, or whose medium the model does not declare, fails the exchange. Only valid with modality media, else the sink fails to start. | string |  |  |
| **documentFilter** | Document Filter | A Predicate bean deciding whether a delivery is ingested, as a `#bean:name` reference; a rejected delivery is answered filtered and releases its dedup claim. | string |  |  |
| **documentIdHeader** | Document Id Header | Name of the header carrying the stable document id, such as CamelAwsS3Key for an S3 source or CamelKafkaKey for a Kafka one; the CamelLangChain4jIngestDocumentId exchange property, when set, takes precedence. | string | CamelLangChain4jIngestDocumentId |  |
| **documentSplitter** | Document Splitter | A DocumentSplitter bean replacing the default recursive splitting, as a `#bean:name` reference; maxSegmentSize and maxOverlapSize are then ignored. With modality media the sink fails to start. | string |  |  |
| **embeddingBatchSize** | Embedding Batch Size | How many segments are embedded per request to the embedding model. | integer | 32 |  |
| **embeddingModel** | Embedding Model | The EmbeddingModel bean to embed with, as a `#bean:name` reference. | string |  |  |
| **embeddingStore** | Embedding Store | The EmbeddingStore bean to write to, as a `#bean:name` reference. | string |  |  |
| **excludeId** | Exclude Id | Comma-separated Ant-style patterns for document ids to skip, for example `***/draft-**`. Exclusion wins over includeId. | string |  |  |
| **idempotentRepository** | Idempotent Repository | An IdempotentRepository bean remembering ingested document ids, as a `#bean:name` reference. A duplicate delivery is answered skipped, first write wins. | string |  |  |
| **includeId** | Include Id | Comma-separated Ant-style patterns the document id must match to be ingested, for example `docs/***,**.md`. A non-matching delivery is answered filtered, before the dedup claim and without reading the body. | string |  |  |
| **maxDocumentSize** | Max Document Size | Maximum size of one document in characters, bytes with modality media; unset means no limit. The pipeline holds a document in memory whole, so set the cap when the source can deliver oversized payloads. An oversized document fails the exchange cleanly. | integer |  |  |
| **maxOverlapSize** | Max Overlap Size | How much of the previous segment each segment repeats, in characters. | integer | 50 |  |
| **maxSegmentSize** | Max Segment Size | Maximum size of one segment, in characters. | integer | 500 |  |
| **minDocumentSize** | Min Document Size | Minimum size of one document in characters, bytes with modality media; unset means no minimum. A shorter document is answered filtered and releases its dedup claim. | integer |  |  |
| **modality** | Modality | What the payload is; text when unset. `text` is split into segments and embedded segment by segment; `media` (audio, an image, video or a PDF) is embedded whole, as one vector, by a model that declares the matching content type; a text-only model fails the start, a medium the model lacks fails the exchange. In media mode the splitter options and embeddingBatchSize do not apply, documentSplitter must not be set, and maxDocumentSize and minDocumentSize count bytes. Enum values: \* text \* media | string |  |  |
| **pipelineName** | Pipeline Name | The pipeline name, stamped on every written segment. | string | ingest |  |

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