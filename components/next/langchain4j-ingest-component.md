# LangChain4j Ingest

**Since Camel 4.23**

**Only producer is supported**

The LangChain4j Ingest component feeds documents into a [LangChain4j](https://github.com/langchain4j/langchain4j) `EmbeddingStore`: the message body is split into overlapping segments, embedded in batches and written to the store. It is the ingestion half of a Retrieval-Augmented Generation (RAG) setup — retrieval is served by the [LangChain4j Embedding Store](langchain4j-embeddingstore-component.md) component or a LangChain4j retriever over the same store.

Every written segment carries two metadata entries, so retrieval can cite where an answer came from and a future synchronising engine can find a document’s vectors again:

-   `camel_ingest_pipeline` — the pipeline name from the endpoint URI
    
-   `camel_ingest_document_id` — the stable document id of the ingested payload
    

## URI format

langchain4j-ingest:pipelineName\[?options\]

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

The LangChain4j Ingest component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration. |  | LangChain4jIngestConfiguration |
| **documentIdHeader** (producer) | Name of the header carrying the document id, such as CamelAwsS3Key for an S3 consumer or CamelKafkaKey for a Kafka one. The CamelLangChain4jIngestDocumentId exchange property, when set, takes precedence - a route that parses documents captures the id into that property before the parse, so a document cannot forge its own identity. An exchange without an id fails. | CamelLangChain4jIngestDocumentId | String |
| **embeddingBatchSize** (producer) | How many segments are embedded per request to the embedding model. Providers with generous per-request limits ingest large documents faster with a bigger batch; a batch carries at most embeddingBatchSize x maxSegmentSize characters, so tune the two together against the provider’s token limits. | 32 | int |
| **embeddingModel** (producer) | **Autowired** The EmbeddingModel to embed segments with. When not set, the single bean of that type in the registry is used; zero or several beans fail the endpoint start with an error naming this option. |  | EmbeddingModel |
| **embeddingStore** (producer) | **Autowired** The EmbeddingStore to write segments to. When not set, the single bean of that type in the registry is used; zero or several beans fail the endpoint start with an error naming this option. |  | EmbeddingStore |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **maxOverlapSize** (producer) | How much of the previous segment each segment repeats, in characters. Overlap keeps a sentence split across a boundary retrievable from either side. | 50 | int |
| **maxSegmentSize** (producer) | Maximum size of one segment, in characters. | 500 | int |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **documentSplitter** (advanced) | The DocumentSplitter deciding how a document becomes segments, referenced as #bean:name - LangChain4j ships alternatives beside the default recursive one. When set, maxSegmentSize and maxOverlapSize are ignored (they parameterize the default splitter only). Segments returned without the identity metadata are re-stamped, so a custom splitter cannot break citation. Not looked up by type on purpose - an application may hold unrelated splitters. |  | DocumentSplitter |
| **idempotentRepository** (advanced) | The IdempotentRepository remembering already ingested document ids, referenced as #bean:name. When set, a delivery whose id was already written is answered with a skipped result instead of being re-ingested: first write wins per id. A blank document releases its claim, so a later, populated delivery under the same id still ingests. The claim is eager: a duplicate racing an in-flight first delivery is answered skipped even if that delivery then fails - with an at-least-once source the skipped duplicate is acknowledged and the failed original may be the only other copy, so pair eager deduplication with a source that redelivers on failure. Not looked up by type on purpose - an application may hold unrelated idempotent repositories. The repository is started but never stopped by the endpoint (it may be shared); a persistent repository’s lifecycle belongs to whoever created it. |  | IdempotentRepository |
| **maxDocumentSize** (advanced) | Maximum size of one document in characters, applied to the text about to be split; 0, the default, means no limit. The pipeline holds a document in memory whole, so the cap is the protection against oversized - on a consumer-fed pipeline, attacker-sized - payloads. An oversized document fails the exchange cleanly and, with a repository configured, releases its dedup claim. | 0 | int |

## Endpoint Options

The LangChain4j Ingest endpoint is configured using URI syntax:

langchain4j-ingest:pipelineName

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **pipelineName** (producer) | **Required** The pipeline name, stamped on every written segment as the camel\_ingest\_pipeline metadata and used in error messages. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **documentIdHeader** (producer) | Name of the header carrying the document id, such as CamelAwsS3Key for an S3 consumer or CamelKafkaKey for a Kafka one. The CamelLangChain4jIngestDocumentId exchange property, when set, takes precedence - a route that parses documents captures the id into that property before the parse, so a document cannot forge its own identity. An exchange without an id fails. | CamelLangChain4jIngestDocumentId | String |
| **embeddingBatchSize** (producer) | How many segments are embedded per request to the embedding model. Providers with generous per-request limits ingest large documents faster with a bigger batch; a batch carries at most embeddingBatchSize x maxSegmentSize characters, so tune the two together against the provider’s token limits. | 32 | int |
| **embeddingModel** (producer) | **Autowired** The EmbeddingModel to embed segments with. When not set, the single bean of that type in the registry is used; zero or several beans fail the endpoint start with an error naming this option. |  | EmbeddingModel |
| **embeddingStore** (producer) | **Autowired** The EmbeddingStore to write segments to. When not set, the single bean of that type in the registry is used; zero or several beans fail the endpoint start with an error naming this option. |  | EmbeddingStore |
| **maxOverlapSize** (producer) | How much of the previous segment each segment repeats, in characters. Overlap keeps a sentence split across a boundary retrievable from either side. | 50 | int |
| **maxSegmentSize** (producer) | Maximum size of one segment, in characters. | 500 | int |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **documentSplitter** (advanced) | The DocumentSplitter deciding how a document becomes segments, referenced as #bean:name - LangChain4j ships alternatives beside the default recursive one. When set, maxSegmentSize and maxOverlapSize are ignored (they parameterize the default splitter only). Segments returned without the identity metadata are re-stamped, so a custom splitter cannot break citation. Not looked up by type on purpose - an application may hold unrelated splitters. |  | DocumentSplitter |
| **idempotentRepository** (advanced) | The IdempotentRepository remembering already ingested document ids, referenced as #bean:name. When set, a delivery whose id was already written is answered with a skipped result instead of being re-ingested: first write wins per id. A blank document releases its claim, so a later, populated delivery under the same id still ingests. The claim is eager: a duplicate racing an in-flight first delivery is answered skipped even if that delivery then fails - with an at-least-once source the skipped duplicate is acknowledged and the failed original may be the only other copy, so pair eager deduplication with a source that redelivers on failure. Not looked up by type on purpose - an application may hold unrelated idempotent repositories. The repository is started but never stopped by the endpoint (it may be shared); a persistent repository’s lifecycle belongs to whoever created it. |  | IdempotentRepository |
| **maxDocumentSize** (advanced) | Maximum size of one document in characters, applied to the text about to be split; 0, the default, means no limit. The pipeline holds a document in memory whole, so the cap is the protection against oversized - on a consumer-fed pipeline, attacker-sized - payloads. An oversized document fails the exchange cleanly and, with a repository configured, releases its dedup claim. | 0 | int |

## Message Headers

The LangChain4j Ingest component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelLangChain4jIngestDocumentId** (producer) Constant: [`DOCUMENT_ID`](https://javadoc.io/doc/org.apache.camel/camel-langchain4j-ingest/latest/org/apache/camel/component/langchain4j/ingest/LangChain4jIngestHeaders.html#DOCUMENT_ID) | The stable document id of the ingested payload, read when the documentIdHeader endpoint option does not name another header. The CamelLangChain4jIngestDocumentId exchange property, when set, takes precedence over any header. |  | String |

## Usage

### Ingesting a directory

Point a file consumer at a folder and the files in it become a knowledge base:

```java
from("file:/var/data/product-docs?noop=true&recursive=true&readLock=changed&charset=UTF-8")
    .to("langchain4j-ingest:products?documentIdHeader=CamelFileName");
```

Each file is read as UTF-8 text, split into overlapping segments (`maxSegmentSize`, `maxOverlapSize`), embedded in batches (`embeddingBatchSize`, 32 by default) and written to the store; a document is held in memory whole while it is split. Providers with generous per-request limits ingest large documents faster with a bigger batch — a batch carries at most `embeddingBatchSize × maxSegmentSize` characters, so tune the two together against the provider’s token limits. A custom LangChain4j `DocumentSplitter` bean can replace the default recursive splitting (`documentSplitter=#bean:name`); the two size options are then ignored, and segments are re-stamped with the identity metadata regardless of what the splitter returns. `noop=true` leaves the documents where they are — a knowledge base reads its source, it does not consume it — and already implies the file consumer’s idempotent register, so unchanged files are not re-ingested within a run. The `changed` read lock keeps a file still being copied in from being half-ingested.

The `embeddingStore` and `embeddingModel` options may be omitted when the registry holds exactly one bean of each type — the endpoint autowires them. With zero or several candidates the endpoint fails to start with a message naming the option to set.

> **Note**
> This component keeps no record of what it wrote: an edited document re-ingests on top of its old segments, and removing a document from the source removes nothing from the store. What can be remembered is which document ids were already ingested — the `idempotentRepository` option below.

### Any consumer as the source

Any Camel consumer can feed the endpoint; where the document id lives in the exchange is the consumer’s business, and `documentIdHeader` names it:

```java
from("aws2-s3://product-docs?region=eu-west-1&deleteAfterRead=false")
    .to("langchain4j-ingest:s3docs?documentIdHeader=CamelAwsS3Key"
        + "&embeddingStore=#bean:productsStore&embeddingModel=#bean:miniLm");
```

Mind each component’s own defaults: the `aws2-s3` consumer **deletes objects after reading them** unless `deleteAfterRead=false` is set. Without a `documentIdHeader` the producer expects the `CamelLangChain4jIngestDocumentId` header and fails the exchange when no id is found — identity is what update and delete semantics are built on, so a generated fallback would silently break replacement.

After ingestion the message body is replaced with the `IngestResult`, so a request-reply caller receives the outcome of its call: the pipeline, the document id, the number of segments written and the outcome — `ingested`, `empty` (blank document, nothing written) or `skipped` (duplicate id, see below).

### Deduplicating deliveries

With an `idempotentRepository` configured, the producer claims each document id before writing: a redelivered record or re-listed object ingests once, and a duplicate is answered `skipped` instead of being written twice — first write wins per id. An update arriving under the same id is skipped, not replaced; streams that carry updates need a version-aware id. Only a delivery that wrote segments keeps its claim: a blank document answers `empty` and releases it, so an object created empty and populated later under the same id still ingests, and a failed write releases it so the delivery can be retried. The claim is eager — a duplicate racing an in-flight first delivery is answered `skipped` even if that delivery then fails.

```java
from("kafka:ingest-events?groupId=ingest")
    .to("langchain4j-ingest:events?documentIdHeader=CamelKafkaKey"
        + "&idempotentRepository=#bean:eventsRegister");
```

The repository is any `IdempotentRepository` bean — in-memory, file-backed or, to deduplicate across application instances, a JDBC one. It is referenced by name on purpose: an application may hold unrelated idempotent repositories, so none is picked up by type. The endpoint starts the repository but never stops it (the bean may be shared); a persistent repository’s lifecycle belongs to whoever created it.

Two limits of this deduplication are worth knowing. The claim is **eager**: a duplicate racing an in-flight first delivery is answered `skipped` even if that delivery then fails and releases the id — with an at-least-once source the skipped duplicate is acknowledged, so the failed original must be redelivered by its own source or the document ends up in neither the store nor a queue. And deduplication tracks **document ids, not segments**: the store is written in one call after all segments are embedded, so a mid-embedding failure writes nothing — but a store that fails half-way through that one write leaves the written half behind, and the retried delivery then duplicates it. The synchronising engine, which can replace a document’s segments by their identity metadata, is the eventual answer to both.

### Parsed documents and the id property

A parser such as Tika copies document metadata over the message headers, so a route that parses untrusted documents must capture the id **before** the parse — a crafted document could otherwise forge its own identity. The `CamelLangChain4jIngestDocumentId` exchange property exists for exactly this and always wins over the header:

```java
from("file:/var/data/reports?noop=true&readLock=changed")
    .setProperty(LangChain4jIngest.DOCUMENT_ID_PROPERTY, header(Exchange.FILE_NAME))
    .to("tika:parse?tikaParseOutputFormat=text&tikaParseOutputEncoding=UTF-8")
    .process(new TikaTextDecode())
    .to("langchain4j-ingest:reports");
```

`TikaTextDecode` ships with this component for exactly this route shape: it decodes Tika’s text output as the pinned UTF-8 without consulting the exchange — a plain `getBody(String.class)` resolves its charset from the `CamelCharsetName` **header** first (then the property), so a message-supplied `CamelCharsetName` surviving up to the conversion would steer the decode. `convertBodyTo(String.class, "UTF-8")` is no substitute: that option sets the exchange property, which the injected header outranks. Tika also copies the parsed document’s remaining metadata over the message headers (Camel-namespace names are filtered out by camel-tika); when the route continues past ingestion, sweep them with a `removeHeaders` step — the same hygiene the docling recipe applies to `CamelDocling*` — so document-chosen values do not leak into later steps.

### Limiting document size

The pipeline holds a document in memory whole — the parsed text, its segments and their embeddings all exist at once — so a single oversized document can exhaust the heap. The `maxDocumentSize` option caps it: unset (the default) means no limit, which is fine for a directory of documents you control, while a consumer-fed pipeline accepts whatever its source delivers and should set the cap.

The cap counts the text handed to the endpoint, in characters, before splitting — a route with a parse step in front should bound the raw payload as well, since a parse is itself memory- and CPU-expensive and a small file can still parse into a lot of text. An oversized document fails the exchange like any other error (see below) and releases its dedup claim, so a trimmed re-delivery under the same id still ingests.

### When ingestion fails

A failure while splitting, embedding or storing — a rate-limited model, an unreachable store — propagates to the consumer, and a claimed document id is released. For a file consumer the file stays where it is and is retried on the next poll; a permanently failing file is retried forever, loudly, on every poll, so remove or fix such a file, or use the file consumer’s `moveFailed` option to quarantine failures. For other consumers the component’s own error handling applies: a request-reply caller receives the exception, while a Kafka consumer with default settings logs the failure and commits the offset, so the record is dropped.