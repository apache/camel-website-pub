# Docling

**Since Camel 4.15**

**Only producer is supported**

The Docling component allows you to convert and process documents using [IBM’s Docling AI document parser](https://github.com/DS4SD/docling). Docling is a powerful Python library that can parse and convert various document formats including PDF, Word documents, PowerPoint presentations, and more into structured formats like Markdown, HTML, JSON, or plain text.

Maven users will need to add the following dependency to their `pom.xml` for this component:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-docling</artifactId>
    <version>x.x.x</version>
    <!-- use the same version as your Camel core version -->
</dependency>
```

## Prerequisites

This component supports two modes of operation:

1.  **CLI Mode (default)**: Requires Docling to be installed on your system via pip:
    
    ```bash
    pip install docling
    ```
    
2.  **API Mode**: Requires a running docling-serve instance. The component uses the official [docling-java](https://github.com/docling-project/docling-java) library for communication with docling-serve, providing robust API integration with native async support. You can run docling-serve using:
    
    ```bash
    # Install docling-serve
    pip install docling-serve
    
    # Run docling-serve
    docling-serve --host 0.0.0.0 --port 5001
    ```
    
    Or using Docker:
    
    ```bash
    docker run -p 5001:5001 ghcr.io/docling-project/docling-serve:latest
    ```
    

## URI format

docling:operation\[?options\]

Where `operation` represents the document processing operation to perform.

### Supported Operations

The component supports the following operations:

 
| Operation | Description |
| --- | --- |
| `CONVERT_TO_MARKDOWN` | Convert document to Markdown format (default) |
| `CONVERT_TO_HTML` | Convert document to HTML format |
| `CONVERT_TO_JSON` | Convert document to JSON format. Returns a `DoclingDocument` object (`ai.docling.core.DoclingDocument`) in both API and CLI modes. |
| `EXTRACT_TEXT` | Extract plain text content from document |
| `EXTRACT_STRUCTURED_DATA` | Extract structured data with table structure recognition enabled by default. Returns a `DoclingDocument` object in both API and CLI modes. Additional enrichment features (code, formula, picture classification) can be enabled via configuration. |
| `EXTRACT_METADATA` | Extract document metadata (title, author, page count, creation date, etc.) |
| `SUBMIT_ASYNC_CONVERSION` | Submit an async conversion and return task ID (docling-serve only) |
| `CHECK_CONVERSION_STATUS` | Check the status of an async conversion task (docling-serve only) |
| `CHUNK_HYBRID` | Chunk document using HybridChunker — token-aware and structure-aware (docling-serve only) |
| `CHUNK_HIERARCHICAL` | Chunk document using HierarchicalChunker — structure-aware (docling-serve only) |

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

The Docling component supports the following options which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **configuration** (producer) | The configuration for the Docling Endpoint. |  | DoclingConfiguration |
| **contentInBody** (producer) | Include the content of the output file in the exchange body and delete the output file. | false | boolean |
| **doclingServeUrl** (producer) | Docling-serve API URL (e.g., [http://localhost:5001](http://localhost:5001)). | [http://localhost:5001](http://localhost:5001) | String |
| **enableOCR** (producer) | Enable OCR processing for scanned documents. | true | boolean |
| **includeLayoutInfo** (producer) | Show layout information with bounding boxes. | false | boolean |
| **lazyStartProducer** (producer) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **ocrLanguage** (producer) | Language code for OCR processing. | en | String |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   CONVERT\_TO\_MARKDOWN
    
-   CONVERT\_TO\_HTML
    
-   CONVERT\_TO\_JSON
    
-   EXTRACT\_TEXT
    
-   EXTRACT\_STRUCTURED\_DATA
    
-   SUBMIT\_ASYNC\_CONVERSION
    
-   CHECK\_CONVERSION\_STATUS
    
-   BATCH\_CONVERT\_TO\_MARKDOWN
    
-   BATCH\_CONVERT\_TO\_HTML
    
-   BATCH\_CONVERT\_TO\_JSON
    
-   BATCH\_EXTRACT\_TEXT
    
-   BATCH\_EXTRACT\_STRUCTURED\_DATA
    
-   EXTRACT\_METADATA
    
-   CHUNK\_HYBRID
    
-   CHUNK\_HIERARCHICAL
    





 | CONVERT\_TO\_MARKDOWN | DoclingOperations |
| **outputFormat** (producer) | Output format for document conversion. | markdown | String |
| **useDoclingServe** (producer) | Use docling-serve API instead of CLI command. | false | boolean |
| **abortOnError** (advanced) | Abort processing on error. | false | Boolean |
| **asyncPollInterval** (advanced) | Polling interval for async conversion status in milliseconds. | 2000 | long |
| **asyncTaskTtl** (advanced) | Time-to-live for pending async conversion tasks in milliseconds. Tasks older than this will be evicted from memory to prevent leaks. | 86400000 | long |
| **asyncTimeout** (advanced) | Maximum time to wait for async conversion completion in milliseconds. | 300000 | long |
| **autowiredEnabled** (advanced) | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | boolean |
| **doclingCommand** (advanced) | Path to Docling Python executable or command. |  | String |
| **doCodeEnrichment** (advanced) | Enable code enrichment in document processing. | false | Boolean |
| **documentTimeout** (advanced) | Document processing timeout in seconds. |  | Long |
| **doFormulaEnrichment** (advanced) | Enable formula enrichment in document processing. | false | Boolean |
| **doOcr** (advanced) | Enable OCR processing in docling-serve API mode. When not set, the server uses its own defaults. Set enableOCR to false to explicitly disable OCR. | false | Boolean |
| **doPictureClassification** (advanced) | Enable picture classification in document processing. | false | Boolean |
| **doPictureDescription** (advanced) | Enable picture description generation in document processing. | false | Boolean |
| **doTableStructure** (advanced) | Enable table structure recognition. | false | Boolean |
| **forceOcr** (advanced) | Force OCR processing even for digital documents. | false | Boolean |
| **imageExportMode** (advanced) | Image export mode for referenced images. |  | String |
| **imagesScale** (advanced) | Scale factor for exported images. |  | Double |
| **includeImages** (advanced) | Include images in the conversion output. | false | Boolean |
| **mdPageBreakPlaceholder** (advanced) | Placeholder string for page breaks in markdown output. |  | String |
| **ocrEngine** (advanced) | OCR engine to use. |  | String |
| **pdfBackend** (advanced) | PDF parsing backend. |  | String |
| **pipeline** (advanced) | Processing pipeline to use. |  | String |
| **processTimeout** (advanced) | Timeout for Docling process execution in milliseconds. | 30000 | long |
| **tableCellMatching** (advanced) | Enable table cell matching post-processing. | false | Boolean |
| **tableMode** (advanced) | Table structure recognition mode. |  | String |
| **useAsyncMode** (advanced) | Use asynchronous conversion mode (docling-serve API only). | false | boolean |
| **workingDirectory** (advanced) | Working directory for Docling execution. |  | String |
| **batchFailOnFirstError** (batch) | Fail entire batch on first error (true) or continue processing remaining documents (false). | true | boolean |
| **batchParallelism** (batch) | Number of parallel threads for batch processing. | 4 | int |
| **batchSize** (batch) | Number of documents to submit per sub-batch. Documents are partitioned into sub-batches of this size and each sub-batch is processed before starting the next one. Within each sub-batch, up to batchParallelism threads are used concurrently. This controls memory usage and back-pressure when processing large document sets. | 10 | int |
| **batchTimeout** (batch) | Maximum time to wait for batch completion in milliseconds. | 300000 | long |
| **splitBatchResults** (batch) | Split batch results into individual exchanges (one per document) instead of single BatchProcessingResults. | false | boolean |
| **chunkingIncludeRawText** (chunking) | Include raw text in chunk output. | false | Boolean |
| **chunkingMaxTokens** (chunking) | Maximum number of tokens per chunk for hybrid chunking. |  | Integer |
| **chunkingMergePeers** (chunking) | Whether to merge peer chunks in hybrid chunking. | true | Boolean |
| **chunkingTokenizer** (chunking) | Tokenizer model for hybrid chunking (e.g. sentence-transformers/all-MiniLM-L6-v2). |  | String |
| **chunkingUseMarkdownTables** (chunking) | Use markdown format for tables in chunk output. | false | Boolean |
| **includeMetadataInHeaders** (metadata) | Include metadata in message headers when extracting metadata. | true | boolean |
| **includeRawMetadata** (metadata) | Include raw metadata as returned by the parser. | false | boolean |
| **allowFilePathSource** (security) | Whether a String message body that starts with / or contains \\ is interpreted as a local filesystem path to read. When disabled, such a body is rejected instead of being read. This does not affect the CamelDoclingInputFilePath header, nor File, byte or explicit path collection bodies used by the batch operations. | false | boolean |
| **allowUrlSource** (security) | Whether a String message body that starts with http:// or https:// is interpreted as a remote URL for Docling to fetch. When disabled, such a body is rejected instead of being fetched. This does not affect the CamelDoclingInputFilePath header, nor bodies of any other type. | false | boolean |
| **apiKeyHeader** (security) | Header name for API key authentication. | X-API-Key | String |
| **authenticationScheme** (security) | 

Authentication scheme (BEARER, API\_KEY, NONE).

Enum values:

-   NONE
    
-   BEARER
    
-   API\_KEY
    





 | NONE | AuthenticationScheme |
| **authenticationToken** (security) | Authentication token for docling-serve API (Bearer token or API key). |  | String |
| **inputBaseDirectory** (security) | When set, every local input file path must resolve inside this directory once normalized. Applies to the CamelDoclingInputFilePath header, to file path message bodies, and to the paths used by the batch operations. When empty, no directory restriction is applied. |  | String |
| **maxFileSize** (security) | Maximum file size in bytes for processing. | 52428800 | long |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used as authenticationToken. Requires camel-oauth on the classpath. |  | String |

## Endpoint Options

The Docling endpoint is configured using URI syntax:

docling:operationId

With the following _path_ and _query_ parameters:

### Path Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operationId** (producer) | **Required** The operation identifier. |  | String |

### Query Parameters

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **contentInBody** (producer) | Include the content of the output file in the exchange body and delete the output file. | false | boolean |
| **doclingServeUrl** (producer) | Docling-serve API URL (e.g., [http://localhost:5001](http://localhost:5001)). | [http://localhost:5001](http://localhost:5001) | String |
| **enableOCR** (producer) | Enable OCR processing for scanned documents. | true | boolean |
| **includeLayoutInfo** (producer) | Show layout information with bounding boxes. | false | boolean |
| **ocrLanguage** (producer) | Language code for OCR processing. | en | String |
| **operation** (producer) | 
**Required** The operation to perform.

Enum values:

-   CONVERT\_TO\_MARKDOWN
    
-   CONVERT\_TO\_HTML
    
-   CONVERT\_TO\_JSON
    
-   EXTRACT\_TEXT
    
-   EXTRACT\_STRUCTURED\_DATA
    
-   SUBMIT\_ASYNC\_CONVERSION
    
-   CHECK\_CONVERSION\_STATUS
    
-   BATCH\_CONVERT\_TO\_MARKDOWN
    
-   BATCH\_CONVERT\_TO\_HTML
    
-   BATCH\_CONVERT\_TO\_JSON
    
-   BATCH\_EXTRACT\_TEXT
    
-   BATCH\_EXTRACT\_STRUCTURED\_DATA
    
-   EXTRACT\_METADATA
    
-   CHUNK\_HYBRID
    
-   CHUNK\_HIERARCHICAL
    





 | CONVERT\_TO\_MARKDOWN | DoclingOperations |
| **outputFormat** (producer) | Output format for document conversion. | markdown | String |
| **useDoclingServe** (producer) | Use docling-serve API instead of CLI command. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **abortOnError** (advanced) | Abort processing on error. | false | Boolean |
| **asyncPollInterval** (advanced) | Polling interval for async conversion status in milliseconds. | 2000 | long |
| **asyncTaskTtl** (advanced) | Time-to-live for pending async conversion tasks in milliseconds. Tasks older than this will be evicted from memory to prevent leaks. | 86400000 | long |
| **asyncTimeout** (advanced) | Maximum time to wait for async conversion completion in milliseconds. | 300000 | long |
| **doclingCommand** (advanced) | Path to Docling Python executable or command. |  | String |
| **doCodeEnrichment** (advanced) | Enable code enrichment in document processing. | false | Boolean |
| **documentTimeout** (advanced) | Document processing timeout in seconds. |  | Long |
| **doFormulaEnrichment** (advanced) | Enable formula enrichment in document processing. | false | Boolean |
| **doOcr** (advanced) | Enable OCR processing in docling-serve API mode. When not set, the server uses its own defaults. Set enableOCR to false to explicitly disable OCR. | false | Boolean |
| **doPictureClassification** (advanced) | Enable picture classification in document processing. | false | Boolean |
| **doPictureDescription** (advanced) | Enable picture description generation in document processing. | false | Boolean |
| **doTableStructure** (advanced) | Enable table structure recognition. | false | Boolean |
| **forceOcr** (advanced) | Force OCR processing even for digital documents. | false | Boolean |
| **imageExportMode** (advanced) | Image export mode for referenced images. |  | String |
| **imagesScale** (advanced) | Scale factor for exported images. |  | Double |
| **includeImages** (advanced) | Include images in the conversion output. | false | Boolean |
| **mdPageBreakPlaceholder** (advanced) | Placeholder string for page breaks in markdown output. |  | String |
| **ocrEngine** (advanced) | OCR engine to use. |  | String |
| **pdfBackend** (advanced) | PDF parsing backend. |  | String |
| **pipeline** (advanced) | Processing pipeline to use. |  | String |
| **processTimeout** (advanced) | Timeout for Docling process execution in milliseconds. | 30000 | long |
| **tableCellMatching** (advanced) | Enable table cell matching post-processing. | false | Boolean |
| **tableMode** (advanced) | Table structure recognition mode. |  | String |
| **useAsyncMode** (advanced) | Use asynchronous conversion mode (docling-serve API only). | false | boolean |
| **workingDirectory** (advanced) | Working directory for Docling execution. |  | String |
| **batchFailOnFirstError** (batch) | Fail entire batch on first error (true) or continue processing remaining documents (false). | true | boolean |
| **batchParallelism** (batch) | Number of parallel threads for batch processing. | 4 | int |
| **batchSize** (batch) | Number of documents to submit per sub-batch. Documents are partitioned into sub-batches of this size and each sub-batch is processed before starting the next one. Within each sub-batch, up to batchParallelism threads are used concurrently. This controls memory usage and back-pressure when processing large document sets. | 10 | int |
| **batchTimeout** (batch) | Maximum time to wait for batch completion in milliseconds. | 300000 | long |
| **splitBatchResults** (batch) | Split batch results into individual exchanges (one per document) instead of single BatchProcessingResults. | false | boolean |
| **chunkingIncludeRawText** (chunking) | Include raw text in chunk output. | false | Boolean |
| **chunkingMaxTokens** (chunking) | Maximum number of tokens per chunk for hybrid chunking. |  | Integer |
| **chunkingMergePeers** (chunking) | Whether to merge peer chunks in hybrid chunking. | true | Boolean |
| **chunkingTokenizer** (chunking) | Tokenizer model for hybrid chunking (e.g. sentence-transformers/all-MiniLM-L6-v2). |  | String |
| **chunkingUseMarkdownTables** (chunking) | Use markdown format for tables in chunk output. | false | Boolean |
| **includeMetadataInHeaders** (metadata) | Include metadata in message headers when extracting metadata. | true | boolean |
| **includeRawMetadata** (metadata) | Include raw metadata as returned by the parser. | false | boolean |
| **allowFilePathSource** (security) | Whether a String message body that starts with / or contains \\ is interpreted as a local filesystem path to read. When disabled, such a body is rejected instead of being read. This does not affect the CamelDoclingInputFilePath header, nor File, byte or explicit path collection bodies used by the batch operations. | false | boolean |
| **allowUrlSource** (security) | Whether a String message body that starts with http:// or https:// is interpreted as a remote URL for Docling to fetch. When disabled, such a body is rejected instead of being fetched. This does not affect the CamelDoclingInputFilePath header, nor bodies of any other type. | false | boolean |
| **apiKeyHeader** (security) | Header name for API key authentication. | X-API-Key | String |
| **authenticationScheme** (security) | 

Authentication scheme (BEARER, API\_KEY, NONE).

Enum values:

-   NONE
    
-   BEARER
    
-   API\_KEY
    





 | NONE | AuthenticationScheme |
| **authenticationToken** (security) | Authentication token for docling-serve API (Bearer token or API key). |  | String |
| **inputBaseDirectory** (security) | When set, every local input file path must resolve inside this directory once normalized. Applies to the CamelDoclingInputFilePath header, to file path message bodies, and to the paths used by the batch operations. When empty, no directory restriction is applied. |  | String |
| **maxFileSize** (security) | Maximum file size in bytes for processing. | 52428800 | long |
| **oauthProfile** (security) | OAuth profile name for obtaining an access token via the OAuth 2.0 Client Credentials grant. When set, the token is acquired from the configured identity provider and used as authenticationToken. Requires camel-oauth on the classpath. |  | String |

## Message Headers

The Docling component supports the following message header(s), which is/are listed below:

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **CamelDoclingOperation** (producer) Constant: [`OPERATION`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#OPERATION) | The operation to perform. |  | DoclingOperations |
| **CamelDoclingOutputFormat** (producer) Constant: [`OUTPUT_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#OUTPUT_FORMAT) | The output format for conversion. |  | String |
| **CamelDoclingInputFilePath** (producer) Constant: [`INPUT_FILE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#INPUT_FILE_PATH) | The input file path or content. |  | String |
| **CamelDoclingOutputFilePath** (producer) Constant: [`OUTPUT_FILE_PATH`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#OUTPUT_FILE_PATH) | The output file path for saving result. |  | String |
| **CamelDoclingProcessingOptions** (producer) Constant: [`PROCESSING_OPTIONS`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#PROCESSING_OPTIONS) | Additional processing options. |  | Map |
| **CamelDoclingEnableOCR** (producer) Constant: [`ENABLE_OCR`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#ENABLE_OCR) | Whether to include OCR processing. |  | Boolean |
| **CamelDoclingOCRLanguage** (producer) Constant: [`OCR_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#OCR_LANGUAGE) | Language for OCR processing. |  | String |
| **CamelDoclingCustomArguments** (producer) Constant: [`CUSTOM_ARGUMENTS`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#CUSTOM_ARGUMENTS) | Custom command line arguments to pass to Docling. |  | List |
| **CamelDoclingUseAsyncMode** (producer) Constant: [`USE_ASYNC_MODE`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#USE_ASYNC_MODE) | Use asynchronous conversion mode (overrides endpoint configuration). |  | Boolean |
| **CamelDoclingAsyncPollInterval** (producer) Constant: [`ASYNC_POLL_INTERVAL`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#ASYNC_POLL_INTERVAL) | Polling interval for async conversion status in milliseconds. |  | Long |
| **CamelDoclingAsyncTimeout** (producer) Constant: [`ASYNC_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#ASYNC_TIMEOUT) | Maximum time to wait for async conversion completion in milliseconds. |  | Long |
| **CamelDoclingTaskId** (producer) Constant: [`TASK_ID`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#TASK_ID) | Task ID for checking async conversion status. |  | String |
| **CamelDoclingBatchSize** (producer) Constant: [`BATCH_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#BATCH_SIZE) | Override batch size for this operation. |  | Integer |
| **CamelDoclingBatchParallelism** (producer) Constant: [`BATCH_PARALLELISM`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#BATCH_PARALLELISM) | Override batch parallelism for this operation. |  | Integer |
| **CamelDoclingBatchFailOnFirstError** (producer) Constant: [`BATCH_FAIL_ON_FIRST_ERROR`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#BATCH_FAIL_ON_FIRST_ERROR) | Override batch fail on first error setting for this operation. |  | Boolean |
| **CamelDoclingBatchTimeout** (producer) Constant: [`BATCH_TIMEOUT`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#BATCH_TIMEOUT) | Override batch timeout for this operation in milliseconds. |  | Long |
| **CamelDoclingBatchTotalDocuments** (producer) Constant: [`BATCH_TOTAL_DOCUMENTS`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#BATCH_TOTAL_DOCUMENTS) | Total number of documents in the batch. |  | Integer |
| **CamelDoclingBatchSuccessCount** (producer) Constant: [`BATCH_SUCCESS_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#BATCH_SUCCESS_COUNT) | Number of successfully processed documents in the batch. |  | Integer |
| **CamelDoclingBatchFailureCount** (producer) Constant: [`BATCH_FAILURE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#BATCH_FAILURE_COUNT) | Number of failed documents in the batch. |  | Integer |
| **CamelDoclingBatchProcessingTime** (producer) Constant: [`BATCH_PROCESSING_TIME`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#BATCH_PROCESSING_TIME) | Total processing time for the batch in milliseconds. |  | Long |
| **CamelDoclingBatchSplitResults** (producer) Constant: [`BATCH_SPLIT_RESULTS`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#BATCH_SPLIT_RESULTS) | Split batch results into individual exchanges instead of single BatchProcessingResults. |  | Boolean |
| **CamelDoclingMetadataPageCount** (producer) Constant: [`METADATA_PAGE_COUNT`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_PAGE_COUNT) | Number of pages in the document. |  | Integer |
| **CamelDoclingMetadataTitle** (producer) Constant: [`METADATA_TITLE`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_TITLE) | Document title. |  | String |
| **CamelDoclingMetadataLanguage** (producer) Constant: [`METADATA_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_LANGUAGE) | Document language code. |  | String |
| **CamelDoclingMetadataDocumentType** (producer) Constant: [`METADATA_DOCUMENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_DOCUMENT_TYPE) | Document type/format. |  | String |
| **CamelDoclingMetadataFormat** (producer) Constant: [`METADATA_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_FORMAT) | Document format (MIME type). |  | String |
| **CamelDoclingMetadataFileSize** (producer) Constant: [`METADATA_FILE_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_FILE_SIZE) | File size in bytes. |  | Long |
| **CamelDoclingMetadataFileName** (producer) Constant: [`METADATA_FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_FILE_NAME) | File name. |  | String |
| **CamelDoclingMetadataRaw** (producer) Constant: [`METADATA_RAW`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_RAW) | Raw metadata fields as a Map. |  | Map |
| **CamelDoclingChunkingTokenizer** (producer) Constant: [`CHUNKING_TOKENIZER`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#CHUNKING_TOKENIZER) | Tokenizer for hybrid chunking (e.g. sentence-transformers/all-MiniLM-L6-v2). |  | String |
| **CamelDoclingChunkingMaxTokens** (producer) Constant: [`CHUNKING_MAX_TOKENS`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#CHUNKING_MAX_TOKENS) | Maximum tokens per chunk for hybrid chunking. |  | Integer |
| **CamelDoclingChunkingMergePeers** (producer) Constant: [`CHUNKING_MERGE_PEERS`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#CHUNKING_MERGE_PEERS) | Whether to merge peer chunks in hybrid chunking. |  | Boolean |

## Usage

### Input Types

The component accepts the following input types in the message body:

-   `String` - Document content. It is only read as a location when the endpoint opts in - see [Input Sources](#_input_sources) below
    
-   `byte[]` - Binary document content
    
-   `File` - File object
    
-   `InputStream` - Input stream containing document data
    

For the batch operations the body may also be a `List<String>` or `String[]` of file paths, a `List<File>` or `File[]`, or a single directory path `String`.

### Input Sources

A `String` body is ambiguous: it could be the document itself, a URL to fetch, or a path to read. By default the component treats it as the document, and the two location readings must be enabled explicitly:

  
| Option | Default | Effect when enabled |
| --- | --- | --- |
| `allowUrlSource` | `false` | A body starting with `http://` or `https://` is handed to Docling as a remote URL to fetch. |
| `allowFilePathSource` | `false` | A body starting with `/`, or containing `\`, is read from the local filesystem. This also covers the single directory-or-file `String` body accepted by the batch operations. |
| `inputBaseDirectory` | _(none)_ | When set, every local input path must resolve inside this directory once normalized. Applies to the `CamelDoclingInputFilePath` header, to file path bodies, and to the paths used by the batch operations. |

With both options left at their defaults, a body that is neither a URL nor a path is written to a temporary file and converted as document content, exactly as before.

The `CamelDoclingInputFilePath` header is an explicit "the document lives here" signal from the route, so it keeps working without `allowFilePathSource`. It is still subject to `inputBaseDirectory` when one is set. Typed bodies - `File`, `byte[]`, `InputStream`, and the explicit path collections used by the batch operations - are unambiguous and are likewise unaffected.

```java
// the body is the document itself - no opt-in needed
from("direct:content")
    .to("docling:convert?operation=CONVERT_TO_MARKDOWN");

// the body is a path, confined to /var/docs
from("direct:paths")
    .to("docling:convert?operation=CONVERT_TO_MARKDOWN&allowFilePathSource=true&inputBaseDirectory=/var/docs");
```

### Output Behavior

The component behavior depends on the `contentInBody` configuration option:

-   When `contentInBody=true` (default: false): The converted content is placed in the exchange body and the output file is automatically deleted
    
-   When `contentInBody=false`: The file path to the generated output file is returned in the exchange body
    

## Examples

### Basic document conversion to Markdown

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
      - to:
          uri: file:///data/output
```

### Convert to HTML with content in body

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_HTML?contentInBody=true")
    .process(exchange -> {
        String htmlContent = exchange.getIn().getBody(String.class);
        // Process the HTML content
    });
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_HTML
          parameters:
            contentInBody: true
      - process:
          ref: "htmlProcessor"
```

### Extract structured data from documents

When using docling-serve API mode, `EXTRACT_STRUCTURED_DATA` returns a `DoclingDocument` object with table structure recognition enabled by default. In CLI mode, the JSON output is parsed into a `DoclingDocument`.

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:EXTRACT_STRUCTURED_DATA?useDoclingServe=true&contentInBody=true")
    .process(exchange -> {
        DoclingDocument doc = exchange.getIn().getBody(DoclingDocument.class);

        // Access tables extracted from the document
        List<DoclingDocument.TableItem> tables = doc.getTables();
        for (DoclingDocument.TableItem table : tables) {
            DoclingDocument.TableData data = table.getData();
            log.info("Table: {}x{}", data.getNumRows(), data.getNumCols());
        }
    });
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:EXTRACT_STRUCTURED_DATA
          parameters:
            useDoclingServe: true
            contentInBody: true
      - process:
          ref: "structuredDataProcessor"
```

### Convert with OCR disabled

In CLI mode, use `enableOCR=false`. In API mode, setting `enableOCR=false` sends `doOcr(false)` to the server. You can also use the `doOcr` property directly for API mode control.

-   Java
    
-   YAML
    

```java
// CLI mode
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?enableOCR=false")
    .to("file:///data/output");

// API mode
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?useDoclingServe=true&doOcr=false&contentInBody=true")
    .to("file:///data/output");
```

```yaml
# CLI mode
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            enableOCR: false
      - to:
          uri: file:///data/output

# API mode
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            useDoclingServe: true
            doOcr: false
            contentInBody: true
      - to:
          uri: file:///data/output
```

### OCR and page headers/footers

Docling recognizes page headers and footers (page numbers, copyright lines, running titles, footnotes, and similar content) during OCR, classifying them as page _furniture_ in docling’s `FURNITURE` content layer.

Since docling v1.30.0, page furniture (headers and footers) is included in the default body export (Markdown, text and HTML). Earlier versions excluded the `FURNITURE` layer, so header and footer text was omitted from the converted output even though the OCR engine read it correctly.

### Using headers to control processing

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .setHeader("CamelDoclingOperation", constant(DoclingOperations.CONVERT_TO_HTML))
    .setHeader("CamelDoclingEnableOCR", constant(true))
    .setHeader("CamelDoclingOCRLanguage", constant("es"))
    .to("docling:CONVERT_TO_MARKDOWN")  // Operation will be overridden by header
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - setHeader:
          name: "CamelDoclingOperation"
          constant: "CONVERT_TO_HTML"
      - setHeader:
          name: "CamelDoclingEnableOCR"
          constant: true
      - setHeader:
          name: "CamelDoclingOCRLanguage"
          constant: "es"
      - to:
          uri: docling:CONVERT_TO_MARKDOWN  # Operation will be overridden by header
      - to:
          uri: file:///data/output
```

### Processing with custom arguments

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .process(exchange -> {
        List<String> customArgs = Arrays.asList("--verbose", "--preserve-tables");
        exchange.getIn().setHeader("CamelDoclingCustomArguments", customArgs);
    })
    .to("docling:CONVERT_TO_MARKDOWN")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - setHeader:
          name: "CamelDoclingCustomArguments"
          expression:
            method:
              ref: "customArgsBean"
              method: "createCustomArgs"
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
      - to:
          uri: file:///data/output
```

### Custom argument validation

When passing custom CLI arguments via the `CamelDoclingCustomArguments` header, the component enforces an **allowlist** of recognized docling CLI flags. Only the following flags are permitted:

 
| Category | Allowed flags |
| --- | --- |
| Input/output format | `--from`, `--to` |
| Pipeline | `--pipeline`, `--vlm-model`, `--asr-model` |
| OCR | `--ocr`, `--no-ocr`, `--force-ocr`, `--no-force-ocr`, `--ocr-engine`, `--ocr-lang`, `--psm` |
| Tables | `--tables`, `--no-tables`, `--table-mode` |
| PDF | `--pdf-backend`, `--pdf-password` |
| Enrichment | `--enrich-code`, `--no-enrich-code`, `--enrich-formula`, `--no-enrich-formula`, `--enrich-picture-classes`, `--no-enrich-picture-classes`, `--enrich-picture-description`, `--no-enrich-picture-description`, `--enrich-chart-extraction`, `--no-enrich-chart-extraction` |
| Output formatting | `--image-export-mode`, `--show-layout`, `--no-show-layout` |
| Advanced | `--headers`, `--artifacts-path`, `--enable-remote-services`, `--no-enable-remote-services`, `--allow-external-plugins`, `--no-allow-external-plugins`, `--show-external-plugins`, `--no-show-external-plugins`, `--document-timeout`, `--device`, `--num-threads`, `--page-batch-size` |
| Debug | `--verbose`, `-v` / `-vv` / `-vvv`, `--debug-visualize-cells`, `--no-debug-visualize-cells`, `--debug-visualize-ocr`, `--no-debug-visualize-ocr`, `--debug-visualize-layout`, `--no-debug-visualize-layout`, `--debug-visualize-tables`, `--no-debug-visualize-tables` |
| Performance | `--abort-on-error`, `--no-abort-on-error`, `--profiling`, `--no-profiling`, `--save-profiling`, `--no-save-profiling` |
| Info | `--version`, `--help`, `--logo` |

The `--output` (`-o`) flag is **not permitted** because the output directory is managed by the producer. Use the `CamelDoclingOutputFilePath` header or endpoint configuration instead.

Additionally, the following are rejected:

-   **Shell metacharacters**: `;`, `|`, `` ` `` , `$()` — blocked as defense-in-depth even though ProcessBuilder does not interpret them.
    
-   **Path traversal**: `../`, `..\`, and paths that resolve to traversal after normalization.
    
-   **Unknown flags**: any flag not in the allowlist above.
    

### Extracting document metadata

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:EXTRACT_METADATA")
    .process(exchange -> {
        DocumentMetadata metadata = exchange.getIn().getBody(DocumentMetadata.class);

        // Access metadata fields
        String title = metadata.getTitle();
        String documentType = metadata.getDocumentType();
        Integer pageCount = metadata.getPageCount();
        String format = metadata.getFormat();

        log.info("Document: {} ({}), Pages: {}, Format: {}",
            title, documentType, pageCount, format);

        // Metadata is also available in headers
        String titleFromHeader = exchange.getIn().getHeader("CamelDoclingMetadataTitle", String.class);
    });
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:EXTRACT_METADATA
      - log:
          message: "Document: ${header.CamelDoclingMetadataTitle} (${header.CamelDoclingMetadataDocumentType})"
      - log:
          message: "Pages: ${header.CamelDoclingMetadataPageCount}"
      - process:
          ref: "metadataProcessor"
```

### Extract metadata with all fields

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:EXTRACT_METADATA?includeRawMetadata=true")
    .process(exchange -> {
        DocumentMetadata metadata = exchange.getIn().getBody(DocumentMetadata.class);

        log.info("Page Count: {}", metadata.getPageCount());

        // Raw metadata from parser
        Map<String, Object> rawMetadata = metadata.getRawMetadata();
        log.info("Raw metadata: {}", rawMetadata);
    });
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:EXTRACT_METADATA
          parameters:
            includeRawMetadata: true
      - process:
          ref: "fullMetadataProcessor"
```

### Route documents based on metadata

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:EXTRACT_METADATA")
    .choice()
        .when(simple("${header.CamelDoclingMetadataPageCount} > 100"))
            .log("Large document with ${header.CamelDoclingMetadataPageCount} pages")
            .to("file:///data/large-docs")
        .when(simple("${header.CamelDoclingMetadataLanguage} == 'fr'"))
            .log("French document")
            .to("file:///data/french-docs")
        .when(simple("${header.CamelDoclingMetadataAuthor} contains 'Smith'"))
            .log("Document by Smith")
            .to("file:///data/smith-docs")
        .otherwise()
            .to("file:///data/other-docs")
    .end();
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:EXTRACT_METADATA
      - choice:
          when:
            - expression:
                simple:
                  expression: "${header.CamelDoclingMetadataPageCount} > 100"
              steps:
                - log:
                    message: "Large document with ${header.CamelDoclingMetadataPageCount} pages"
                - to:
                    uri: file:///data/large-docs
            - expression:
                simple:
                  expression: "${header.CamelDoclingMetadataLanguage} == 'fr'"
              steps:
                - log:
                    message: "French document"
                - to:
                    uri: file:///data/french-docs
            - expression:
                simple:
                  expression: "${header.CamelDoclingMetadataAuthor} contains 'Smith'"
              steps:
                - log:
                    message: "Document by Smith"
                - to:
                    uri: file:///data/smith-docs
          otherwise:
            steps:
              - to:
                  uri: file:///data/other-docs
```

### Extract metadata without headers

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:EXTRACT_METADATA?includeMetadataInHeaders=false")
    .process(exchange -> {
        DocumentMetadata metadata = exchange.getIn().getBody(DocumentMetadata.class);

        // All metadata is in the body object only
        // Headers are not populated with metadata fields
        log.info("Metadata: {}", metadata);
    });
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:EXTRACT_METADATA
          parameters:
            includeMetadataInHeaders: false
      - process:
          ref: "metadataBodyProcessor"
```

### Content in body vs file path output

-   Java
    
-   YAML
    

```java
// Get content directly in body (file is automatically deleted)
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?contentInBody=true")
    .process(exchange -> {
        String markdownContent = exchange.getIn().getBody(String.class);
        log.info("Converted content: {}", markdownContent);
    });

// Get file path (file is preserved)
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?contentInBody=false")
    .process(exchange -> {
        String outputFilePath = exchange.getIn().getBody(String.class);
        log.info("Output file saved at: {}", outputFilePath);
    });
```

```yaml
# Get content directly in body (file is automatically deleted)
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            contentInBody: true
      - process:
          ref: "contentProcessor"

# Get file path (file is preserved)
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            contentInBody: false
      - process:
          ref: "filePathProcessor"
```

### Processor Bean Examples

When using YAML DSL, the processor references used in the examples above would be implemented as Spring beans:

_Java-only: Spring bean Processor implementation_

```java
@Component("htmlProcessor")
public class HtmlProcessor implements Processor {
    @Override
    public void process(Exchange exchange) throws Exception {
        String htmlContent = exchange.getIn().getBody(String.class);
        // Process the HTML content
        log.info("Processing HTML content of length: {}", htmlContent.length());
    }
}

@Component("structuredDataProcessor")
public class StructuredDataProcessor implements Processor {
    private static final Logger log = LoggerFactory.getLogger(StructuredDataProcessor.class);

    @Override
    public void process(Exchange exchange) throws Exception {
        DoclingDocument doc = exchange.getIn().getBody(DoclingDocument.class);
        log.info("Document schema: {}, tables: {}", doc.getSchemaName(), doc.getTables().size());
    }
}

@Component("contentProcessor")
public class ContentProcessor implements Processor {
    private static final Logger log = LoggerFactory.getLogger(ContentProcessor.class);

    @Override
    public void process(Exchange exchange) throws Exception {
        String markdownContent = exchange.getIn().getBody(String.class);
        log.info("Converted content: {}", markdownContent);
    }
}

@Component("filePathProcessor")
public class FilePathProcessor implements Processor {
    private static final Logger log = LoggerFactory.getLogger(FilePathProcessor.class);

    @Override
    public void process(Exchange exchange) throws Exception {
        String outputFilePath = exchange.getIn().getBody(String.class);
        log.info("Output file saved at: {}", outputFilePath);
    }
}

@Component("customArgsBean")
public class CustomArgsBean {
    public List<String> createCustomArgs() {
        return Arrays.asList("--verbose", "--preserve-tables");
    }
}
```

## Document Chunking

The component supports document chunking via docling-serve, which splits documents into semantically meaningful chunks suitable for RAG (Retrieval-Augmented Generation) pipelines, vector databases, and other NLP workflows. Unlike naive text splitting, docling chunking is structure-aware — it respects document headings, paragraphs, and tables — and the hybrid chunker is also token-aware, ensuring chunks fit within model token limits.

> **Note**
> Both chunking operations require `useDoclingServe=true`. The Docling CLI does not expose chunking as a command — chunking is only available through the docling-serve REST API.

`CHUNK_HYBRID` uses the HybridChunker, which is both structure-aware and token-aware. It respects document structure while ensuring each chunk stays within a configurable token limit. Best for RAG pipelines with embedding models that have fixed token windows. Configure it with the `chunkingTokenizer`, `chunkingMaxTokens`, and `chunkingMergePeers` options (see the endpoint options table above).

`CHUNK_HIERARCHICAL` uses the HierarchicalChunker, which is structure-aware only. It splits at document structure boundaries (sections, paragraphs) without enforcing token limits. Best when chunk size is less important than preserving complete structural units.

When `contentInBody=true`, the exchange body is set to a `List<Chunk>` (`ai.docling.serve.api.chunk.response.Chunk`), ready for use with Camel’s `.split(body())` EIP. Each `Chunk` object provides:

-   `text` — the chunk text content
    
-   `chunkIndex` — zero-based position in the document
    
-   `filename` — source document filename
    
-   `headings` — list of heading strings leading to this chunk
    
-   `pageNumbers` — list of page numbers this chunk spans
    
-   `captions` — list of captions (e.g., table or figure captions)
    
-   `numTokens` — token count (hybrid chunker only)
    

When `contentInBody=false`, the full `ChunkDocumentResponse` is returned.

### Basic Chunking

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .setHeader("CamelDoclingInputFilePath", simple("${file:absolute.path}"))
    .to("docling:CHUNK_HYBRID?" +
        "useDoclingServe=true&" +
        "contentInBody=true&" +
        "chunkingTokenizer=sentence-transformers/all-MiniLM-L6-v2&" +
        "chunkingMaxTokens=128&" +
        "chunkingMergePeers=true")
    .split(body())
        .log("Chunk ${body.chunkIndex}: ${body.text}")
    .end();
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - setHeader:
          name: CamelDoclingInputFilePath
          expression:
            simple:
              expression: "${file:absolute.path}"
      - to:
          uri: docling:CHUNK_HYBRID
          parameters:
            useDoclingServe: true
            contentInBody: true
            chunkingTokenizer: "sentence-transformers/all-MiniLM-L6-v2"
            chunkingMaxTokens: 128
            chunkingMergePeers: true
      - split:
          expression:
            simple:
              expression: "${body}"
          steps:
            - log:
                message: "Chunk ${body.chunkIndex}: ${body.text}"
```

### Chunking for RAG Pipelines

A common use case is to chunk documents, generate embeddings, and store them in a vector database:

-   Java
    
-   YAML
    

```java
from("direct:ingest-pdf")
    .setHeader("CamelDoclingInputFilePath", header("pdfFilePath"))
    .to("docling:CHUNK_HYBRID?" +
        "useDoclingServe=true&" +
        "contentInBody=true&" +
        "chunkingTokenizer={{embedding.tokenizer}}&" +
        "chunkingMaxTokens={{embedding.max-tokens}}&" +
        "chunkingMergePeers=true")
    .split(body())
        .setBody(simple("${body.text}"))
        .to("openai:embeddings?embeddingModel={{embedding.model}}")
        // store embedding in vector database
        .to("direct:store-embedding")
    .end();
```

```yaml
- route:
    id: ingest-pdf
    from:
      uri: direct:ingest-pdf
    steps:
      - setHeader:
          name: CamelDoclingInputFilePath
          expression:
            simple:
              expression: "${header.pdfFilePath}"
      - to:
          uri: docling:CHUNK_HYBRID
          parameters:
            useDoclingServe: true
            contentInBody: true
            chunkingTokenizer: "{{embedding.tokenizer}}"
            chunkingMaxTokens: "{{embedding.max-tokens}}"
            chunkingMergePeers: true
      - split:
          expression:
            simple:
              expression: "${body}"
          steps:
            - setBody:
                expression:
                  simple:
                    expression: "${body.text}"
            - to:
                uri: openai:embeddings
                parameters:
                  embeddingModel: "{{embedding.model}}"
            - to:
                uri: direct:store-embedding
```

### Hierarchical Chunking

Use hierarchical chunking when you want to preserve complete structural units without token limits:

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .setHeader("CamelDoclingInputFilePath", simple("${file:absolute.path}"))
    .to("docling:CHUNK_HIERARCHICAL?" +
        "useDoclingServe=true&" +
        "contentInBody=true")
    .split(body())
        .log("Section [${body.headings}] page ${body.pageNumbers}: ${body.text}")
    .end();
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - setHeader:
          name: CamelDoclingInputFilePath
          expression:
            simple:
              expression: "${file:absolute.path}"
      - to:
          uri: docling:CHUNK_HIERARCHICAL
          parameters:
            useDoclingServe: true
            contentInBody: true
      - split:
          expression:
            simple:
              expression: "${body}"
          steps:
            - log:
                message: "Section [${body.headings}] page ${body.pageNumbers}: ${body.text}"
```

## Advanced Processing Options (API Mode)

When using docling-serve API mode (`useDoclingServe=true`), the component exposes advanced processing options that control how the server processes documents. These options are passed directly to the docling-serve API and provide fine-grained control over OCR, table recognition, enrichment features, and output formatting.

### OCR Options

  
| Parameter | Default | Description |
| --- | --- | --- |
| `doOcr` | _not set_ | Enable OCR processing in docling-serve API mode. When not set, the server uses its own defaults. Set `enableOCR` to `false` to explicitly disable OCR. |
| `forceOcr` | _not set_ | Force OCR processing even for digital documents (documents with selectable text). |
| `ocrEngine` | _not set_ | OCR engine to use. Supported values: `AUTO`, `EASYOCR`, `OCRMAC`, `RAPIDOCR`, `TESSEROCR`, `TESSERACT`. |
> **Note**
> The `enableOCR` and `ocrLanguage` settings are primarily for CLI mode. In API mode, use `doOcr` to explicitly control OCR behavior. When `doOcr` is not set, the server uses its own defaults. Setting `enableOCR=false` will send `doOcr(false)` to the server to disable OCR.

### Table and Structure Options

  
| Parameter | Default | Description |
| --- | --- | --- |
| `doTableStructure` | _not set_ | Enable table structure recognition. Automatically enabled for `EXTRACT_STRUCTURED_DATA` operations. |
| `tableMode` | _not set_ | Table structure recognition mode. Supported values: `ACCURATE`, `FAST`. |
| `tableCellMatching` | _not set_ | Enable table cell matching post-processing for better cell boundary detection. |

### Enrichment Options

  
| Parameter | Default | Description |
| --- | --- | --- |
| `doCodeEnrichment` | _not set_ | Enable code enrichment in document processing. Identifies and annotates code blocks. |
| `doFormulaEnrichment` | _not set_ | Enable formula enrichment in document processing. Detects and processes mathematical formulas. |
| `doPictureClassification` | _not set_ | Enable picture classification (e.g., chart, photo, diagram). May require additional ML models on the server. |
| `doPictureDescription` | _not set_ | Enable picture description generation. May require a Vision Language Model (VLM) on the server. |

### Pipeline and Output Options

  
| Parameter | Default | Description |
| --- | --- | --- |
| `pipeline` | _not set_ | Processing pipeline to use. Supported values: `ASR`, `STANDARD`, `VLM`. |
| `pdfBackend` | _not set_ | PDF parsing backend. Supported values: `DLPARSE_V1`, `DLPARSE_V2`, `DLPARSE_V4`, `PYPDFIUM2`. |
| `includeImages` | _not set_ | Include images in the conversion output. |
| `imageExportMode` | _not set_ | Image export mode for referenced images. Supported values: `EMBEDDED`, `PLACEHOLDER`, `REFERENCED`. |
| `imagesScale` | _not set_ | Scale factor for exported images (e.g., `2.0` for double resolution). |
| `mdPageBreakPlaceholder` | _not set_ | Placeholder string for page breaks in markdown output. |
| `abortOnError` | _not set_ | Abort processing on error instead of continuing with partial results. |
| `documentTimeout` | _not set_ | Document processing timeout in seconds (server-side timeout). |

### Example: Advanced Processing Configuration

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:EXTRACT_STRUCTURED_DATA?" +
        "useDoclingServe=true&" +
        "doOcr=true&" +
        "ocrEngine=TESSERACT&" +
        "doTableStructure=true&" +
        "tableMode=ACCURATE&" +
        "doCodeEnrichment=true&" +
        "pdfBackend=DLPARSE_V4&" +
        "processTimeout=120000&" +     // 2 minutes for complex PDFs
        "contentInBody=true")
    .process(exchange -> {
        DoclingDocument doc = exchange.getIn().getBody(DoclingDocument.class);
        // Process the structured document
    });
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:EXTRACT_STRUCTURED_DATA
          parameters:
            useDoclingServe: true
            doOcr: true
            ocrEngine: "TESSERACT"
            doTableStructure: true
            tableMode: "ACCURATE"
            doCodeEnrichment: true
            pdfBackend: "DLPARSE_V4"
            processTimeout: 120000
            contentInBody: true
      - process:
          ref: "structuredDataProcessor"
```

## DoclingDocument Return Type

When using docling-serve API mode, the `CONVERT_TO_JSON` and `EXTRACT_STRUCTURED_DATA` operations return a `DoclingDocument` object (from the `ai.docling.core` package) instead of a raw JSON string. This object provides type-safe access to the document structure.

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_JSON?" +
        "useDoclingServe=true&" +
        "contentInBody=true")
    .process(exchange -> {
        DoclingDocument doc = exchange.getIn().getBody(DoclingDocument.class);

        // Access document structure
        String schemaName = doc.getSchemaName();

        // Access tables
        List<DoclingDocument.TableItem> tables = doc.getTables();
        for (DoclingDocument.TableItem table : tables) {
            DoclingDocument.TableData data = table.getData();
            int rows = data.getNumRows();
            int cols = data.getNumCols();
            log.info("Table: {}x{}", rows, cols);
        }

        // Access pictures
        List<DoclingDocument.PictureItem> pictures = doc.getPictures();
        log.info("Found {} pictures", pictures.size());
    });
```

```yaml
- route:
    from:
      uri: file:///data/documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_JSON
          parameters:
            useDoclingServe: true
            contentInBody: true
      - process:
          ref: "doclingDocumentProcessor"
```

## Error Handling

The component handles various error scenarios:

-   **File size limit exceeded**: Files larger than `maxFileSize` are rejected
    
-   **Process timeout**: Long-running conversions are terminated after `processTimeout` milliseconds
    
-   **Invalid file formats**: Unsupported file formats result in processing errors
    
-   **Docling not found**: Missing Docling installation causes startup failures (CLI mode)
    
-   **Connection errors**: When using docling-serve API mode, connection failures to the API endpoint will result in errors
    
-   **Authentication errors**: Invalid or missing authentication credentials will result in 401 Unauthorized errors from the docling-serve API
    

## Performance Considerations

-   **Process Timeout**: The `processTimeout` setting (default: 30000ms / 30 seconds) controls both the CLI subprocess timeout and the HTTP read timeout for docling-serve API mode. For complex PDF documents that require OCR or enrichment processing, increase this value (e.g., `processTimeout=120000` for 2 minutes).
    
-   OCR processing significantly increases processing time for scanned documents.
    
-   Consider using `contentInBody=true` when using docling-serve API mode to get results directly in the body.
    
-   The `maxFileSize` setting helps prevent resource exhaustion.
    
-   **API Mode vs CLI Mode**: The docling-serve API mode typically offers better performance and resource utilization for high-volume document processing, as it maintains a persistent server instance.
    
-   **Async Mode**: For large documents or high-volume processing, enable `useAsyncMode=true` to prevent blocking the Camel thread pool. The component will poll the docling-serve API for completion status while freeing up processing threads.
    
-   **Async Configuration**: Adjust `asyncPollInterval` (default 2000ms) and `asyncTimeout` (default 300000ms/5 minutes) based on your document size and processing requirements.
    
-   **Batch Processing**: When processing multiple documents, async mode allows better parallelization as the docling-serve instance can process multiple documents concurrently while Camel polls for results.
    
-   **Enrichment Features**: Enabling advanced options like `doPictureClassification` or `doPictureDescription` may require additional ML models on the server and can increase processing time.
    

## Sub-Pages

For more details on specific features, see:

-   [Batch Processing](others/docling-batch-processing.md) - Batch operations, queue-based processing, error handling, and result splitting
    
-   [Asynchronous Processing](others/docling-async-processing.md) - Async mode, custom timeouts, polling patterns, and parallel processing
    
-   [Using Docling-Serve API](others/docling-serve.md) - Remote API usage, URL processing, and authentication methods
    

## HTTP Client Configuration

When using docling-serve API mode, the component uses the [docling-java](https://github.com/docling-project/docling-java) library which internally uses Java’s built-in `HttpClient`. The HTTP client is configured with sensible defaults and connection management is handled automatically by the library.

### Timeout Configuration

  
| Parameter | Default | Description |
| --- | --- | --- |
| `processTimeout` | 30000 | HTTP read timeout in milliseconds for synchronous API calls. Also used as the CLI subprocess timeout. Increase this for large or complex documents (e.g., 120000 for 2 minutes). |
| `asyncPollInterval` | 2000 | Poll interval in milliseconds when checking async task status. |
| `asyncTimeout` | 300000 | Maximum time to wait for async conversion completion in milliseconds (5 minutes). |
| `asyncTaskTtl` | 86400000 | Time-to-live for pending async conversion tasks in milliseconds (24 hours). Tasks older than this will be automatically evicted from memory to prevent leaks. A background cleanup task runs periodically to remove expired entries. |
> **Important**
> The default `processTimeout` of 30 seconds may not be sufficient for complex PDF documents, especially when OCR or enrichment options are enabled. For production use with PDF files, consider increasing `processTimeout` to at least 120000 (2 minutes).

### Configuration Examples

#### Long-Running Document Processing

For large documents that take a long time to process, increase the async timeout:

-   Java
    
-   YAML
    

```java
from("file:///data/large-documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "useAsyncMode=true&" +
        "asyncPollInterval=5000&" +      // Check every 5 seconds
        "asyncTimeout=600000&" +          // 10 minutes timeout
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: file:///data/large-documents
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: docling:CONVERT_TO_MARKDOWN
          parameters:
            useDoclingServe: true
            useAsyncMode: true
            asyncPollInterval: 5000
            asyncTimeout: 600000
            contentInBody: true
      - to:
          uri: file:///data/output
```

### Best Practices

1.  **Use async mode for large documents**: Enable `useAsyncMode=true` for documents that may take longer to process. The docling-java library handles polling automatically.
    
2.  **Adjust poll interval appropriately**: For high-volume scenarios, increase `asyncPollInterval` to reduce polling overhead. For interactive use cases, a shorter interval provides faster feedback.
    
3.  **Set appropriate timeouts**: Adjust `asyncTimeout` based on your largest expected document size. The default 5 minutes is suitable for most documents.
    
4.  **Monitor with logging**: Use DEBUG level logging to monitor API calls and async task status.