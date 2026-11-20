# ![docling convert action](_images/kamelets/docling-convert-action.svg) Docling Convert Action

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Turns each document, such as a PDF, an office document or an HTML page, into Markdown, HTML or plain text with Docling, keeping its headings, lists and tables.

Use it to get well-structured text out of documents before an AI step, for example in front of `langchain4j-ingest-sink` to load them into a vector store. For plain text without a Docling server, use `tika-extract-text-action`.

Input: the document, as bytes, a stream, a file or text. The header named in `documentIdHeader` (by default `CamelLangChain4jIngestDocumentId`) is the id of the document, if any; it is kept for `langchain4j-ingest-sink` further on.

Output: the body is the document as Markdown, as text, or as HTML or plain text with `operation`. The `Content-Type` header is set to `text/plain`, also for HTML. The other headers of the message are kept.

Good to know: to use a Docling Serve server, which is the usual setup, set both `useDoclingServe` to true and `doclingServeUrl`; otherwise it runs the `docling` command-line program, which must be installed on the machine of the integration. A server started with an API key needs `authenticationScheme` set to `API_KEY` and the key in `authenticationToken`. A conversion that takes longer than `processTimeout`, 30 seconds when it is not set, fails the message; the first conversion after a Docling Serve server starts, and a large PDF on a server without a GPU, can take longer than that. The text in images, such as scanned pages, is read with OCR unless `enableOcr` is false. With `maxDocumentSize`, a larger document fails the message without being sent.

## Configuration Options

The following table summarizes the configuration options available for the `docling-convert-action` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **authenticationScheme** | Authentication Scheme | How to send `authenticationToken` to the Docling Serve server. `API_KEY` sends it in the `X-Api-Key` header, which is what a Docling Serve server started with an API key (`DOCLING_SERVE_API_KEY`) expects. `BEARER` sends it in the `Authorization` header as `Bearer` followed by the token, for a server behind a gateway that asks for one. Set it together with `authenticationToken`. Enum values: \* API\_KEY \* BEARER | string |  |  |
| **authenticationToken** | Authentication Token | The API key or token to log in to the Docling Serve server with, sent as `authenticationScheme` says. Only used with Docling Serve. | string |  |  |
| **doclingServeUrl** | Docling Serve URL | The address of a Docling Serve server, starting with `http://` or `https://`. Only used when `useDoclingServe` is true. | string |  | http://docling-serve:5001 |
| **documentIdHeader** | Document ID Header | The name of the header that holds the id of the document, such as its file name. The id is kept for `langchain4j-ingest-sink`, which writes it on every piece of the document in the store, and takes precedence over the headers it reads. Change it when the id comes in another header. | string | CamelLangChain4jIngestDocumentId | CamelFileName |
| **documentTimeout** | Document Timeout | How long the Docling Serve server may work on one document, in seconds. When the time is up, the server stops, and the body holds only the part of the document it converted, without failing the message. Only used with Docling Serve. When it is not set, the server uses its own limit. | integer |  | 120 |
| **enableOcr** | Enable OCR | If false, the text in images, such as the pages of a scanned PDF, is not read (OCR, optical character recognition), which is faster, and a scanned page gives no text. If true, OCR is asked for, in `ocrLanguage`. When it is not set, a Docling Serve server uses its own setting, which is to read the images. | boolean |  |  |
| **forceOcr** | Force OCR | If true, every page is read with OCR, even a page that holds text, whose text is then replaced by what OCR reads. Use it for a PDF whose text layer is wrong. Only used with Docling Serve. | boolean |  |  |
| **maxDocumentSize** | Max Document Size | The largest document to convert, in bytes. A larger document fails the message without being converted. 0, the default, means no limit. | integer | 0 | 10485760 |
| **ocrEngine** | OCR Engine | The OCR engine that reads the images, which must be installed on the Docling Serve server, else the message fails; `OCRMAC` works only on a Mac. With `TESSERACT`, also set `enableOcr` to true and `ocrLanguage` to a language installed for it. When it is not set, the server chooses. Only used with Docling Serve. Enum values: \* AUTO \* EASYOCR \* RAPIDOCR \* TESSERACT \* TESSEROCR \* OCRMAC | string |  |  |
| **ocrLanguage** | OCR Language | The language of the text in images, as a code that the OCR engine knows, such as `en` or `de`, or `eng` or `iso:en` for Tesseract. The engine must have a model for the language, else the message fails. With Docling Serve, it is used only when `enableOcr` is true. When it is not set, `en` is used. | string |  | de |
| **operation** | Operation | What the document is turned into. `CONVERT_TO_MARKDOWN`, the default, gives Markdown text. `CONVERT_TO_HTML` gives a whole HTML page, with its styles, as text. `EXTRACT_TEXT` gives the text without the Markdown marks of headings and images; tables are still drawn with `|` characters. Enum values: \* CONVERT\_TO\_MARKDOWN \* CONVERT\_TO\_HTML \* EXTRACT\_TEXT | string | CONVERT\_TO\_MARKDOWN |  |
| **processTimeout** | Process Timeout | How long to wait for a document to be converted, in milliseconds. A slower conversion fails the message. With Docling Serve, it is how long to wait for the answer of the server. When it is not set, 30000 (30 seconds) is used, which is often too short for a large PDF. | integer |  | 300000 |
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

