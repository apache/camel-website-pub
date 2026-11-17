# ![docling convert action](_images/kamelets/docling-convert-action.svg) Docling Convert Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Turns each document, such as a PDF, an office document or an HTML page, into Markdown text with Docling, keeping its headings, lists and tables.

Use it to get well-structured text out of documents before an AI step, for example in front of `langchain4j-ingest-sink` to load them into a vector store. For plain text without a Docling server, use `tika-extract-text-action`.

Input: the document, as bytes, a stream, a file or text. The header named in `documentIdHeader` (by default `CamelLangChain4jIngestDocumentId`) is the id of the document, if any; it is kept for `langchain4j-ingest-sink` further on.

Output: the body is the document as Markdown, as text. The headers of the message are kept.

Good to know: to use a Docling Serve server, which is the usual setup, set both `useDoclingServe` to true and `doclingServeUrl`; otherwise it runs the `docling` command-line program, which must be installed on the machine of the integration. With `maxDocumentSize`, a larger document fails the message without being sent.

## Configuration Options

The following table summarizes the configuration options available for the `docling-convert-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **doclingServeUrl** | Docling Serve URL | The address of a Docling Serve server, starting with `http://` or `https://`. Only used when `useDoclingServe` is true. | string |  | http://docling-serve:5001 |
| **documentIdHeader** | Document ID Header | The name of the header that holds the id of the document, such as its file name. The id is kept for `langchain4j-ingest-sink`, which writes it on every piece of the document in the store, and takes precedence over the headers it reads. Change it when the id comes in another header. | string | CamelLangChain4jIngestDocumentId | CamelFileName |
| **maxDocumentSize** | Max Document Size | The largest document to convert, in bytes. A larger document fails the message without being converted. 0, the default, means no limit. | integer | 0 | 10485760 |
| **useDoclingServe** | Use Docling Serve | If true, the documents are converted by the Docling Serve server at `doclingServeUrl`. When it is not set, the `docling` command-line program is run on the machine of the integration. | boolean |  |  |

## Dependencies

At runtime, the `docling-convert-action` Kamelet relies upon the presence of the following dependencies:

-   camel:docling
    
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
            uri: "kamelet:docling-convert-action"
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

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/docling-convert-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/docling-convert-action.kamelet.yaml)