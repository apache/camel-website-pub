# ![tika extract text action](_images/kamelets/tika-extract-text-action.svg) Tika Extract Text Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Turns each document, such as an HTML page, a text file or a PDF, into its plain text, or into XHTML, with Apache Tika, inside the integration.

Use it to get the text of documents before searching, indexing or summarising them, for example in front of `langchain4j-ingest-sink` to load documents into a vector store for an AI assistant. For a richer conversion to Markdown that keeps headings and tables, use `docling-convert-action`, which needs a Docling server.

Input: the document, as bytes, a stream, a file or text. The header named in `documentIdHeader` (by default `CamelLangChain4jIngestDocumentId`) is the id of the document, if any; it is kept for `langchain4j-ingest-sink` further on.

Output: the body is the plain text of the document, as text in UTF-8, with its blocks on separate lines; with `outputFormat` set to `html` or `xml`, it is the document as XHTML text instead. The `Content-Type` header is set to `text/plain`, also for XHTML. All the other headers of the message are removed, except the Camel ones, such as the file name headers of `langchain4j-ingest-file-source`.

Good to know: only HTML and plain text are read out of the box. For PDF, add the Tika PDF parser module (`org.apache.tika:tika-parser-pdf-module`, in the Tika version of your Camel) to the integration, and add the other Tika parser modules for other formats; without the module, a PDF gives an empty text, and does not fail. With `maxDocumentSize`, a larger document fails the message without being read.

## Configuration Options

The following table summarizes the configuration options available for the `tika-extract-text-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **documentIdHeader** | Document ID Header | The name of the header that holds the id of the document, such as its file name. The id is kept for `langchain4j-ingest-sink`, which writes it on every piece of the document in the store, and takes precedence over the headers it reads. Change it when the id comes in another header. | string | CamelLangChain4jIngestDocumentId | CamelFileName |
| **maxDocumentSize** | Max Document Size | The largest document to read, in bytes. A larger document fails the message without being read. 0, the default, means no limit. | integer | 0 | 10485760 |
| **outputFormat** | Output Format | What the body becomes. `text`, the default, is the plain text of the document. `html` is the document as an XHTML page, with its paragraphs, and for some formats its headings, lists and tables, as HTML elements, and with the metadata Tika found, such as the title, as `meta` elements in the `head`. `xml` is the same page with an XML declaration on top. A document without a title, such as plain text or the text of an earlier extraction, gets an empty `title` element. Enum values: \* text \* html \* xml | string | text |  |

## Dependencies

At runtime, the `tika-extract-text-action` Kamelet relies upon the presence of the following dependencies:

-   camel:tika
    
-   camel:kamelet
    
-   camel:bean
    

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
            uri: "kamelet:tika-extract-text-action"
            parameters:
            .
            .
            .
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Tika Extract Text Action Kamelet Description

### Output Formats

`outputFormat` chooses what the body becomes:

 
| `outputFormat` | Body |
| --- | --- |
| `text` (the default) | The plain text of the document, with its blocks on separate lines. |
| `html` | The document as an XHTML page. The `head` holds the metadata Tika found, such as the title and the content type, as `meta` elements. The `body` holds the text in paragraphs, and for some formats, such as HTML, in headings, lists and tables too. A PDF gives a `div` per page. |
| `xml` | The same XHTML page, with an XML declaration on top. |

With `html` and `xml`, a document whose metadata holds a character that XML does not allow, such as the NUL character that some PDF writers put in it, fails the message; `text` reads it.

### Example

The following route reads the PDF files of a directory and writes each one as an XHTML page to another directory. The Tika PDF parser module must be added to the integration, in the Tika version of your Camel, such as with `camel run route.yaml --dep=org.apache.tika:tika-parser-pdf-module:4.1.0`.

```yaml
- route:
    from:
      uri: "kamelet:langchain4j-ingest-file-source"
      parameters:
        directory: "/data/manuals"
        include: "**/*.pdf"
      steps:
        - to:
            uri: "kamelet:tika-extract-text-action"
            parameters:
              outputFormat: html
        - to:
            uri: "file:/data/manuals-html"
            parameters:
              fileName: "$\{file:name.noext}.html"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/tika-extract-text-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/tika-extract-text-action.kamelet.yaml)