## Docling Convert Action Kamelet Description

### Docling Serve

Set `useDoclingServe` to true and `doclingServeUrl` to the address of a Docling Serve server, such as one started from the `quay.io/docling-project/docling-serve` image. Without them, the Kamelet runs the `docling` command-line program on the machine of the integration.

A server started with an API key, in the `DOCLING_SERVE_API_KEY` environment variable, answers `Unauthorized` to any request without it. Set `authenticationScheme` to `API_KEY` and the key in `authenticationToken`: it is sent in the `X-Api-Key` header. For a server behind a gateway that asks for a token in the `Authorization` header, set `authenticationScheme` to `BEARER` instead.

### Timeouts

`processTimeout` is how long the Kamelet waits for the answer of the server, in milliseconds, 30000 when it is not set. A server without a GPU can take longer than that for the first document after it starts, while it loads its models, and for a large PDF: the message then fails. Set it to a few minutes for such a server.

`documentTimeout` is how long the server may work on one document, in seconds. When the time is up, the body holds only the part of the document converted so far, and the message does not fail.

### OCR

OCR (optical character recognition) reads the text in images, such as the pages of a scanned PDF.

 
| Option | Effect with Docling Serve |
| --- | --- |
| `enableOcr` not set | The server decides; the Docling Serve image reads the images. |
| `enableOcr: false` | The images are not read, which is faster. A scanned page gives no text. |
| `enableOcr: true` | The images are read, in the language of `ocrLanguage` (`en` when it is not set). |
| `ocrLanguage` | A code the OCR engine knows, such as `de`; `eng` or `iso:en` for Tesseract. Used only with `enableOcr: true`. A language the engine has no model for fails the message. |
| `forceOcr: true` | Every page is read with OCR, and its text layer is replaced, for a PDF whose text layer is wrong. |
| `ocrEngine` | The engine, which must be installed on the server. `TESSERACT` needs `enableOcr: true` and an `ocrLanguage` installed for it; `OCRMAC` works only on a Mac. |

### Example

The following route converts the PDF files of a directory with a Docling Serve server that has an API key, reading scanned pages in German, and writes each one as Markdown to another directory.

```yaml
- route:
    from:
      uri: "kamelet:langchain4j-ingest-file-source"
      parameters:
        directory: "/data/scans"
        include: "**/*.pdf"
      steps:
        - to:
            uri: "kamelet:docling-convert-action"
            parameters:
              useDoclingServe: true
              doclingServeUrl: "http://docling-serve:5001"
              authenticationScheme: API_KEY
              authenticationToken: "{{docling.api.key}}"
              processTimeout: 300000
              enableOcr: true
              ocrLanguage: de
        - to:
            uri: "file:/data/scans-markdown"
            parameters:
              fileName: "$\{file:name.noext}.md"
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/docling-convert-action.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/docling-convert-action.kamelet.yaml)