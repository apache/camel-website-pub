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

The Docling component supports 46 options, which are listed below.

   
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
    





 | CONVERT\_TO\_MARKDOWN | DoclingOperations |
| **outputFormat** (producer) | Output format for document conversion. | markdown | String |
| **useDoclingServe** (producer) | Use docling-serve API instead of CLI command. | false | boolean |
| **abortOnError** (advanced) | Abort processing on error. | false | Boolean |
| **asyncPollInterval** (advanced) | Polling interval for async conversion status in milliseconds. | 2000 | long |
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
| **batchSize** (batch) | Maximum number of documents to process in a single batch (batch operations only). | 10 | int |
| **batchTimeout** (batch) | Maximum time to wait for batch completion in milliseconds. | 300000 | long |
| **splitBatchResults** (batch) | Split batch results into individual exchanges (one per document) instead of single BatchProcessingResults. | false | boolean |
| **includeMetadataInHeaders** (metadata) | Include metadata in message headers when extracting metadata. | true | boolean |
| **includeRawMetadata** (metadata) | Include raw metadata as returned by the parser. | false | boolean |
| **apiKeyHeader** (security) | Header name for API key authentication. | X-API-Key | String |
| **authenticationScheme** (security) | 

Authentication scheme (BEARER, API\_KEY, NONE).

Enum values:

-   NONE
    
-   BEARER
    
-   API\_KEY
    





 | NONE | AuthenticationScheme |
| **authenticationToken** (security) | Authentication token for docling-serve API (Bearer token or API key). |  | String |
| **maxFileSize** (security) | Maximum file size in bytes for processing. | 52428800 | long |

## Endpoint Options

The Docling endpoint is configured using URI syntax:

docling:operationId

With the following _path_ and _query_ parameters:

### Path Parameters (1 parameters)

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **operationId** (producer) | **Required** The operation identifier. |  | String |

### Query Parameters (44 parameters)

   
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
    





 | CONVERT\_TO\_MARKDOWN | DoclingOperations |
| **outputFormat** (producer) | Output format for document conversion. | markdown | String |
| **useDoclingServe** (producer) | Use docling-serve API instead of CLI command. | false | boolean |
| **lazyStartProducer** (producer (advanced)) | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | boolean |
| **abortOnError** (advanced) | Abort processing on error. | false | Boolean |
| **asyncPollInterval** (advanced) | Polling interval for async conversion status in milliseconds. | 2000 | long |
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
| **batchSize** (batch) | Maximum number of documents to process in a single batch (batch operations only). | 10 | int |
| **batchTimeout** (batch) | Maximum time to wait for batch completion in milliseconds. | 300000 | long |
| **splitBatchResults** (batch) | Split batch results into individual exchanges (one per document) instead of single BatchProcessingResults. | false | boolean |
| **includeMetadataInHeaders** (metadata) | Include metadata in message headers when extracting metadata. | true | boolean |
| **includeRawMetadata** (metadata) | Include raw metadata as returned by the parser. | false | boolean |
| **apiKeyHeader** (security) | Header name for API key authentication. | X-API-Key | String |
| **authenticationScheme** (security) | 

Authentication scheme (BEARER, API\_KEY, NONE).

Enum values:

-   NONE
    
-   BEARER
    
-   API\_KEY
    





 | NONE | AuthenticationScheme |
| **authenticationToken** (security) | Authentication token for docling-serve API (Bearer token or API key). |  | String |
| **maxFileSize** (security) | Maximum file size in bytes for processing. | 52428800 | long |

## Message Headers

