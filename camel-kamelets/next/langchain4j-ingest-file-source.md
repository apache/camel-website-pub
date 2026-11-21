# ![langchain4j ingest file source](_images/kamelets/langchain4j-ingest-file-source.svg) LangChain4j Ingest File Source

**Provided by: "Apache Software Foundation"**

**Support Level for this Kamelet is: "Preview"**

Reads the documents in a directory and its subdirectories, one message per file, leaves them in place, and reads a file again when it changes.

Use it to feed a knowledge base for an AI assistant: put it in front of `langchain4j-ingest-sink`, with `tika-extract-text-action` or `docling-convert-action` in between for PDF or office documents.

Output: the body is the file, read as bytes unless `charset` is set, and the `Content-Type` header is `application/octet-stream`. The `CamelLangChain4jIngestDocumentId` header is the path of the file relative to `directory`, such as `manuals/pump.pdf`, which `langchain4j-ingest-sink` uses as the document id. The usual file headers, such as `CamelFileName`, are set too.

Good to know: the files are never deleted or moved. A file is read again when its modification time or size changes, and `langchain4j-ingest-sink` then adds the new version next to the old one, unless it has an `idempotentRepository`, which skips it. The files already read are remembered in memory only, by default the last 1000, so after a restart every file is read again; set `idempotentRepository` to keep them. A file that is still being copied in is read only once it stops changing; for a slow copy, which can pause for more than a second, set `readLockMinAge`.

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
| **initialDelay** | Initial Delay | How long to wait after the integration starts before the first look at the directory, in milliseconds. When it is not set, 1000 (one second) is used. | integer |  | 30000 |
| **maxMessagesPerPoll** | Max Messages Per Poll | The largest number of files to read in one look at the directory; the others are read in the next looks, one `delay` later. Use it to spread out the first load of a large directory. Which files come first is not defined. When it is not set, there is no limit. | integer |  | 100 |
| **readLockMinAge** | Read Lock Min Age | How long ago a file must have last changed before it is read, in milliseconds, such as 60000 for a file copied in slowly. It replaces the usual check, which reads each file only once its size and modification time have not changed for one second, so that an older file is read at once, and a newer one once it is old enough. | integer |  | 60000 |
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

## LangChain4j Ingest File Source Kamelet Description

### When Files Are Read

The Kamelet looks at the directory one second after it starts, or `initialDelay` milliseconds, and then every `delay` milliseconds.

By default, it reads each file only once its size and modification time have not changed for one second, so that a file still being copied in is not read half-written. That check costs one second per file, also for a file that has not changed in months. With `readLockMinAge`, a file is read when it last changed at least that many milliseconds ago: an older file is read at once, and a newer one once it is old enough. Set it for a copy that can pause for more than a second, such as over a slow network share.

`maxMessagesPerPoll` limits how many files are read in one look at the directory; the others are read in the next looks. It spreads the first load of a large directory over time, such as for an embedding model with a rate limit.

### Example

The following route loads the Markdown and PDF files of a directory into a vector store. It starts 30 seconds after the application, reads at most 100 files a minute, and reads a file only one minute after it last changed.

```yaml
- route:
    from:
      uri: "kamelet:langchain4j-ingest-file-source"
      parameters:
        directory: "/data/knowledge-base"
        include: "**/*.md,**/*.pdf"
        initialDelay: 30000
        delay: 60000
        maxMessagesPerPoll: 100
        readLockMinAge: 60000
      steps:
        - to:
            uri: "kamelet:tika-extract-text-action"
        - to:
            uri: "kamelet:langchain4j-ingest-sink"
```

The embedding store and the embedding model of `langchain4j-ingest-sink` are beans of the application.

## Kamelet source file

[https://github.com/apache/camel-kamelets/blob/main/kamelets/langchain4j-ingest-file-source.kamelet.yaml](https://github.com/apache/camel-kamelets/blob/main/kamelets/langchain4j-ingest-file-source.kamelet.yaml)