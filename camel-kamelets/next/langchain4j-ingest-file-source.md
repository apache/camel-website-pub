# ![langchain4j ingest file source](_images/kamelets/langchain4j-ingest-file-source.svg) LangChain4j Ingest File Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Reads the documents in a directory and its subdirectories, one message per file, leaves them in place, and reads a file again when it changes.

Use it to feed a knowledge base for an AI assistant: put it in front of `langchain4j-ingest-sink`, with `tika-extract-text-action` or `docling-convert-action` in between for PDF or office documents.

Output: the body is the file, read as bytes unless `charset` is set. The `CamelLangChain4jIngestDocumentId` header is the path of the file relative to `directory`, such as `manuals/pump.pdf`, which `langchain4j-ingest-sink` uses as the document id. The usual file headers, such as `CamelFileName`, are set too.

Good to know: the files are never deleted or moved. A file is read again when its modification time or size changes, and `langchain4j-ingest-sink` then adds the new version next to the old one, unless it has an `idempotentRepository`, which skips it. The files already read are remembered in memory only, by default the last 1000, so after a restart every file is read again; set `idempotentRepository` to keep them. A file that is still being copied in is read only once it stops changing.

## Configuration Options

The following table summarizes the configuration options available for the `langchain4j-ingest-file-source` Kamelet:

     
| Property | Name | Description | Type | Default | Example |
| --- | --- | --- | --- | --- | --- |
| **directory** | Directory | **Required** The path of the directory to read the documents from, on the machine where the integration runs. | string |  | /data/knowledge-base |
| **charset** | Charset | The character set to read text files with, such as `UTF-8`; the body is then text. Leave it unset when a `tika-extract-text-action`, a `docling-convert-action` or a `langchain4j-ingest-sink` with `modality` set to `media` comes next, because they need the bytes of the file, and a conversion breaks a binary file such as a PDF. | string |  | UTF-8 |
| **delay** | Delay | How long to wait between two looks at the directory, in milliseconds. When it is not set, the directory is looked at every 500 milliseconds; a longer delay, such as one minute, is usually enough for a knowledge base. | integer |  | 60000 |
| **exclude** | Exclude | Ant-style patterns of the files to leave out, separated by commas, in the same form as `include`. It wins over `include`. | string |  | **\*/draft-** |
| **idempotentRepository** | Idempotent Repository | A Camel `IdempotentRepository` defined in the application, as `#bean:` followed by its name, that remembers the files already read, by path, modification time and size. Use a persistent one, so that the files are not read again after a restart. When it is not set, the last 1000 files are remembered in memory. | string |  | #bean:readFiles |
| **include** | Include | Ant-style patterns of the files to read, separated by commas, matched on the path relative to `directory`. `***/**.pdf` matches the PDF files in any subdirectory. When it is not set, every file is read. | string |  | **/**.pdf,**/**.md |
| **recursive** | Recursive | If true, the files in the subdirectories are read too. | boolean | true |  |

## Dependencies

At runtime, the `langchain4j-ingest-file-source` Kamelet relies upon the presence of the following dependencies:

-   camel:file
    
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
      uri: "kamelet:langchain4j-ingest-file-source"
      parameters:
        .
        .
        .
      steps:
        - to:
            uri: "kamelet:log-sink"
```

You can now run it directly through the following command

```shell
camel run route.yaml
```

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/langchain4j-ingest-file-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/langchain4j-ingest-file-source.kamelet.yaml)