The Docling component supports 28 message header(s), which is/are listed below:

   
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
| **CamelDoclingMetadataLanguage** (producer) Constant: [`METADATA_LANGUAGE`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_LANGUAGE) | Document language code. |  | String |
| **CamelDoclingMetadataDocumentType** (producer) Constant: [`METADATA_DOCUMENT_TYPE`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_DOCUMENT_TYPE) | Document type/format. |  | String |
| **CamelDoclingMetadataFormat** (producer) Constant: [`METADATA_FORMAT`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_FORMAT) | Document format (MIME type). |  | String |
| **CamelDoclingMetadataFileSize** (producer) Constant: [`METADATA_FILE_SIZE`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_FILE_SIZE) | File size in bytes. |  | Long |
| **CamelDoclingMetadataFileName** (producer) Constant: [`METADATA_FILE_NAME`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_FILE_NAME) | File name. |  | String |
| **CamelDoclingMetadataRaw** (producer) Constant: [`METADATA_RAW`](https://javadoc.io/doc/org.apache.camel/camel-docling/latest/org/apache/camel/component/docling/DoclingHeaders.html#METADATA_RAW) | Raw metadata fields as a Map. |  | Map |

## Usage

### Input Types

The component accepts the following input types in the message body:

-   `String` - File path or document content
    
-   `byte[]` - Binary document content
    
-   `File` - File object
    
-   `InputStream` - Input stream containing document data
    

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
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
      - to:
          uri: "file:///data/output"
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
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_HTML"
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
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:EXTRACT_STRUCTURED_DATA"
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
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            enableOCR: false
      - to:
          uri: "file:///data/output"

# API mode
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            doOcr: false
            contentInBody: true
      - to:
          uri: "file:///data/output"
```

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
      uri: "file:///data/documents"
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
          uri: "docling:CONVERT_TO_MARKDOWN"  # Operation will be overridden by header
      - to:
          uri: "file:///data/output"
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
      uri: "file:///data/documents"
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
          uri: "docling:CONVERT_TO_MARKDOWN"
      - to:
          uri: "file:///data/output"
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
        String author = metadata.getAuthor();
        Integer pageCount = metadata.getPageCount();
        Instant creationDate = metadata.getCreationDate();

        log.info("Document: {} by {}, Pages: {}, Created: {}",
            title, author, pageCount, creationDate);

        // Metadata is also available in headers
        String titleFromHeader = exchange.getIn().getHeader("CamelDoclingMetadataTitle", String.class);
    });
```

```yaml
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:EXTRACT_METADATA"
      - log: "Document: ${header.CamelDoclingMetadataTitle} by ${header.CamelDoclingMetadataAuthor}"
      - log: "Pages: ${header.CamelDoclingMetadataPageCount}"
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
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:EXTRACT_METADATA"
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
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:EXTRACT_METADATA"
      - choice:
          when:
            - simple: "${header.CamelDoclingMetadataPageCount} > 100"
              steps:
                - log: "Large document with ${header.CamelDoclingMetadataPageCount} pages"
                - to: "file:///data/large-docs"
            - simple: "${header.CamelDoclingMetadataLanguage} == 'fr'"
              steps:
                - log: "French document"
                - to: "file:///data/french-docs"
            - simple: "${header.CamelDoclingMetadataAuthor} contains 'Smith'"
              steps:
                - log: "Document by Smith"
                - to: "file:///data/smith-docs"
          otherwise:
            steps:
              - to: "file:///data/other-docs"
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
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:EXTRACT_METADATA"
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
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            contentInBody: true
      - process:
          ref: "contentProcessor"

# Get file path (file is preserved)
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            contentInBody: false
      - process:
          ref: "filePathProcessor"
```

### Processor Bean Examples

When using YAML DSL, the processor references used in the examples above would be implemented as Spring beans:

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

## Batch Processing

The component supports batch processing of multiple documents when using docling-serve API mode. This is particularly useful for: - Processing multiple documents efficiently with parallel execution - Queue-based document processing workflows - High-volume document conversion scenarios - Better resource utilization with configurable parallelism

### Batch Operations

The following batch operations are available (all require `useDoclingServe=true`):

 
| Operation | Description |
| --- | --- |
| `BATCH_CONVERT_TO_MARKDOWN` | Convert multiple documents to Markdown format in parallel |
| `BATCH_CONVERT_TO_HTML` | Convert multiple documents to HTML format in parallel |
| `BATCH_CONVERT_TO_JSON` | Convert multiple documents to JSON format in parallel |
| `BATCH_EXTRACT_TEXT` | Extract text from multiple documents in parallel |
| `BATCH_EXTRACT_STRUCTURED_DATA` | Extract structured data from multiple documents in parallel with table structure recognition enabled by default |

### Basic Batch Processing

-   Java
    
-   YAML
    

```java
from("direct:documents")
    .process(exchange -> {
        List<String> documents = Arrays.asList(
            "/data/doc1.pdf",
            "/data/doc2.pdf",
            "/data/doc3.docx"
        );
        exchange.getIn().setBody(documents);
    })
    .to("docling:convert?" +
        "operation=BATCH_CONVERT_TO_MARKDOWN&" +
        "useDoclingServe=true&" +
        "batchParallelism=4&" +
        "batchFailOnFirstError=true")
    .process(exchange -> {
        BatchProcessingResults results = exchange.getIn().getBody(BatchProcessingResults.class);
        log.info("Processed {} documents, {} succeeded, {} failed",
            results.getTotalDocuments(),
            results.getSuccessCount(),
            results.getFailureCount());

        // Access individual results
        for (BatchConversionResult result : results.getResults()) {
            if (result.isSuccess()) {
                log.info("Document {}: {}", result.getOriginalPath(), result.getResult());
            } else {
                log.error("Document {} failed: {}", result.getOriginalPath(), result.getErrorMessage());
            }
        }
    });
```

```yaml
- route:
    id: batch-convert
    from:
      uri: "direct:documents"
    steps:
      - to:
          uri: "docling:convert"
          parameters:
            operation: "BATCH_CONVERT_TO_MARKDOWN"
            useDoclingServe: true
            batchParallelism: 4
            batchFailOnFirstError: true
      - log: "Processed ${header.CamelDoclingBatchSuccessCount}/${header.CamelDoclingBatchTotalDocuments} documents successfully"
      - split:
          simple: "${body.results}"
          steps:
            - choice:
                when:
                  - simple: "${body.success}"
                    steps:
                      - to: "file:///data/output?fileName=${body.documentId}.md"
                otherwise:
                  steps:
                    - log: "Failed: ${body.originalPath} - ${body.errorMessage}"
```

### Queue-Based Batch Processing

This example shows a queue-based batch processing workflow:

Java

```java
// Route 1: Collect documents from file system and send to queue
from("file:///data/incoming?noop=true&maxMessagesPerPoll=50")
    .convertBodyTo(String.class)
    .setHeader("documentPath", simple("${body}"))
    .to("seda:document-queue?waitForTaskToComplete=Never");

// Route 2: Aggregate documents from queue into batches
from("seda:document-queue?concurrentConsumers=1")
    .aggregate(constant(true))
        .completionSize(10)          // Batch size
        .completionTimeout(5000)     // Or timeout after 5 seconds
    .process(exchange -> {
        // Convert aggregated exchanges to document list
        @SuppressWarnings("unchecked")
        List<Exchange> exchanges = exchange.getProperty(Exchange.GROUPED_EXCHANGE, List.class);
        List<String> documentPaths = exchanges.stream()
            .map(e -> e.getIn().getHeader("documentPath", String.class))
            .collect(Collectors.toList());
        exchange.getIn().setBody(documentPaths);
    })
    .to("direct:batch-process");

// Route 3: Process batch with docling
from("direct:batch-process")
    .to("docling:convert?" +
        "operation=BATCH_CONVERT_TO_MARKDOWN&" +
        "useDoclingServe=true&" +
        "batchParallelism=5&" +
        "batchFailOnFirstError=false")
    .process(exchange -> {
        BatchProcessingResults results = exchange.getIn().getBody(BatchProcessingResults.class);
        log.info("Batch completed: {}/{} successful",
            results.getSuccessCount(), results.getTotalDocuments());
    })
    .split(simple("${body.results}"))
        .choice()
            .when(simple("${body.success}"))
                .to("file:///data/output?fileName=${body.documentId}.md")
            .otherwise()
                .to("file:///data/failed?fileName=${body.documentId}.error");
```

YAML

```yaml
# Define beans for processing
- beans:
  - name: documentListProcessor
    type: "#class:org.apache.camel.processor.aggregate.GroupedBodyAggregationStrategy"
    properties:
      strategyMethodName: "aggregate"

# Route 1: Collect documents
- route:
    from:
      uri: "file:///data/incoming"
      parameters:
        noop: true
        maxMessagesPerPoll: 50
    steps:
      - convertBodyTo:
          type: "java.lang.String"
      - setHeader:
          name: "documentPath"
          simple: "${body}"
      - to:
          uri: "seda:document-queue"
          parameters:
            waitForTaskToComplete: "Never"

# Route 2: Aggregate into batches
- route:
    from:
      uri: "seda:document-queue"
      parameters:
        concurrentConsumers: 1
    steps:
      - aggregate:
          aggregationStrategy:
            bean: "documentListProcessor"
          correlationExpression:
            constant: true
          completionSize: 10
          completionTimeout: 5000
      - to: "direct:batch-process"

# Route 3: Process batch
- route:
    from:
      uri: "direct:batch-process"
    steps:
      - to:
          uri: "docling:convert"
          parameters:
            operation: "BATCH_CONVERT_TO_MARKDOWN"
            useDoclingServe: true
            batchParallelism: 5
            batchFailOnFirstError: false
      - split:
          simple: "${body.results}"
          steps:
            - choice:
                when:
                  - simple: "${body.success}"
                    steps:
                      - to: "file:///data/output?fileName=${body.documentId}.md"
                otherwise:
                  steps:
                    - to: "file:///data/failed?fileName=${body.documentId}.error"
```

> **Note**
> For the aggregation example above, you can also use a custom processor. Create a Java class:

```java
public class DocumentListProcessor implements Processor {
    @Override
    public void process(Exchange exchange) throws Exception {
        @SuppressWarnings("unchecked")
        List<Exchange> exchanges = exchange.getProperty(Exchange.GROUPED_EXCHANGE, List.class);
        List<String> documentPaths = exchanges.stream()
            .map(e -> e.getIn().getHeader("documentPath", String.class))
            .collect(Collectors.toList());
        exchange.getIn().setBody(documentPaths);
    }
}
```

Then reference it in the YAML:

```yaml
- beans:
  - name: documentListProcessor
    type: "com.example.DocumentListProcessor"
```

### Batch Processing with Error Handling

Control how errors are handled during batch processing:

-   Java
    
-   YAML
    

```java
// Fail entire batch on first error
from("direct:batch-strict")
    .to("docling:convert?" +
        "operation=BATCH_CONVERT_TO_MARKDOWN&" +
        "useDoclingServe=true&" +
        "batchFailOnFirstError=true")
    .log("All documents converted successfully");

// Continue processing on errors
from("direct:batch-lenient")
    .to("docling:convert?" +
        "operation=BATCH_CONVERT_TO_MARKDOWN&" +
        "useDoclingServe=true&" +
        "batchFailOnFirstError=false")
    .process(exchange -> {
        BatchProcessingResults results = exchange.getIn().getBody(BatchProcessingResults.class);

        if (results.hasAnyFailures()) {
            log.warn("Batch completed with {} failures", results.getFailureCount());

            // Handle failed documents
            for (BatchConversionResult failure : results.getFailed()) {
                log.error("Failed: {} - {}",
                    failure.getOriginalPath(),
                    failure.getErrorMessage());
            }
        }
    });
```

```yaml
# Fail on first error
- route:
    id: batch-strict
    from:
      uri: "direct:batch-strict"
    steps:
      - to:
          uri: "docling:convert"
          parameters:
            operation: "BATCH_CONVERT_TO_MARKDOWN"
            useDoclingServe: true
            batchFailOnFirstError: true
      - log: "All documents converted successfully"

# Continue on errors and process failures
- route:
    id: batch-lenient
    from:
      uri: "direct:batch-lenient"
    steps:
      - to:
          uri: "docling:convert"
          parameters:
            operation: "BATCH_CONVERT_TO_MARKDOWN"
            useDoclingServe: true
            batchFailOnFirstError: false
      - log: "Batch completed: ${header.CamelDoclingBatchSuccessCount} succeeded, ${header.CamelDoclingBatchFailureCount} failed"
      - choice:
          when:
            - simple: "${header.CamelDoclingBatchFailureCount} > 0"
              steps:
                - split:
                    simple: "${body.failed}"
                    steps:
                      - log: "Failed document: ${body.originalPath} - ${body.errorMessage}"
                      - to: "file:///data/failed?fileName=${body.documentId}.error"
          otherwise:
            steps:
              - log: "All documents processed successfully"
```

### Batch Configuration Parameters

  
| Parameter | Default | Description |
| --- | --- | --- |
| `batchSize` | 10 | Maximum number of documents in a single batch |
| `batchParallelism` | 4 | Number of parallel threads for processing documents |
| `batchFailOnFirstError` | true | If true, fail entire batch on first error; if false, continue processing |
| `batchTimeout` | 300000 | Maximum time to wait for batch completion in milliseconds |
| `splitBatchResults` | false | Split batch results into individual exchanges (List) instead of single BatchProcessingResults object |

### Batch Processing Headers

Headers can be used to override batch configuration per-message:

  
| Header | Type | Description |
| --- | --- | --- |
| `CamelDoclingBatchSize` | Integer | Override batch size for this operation |
| `CamelDoclingBatchParallelism` | Integer | Override parallelism for this operation |
| `CamelDoclingBatchFailOnFirstError` | Boolean | Override fail-on-first-error setting |
| `CamelDoclingBatchTimeout` | Long | Override batch timeout in milliseconds |
| `CamelDoclingBatchTotalDocuments` | Integer | Total documents in batch (output header) |
| `CamelDoclingBatchSuccessCount` | Integer | Number of successful conversions (output header) |
| `CamelDoclingBatchFailureCount` | Integer | Number of failed conversions (output header) |
| `CamelDoclingBatchProcessingTime` | Long | Total processing time in milliseconds (output header) |
| `CamelDoclingBatchSplitResults` | Boolean | Override splitBatchResults setting for this operation |

### Input Formats for Batch Processing

The batch operations accept multiple input formats:

```java
// List of file paths
List<String> paths = Arrays.asList("/data/doc1.pdf", "/data/doc2.pdf");

// List of File objects
List<File> files = Arrays.asList(new File("doc1.pdf"), new File("doc2.pdf"));

// Array of paths
String[] pathArray = {"/data/doc1.pdf", "/data/doc2.pdf"};

// Array of File objects
File[] fileArray = {new File("doc1.pdf"), new File("doc2.pdf")};

// Directory path (processes all files in directory)
String dirPath = "/data/documents";
```

### BatchProcessingResults Object

The batch operations return a `BatchProcessingResults` object with:

**Properties:** - `results`: List of individual BatchConversionResult objects - `totalDocuments`: Total number of documents processed - `successCount`: Number of successful conversions - `failureCount`: Number of failed conversions - `totalProcessingTimeMs`: Total processing time in milliseconds

**Helper Methods:** - `getSuccessful()`: Returns list of successful results - `getFailed()`: Returns list of failed results - `isAllSuccessful()`: Returns true if all documents succeeded - `hasAnySuccessful()`: Returns true if at least one document succeeded - `hasAnyFailures()`: Returns true if at least one document failed - `getSuccessRate()`: Returns success rate as percentage (0.0-100.0)

**BatchConversionResult Properties:** - `documentId`: Unique identifier for the document - `originalPath`: Original file path or URL - `result`: Converted content (if successful) - `success`: Whether conversion succeeded - `errorMessage`: Error message (if failed) - `processingTimeMs`: Processing time for this document - `batchIndex`: Index in the batch (0-based)

### Splitting Batch Results into Individual Exchanges

By default, batch operations return a single `BatchProcessingResults` object containing all results. You can enable `splitBatchResults=true` to return a `List<BatchConversionResult>` instead, allowing you to process each document individually using Camel’s split EIP.

**Use Cases:** - Process each document result independently - Route successful and failed documents to different destinations - Apply individual transformations per document - Integrate with streaming or async processing patterns

-   Java
    
-   YAML
    

```java
// Example 1: Split and process each document individually
from("direct:batch-documents")
    .to("docling:convert?" +
        "operation=BATCH_CONVERT_TO_MARKDOWN&" +
        "useDoclingServe=true&" +
        "splitBatchResults=true&" +
        "contentInBody=true")
    .split(body())
        .process(exchange -> {
            BatchConversionResult result = exchange.getIn().getBody(BatchConversionResult.class);
            log.info("Processing document: {}", result.getDocumentId());

            if (result.isSuccess()) {
                // Process successful conversion
                String content = result.getResult();
                // ... do something with content
            } else {
                // Handle failed conversion
                log.error("Failed to convert {}: {}",
                    result.getOriginalPath(), result.getErrorMessage());
            }
        })
    .end();

// Example 2: Route based on success/failure
from("direct:batch-with-routing")
    .to("docling:convert?" +
        "operation=BATCH_CONVERT_TO_MARKDOWN&" +
        "useDoclingServe=true&" +
        "splitBatchResults=true&" +
        "batchFailOnFirstError=false&" +
        "contentInBody=true")
    .split(body())
        .choice()
            .when(simple("${body.success} == true"))
                .log("Success: ${body.documentId}")
                .to("file:///data/success?fileName=${body.documentId}.md")
            .otherwise()
                .log("Failed: ${body.documentId} - ${body.errorMessage}")
                .to("file:///data/failed?fileName=${body.documentId}.error")
        .end()
    .end();

// Example 3: Parallel processing with threads
from("direct:batch-parallel-individual")
    .to("docling:convert?" +
        "operation=BATCH_CONVERT_TO_MARKDOWN&" +
        "useDoclingServe=true&" +
        "splitBatchResults=true&" +
        "contentInBody=true")
    .split(body())
        .parallelProcessing()
        .threads(5)
        .process(exchange -> {
            BatchConversionResult result = exchange.getIn().getBody(BatchConversionResult.class);
            // Process each document in parallel
            processDocument(result);
        })
    .end();
```

```yaml
# Example 1: Split and route based on success
- route:
    from:
      uri: "direct:batch-with-split"
    steps:
      - to:
          uri: "docling:convert"
          parameters:
            operation: "BATCH_CONVERT_TO_MARKDOWN"
            useDoclingServe: true
            splitBatchResults: true
            contentInBody: true
      - split:
          simple: "${body}"
          steps:
            - choice:
                when:
                  - simple: "${body.success}"
                    steps:
                      - log: "Success: ${body.documentId}"
                      - to: "file:///data/success?fileName=${body.documentId}.md"
                otherwise:
                  steps:
                    - log: "Failed: ${body.documentId}"
                    - to: "file:///data/failed?fileName=${body.documentId}.error"

# Example 2: Split with parallel processing
- route:
    id: batch-split-parallel
    from:
      uri: "direct:batch-parallel"
    steps:
      - to:
          uri: "docling:convert"
          parameters:
            operation: "BATCH_CONVERT_TO_MARKDOWN"
            useDoclingServe: true
            splitBatchResults: true
            batchParallelism: 4
            contentInBody: true
      - split:
          simple: "${body}"
          parallelProcessing: true
          steps:
            - log: "Processing document ${body.documentId} (index ${body.batchIndex})"
            - choice:
                when:
                  - simple: "${body.success}"
                    steps:
                      - log: "Successfully converted ${body.documentId}"
                      - to: "file:///data/processed?fileName=${body.documentId}.md"
                otherwise:
                  steps:
                    - log: "Failed to convert ${body.documentId}: ${body.errorMessage}"
                    - to: "file:///data/errors?fileName=${body.documentId}.error"
```

**Comparison: BatchProcessingResults vs Split Results**

  
| Scenario | splitBatchResults=false | splitBatchResults=true |
| --- | --- | --- |
| Return type | `BatchProcessingResults` | `List<BatchConversionResult>` |
| Number of exchanges | 1 exchange with all results | Use `.split(body())` to create 1 exchange per document |
| Use case | Aggregate statistics, batch-level processing | Individual document processing, routing per result |
| Access to batch stats | Direct via object methods | Via headers (CamelDoclingBatch\*) |
| Camel pattern | Process entire batch together | Split and process individually |

**Note:** When using `splitBatchResults=true`, batch statistics are still available via headers: - `CamelDoclingBatchTotalDocuments` - `CamelDoclingBatchSuccessCount` - `CamelDoclingBatchFailureCount` - `CamelDoclingBatchProcessingTime`

## Asynchronous Processing

The component supports asynchronous document conversion when using docling-serve API mode. This is particularly useful for: - Large documents that take a long time to process - High-volume batch processing scenarios - Better resource utilization on the server side

### Enabling Async Mode

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "useAsyncMode=true&" +
        "asyncPollInterval=2000&" +
        "asyncTimeout=300000&" +
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            useAsyncMode: true
            asyncPollInterval: 2000
            asyncTimeout: 300000
            contentInBody: true
      - to:
          uri: "file:///data/output"
```

### Async Processing with Custom Timeout

For very large documents, you may need to increase the timeout:

-   Java
    
-   YAML
    

```java
from("file:///data/large-documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "useAsyncMode=true&" +
        "asyncPollInterval=5000&" +
        "asyncTimeout=600000&" +  // 10 minutes
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: "file:///data/large-documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            useAsyncMode: true
            asyncPollInterval: 5000
            asyncTimeout: 600000
            contentInBody: true
      - to:
          uri: "file:///data/output"
```

### Using Headers to Control Async Behavior

You can override async settings per-message using headers:

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .process(exchange -> {
        File file = exchange.getIn().getBody(File.class);
        // Use async mode only for large files
        if (file.length() > 10 * 1024 * 1024) { // > 10MB
            exchange.getIn().setHeader("CamelDoclingUseAsyncMode", true);
            exchange.getIn().setHeader("CamelDoclingAsyncTimeout", 600000L);
        }
    })
    .to("docling:CONVERT_TO_MARKDOWN?useDoclingServe=true&contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - process:
          ref: "asyncDecisionProcessor"
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            contentInBody: true
      - to:
          uri: "file:///data/output"
```

### Custom Async Workflows

For advanced use cases, you can use the `SUBMIT_ASYNC_CONVERSION` and `CHECK_CONVERSION_STATUS` operations to build custom async workflows with full control over task submission and status polling.

**When to use custom workflows:**

-   You need custom polling intervals that vary per task
    
-   You want to implement custom retry or backoff strategies
    
-   You need to coordinate multiple async tasks
    
-   You want to store task IDs in a database for later retrieval
    
-   You need fine-grained control over timeout and error handling
    

**When to use built-in async mode (useAsyncMode=true):**

-   Standard use cases where automatic polling is sufficient
    
-   You want the simplest configuration
    
-   Default polling intervals and timeouts work for your needs
    

> **Note**
> Custom polling workflows require Java processors and are more complex. The built-in async mode (`useAsyncMode=true`) is recommended for most use cases.

#### Simple Manual Polling (Java)

The simplest custom workflow uses a Java loop to poll for status:

```java
// Submit conversion
String taskId = template.requestBody(
    "docling:convert?operation=SUBMIT_ASYNC_CONVERSION&useDoclingServe=true",
    "/path/to/document.pdf", String.class);

// Poll for completion
ConversionStatus status;
int attempts = 0;
do {
    Thread.sleep(1000);
    status = template.requestBody(
        "docling:convert?operation=CHECK_CONVERSION_STATUS&useDoclingServe=true",
        taskId, ConversionStatus.class);
    attempts++;
} while (status.isInProgress() && attempts < 60);

// Get result
if (status.isCompleted()) {
    String result = status.getResult();
    // Process result...
}
```

#### Submit and Poll Pattern (Camel Route)

-   Java
    
-   YAML
    

```java
// Submit async conversion and poll until complete
from("file:///data/documents?include=.*\\.pdf")
    .log("Starting async conversion for: ${header.CamelFileName}")
    // Step 1: Submit conversion
    .to("docling:convert?operation=SUBMIT_ASYNC_CONVERSION&useDoclingServe=true")
    .log("Submitted conversion with task ID: ${body}")
    .setHeader("taskId", body())
    .setProperty("maxAttempts", constant(60))
    .setProperty("attempt", constant(0))
    // Step 2: Poll for completion
    .loopDoWhile(method(MyPollingHelper.class, "shouldContinuePolling"))
        .process(exchange -> {
            // Increment attempt counter
            Integer attempt = exchange.getProperty("attempt", Integer.class);
            exchange.setProperty("attempt", attempt != null ? attempt + 1 : 1);
        })
        .log("Polling attempt ${exchangeProperty.attempt} of ${exchangeProperty.maxAttempts}")
        .setBody(header("taskId"))
        .to("docling:convert?operation=CHECK_CONVERSION_STATUS&useDoclingServe=true")
        .setProperty("conversionStatus", body())
        .process(exchange -> {
            ConversionStatus status = exchange.getProperty("conversionStatus", ConversionStatus.class);
            if (status.isCompleted()) {
                exchange.setProperty("isCompleted", true);
            } else if (status.isFailed()) {
                exchange.setProperty("isFailed", true);
                exchange.setProperty("errorMessage", status.getErrorMessage());
            }
        })
        .choice()
            .when(exchangeProperty("isCompleted").isEqualTo(true))
                .stop()
            .when(exchangeProperty("isFailed").isEqualTo(true))
                .throwException(new RuntimeException("Conversion failed"))
        .end()
        .delay(1000)
    .end()
    // Step 3: Extract result
    .process(exchange -> {
        ConversionStatus status = exchange.getProperty("conversionStatus", ConversionStatus.class);
        if (status != null && status.isCompleted() && status.getResult() != null) {
            exchange.getIn().setBody(status.getResult());
        } else {
            throw new RuntimeException("Conversion did not complete");
        }
    })
    .to("file:///data/output");

// Helper class for loop condition
public class MyPollingHelper {
    public static boolean shouldContinuePolling(Exchange exchange) {
        Integer attempt = exchange.getProperty("attempt", Integer.class);
        Integer maxAttempts = exchange.getProperty("maxAttempts", Integer.class);
        Boolean isCompleted = exchange.getProperty("isCompleted", Boolean.class);
        Boolean isFailed = exchange.getProperty("isFailed", Boolean.class);

        if (Boolean.TRUE.equals(isCompleted) || Boolean.TRUE.equals(isFailed)) {
            return false;
        }
        if (attempt != null && maxAttempts != null && attempt >= maxAttempts) {
            return false;
        }
        return true;
    }
}
```

```yaml
# Note: For YAML, consider using the built-in async mode (useAsyncMode=true)
# which handles polling automatically. Custom polling is easier in Java DSL.

- route:
    id: async-with-custom-polling
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - log: "Starting async conversion for: ${header.CamelFileName}"
      - to:
          uri: "docling:convert"
          parameters:
            operation: "SUBMIT_ASYNC_CONVERSION"
            useDoclingServe: true
      - log: "Submitted conversion with task ID: ${body}"
      - setHeader:
          name: "taskId"
          simple: "${body}"
      # For YAML, simpler to use Java processor bean or built-in async mode
      - to:
          uri: "bean:asyncPollingProcessor"
      - to: "file:///data/output"
```

#### ConversionStatus Object

The `CHECK_CONVERSION_STATUS` operation returns a `ConversionStatus` object with the following properties:

-   **taskId** (String) - The task identifier
    
-   **status** (enum) - PENDING, IN\_PROGRESS, COMPLETED, FAILED, or UNKNOWN
    
-   **result** (String) - Converted document content (available when status is COMPLETED)
    
-   **errorMessage** (String) - Error details (available when status is FAILED)
    
-   **progress** (Integer) - Task queue position
    

Helper methods: - `isCompleted()` - Returns true if conversion completed successfully - `isFailed()` - Returns true if conversion failed - `isInProgress()` - Returns true if conversion is still processing

#### Parallel Processing with Custom Workflow

-   Java
    
-   YAML
    

```java
// Submit multiple conversions
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:convert?operation=SUBMIT_ASYNC_CONVERSION&useDoclingServe=true")
    .to("seda:task-queue");

// Process task queue with multiple threads
from("seda:task-queue?concurrentConsumers=5")
    .log("Processing task: ${body}")
    .setHeader("taskId", body())
    .setProperty("maxAttempts", constant(60))
    .setProperty("attempt", constant(0))
    .loopDoWhile(method(MyPollingHelper.class, "shouldContinuePolling"))
        .process(exchange -> {
            Integer attempt = exchange.getProperty("attempt", Integer.class);
            exchange.setProperty("attempt", attempt != null ? attempt + 1 : 1);
        })
        .setBody(header("taskId"))
        .to("docling:convert?operation=CHECK_CONVERSION_STATUS&useDoclingServe=true")
        .setProperty("conversionStatus", body())
        .process(exchange -> {
            ConversionStatus status = exchange.getProperty("conversionStatus", ConversionStatus.class);
            if (status.isCompleted()) {
                exchange.setProperty("isCompleted", true);
            } else if (status.isFailed()) {
                exchange.setProperty("isFailed", true);
            }
        })
        .choice()
            .when(exchangeProperty("isCompleted").isEqualTo(true))
                .stop()
            .when(exchangeProperty("isFailed").isEqualTo(true))
                .stop()
        .end()
        .delay(1000)
    .end()
    .process(exchange -> {
        ConversionStatus status = exchange.getProperty("conversionStatus", ConversionStatus.class);
        if (status != null && status.isCompleted()) {
            exchange.getIn().setBody(status.getResult());
        }
    })
    .choice()
        .when(body().isNotNull())
            .to("file:///data/output?fileName=${header.CamelFileName}")
    .end();
```

```yaml
# For parallel processing in YAML, recommend using built-in async mode
# which is simpler and handles concurrency automatically

- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:convert"
          parameters:
            operation: "CONVERT_TO_MARKDOWN"
            useDoclingServe: true
            useAsyncMode: true
            asyncPollInterval: 1000
            asyncTimeout: 120000
            contentInBody: true
      - to:
          uri: "file:///data/output"
          parameters:
            fileName: "${header.CamelFileName}"
```

> **Tip**
> For a complete working example of custom polling workflow, see the `testCustomPollingWorkflowWithRoute()` test in `DoclingServeProducerIT.java` in the camel-docling test sources.

## Using Docling-Serve API

### Basic usage with docling-serve

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?useDoclingServe=true&doclingServeUrl=http://localhost:5001&contentInBody=true")
    .process(exchange -> {
        String markdown = exchange.getIn().getBody(String.class);
        log.info("Converted content: {}", markdown);
    });
```

```yaml
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            doclingServeUrl: "http://localhost:5001"
            contentInBody: true
      - process:
          ref: "markdownProcessor"
```

### Converting documents from URLs using docling-serve

When using docling-serve API mode, you can also process documents from URLs:

-   Java
    
-   YAML
    

```java
from("timer:convert?repeatCount=1")
    .setBody(constant("https://arxiv.org/pdf/2501.17887"))
    .to("docling:CONVERT_TO_MARKDOWN?useDoclingServe=true&contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: "timer:convert"
      parameters:
        repeatCount: 1
    steps:
      - setBody:
          constant: "https://arxiv.org/pdf/2501.17887"
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            contentInBody: true
      - to:
          uri: "file:///data/output"
```

### Batch processing with docling-serve

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.(pdf|docx)")
    .to("docling:CONVERT_TO_HTML?useDoclingServe=true&doclingServeUrl=http://localhost:5001&contentInBody=true")
    .to("file:///data/converted?fileName=${file:name.noext}.html");
```

```yaml
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.(pdf|docx)"
    steps:
      - to:
          uri: "docling:CONVERT_TO_HTML"
          parameters:
            useDoclingServe: true
            doclingServeUrl: "http://localhost:5001"
            contentInBody: true
      - to:
          uri: "file:///data/converted"
          parameters:
            fileName: "${file:name.noext}.html"
```

### Authentication with docling-serve

The component supports multiple authentication mechanisms for secured docling-serve instances.

#### Bearer Token Authentication

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "doclingServeUrl=http://localhost:5001&" +
        "authenticationScheme=BEARER&" +
        "authenticationToken=your-bearer-token-here&" +
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            doclingServeUrl: "http://localhost:5001"
            authenticationScheme: "BEARER"
            authenticationToken: "your-bearer-token-here"
            contentInBody: true
      - to:
          uri: "file:///data/output"
```

#### API Key Authentication

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "doclingServeUrl=http://localhost:5001&" +
        "authenticationScheme=API_KEY&" +
        "authenticationToken=your-api-key-here&" +
        "apiKeyHeader=X-API-Key&" +
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            doclingServeUrl: "http://localhost:5001"
            authenticationScheme: "API_KEY"
            authenticationToken: "your-api-key-here"
            apiKeyHeader: "X-API-Key"
            contentInBody: true
      - to:
          uri: "file:///data/output"
```

#### Using Custom API Key Header

If your docling-serve instance uses a custom header name for API keys:

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "doclingServeUrl=http://localhost:5001&" +
        "authenticationScheme=API_KEY&" +
        "authenticationToken=your-api-key-here&" +
        "apiKeyHeader=X-Custom-API-Key&" +
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            doclingServeUrl: "http://localhost:5001"
            authenticationScheme: "API_KEY"
            authenticationToken: "your-api-key-here"
            apiKeyHeader: "X-Custom-API-Key"
            contentInBody: true
      - to:
          uri: "file:///data/output"
```

#### Using Authentication Token from Properties

For better security, store authentication tokens in properties or environment variables:

-   Java
    
-   YAML
    

```java
from("file:///data/documents?include=.*\\.pdf")
    .to("docling:CONVERT_TO_MARKDOWN?" +
        "useDoclingServe=true&" +
        "doclingServeUrl={{docling.serve.url}}&" +
        "authenticationScheme=BEARER&" +
        "authenticationToken={{docling.serve.token}}&" +
        "contentInBody=true")
    .to("file:///data/output");
```

```yaml
- route:
    from:
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            doclingServeUrl: "{{docling.serve.url}}"
            authenticationScheme: "BEARER"
            authenticationToken: "{{docling.serve.token}}"
            contentInBody: true
      - to:
          uri: "file:///data/output"
```

Then define in `application.properties`:

```properties
docling.serve.url=http://localhost:5001
docling.serve.token=your-bearer-token-here
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
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:EXTRACT_STRUCTURED_DATA"
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
      uri: "file:///data/documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_JSON"
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
    

## HTTP Client Configuration

When using docling-serve API mode, the component uses the [docling-java](https://github.com/docling-project/docling-java) library which internally uses Java’s built-in `HttpClient`. The HTTP client is configured with sensible defaults and connection management is handled automatically by the library.

### Timeout Configuration

  
| Parameter | Default | Description |
| --- | --- | --- |
| `processTimeout` | 30000 | HTTP read timeout in milliseconds for synchronous API calls. Also used as the CLI subprocess timeout. Increase this for large or complex documents (e.g., 120000 for 2 minutes). |
| `asyncPollInterval` | 2000 | Poll interval in milliseconds when checking async task status. |
| `asyncTimeout` | 300000 | Maximum time to wait for async conversion completion in milliseconds (5 minutes). |
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
      uri: "file:///data/large-documents"
      parameters:
        include: ".*\\.pdf"
    steps:
      - to:
          uri: "docling:CONVERT_TO_MARKDOWN"
          parameters:
            useDoclingServe: true
            useAsyncMode: true
            asyncPollInterval: 5000
            asyncTimeout: 600000
            contentInBody: true
      - to:
          uri: "file:///data/output"
```

### Best Practices

1.  **Use async mode for large documents**: Enable `useAsyncMode=true` for documents that may take longer to process. The docling-java library handles polling automatically.
    
2.  **Adjust poll interval appropriately**: For high-volume scenarios, increase `asyncPollInterval` to reduce polling overhead. For interactive use cases, a shorter interval provides faster feedback.
    
3.  **Set appropriate timeouts**: Adjust `asyncTimeout` based on your largest expected document size. The default 5 minutes is suitable for most documents.
    
4.  **Monitor with logging**: Use DEBUG level logging to monitor API calls and async task status.
    

## Spring Boot Auto-Configuration

When using docling with Spring Boot make sure to use the following Maven dependency to have support for auto configuration:

```xml
<dependency>
  <groupId>org.apache.camel.springboot</groupId>
  <artifactId>camel-docling-starter</artifactId>
  <version>x.x.x</version>
  <!-- use the same version as your Camel core version -->
</dependency>
```

The component supports 47 options, which are listed below.

   
| Name | Description | Default | Type |
| --- | --- | --- | --- |
| **camel.component.docling.abort-on-error** | Abort processing on error. | false | Boolean |
| **camel.component.docling.api-key-header** | Header name for API key authentication. | X-API-Key | String |
| **camel.component.docling.async-poll-interval** | Polling interval for async conversion status in milliseconds. | 2000 | Long |
| **camel.component.docling.async-timeout** | Maximum time to wait for async conversion completion in milliseconds. | 300000 | Long |
| **camel.component.docling.authentication-scheme** | Authentication scheme (BEARER, API\_KEY, NONE). | none | AuthenticationScheme |
| **camel.component.docling.authentication-token** | Authentication token for docling-serve API (Bearer token or API key). |  | String |
| **camel.component.docling.autowired-enabled** | Whether autowiring is enabled. This is used for automatic autowiring options (the option must be marked as autowired) by looking up in the registry to find if there is a single instance of matching type, which then gets configured on the component. This can be used for automatic configuring JDBC data sources, JMS connection factories, AWS Clients, etc. | true | Boolean |
| **camel.component.docling.batch-fail-on-first-error** | Fail entire batch on first error (true) or continue processing remaining documents (false). | true | Boolean |
| **camel.component.docling.batch-parallelism** | Number of parallel threads for batch processing. | 4 | Integer |
| **camel.component.docling.batch-size** | Maximum number of documents to process in a single batch (batch operations only). | 10 | Integer |
| **camel.component.docling.batch-timeout** | Maximum time to wait for batch completion in milliseconds. | 300000 | Long |
| **camel.component.docling.configuration** | The configuration for the Docling Endpoint. The option is a org.apache.camel.component.docling.DoclingConfiguration type. |  | DoclingConfiguration |
| **camel.component.docling.content-in-body** | Include the content of the output file in the exchange body and delete the output file. | false | Boolean |
| **camel.component.docling.do-code-enrichment** | Enable code enrichment in document processing. | false | Boolean |
| **camel.component.docling.do-formula-enrichment** | Enable formula enrichment in document processing. | false | Boolean |
| **camel.component.docling.do-ocr** | Enable OCR processing in docling-serve API mode. When not set, the server uses its own defaults. Set enableOCR to false to explicitly disable OCR. | false | Boolean |
| **camel.component.docling.do-picture-classification** | Enable picture classification in document processing. | false | Boolean |
| **camel.component.docling.do-picture-description** | Enable picture description generation in document processing. | false | Boolean |
| **camel.component.docling.do-table-structure** | Enable table structure recognition. | false | Boolean |
| **camel.component.docling.docling-command** | Path to Docling Python executable or command. |  | String |
| **camel.component.docling.docling-serve-url** | Docling-serve API URL (e.g., [http://localhost:5001](http://localhost:5001)). | [http://localhost:5001](http://localhost:5001) | String |
| **camel.component.docling.document-timeout** | Document processing timeout in seconds. |  | Long |
| **camel.component.docling.enable-o-c-r** | Enable OCR processing for scanned documents. | true | Boolean |
| **camel.component.docling.enabled** | Whether to enable auto configuration of the docling component. This is enabled by default. |  | Boolean |
| **camel.component.docling.force-ocr** | Force OCR processing even for digital documents. | false | Boolean |
| **camel.component.docling.image-export-mode** | Image export mode for referenced images. |  | String |
| **camel.component.docling.images-scale** | Scale factor for exported images. |  | Double |
| **camel.component.docling.include-images** | Include images in the conversion output. | false | Boolean |
| **camel.component.docling.include-layout-info** | Show layout information with bounding boxes. | false | Boolean |
| **camel.component.docling.include-metadata-in-headers** | Include metadata in message headers when extracting metadata. | true | Boolean |
| **camel.component.docling.include-raw-metadata** | Include raw metadata as returned by the parser. | false | Boolean |
| **camel.component.docling.lazy-start-producer** | Whether the producer should be started lazy (on the first message). By starting lazy you can use this to allow CamelContext and routes to startup in situations where a producer may otherwise fail during starting and cause the route to fail being started. By deferring this startup to be lazy then the startup failure can be handled during routing messages via Camel’s routing error handlers. Beware that when the first message is processed then creating and starting the producer may take a little time and prolong the total processing time of the processing. | false | Boolean |
| **camel.component.docling.max-file-size** | Maximum file size in bytes for processing. | 52428800 | Long |
| **camel.component.docling.md-page-break-placeholder** | Placeholder string for page breaks in markdown output. |  | String |
| **camel.component.docling.ocr-engine** | OCR engine to use. |  | String |
| **camel.component.docling.ocr-language** | Language code for OCR processing. | en | String |
| **camel.component.docling.operation** | The operation to perform. | convert-to-markdown | DoclingOperations |
| **camel.component.docling.output-format** | Output format for document conversion. | markdown | String |
| **camel.component.docling.pdf-backend** | PDF parsing backend. |  | String |
| **camel.component.docling.pipeline** | Processing pipeline to use. |  | String |
| **camel.component.docling.process-timeout** | Timeout for Docling process execution in milliseconds. | 30000 | Long |
| **camel.component.docling.split-batch-results** | Split batch results into individual exchanges (one per document) instead of single BatchProcessingResults. | false | Boolean |
| **camel.component.docling.table-cell-matching** | Enable table cell matching post-processing. | false | Boolean |
| **camel.component.docling.table-mode** | Table structure recognition mode. |  | String |
| **camel.component.docling.use-async-mode** | Use asynchronous conversion mode (docling-serve API only). | false | Boolean |
| **camel.component.docling.use-docling-serve** | Use docling-serve API instead of CLI command. | false | Boolean |
| **camel.component.docling.working-directory** | Working directory for Docling execution. |  | String |